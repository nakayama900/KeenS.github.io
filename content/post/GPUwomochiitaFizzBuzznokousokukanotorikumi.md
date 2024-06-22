---
categories: [FizzBuzz, OpenCL, GPU]
date: 2022-04-01T00:00:00+09:00
title: "GPUを用いたFizzBuzzの高速化の取り組み"
---

ハ〜イ、κeenさんだよー。FizzBuzzを高速化したから紹介するねー。

<!--more-->

# 背景
## FizzBuzz問題とは
FizzBuzz問題[^fizzbuzz]とは以下のような動作を行うプログラムを書けという問題です。

1. 数を0から順に表示する
2. 数が3の倍数なら数の代わりに"Fizz"と表示する
3. 数が5の倍数なら数の代わりに"Buzz"と表示する
4. 数が15の倍数なら数の代わりに"FizzBuzz"と表示する

[^fizzbuzz]: https://ja.wikipedia.org/wiki/Fizz_Buzz


このプログラムはループや分岐といった基本的な要素を含んでおり、プログラムの例示として大変よく使われるものです。
また、プログラマであるか試す試金石として面接で使われるケースもあるなど、使用頻度と重要度がともに高いプログラムです。このプログラムの高速化は非常に価値があると考えられ、本稿で高速化に取り組みます。

## Graphics Processing Unit（GPU）とは
GPU[^gpu]はリアルタイム画像処理に特化した演算装置です。近年のGPUは画像処理に限らない汎用の処理を行えるようになっており、これを使ったGPGPU[^gpgpu]はAIやビッグデータなどの高速化に寄与しています。本稿では同様の手法でFizzBuzzを高速化できると考え、GPGPUを用いてFizzBuzzの高速化に取り組みます。

[^gpu]: (https://ja.wikipedia.org/wiki/Graphics_Processing_Unit)
[^gpgpu]: https://ja.wikipedia.org/wiki/GPGPU

# 実装
実装はGPGPUフレームワークとしてOpenCL[^opencl]を使い、記述しました。OpenCLはGPUを使う手段を提供してはくれるものの、高速なプログラムを書くには多少の工夫が必要になります。今回は2点の工夫ありました。分岐発散への対策とメモリレイアウトです。
[^opencl]: https://opencl.org

## 分岐発散への対策
OpenCLはGPUを駆動するためのホストプログラムとGPU内で動くカーネルプログラムをプログラマが書きます。カーネルプログラムは指定した並列数で動くので `0` から `n-1` までのFizzBuzzを実行するのに `n` 並列で動かすとして、素直に実装すると以下の疑似コードようなカーネルが書けます。

```c
kernel void fizzbuzz(global char *dst)
{
  int n = get_global_id(0);
  if(n % 15 == 0) {
    output "fizzbuzz";
  } else if(n % 3 == 0) {
    output "fizz";
  } else if(n % 5 == 0) {
    output "buzz";
  } else {
    output n;
  }
}
```

これでも正しく動くのですが、かなり効率が悪くなります。今回用いたAMDのGPUでは複数のワークアイテムが同じ命令を実行します。ところがワークアイテムごとに分岐処理が違うと、各々で違う命令を実行することになります。これはGPUが実行するときにはあるワークアイテムでしか実行されない処理の間、他のワークアイテムの処理を止めることで疑似的に分岐のようなことをしています。例えば上記のコードを0~15の15並列で実行した場合は以下のようなスケジューリングになります。

```text
x … 実行
  … 休み

  0   1   2   3       15
+---+---+---+---+ ~ +----+
| x | x | x | x | ~ | x  | kernel void fizzbuzz(global char *dst)
| x | x | x | x | ~ | x  | {
| x | x | x | x | ~ | x  |   int n = get_global_id(0);
| x | x | x | x | ~ | x  |   if(n % 15 == 0) {
| x |   |   |   | ~ | x  |     output "fizzbuzz";
|   | x | x | x | ~ |    |   } else if(n % 3 == 0) {
|   |   |   | x | ~ |    |     output "fizz";
|   | x | x |   | ~ |    |   } else if(n % 5 == 0) {
|   |   |   |   | ~ |    |     output "buzz";
|   | x | x |   | ~ |    |   } else {
|   | x | x |   | ~ |    |     output n;
| x | x | x | x | ~ | x  |   }
| x | x | x | x | ~ | x  | }
+---+---+---+---+ ~ +----+
```

これだと処理が走っている割合が小さくなり、非効率になります。そこで1ワークアイテムが15こ分の数を担当するようにして分岐を行わないようにしました。

```c
kernel void fizzbuzz(global char *dst)
{
  int n = get_global_id(0) * 15;
  output "fizzbuzz";
  output n + 1;
  output n + 2;
  output "fizz";
  output n + 4;
  output "buzz";
  output "fizz";
  output n + 7;
  output n + 8;
  output "fizz";
  output "buzz";
  output n + 11;
  output "fizz";
  output n + 13;
  output n + 14;
}

```

ただし端数処理の関係で `n` が15の倍数に切り上げられてしまいます。

## メモリレイアウト

上記疑似コードでは `output` と書きましたが計算した値の出力には慎重な設計が必要です。一応OpenCLには [`printf` 関数はある](https://www.khronos.org/registry/OpenCL/sdk/2.2/docs/man/html/printfFunction.html)ものの、大量の出力には向きません。最適な出力はホストプログラムに任せるとしてカーネル側ではメモリにデータを書き込むに留めます。

ところがそのメモリにデータを書き込むのが意外と難しいです。n番目のFizzBuzzがメモリどこに値を書き込むべきか簡単には分かりません。また、CPUとやりとりできるグローバルなメモリへのアクセスは遅めなので何度かアクセスするデータはローカルなメモリ（ローカルデータストレージ）を使うと速くなります。

そこで、1ワークアイテムごとに少し多めにローカルメモリをあてがい、そこに書き込ませます。これならワークアイテム番号から書き込むべきメモリアドレスが決まるので複雑な計算が不要になります。

```text
  0               1               2               3
+---------------+---------------+---------------+---------------+
| fizzbuzz| ... | fizzbuzz| ... | fizzbuzz| ... | fizzbuzz| ... | local
+---------------+---------------+---------------+---------------+
```

しかし、このままだと今度はホスト側で書き出すときにメモリが断片的すぎて不便になってしまいます。そこで各々のワークアイテムが値を書き出したあとある程度の数のワークアイテムのグループ間でメモリをよせ集めてグローバルなメモリに移すことで多少は断片化を解消するようにしています。

```text
  0               1               2               3
+---------------+---------------+---------------+---------------+
| fizzbuzz| ... | fizzbuzz| ... | fizzbuzz| ... | fizzbuzz| ... | local
+---------------+---------------+---------------+---------------+
  |              /                |              /
  |             /                 |             /
  v            v                  v            v
  0                               1
+-------------------------------+-------------------------------+
| fizzbuzz fizzbuzz| .......... | fizzbuzz fizzbuzz| .......... | global
+-------------------------------+-------------------------------+
```

---

また、その他ホスト側ではIOを工夫するなどした。

# 計測

上記のようにOpenCLプログラムを実行したところ、約845 MiB/s の速度になりました。

```console
$ ./main 500000000 | wc -c
3907412008
$ time ./main 500000000 > /dev/null
./main 500000000 > /dev/null  0.47s user 0.84s system 29% cpu 4.408 total
```

これは高速であると考えられます。

# まとめと将来へ向けた課題

本稿ではFizzBuzzと呼ばれる非常に重要なプログラムをGPUを用いて高速化し、その速度は約845 MiB/sになりました。
本稿で用いたプログラムはGPUが1枚の場合のみを想定しているので複数枚ある場合はそれらを使うようにしてさらなる高速化が望めます。また、同様に処理をGPUでのみ行っているのでCPUでも処理をすることでさらなる高速化が期待できます。

コードは以下にあります。

https://github.com/KeenS/opencl-fizzbuzz