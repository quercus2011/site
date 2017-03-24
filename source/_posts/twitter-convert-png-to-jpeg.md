---
title: Twitter が PNG 画像を JPEG に強制変換
date: 2017-03-07 14:29:34
tags:
---
今まで知らなかったのですが、Twitter でツイートに添付した PNG 画像は JPEG に強制的に変換されるようです。

JPEG への強制変換を回避するためには、PNG 画像にアルファチャネルを追加して、
さらに、（半）透明なピクセルが１個以上含まれるようにしなければならないようです。

たとえば、
FF14 の Windows クライアントで「高品質」設定のスクリーンショットを撮ると、
アルファチャネルを含まない PNG 画像として保存されるため、
そのまま Twitter に up すると JPEG に変換されてしまいます。

せっかくキレイな SS が撮れるのに、もったいない！

SS 加工とかされている方は要注意です。

この問題への対策として、
JPEG への強制変換を避けるために PNG 画像を加工してくれるツールが公開されています。
というか、このツールの紹介記事（窓の杜）でこの問題を知ったのでした。

 - Twitterにアップする画像の劣化を防ぐ「Twitter向け画像最適化ツール」 - 窓の杜    
   http://forest.watch.impress.co.jp/docs/serial/netserv/1047319.html
 - Twitter向け画像最適化ツール - SDN Project    
   https://sdn-project.net/labo/twitter_image.html

このツールは、「左上1ピクセルを透明度99%にする事で実現しています」とのことです。
すばらしいアイディアです。

作者の[栃尾トメさん](https://sdn-project.net)に感謝！


{% blockquote %}
★2017/Mar/24 追記★

Windows デスクトップクライアントの OpenTween が最新版 1.3.7 で
この問題に対応してくれました！　感謝！！

https://ja.osdn.net/projects/opentween/

バージョンアップしてもデフォルトでは機能が OFF になっているので、
「ファイル」メニューの「設定」ダイアログを開いて、「動作」の「投稿」のページで、
「PNG画像の投稿時にJPEGへの変換を回避する（pic.twitter.com のみ）」
にチェックを入れてください。

ちなみに対処方法は「Twitter向け画像最適化ツール」と同じです。
{% endblockquote %}


## おまけ

実際に Twitter に PNG 画像を投稿してみて、挙動を確認してみました。
(2017/Mar/07)

実験その１。
まず、アルファチャネルの無い PNG 画像をツイートしてみます。

{% asset_img bg20170129b.png "アルファチャネルの無い PNG 画像" %}

https://twitter.com/quercus_maris/status/838803302661808128

上記ツイートに Twitter Web でアクセスして画像をダウンロードしようとすると、
JPEG 画像になっていることがわかります。

実験その２。
[画像編集ソフト GIMP](https://www.gimp.org)
で単にアルファチャネルを追加しただけの PNG 画像を作って、ツイートしてみます。

{% asset_img bg20170129b-add-alpha-channel.png "単にアルファチャネルを追加しただけの PNG 画像" %}

https://twitter.com/quercus_maris/status/838804383513006080

上記ツイートにアクセスしてみると、これも JPEG 画像になってしまっています。

実験その３。
左上隅の１ピクセルだけ切り取って透明にした PNG 画像を作って、
ツイートしてみます。

{% asset_img bg20170129b-transparent.png "左上隅の１ピクセルだけ切り取って透明にした PNG 画像" %}

https://twitter.com/quercus_maris/status/838806270173827072

上記ツイートにアクセスしてみると、今度は PNG 画像としてダウンロードできました！

以上の実験から、単にアルファチャネルを追加するだけではダメで、
少なくとも１ピクセルは（半）透明でなければならないようです。

「Twitter向け画像最適化ツール」の手法はおそらく最善の手かと思われます。


{% raw %}
<!--
## おまけ２

念のため、画像処理ツール ImageMagick を使って PNG 画像の比較をしてみました。

 - ImageMagick 公式サイト    
   https://www.imagemagick.org
 - ImageMagickで2枚の画像を比較 - Qiita    
   http://qiita.com/kwst/items/c40817b3cdf841995257

ちなみに、ImageMagick は Windows 上でも使えます（使っています）。

 - 画像１：オリジナル画像<br />
   {% asset_link bg20170129b.png %}
 - 画像２：画像１の左上隅の１ピクセルだけ透明にした画像<br />
   {% asset_link bg20170129b-transparent.png %}
 - 画像３：画像２をツイートして Twitter からダウンロードした画像<br />
   {% asset_link bg20170129b-transparent.download.png %}
 - 画像４：画像１を「Twitter向け画像最適化ツール」で変換した画像<br />
   {% asset_link bg20170129b_tw.png %}

まず、ふつうに画像１と画像２を比較してみると、「一致」と言われてしまいます。

```bash
$ magick composite -compose difference bg20170129b.png bg20170129b-transparent.png bmp:- | magick identify -verbose -format "%[mean]" bmp:-
0
$
```

これは、左上隅の１ピクセルだけ透明にする際、色情報 (RGB) には手を加えず、
アルファ値（透明度）だけ `0` にしているため、
RGB のみで比較すると同一と判断されてしまったものです。

アルファ値を含めて（RGBA で）比較すると、ちゃんと差が出ます。

```bash
$ magick convert bg20170129b.png -alpha Set -channel RGBA -channel-fx 'alpha=100%' zzz.png


$ magick composite -compose difference -channel RGBA zzz.png bg20170129b-transparent.png zzz.bmp
$ magick composite zzz.png -channel Alpha bg20170129b-transparent.png -channel Alpha -compose difference zzz.bmp



$ magick identify -verbose -format "%[mean]" zzz.bmp






$ magick convert bg20170129b.png -alpha Set -channel RGBA -channel-fx 'alpha=100%' png:- | magick composite -channel RGBA -compose difference png:- bg20170129b-transparent.png bmp:- | magick identify -verbose -format "%[mean]" bmp:-
0
$
```
-->
{% endraw %}
