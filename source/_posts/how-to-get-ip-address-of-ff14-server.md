---
title: FF14 サーバの IP アドレスを調べる方法（Windows 版限定）
date: 2018-03-06 11:29:00
tags:
 - Technical
 - FF14
---

Windows 版 FF14 クライアントでプレイ中に、通信相手の FF14 サーバの IP アドレスを調べる方法を解説します。
特別なツールは要りません。Windows に最初からインストールされているプログラムだけで可能です。

なお、FF14 クライアントプログラムやメモリ上のデータには一切触らないので、
FF14 規約には抵触しないと思います。

<!-- toc -->


## まえがき

FF14 に限らずオンラインゲームの分野で広く使われる「ping 値」という言葉があります。
「ping 値」は、ゲームクライアントとサーバとの通信状態を表す指標のひとつです。

サーバの「ホスト名」か「IP アドレス」がわかれば、
「ping 値」は Windows 標準のツールで簡単に測定できます。

⇒ {% post_link how-to-measure-ping-value %}

FF14 のプレイ中に正確な「ping 値」を測定するためには、
FF14 のゲームサーバの IP アドレスを知る必要があります。

いちおうデータセンターごとの IP アドレスを掲載してくれている非公式サイトもあるのですが、
わたしの環境では異なる IP アドレスのサーバと通信していたので、
あくまで参考程度にしかならない模様です。

- ARRstatus - FFXIV Server Status   
  https://arrstatus.com


## FF14 サーバの IP アドレスを調べる方法

Windows にデフォルトでインストールされている `netstat` コマンドを使うと、
現在 Windows 上で行われているすべてのネットワーク通信をリストアップしてくれます。
そのリストには、「通信相手の IP アドレス」や「どのプログラムが通信しているのか」という情報も含まれています。

普通に `netstat` コマンドを実行すると、大量のログが出力されてしまって読めません。
そこで、出力をテキストファイルに「リダイレクト」して、そのテキストファイルをメモ帳で開いて「検索」します。

まず、適当なフォルダで「コマンドプロンプト」を開きます。
たとえば、エクスプローラーで「マイドキュメント」を開いて、そのアドレス欄に「`cmd`」と入力して ENTER キーを押します。

{% asset_img SS_20180208a0a_explorer_Documents.png "エクスプローラーで「マイドキュメント」を開く" %}

↓

{% asset_img SS_20180208b0a_explorer_input_cmd.png "アドレス欄に「cmd」と入力して ENTER" %}

↓

{% asset_img SS_20180208c0a_cmd_initial.png "「コマンドプロンプト」が開く" %}

コマンドプロンプト上で、`netstat -a -b -n > z.txt` と入力して ENTER キーを押します。

{% asset_img SS_20180208d0a_cmd_netstat_input.png "コマンドを入力" %}

実行しても何も表示されず、数秒以内に完了して、新しいプロンプトが表示されるハズです。
（`netstat` コマンドの出力先をディスプレイからテキストファイル `z.txt` に変更しているため、何も表示されないのです）

{% asset_img SS_20180208e0a_cmd_netstat_done.png "実行した結果" %}

次に、このテキストファイル `z.txt` を「メモ帳」で開きます。

エクスプローラーで `z.txt` を開いてもいいのですが、
コマンドプロンプト上で `notepad z.txt` と打ち込んだほうが早いです。

{% asset_img SS_20180208f0a_cmd_notepad_input.png "メモ帳を起動" %}

「メモ帳」が起動すると、次のようなウインドウが表示されるハズです。

{% asset_img SS_20180208g0a_notepad_initial.png "メモ帳の初期画面" %}

ここで `Ctrl-F` を押すと、「検索」ダイアログが開くので、「`ffxiv`」と入力します。

{% asset_img SS_20180208h0a_notepad_searching.png "「検索」ダイアログに「ffxiv」と入力" %}

ENTER キーを押すと、検索先に飛びます。

{% asset_img SS_20180208i0a_notepad_searched.png "検索先に飛ぶ" %}

DirectX11 版のクライアントを起動していれば、このように「`ffxiv_dx11.exe`」がヒットするハズです。

検索にヒットした行の前の行の3列目が、FF14 クライアントの通信相手（つまり FF14 サーバ）のアドレスです。

{% asset_img SS_20180208j0a_notepad_marking.png "FF14 サーバのアドレスが読める" %}

サーバのアドレスは、「IP アドレス + コロン (`:`) + ポート番号」という表記になっています。
コロンの直前までの「ピリオドで区切られた4個の数字の組」が IP アドレスです。
上記の例では「`124.150.157.25`」ということになります。

試しに `ping` コマンドを実行してみると、「ping 値」が測定できます。

{% asset_img SS_20180208k0a_cmd_ping_input.png "ping コマンドを入力" %}

↓ （最後に ENTER キーを押すと実行される）

{% asset_img SS_20180208l0a_cmd_ping_running.png "ping コマンドを実行すると測定が始まる" %}

↓ （`Ctrl-C` で停止）

{% asset_img SS_20180208m0a_cmd_ping_stopped.png "ping コマンドによる測定結果" %}

この例では、「ping 値」は「16ms」ということになります。


## おまけ（スクリプト化）

Git for Windows というフリーソフトをインストールした環境では、
シェルスクリプトを利用できます。

※ Windows 10 公式機能の Bash on Windows (BoW) / Windows Subsystem for Linux (WSL) とは別モノです。*Windows 7 でも使えます。*

- Git for Windows   
  https://gitforwindows.org

わたしの使っている「FF14 サーバとの ping 値を5分おきに自動測定するシェルスクリプト」を GitHub で公開しています：

- https://gist.github.com/quercus2011/4e9b92a54181a3eb559e4936dcaa4d1a

このシェルスクリプトを実行すると、5分おきに FF14 クライアントが起動しているかチェックして、
起動していたら、その通信相手（FF14 サーバ）に ping を10回投げて、
結果を CSV ファイルに追記していきます。

別の `bash` ウインドウで `tail -f` コマンドとか使えば、その CSV ファイルを監視できます。

このスクリプトは MIT ライセンスとしますので、ご自由にお使いください。
改造などもお好きなように。
もちろん無保証・自己責任なのはお約束です。
