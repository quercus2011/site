---
title: Bandicam から After Effects へ
date: 2014-06-05 22:23:00
tags:
  - Video
  - ImportedFromFC2
imported_from: http://quercus2011.blog.fc2.com/blog-entry-35.html
---
動画編集やりたい、ということで、まったくのシロウトにもかかわらず、
<a href="http://www.adobe.com/jp/products/aftereffects.html">Adobe After Effects</a>
にチャレンジすることにしました！
<!-- more -->

無謀かもですが、まぁ、がんばってみる。
月 5000 円の課金も覚悟しました。
入門書も買ってきました！



で、さっそく遊んでみようと思ったのですが、ひとつ問題が発生。
Bandicam で録画した動画ファイルを取り込もうとするとエラーに！

<a href="http://www.videolan.org/">VLC media player</a>
で問題なく再生できていたので気がつかなかったのですが、
どっか違う avi ファイルのようです。

<a href="http://www.kurohane.net/">真空波動研Lite</a>
で見てみても異常はなさそうなのですが、
TMPGEnc 4.0 XPress でも取り込みエラーになったので、
やっぱりなにか違うのかもしれません。
<a href="http://sourceforge.jp/projects/ecodecotool/">えこでこツール</a>
でもエラーになったし。

ためしに Bandicam と同じ開発元の
<a href="http://www.gomplayer.jp/encoder/">GOM ENCODER</a>
体験版で mp4 ファイルに変換してみたところ、問題なく After Effects に取り込めました。
しかしながら、再エンコードされてしまうのがとっても残念・・・・。


ふと、avi コンテナの問題かもしれないと思って、
再エンコード無しにコンテナだけ mp4 に変換できないか調べてみると、
<a href="http://phperera.wordpress.com/">Video Container Changer</a>
というフリーソフトを発見！

さっそく試すと、とくに設定とか無しにあっさり mp4 に変換できました。
動画データを再エンコードしないからあっという間に変換完了。
できた mp4 ファイルを After Effects に食べさせてみるとあっさり OK。
「TMPGEnc 4.0 XPress」でも「えこでこツール」でも OK でした。


というわけで、

    Bandicam ⇒ Video Container Changer ⇒ After Effects

というパスを確立することができました！


ちなみに、もしかすると、Bandicam でコーデックを「H264 (CUDA)」に
しているのが原因かもしれません。こんど Xvid でも試してみます。    
<small># 試そうとしたら FF14 緊急メンテでログインできず・・・・</small>
