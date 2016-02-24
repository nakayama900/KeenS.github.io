---
categories: [isucon, isucon5]
date: 2015-09-27T23:58:24+09:00
title: isucon にCommon Lispチームで出た
---
κeenです。 [isucon](isucon.net) に[@nitro_idiot](https://twitter.com/i/notifications?lang=ja)(深町さん)と[@Rudolph_Miller](https://twitter.com/Rudolph_Miller?lang=ja)のCommon Lispチームで出てきました。チーム名clfreaks。勿論Common Lispで再実装しました。
<!--more-->
因みに深町さんは今回使ったWebサーバーのwooを含めCommon Lispのライブラリを多数公開している[世界一のCommon Lisper](http://github-awards.com/users/search?login=fukamachi)、ルドルフさんは元Common Lispの会社のCTO。

# 前日
κeen 「あとはwooがunixソケット使えたら嬉しいんですがまあ、いいでしょう。」  
fukamachi 「今からやれば明日には間に合うな」  
fukamachi 「ローカルでは一応動いた。間に合いそうである」  
fukamachi 「5倍ちょっとくらい速いかな」  


この間1時間半足らず。



κeen 「練習してて気付いたんですけどデプロイツールってどうしましょう。」  
fukamachi 「κeenさんが使い慣れてるツールで良いです」  
κeen 「シェルスクリプトかー。」  
fukamachi 「やめろ」  


結局capistranoを使うことに。


# 当日の作業

私がマシン立ち上げてソースをgitに上げるまでやる。残りの二人はソースを読む、私はNginXやMySQLやCapistranの基本設定をする。

## 午前中 Common Lispでの再実装
ルドルフさんが見付けた遅い部分を書き出し、深町さんがCommon Lispの実装を進める。

私がmysqlの設定をするもなぜか反映されずに詰まる。ルドルフさんと一緒にやるも数時間やっても解決せず。結局新しいインスタンスを立ち上げたら動いた。my.cnfにsym linkを貼ったのが問題だったよう。/etc/my.cnfの問題ではない。

## 午後 実装を進めつつチューニング
私の方がどうにかなったのでルドルフさんも実装をすすめる。私はインデックスを張ろうとしてalterが帰ってこなくて諦めたりどうせ使わないけどunicornのワーカー数を増やして気分だけでもスコアを上げたりN+1クエリをJOINで書き直したり。

## Comon Lispの実装がとりあえず終了
バグは残ってる、と言われつつCL実装をmasterにマージしたのがgitのログを見るに15:28。そこからデバッグ。色々ハマったりライブラリにバグがあったり（深町さんのライブラリだったのでその場でbug fix）してログイン処理が通ったのが17時くらい？そこからベンチマークを走らせるとまたtypoとかのバグがあってちまちま直していくも結局間に合わず0点のままFINISH。

# 反省とか
思ったよりアプリケーションが重厚で再実装に時間取られすぎたなー、が一番。あとMysqlの設定でハマったのは本当にやりたくなかった。

ベンチマーク走らせるとデータが溜まることに気付かずに大分走らせた後でインデックスを張ろうとしたら20分くらい待っても帰ってこなかったのでインデックスを諦めた。なのでruby実装のスコアも800点くらい。
やろうとしたことはN+1クエリを消すとかuserをメモリに載せるとか。

かなり苦い思いはしたけどCommon Lispに足りないものとか今後の課題とかも見えたし出た価値はあったと思う。例えばデプロイの度にコンパイルが走るが、コンパイルの重いライブラリを使ってるとデプロイが遅くなるので並列ビルド欲しいよね、とか。ただ、大きな目的だったWeサーバーのチューニングまではいけなかった。

今年は知り合いと出ちゃったので来年は知らない人とチームを組もうかと。

運営、出題の方々、お疲れ様でした。来年こそは本戦出ます。