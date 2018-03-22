---
categories: [オブジェクト指向, 関数型]
date: 2018-03-14T22:22:40+09:00
description:
title: "オブジェクト指向言語と関数型言語"
---
<section data-markdown
    data-separator="\n===\n"
    data-vertical="\n---\n"
    data-notes="^Note:">
<script type="text/template">

# オブジェクト指向言語と関数型言語
----------------------
[MANABIYA](https://manabiya.tech/) 2日目5時間目

<!-- .slide: class="center" -->
===
# About Me
---------
![κeenのアイコン](/images/kappa.png) <!-- .element: style="position:absolute;right:0;z-index:-1" width="20%" -->

 * κeen
 * [@blackenedgold](https://twitter.com/blackenedgold)
 * Github: [KeenS](https://github.com/KeenS)
 * [Idein Inc.](https://idein.jp/)のエンジニア
 * 言語処理系を作るのが好き
 * 仕事での経験: Java, Scala, Rust
 * 趣味: C, Common Lisp, Standard ML, Rust

===

# 理想のソフトウェア
-------------------

* 凝集度を高めて結合度を低めたい
  + 似たようなものは同じところに
  + 互いの依存関係を減らす
* 変更に強いソフトウェア
* バグの少ないソフトウェア
* Open Closed Principle
  + 変更に開いて修正に閉じる
* 理想のソフトウェアを作るには？

===
# パラダイム
-----------

* [Wikipedia](https://ja.wikipedia.org/wiki/%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0%E3%83%91%E3%83%A9%E3%83%80%E3%82%A4%E3%83%A0)
* プログラミングにおける思考のフレームワーク
  + 一貫性の取れた設計
  + 組み合わせたときの相性の良さ
  + 一度理解するとその後の学習コストが下がる
* ある程度成功しやすい手法のパターン化

===

# 複数の言語パラダイムを知ろう
----------------------------


[<img src="/images/manabiya/9_langs.png" alt="いま学ぶべき第二のプログラミング言語はコレだ！ 未来のために挑戦したい9つの言語とその理由" width="320px">](https://employment.en-japan.com/engineerhub/entry/2017/05/19/110000)<!-- .element: style="float:left;"  -->

> 「ハンマーしか持っていなかったら、なんでも釘に見える」という戒めがありますが、第二言語を学ぶことは、まさにハンマー以外の道具を持つことだといえます。

===
# オブジェクト指向プログラミング と 関数型プログラミング
----------

* 何故この２つのパラダイム？
  + → よく使われるパラダイム2つ
  + 他には論理型プログラミングなどなどのパラダイムも
* 片方しか経験ない人はもう片方も学んでみよう
  + パラダイムが違うので最初は馴れない
  + コツは過去の成功体験を捨てること
    - パラダイムが違うのだから今まで通りにできないのは当たり前
* どちらもベタな手続き型プログラミングよりいいコードを書きたい

===
# 参考図書
----------

[![オブジェクト指向設計実践ガイド](http://image.gihyo.co.jp/assets/images/cover/2016/9784774183619.jpg)](http://gihyo.jp/book/2016/978-4-7741-8361-9) <!-- .element: style="float:left;"-->
[![関数プログラミング実践入門](http://image.gihyo.co.jp/assets/images/cover/2016/9784774183909.jpg)](http://gihyo.jp/book/2016/978-4-7741-8390-9)     <!-- .element: style="float:right;"-->

===

# OOPって？
----------------------
**オブジェクト** 同士の **メッセージング** によるプログラミング手法

* コード同士の依存関係を上手く管理したい
* 依存関係を上手く扱うことで変更に強いソフトウェアへ
  * DDDなどの設計手法
* コードの分割
* コードの再利用

===

# FPって？
--------------------
**副作用** を出来るだけ使わないプログラミング手法

* 副作用 = 計算以外のもの
  + 破壊的変更、出入力など
    - (深入りするとややこしい)
* 状態を排除することで文脈に依存しないわかりやすいコードへ
  * 読みやすくなる
  * バグが少なくなる
* コードの分割と合成



<blockquote class="twitter-tweet" data-conversation="none" data-lang="ja"><p lang="ja" dir="ltr"><a href="https://twitter.com/esumii?ref_src=twsrc%5Etfw">@esumii</a> 前にも書いたかもしれないけど「関数型＝λ計算ベース」とか「関数型＝関数が第一級」とかいう定義だと、「関数型データ構造」みたいな用語も説明がつかない。ので、やっぱり「破壊的代入などの副作用がない（ないし少ない）」が妥当だと思う</p>&mdash; Eijiro Sumii (@esumii) <a href="https://twitter.com/esumii/status/638591159518887936?ref_src=twsrc%5Etfw">2015年9月1日</a></blockquote>


===

# 何が違うの？
------------

<table style="width:100%">
<tr style="border-bottom: solid 3px #000"><th style="border-right: solid 3px #000"></th><th>OOP</th><th>FP</th></tr>
<tr><th style="border-right: solid 3px #000">状態</th><td>隠蔽</td><td>排除</td></tr>
<tr><th style="border-right: solid 3px #000">誰が</th><td>オブジェクト</td><td>関数</td></tr>
<tr><th style="border-right: solid 3px #000">対象</th><td>メッセージ</td><td>データ</td></tr>
<tr><th style="border-right: solid 3px #000">抽象</th><td>データ</td><td>処理</td></tr>
</table>


===
# 手続き的(自然言語)
-------------------------

入力: `array` - 配列,  `n` - 配列の長さ  
出力: `array`の要素の合計

1. `sum = 0`, `i=0` とする
2. もし`i` が`n`未満ならへ飛ぶ
3. 7へ飛ぶ
4. `sum`に`array`の`i`番目を足したものを`sum`に代入
5. `i`をインクリメント
6. 2へ飛ぶ
7. `sum`を返す

===

# 手続き的(C言語)
----------------

``` c
int
procedual_sum(const int array[], size_t n)
{
  int sum = 0;

  for(size_t i = 0; i < n; i++) {
    sum += array[i];
  }

  return sum;
}
```
===

# OOP的発想
----------

* 手続きがデータについて知りすぎている
  + 配列という具体的実装
  + 繰り返しの終了条件
  + インデックスによってアクセス可能なこと
* もっと具体的実装を抽象化しよう

===
# イメージ

<img src="/images/manabiya/object.png" width="100%" height="100%">


===

# OOPコード例(C言語)
-------------------

``` c
struct list {
  int (*get)(const struct list *, size_t i);
  size_t (*len)(const struct list *);
  struct iter *(*iter)(const struct list *);
  void (*fin)(struct list *);
};

struct iter {
  int (*next)(struct iter *);
  bool (*has_next)(const struct iter *);
  void (*fin)(struct iter *);
};

int
objective_sum(const struct list *list)
{
  int sum = 0;
  struct iter *iter = list->iter(list);
  while (iter->has_next(iter)) {
    sum += iter->next(iter);
  }
  iter->fin(iter);

  return sum;
}
```

===
# 実装イメージ

<img src="/images/manabiya/object_impl.png" width="100%" height="100%">


===
# OOPコード例(C言語) 実装
-------------------

``` c++
struct array_list {
  struct list super;
  int *inner;
  size_t n;
};


struct array_list_iter {
  struct iter super;
  const struct array_list *array;
  size_t i;
};

void array_list_fin(struct list *);
int array_list_get(const struct list *, size_t);
size_t array_list_len(const struct list *);
struct iter *array_list_iter(const struct list *);

struct array_list_iter *array_list_iter_new(const struct array_list *);
void array_list_iter_fin(struct iter *);
int array_list_iter_next(struct iter *);
bool array_list_iter_has_next(const struct iter *);


struct array_list *
array_list_new(int *inner, size_t n)
{
  struct array_list *array = (struct array_list *)malloc(sizeof(struct array_list));
  if (! array) {
    return array;
  }

  array->super.get = array_list_get;
  array->super.len = array_list_len;
  array->super.iter = array_list_iter;
  array->super.fin = array_list_fin;
  array->inner = inner;
  array->n = n;

  return array;
}

void
array_list_fin(struct list *super)
{
  struct array_list *self = (struct array_list *) super;
  free(self);
}

int
array_list_get(const struct list *super, size_t i)
{
  const struct array_list *self = (struct array_list *) super;

  return self->inner[i];
}

size_t
array_list_len(const struct list *super)
{
  const struct array_list *self = (struct array_list *) super;

  return self->n;
}

struct iter *
array_list_iter(const struct list *super)
{
  struct array_list *self = (struct array_list *) super;
  return (struct iter *)array_list_iter_new(self);
}

struct array_list_iter *
array_list_iter_new(const struct array_list *array)
{
  struct array_list_iter *iter = malloc(sizeof(struct array_list_iter));
  if (! iter) {
    return iter;
  }

  iter->array = array;
  iter->i = 0;
  iter->super.fin = array_list_iter_fin;
  iter->super.next = array_list_iter_next;
  iter->super.has_next = array_list_iter_has_next;

  return iter;

}

void
array_list_iter_fin(struct iter *super)
{
  struct array_list_iter *self = (struct array_list_iter *)super;
  free(self);
}

int
array_list_iter_next(struct iter *super)
{
  struct array_list_iter *self = (struct array_list_iter *)super;
  int ret = self->array->super.get((struct list *)self->array, self->i);

  self->i++;

  return ret;
}

bool
array_list_iter_has_next(const struct iter *super)
{
  const struct array_list_iter *self = (struct array_list_iter *)super;
  return self->i < self->array->super.len((struct list *)self->array);
}
```

===
# OOP
-----

* オブジェクト(`iter_t`)にメッセージ(`has_next`、`next`)を送ってループを書いた
* インターフェース(`list_t`、`iter_t`)と実装(`array_list_t`、`array_list_iter_t`)を分離してコードを書いた
* データの中身を知らなくてもコードを書けた
* 具体的実装がなくてもコードを書けた

===

# FP的発想
----------

* 手続き的過ぎる
  + 1つ1つ順番に操作しないといけない
  + 順番に追っていかないと変数の中身もわからない
* もっと操作を抽象化しよう

===
# FP的記述

\\\[
\begin{align}
S\_0 &= 0 \\\\
S\_n &= S\_{n-1} + arr[n]
\end{align}
\\\]


===
# FP的記述

\\\[
\begin{align}
S\_0 &= 0 \\\\
S\_n &= f(S\_{n-1}, arr[n])
\end{align}
\\\]

===
# FPコード例(C言語)
-------------------

``` c++
int
reduce(const int array[], const size_t n, const int init, int(*f)(const int, const int))
{
  if (n == 0) {
    return init;
  } else {
    return f(reduce(array, n - 1, init, f), array[n - 1]);
  }
}


int
add(const int x, const int y)
{
  return x + y;
}

int
functional_sum(const int array[], const size_t n)
{
  return reduce(array, n, 0, add);
}
```

===

# FP
-----

* ループ(`reduce`)と中身(`add`)に分解してコードを書いた
  + 制御構造(`for`文)を関数にできた
* 副作用(変数の更新)を行わずにコードを書いた
* 宣言的になった

===
# OOPって実用的？
----------------
* メッセージパッシングの構文面倒
  ```
  obj->msg(obj)
  ```
* 遅くない？
  + 毎回関数ポインタ経由でメッセージ
  + ことある毎にオブジェクトをアロケート
* プリミティブどうするの
* メッセージ増やすとデータサイズが増えそう

===
# FPって実用的？
---------------

* 一々足し算する関数定義するの？
* データに依存したコードになってるけど大丈夫？
* 遅くない？
  + 毎回データのコピーが発生する
    - 今回の例では運良くintしかコピーしなかった
* 副作用使わずにプログラミングできるの？
  + ひとまずループは書けたけど他は？

===

# 答え
------
言語による<!-- .element: class="fragment" data-fragment-index="1" -->

* 対象にしているものが広すぎる<!-- .element: class="fragment" data-fragment-index="2" -->
* 具体的な言語抜きに語っても意味がない<!-- .element: class="fragment" data-fragment-index="2" -->

===
そのまえに

# XXX言語とは
------------

[関数型プログラミングの今昔](https://www.slideshare.net/ksknac/120901fp-key)
* オブジェクト指向(プログラミングを支援する)言語
* 関数型(プログラミングを支援する)言語
* マルチパラダイム言語もある
  + 複数のプログラミングパラダイムを支援
  + それらを混ぜて使うことも

===
# OOP言語色々
---------------------
* メソッド呼び出し構文があればOOPを支援(?)
  ```
  obj->msg(obj)
  ```
  が
  ```
  obj.msg()
  ```
  に
* クラスベース
  + 単一継承
    - Ruby Java C# ...
  + 多重継承
    - Python  C++ ...
* プロトタイプベース
  + Smalltalk JS ...
* その他
  + go rust ...


===

# クラスベース
---------------------
* メッセージはクラスが知っている
* 継承によるインターフェースと実装の継承

  > 「オブジェクトの階層構造をコストとして払う代わりに、メッセージの移譲は無料で手に入れられる」

  + ある意味では親と子の密結合

  > 「サブクラスがsuperを送らなければならないようなコードを書くと、さらに依存が追加されます。」
* リスコフの置換則
  + 親クラスはいつでもサブクラスに置き換えられるべき

===

<img src="/images/manabiya/class_method.png" width="100%" height="100%">

===
抽象の境界と差分プログラミングとスパゲッティコードの話

<img src="/images/manabiya/abstract.png" width="100%" height="100%">

===
抽象の境界と差分プログラミングとスパゲッティコードの話

<img src="/images/manabiya/bad_abstract.png" width="100%" height="100%">


===
# Java
------
* クラスベース単一継承
* 抽象クラスやインターフェースによる抽象化
* 遅くない？
  + → プリミティブ型はオブジェクトじゃない
  + → JITによる高速化
  + → GCアルゴリズムの改善
* 割とクラスの機能が強い
  + クラスが名前空間も兼任
  + スタンドアロンな関数が書けない（かった）
  + コールバックには無名クラスとか

===
# Java
------

``` java
abstract class Figure {
  void draw() {}
  abstract void move(int dx, int dy);
}

class Triangle extends Figure {
  Point a;
  Point b;
  Point c;

  @Override
  void draw() {
    drawLine(a, b);
    drawLine(b, c);
    drawLine(c, a);
  }

  @Override
  void move(int dx, int dy) {
    a.move(dx, dy);
    b.move(dx, dy);
    c.move(dx, dy);
  }

  void drawLine(Point from, Point to) {}

  class Point {
    int x;
    int y;

    void move(int dx, int dy) {
      x += dx;
      y += dy;
    }
  }
}
```

===
# Java
------

* 設計は難しい
* `drawLine` はだれが持つべき？
  + `drawLine` ってTriangleだけのものじゃないよね
  + 本来は `new Line().draw()` では？
  + でも毎回オブジェクト作るの？
* `ColoredTriangle` を作ろうとしたらどうする？
  + `drawLine` をオーバーライドする？
  + `new ColoredLine` にする？

===
# Ruby
-------

* クラスベース単一継承
* 遅くない？→気にしない
  + 生産性の方が大事
* ダックタイピング
  + メッセージに応答すればなんでもいい
* 数値や`+`などもオブジェクト/メソッド
* オープンクラス、モンキーパッチ
* クラスだけでなくモジュールも
  * mix-in
  * たとえばイテレータ相当のものは`Enumerable`モジュールが担当
  * `for`文相当のものは`each`で可能
* クラスの権限がそんなに強くない

===

# Ruby
-------
* for文なしでの繰り返し
  + ブロック構文

``` ruby
(1..10).each{|i| puts i}
```

* [ActiveSupport](https://railsguides.jp/active_support_core_extensions.html#time)による数値の拡張など
  + オープンクラス 数値もオブジェクト `+`もメソッド

```ruby
1.week - 2.days
```

===
# Go
------

* メソッド呼び出し構文がある
* クラスや継承はない
  + 代わりにインターフェースとインクルードがある

===
# Go
------

``` go
type Drawer interface {
	draw();
}
type Mover interface {
	move(int, int);
}



type Point struct {
	x int;
	y int;
}

func (p Point) move(dx int, dy int) {
	p.x += dx;
	p.y += dy;
}

type Triangle struct {
	a Point;
	b Point;
	c Point;
}

func (t Triangle) draw() {
	drawLine(t.a, t.b);
	drawLine(t.b, t.c);
	drawLine(t.c, t.a);
}

func drawLine(from Point, to Point) {}

func (t Triangle) move(dx int, dy int) {
	t.a.move(dx, dy);
	t.b.move(dx, dy);
	t.c.move(dx, dy);
}
```

===
# Go(拡張)
------

``` go
type Color struct {
	r int;
	g int;
	b int;
}

type ColoredTriangle struct {
	*Triangle;
	color Color;
}

func (t ColoredTriangle) draw() {
	drawColoredLine(t.a, t.b, t.color);
	drawColoredLine(t.b, t.c, t.color);
	drawColoredLine(t.c, t.a, t.color);
}


func drawColoredLine(from Point, to Point, color Color) {}
```

===

# 関数型言語色々
---------------
* ML系
 + SML
 + OCaml
 + F#
* Haskell
* Erlang
* Clojure

===
# ありがちな機能
---------------
* 破壊的変更できないorあまりしない
* 関数の便利な扱い
  + 無名関数
  + 演算子も関数
  + 関数合成
  + 高階関数
  + カリー化
* ADTとパターンマッチと網羅性検査
* ※「関数型 = Haskell」はHaskellプログラマの麻疹

===
# 便利な関数の扱い
-----------------
* 高階関数 演算子も関数 関数合成

``` sml
val sum = List.foldl op+ 0;
```

``` standard-ml
val inner_product = List.foldl op+ 0 o List.map op* o ListPair.zip;
inner_product ([1, 2, 3], [1, 2, 3]); (* => 14 *)
```

* カリー化

``` standard-ml
fun findManabiya list = List.find (String.isPrefix "manabiya") list
val findManabiya = List.find (String.isPrefix "manabiya")
```

* 無名関数

``` standard-ml
String.tokens (fn c => c = #" " orelse c = #"\n")
```

===
# ADTとパターンマッチ
--------------------

``` sml
datatype expr = Plus of expr * expr
              | Mul of expr * expr
              | Int of int

fun eval (Plus(e1, e2)) = eval e1 + eval e2
  | eval (Mul(e1, e2)) = eval e1 * eval e2
  | eval (Int(e)) = e

fun show (Plus(e1, e2)) = show e1 ^ " + " ^ show e2
  | show (Mul(e1, e2)) = show e1 ^ " * " ^ show e2
  | show (Int(e)) = Int.toString e

val () = let
    val expr = Plus(Int 1, Mul(Int 2, Int 3))
in
    print (show expr);
    print " = ";
    print (Int.toString (eval expr));
    print "\n"
end
```

Note:
クラスベースオブジェクト指向でやろうとするとvisitorパターンになってかなり面倒

===
# データコピーの話
------------------

* リストを2回コピーしてるけど遅くない？

``` standard-ml
fun inner_product l1 = let
  val l2 = ListPair.zip l1
  val l3 = List.map op* l2
in
  List.foldl op+ 0 l3
end
```

* もうちょっと一般に世の中のアルゴリズムを実装すると遅くない？

===
# データコピーの話
------------------

* リストを2回コピーしてるけど遅くない？
  + 言語による
  + [基本は10倍〜100倍遅いけど全く変わらない言語(処理系)もある](https://gist.github.com/KeenS/35345a4661dc696f467abd2de830568d)
    - 10倍しか遅くならないのはけっこう頑張ってる方
    - 関数型言語に向いたGCアルゴリズム(Copy GC)の採用
    - 最適化で消せる
* もうちょっと一般に世の中のアルゴリズムを実装すると遅くない？
  + A1. 遅い部分は諦めて副作用を使う
  + A2. 関数型向きデータ構造/アルゴリズムを使う
     - [純粋関数型データ構造](http://asciidwango.jp/post/160831986220/%E7%B4%94%E7%B2%8B%E9%96%A2%E6%95%B0%E5%9E%8B%E3%83%87%E3%83%BC%E3%82%BF%E6%A7%8B%E9%80%A0)
     - [関数プログラミング 珠玉のアルゴリズムデザイン](http://shop.ohmsha.co.jp/shopdetail/000000004066/)


===

# Clojure
---------

* デフォルトイミュータブルなLisp方言
* イミュータブルHashMap/Set
  + イミュータブルだけどデータを全部コピーする訳ではない
  + [HAMT](https://en.wikipedia.org/wiki/Hash_array_mapped_trie)
``` clojure
(aoosc {:name "κeen"} :age 25)
  ; ->{:age 25, :name "κeen"}
```

* 並列プログラミングに強い
  + データ競合が起きない

===
# SML
------
* 強い静的型付
* 普通に破壊的変更あるよ
* モジュールによるカプセル化
* ファンクタによる依存の注入

===
# SML
------
* モジュールによるカプセル化
  + データに対する操作を一箇所に集めるのは変わらない

``` standard-ml
structure MyList: sig
              type t
              val len: t -> int
              val get: t -> int -> int
          end = struct
    type t = int list
    val len = List.length
    fun get (x::xs) 0 = x
      | get (x::xs) n = get xs (n-1)
end

```

===
# SML
------
* ファンクタによる依存の注入

``` standard-ml
functor Make(Foldable: sig
                 type 'a t
                 val fold: ('a * 'b -> 'b) -> 'b -> 'a t -> 'b
             end) = struct
    val sum = Foldable.fold op+ 0
end
```

===
# Haskell(GHC)
----------
* 強い静的型付け
* 強力な型システム
* 型クラスによるデータ抽象
* 純粋
  + 破壊的変更とIOを基本許さない
  + 全て式になる
    - 雑にいうとセミコロンなしでプログラミングする
  + 入力からのみ出力が決まる → 型をみたら関数の中身が分かる
* 遅延評価
  + 必要になるまで値を計算しない
  + 純粋なのでプログラムの結果は変わらない
    - (細かいことを言うと無限ループの挙動が違うけど)
===
# Haskell(GHC)
----------

* 型クラスによるデータ抽象

``` haskell
{-# LANGUAGE NamedFieldPuns #-}

class Drawable a where
  draw :: a -> ()

class Movable a where
  move :: a -> (Int, Int) -> a


data Point = Point Int Int
  deriving Show

instance Movable Point where
  move (Point x y) (dx, dy) = Point (x + dx) (y + dy)

data Triangle = Triangle {
  a:: Point,
  b:: Point,
  c:: Point
}
  deriving Show

instance Drawable Triangle where
  draw _ = ()

instance Movable Triangle where
  move Triangle{a, b, c} d = Triangle {
    a = move a d,
    b = move b d,
    c = move c d
    }
```

===

# Haskell(GHC)
----------
> 雑にいうとセミコロンなしでプログラミングする

* 逐次処理はどうするの？
  1. プログラムを値として扱って合成する
    ```haskell
    Program a -> Program b -> Program b
    ```
  2. 直前の値も受け取れる
    ```haskell
    Program a -> (a -> Program b) -> Program b
    ```
  3. 色々な種類のプログラムに対応可能
    ```haskell
    m a -> (a -> m b) -> m b
    ```
  4. 具体的には`>>=`という演算子で合成
     ```haskell
     getLine >>= putStrLn
     ```
  5.シンタックスシュガー
    ```haskell
    do
      s <- getLine
      putStrLn s
    ```

===

# Haskell(GHC)
----------
* 遅延評価
  + 計算量が変わる
    `tarai(12, 6, 0)`で2,604,860回 vs 110回
  + 同等のCのコードよりずっと速い

``` haskell
tarai:: Int -> Int -> Int -> Int
tarai x y z = if x <= y
              then y
              else tarai (tarai (x-1) y z) (tarai (y-1) z x) (tarai (z-1) x y)
```

``` c
int
tarai(int x, int y, int z)
{
  if (x <= y) {
    return y;
  } else {
    return tarai(
                 tarai(x - 1, y, z),
                 tarai(y - 1, z, x),
                 tarai(z - 1, x, y)
                 );
  }
}
```


===

# 関数型言語のOOP
-----------------
* OCamlのO
* SMLのモジュールは割とOOPに似てる？
* `|>` は割とメソッドチェーンに似てる？

``` elixir
1..999
 |> Enum.filter(&(rem(&1, 3) == 0 || rem(&1, 5) == 0))
 |> Enum.sum
 |> IO.puts
```

===
# オブジェクト指向言語のFP
-------------------------

* 高階関数
  + Rubyのブロックも
* JavaのStreaming API
  + FP in Java
* typeclassやADT
  + RustやSwift

===
# 結局どういう関係なの？
----------------------

* 大きな部分では変わらない
  + 関心毎にコードを集めて粗結合な部品を組み立てる
* オブジェクト指向は設計より
* 関数型はコーディングより
* 完全に相反するものでもない
  + マルチパラダイム言語
* 相性の悪い点もある

===
# プログラミング言語のこれから
--------------------------

* 今回挙げた言語はかなり古い言語
  + Ruby, Java, Haskell, SMLは20年以上前に出来た
* 古い言語は当時技術を元に設計される
  + ハードウェア
  + コンパイル技法
  + ベストプラクティス
* これからは新しい概念、いいとこ取りの言語設計も出てくる？
  + 並列並行サポート
  + ADTとパターンマッチ、無名関数
  + 所有権
  + などなど

===
# まとめ
--------

* オブジェクト指向/関数型とはパラダイムのことだよ
* オブジェクト指向/関数型とはそのパラダイムを支援する言語のことだよ
  + 言語とパラダイムの区別を明確に！
* それぞれ目的もアプローチも違うよ
* 両方手札に持って使い分けようね
* これ以外にも新しい言語にも注目


</script>
</section>

