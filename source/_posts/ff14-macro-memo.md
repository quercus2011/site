---
title: マクロめも
date: 2017-02-16 11:11:18
tags:
  - FF14
  - Memo
---
FF14 のマクロに関するメモです。

 - テキストコマンドの一覧（公式）    
   http://jp.finalfantasyxiv.com/lodestone/playguide/win/text_command/
 - マクロ - FF14 Online Wiki    
   http://ff14wiki.info/?%E3%83%9E%E3%82%AF%E3%83%AD
 - テキストコマンド - FINAL FANTASY XIV n Wiki    
   http://ff14n.wikiwiki.jp/?%A5%C6%A5%AD%A5%B9%A5%C8%A5%B3%A5%DE%A5%F3%A5%C9


## グラウンドターゲットスキル発動マクロ

まりすはパッチノートを読んでも気がつかなかったのですが、
Patch 3.2 からグラウンドターゲットスキルの設置場所として
代名詞によるターゲット指定ができるようになっていました。

 - [Patch 3.2 パッチノート](http://jp.finalfantasyxiv.com/lodestone/topics/detail/7abc9fa4bbf7e73d1c94eaaeea46fcff603aa97a)
 - FF14 グラウンドターゲットスキルのマクロ関連いろいろ - Eorzean    
   http://www.eorzean.info/archives/3638082.html


たとえば、

```
/ac アサイラム <me>
```

というマクロを発動させると、自分の足元にアサイラムが設置されます。

また、

```
/ac フレイミングアロー <t>
```

とすれば、ターゲットしている敵の足元にフレイミングアローが設置されます。

まりすはグラウンドターゲットの指定動作が苦手で
ずっとまともに使えていなかったのですが、
このマクロのおかげで使えるようになってきました。

Eorzean さまに感謝！


## マウスオーバーでケアル

親指ボタンの付いた多機能マウスを使っている白魔道士向けのマクロです。

```
/micon ケアル
/ac ケアル <mo>
```

まりすは Logicool G602 マウスを愛用していて、
６個の親指ボタンに `Ctrl+3` ～ `Ctrl+8` を割り当てています。

Windows 版の FF14 クライアントでは、デフォルトでホットバー１に
`Ctrl+1` ～ `Ctrl+=` が割り当てられているので、
たとえば上記マクロをホットバー１のスロット３とかにセットすると、
パーティーリスト上で親指ボタンを押すだけでケアルが発動します。

まりすは白魔道士のとき
「左手ゲームパッド（移動）、右手マウス（アクション）」
というプレイスタイルなのですが、
基本的にマウスカーソルはパーティーリスト上にあります。
パーティーメンバーがどこにいても（ケアルが届く範囲にいれば）
即座に発動できるので、とても楽です。

ちなみに親指ボタンに割り当てているアクションは
「エスナ」「ケアル」「テトラグラマトン」
「リジェネ」「ケアルラ」「ベネディクション」の６個です。
範囲魔法はパーティーリストのすぐ横に置いた縦ホットバーにセットしてあります。


## HB/XHB の共有・非共有の一括切り替え

まりすの HUD 設定では、バトル職のときは HB/XHB 非共有モード、
クラフター＆ギャザラーのときは HB/XHB 共有モード、としています。
ちなみに HB4 と XHB8 は常に共有モード（マウント呼び出しとか用）、
XHB1-3 は常に非共有モードです。

この切り替えを簡単に行うため、簡単なマクロを作りました。

```
/hotbar share 1 off
/hotbar share 2 off
/hotbar share 3 off
/hotbar share 5 off
/hotbar share 6 off
/hotbar share 7 off
/hotbar share 8 off
/hotbar share 9 off
/hotbar share 10 off
/crosshotbar share 4 off
/crosshotbar share 5 off
/crosshotbar share 6 off
/crosshotbar share 7 off
```

```
/hotbar share 1 on
/hotbar share 2 on
/hotbar share 3 on
/hotbar share 5 on
/hotbar share 6 on
/hotbar share 7 on
/hotbar share 8 on
/hotbar share 9 on
/hotbar share 10 on
/crosshotbar share 4 on
/crosshotbar share 5 on
/crosshotbar share 6 on
/crosshotbar share 7 on
```

で、ポイントは、
これらのマクロをお互いのホットバーの同じ位置
（たとえばホットバー10のスロット12）にセットすること、です。

そうすると、同じ場所を押すたびにモードがトグルします。
わかりやすくてオススメです。

{% asset_img hotbar_sample_20170219a.png "ホットバーの例" %}

ちなみに「着替えマクロ」はバトル職（白魔道士と吟遊詩人）だけ作りました。
クラフター８職＋ギャザラー３職で11枠もマクロを作りたくなかったのです。
共有モードのホットバーにギアセットをセットして着替えています。
たとえば白魔道士から園芸師に着替える場合、
上記マクロを押してホットバーを共有モードに切り替えると
園芸師ギアセットアイコンが出現して、
それを押せば園芸師になれます。
一発で着替えられないのは不便に思うかもしれませんが、
逆に言うと誤爆が避けられるので安全だったりします。


## クラフターのアディショナル一括設定

まりすの場合、クラフターのアディショナルとして使うアクションは決まっていて、
どのクラスでも同じクラフター製作マクロが使えるようにしています。
（たぶんマイスターになるとスキル回しも変わってくると思いますが）

クラスごとに「自クラス以外のものぜんぶ」を設定することになるわけですが、
面倒なので全部列挙してしまうことにしました。
自クラスのものは自動的にスキップしてくれるので、1個のマクロで全クラス使えます。

```
/additionalaction clear
/additionalaction 模範作業II on
/additionalaction ヘイスティタッチ on
/additionalaction 倹約 on
/additionalaction ステディハンドII on
/additionalaction ビエルゴの祝福 on
/additionalaction コンファートゾーン on
/additionalaction マニピュレーション on
/additionalaction 工面算段II on
/additionalaction 堅実の心得 on
/additionalaction 堅実作業 on
/additionalaction イノベーション on
/additionalaction 確信 on
/additionalaction 秘訣 on
/additionalaction 突貫作業 on
```


## クラフターの XHB 一括設定

クラフターの XHB って、共有モードにしておけば良いじゃないか、
と思われるかもしれませんが、
実は「作業」とか「中級加工」とかのアクションは同じ名前でも
クラスごとに別アクションになっています。
（理由は謎・・・・ "4.0" で改善されそうな気も）

そこで、一括設定マクロを使うわけです。

```
/crosshotbar set 蒐集品製作           1 RAR
/crosshotbar set 蒐集品製作           2 RAR
/crosshotbar set 蒐集品製作           3 RAR
```

```
/crosshotbar set イノベーション       1 RAL
/crosshotbar set 確信                 1 RAU
/crosshotbar set 中級加工             1 RAD
/crosshotbar set インナークワイエット 1 LAL
/crosshotbar set 堅実の心得           1 LAU
/crosshotbar set 堅実作業             1 LAR
/crosshotbar set コンファートゾーン   1 LAD
/crosshotbar set 倹約                 1 RDL
/crosshotbar set ヘイスティタッチ     1 RDU
/crosshotbar set 模範作業II           1 RDR
/crosshotbar set ステディハンドII     1 RDD
/crosshotbar set マニピュレーション   1 LDL
/crosshotbar set ビエルゴの祝福       1 LDU
/crosshotbar set グレートストライド   1 LDR
/crosshotbar set 工面算段II           1 LDD
```

```
/crosshotbar set イノベーション       2 RAL
/crosshotbar set 確信                 2 RAU
/crosshotbar set 中級加工             2 RAD
/crosshotbar set インナークワイエット 2 LAL
/crosshotbar set 秘訣                 2 LAU
/crosshotbar set 突貫作業             2 LAR
/crosshotbar set コンファートゾーン   2 LAD
/crosshotbar set 倹約                 2 RDL
/crosshotbar set ヘイスティタッチ     2 RDU
/crosshotbar set 模範作業II           2 RDR
/crosshotbar set ステディハンドII     2 RDD
/crosshotbar set マニピュレーション   2 LDL
/crosshotbar set ビエルゴの祝福       2 LDU
/crosshotbar set グレートストライド   2 LDR
/crosshotbar set 工面算段II           2 LDD
```

ちなみに XHB3 はマイスター用に予約してあります（現時点では使っていません）。


## ひとつのジョブで複数の HB/XHB 設定を使いたい

たとえば白魔道士で、PvE と PvP とで HB/XHB 設定を変えたい場合があります。

そんなときは、「自分が今後絶対に使わないであろうと思われる」ジョブを決めて、
そのジョブの非共有 HB/XHB を待避先に使います。
未習得のジョブでも OK です。

たとえば、まりすの場合、機工士と召喚士をやることはたぶん無いので、
以下のふたつのマクロを使えば XHB1-7 を丸ごと切り替えられます。

```
/crosshotbar copy current  1 機工士  1
/crosshotbar copy current  2 機工士  2
/crosshotbar copy current  3 機工士  3
/crosshotbar copy current  4 機工士  4
/crosshotbar copy current  5 機工士  5
/crosshotbar copy current  6 機工士  6
/crosshotbar copy current  7 機工士  7
/crosshotbar copy 召喚士  1 current  1
/crosshotbar copy 召喚士  2 current  2
/crosshotbar copy 召喚士  3 current  3
/crosshotbar copy 召喚士  4 current  4
/crosshotbar copy 召喚士  5 current  5
/crosshotbar copy 召喚士  6 current  6
/crosshotbar copy 召喚士  7 current  7
/hotbar      copy 召喚士  9 current  9
```

```
/crosshotbar copy current  1 召喚士  1
/crosshotbar copy current  2 召喚士  2
/crosshotbar copy current  3 召喚士  3
/crosshotbar copy current  4 召喚士  4
/crosshotbar copy current  5 召喚士  5
/crosshotbar copy current  6 召喚士  6
/crosshotbar copy current  7 召喚士  7
/crosshotbar copy 機工士  1 current  1
/crosshotbar copy 機工士  2 current  2
/crosshotbar copy 機工士  3 current  3
/crosshotbar copy 機工士  4 current  4
/crosshotbar copy 機工士  5 current  5
/crosshotbar copy 機工士  6 current  6
/crosshotbar copy 機工士  7 current  7
/hotbar      copy 機工士  9 current  9
```

ひと工夫して、ホットーバー9のスロット12あたりに上記マクロをセットして、
同じボタンでトグルできるようにすると、便利＆確実です。
上記マクロは同じものを２回実行すると他方が上書きされてしまう危険があるので・・・。
あるいは、保存用マクロと切り替えマクロは分けたほうが安全かもしれません
（ホットバーも同時に切り替えようとするとそもそも15行に収まらないし）。


## ピーアンマクロ

 - FF14 固定PT用ピーアンマクロ - Eorzean    
   http://www.eorzean.info/archives/2785161.html


## ギルドリーヴ納品用移動マクロ

同じマップに受注 NPC と納品先 NPC がいる場合、
自動で起動できるみたいです。

 - FF14 ギルドリーヴ納品用移動マクロ    
   http://www.eorzean.info/archives/3135969.html
