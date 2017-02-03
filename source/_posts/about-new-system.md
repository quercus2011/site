---
title: 新ブログのシステムについて
date: 2017-02-03 14:33:36
tags:
 - Technical
---
新ブログの技術的なお話です。

この新ブログは、
[Hexo](https://hexo.io) というソフトウェアを使ってコンテンツを生成して、
[GitHub Pages](https://help.github.com/categories/github-pages-basics/)
上で運用しています。

この新ブログを構築するためのファイル（投稿記事の原稿を含む）は、
すべて GitHub 上で公開されています。    
https://github.com/quercus2011/site

ご質問などあれば、お気軽にどうぞ。


## Hexo とは

[Hexo](https://hexo.io) というのは、
ブログみたいなサイトを自動生成してくれるソフトウェアです。

一般的にブログ構築システムというと Wordpress とか MovableType とかが有名ですが、
それらはコンテンツを動的に（ユーザーがサーバーにアクセスしたときに）生成するのに対し、
Hexo はすべてのコンテンツのファイルを事前に一括生成してしまうのが大きな違いです。
静的サイトジェネレータ (Static Site Generator, SSG) と呼ばれています。
Hexo 以外にも Jekyll とかが知られています。

Hexo は [Node.js](https://nodejs.org) という JavaScript 処理系で動くプログラムです。
Web ブラウザ向けの JavaScript が書ける人なら、
ある程度ソースコードが読めるのが利点です。
あと、処理速度が速いと言われています。

もともと趣味で [Hexo のソースコード](https://github.com/hexojs/hexo/)を改造したりしていたので、
この新ブログはその実証実験的な意味合いもあります。

Hexo はいちおう Windows 上でも動くらしいですが（Mac でも動く）、
クラウド上の仮想サーバ (VPS) に Linux (Ubuntu) をインストールして、
その上で実行しています。

Hexo では「テーマ」を選ぶことでサイトのデザイン（見た目）を簡単に変えられます。
また、HTML/CSS/JavaScript の知識があれば、テーマを自由にカスタマイズすることができます。
この新ブログは、[Charles Zheng さん](https://github.com/chaooo) が作られた
[BlueLake というテーマ](https://github.com/chaooo/hexo-theme-BlueLake)をベースに、
[独自にカスタマイズしたテーマ](https://github.com/quercus2011/hexo-theme-BlueLake)を使用しています。


## GitHub Pages とは

What is GitHub Pages? - GitHub    
https://help.github.com/articles/what-is-github-pages/

静的な Web サイトを無料で運用できるサービスです。
CGI とか PHP とか Ruby とか Perl とかは動かせません。    
<small># なので、このブログにはコメント機能がまだありません（実装する方法はあります）</small>

デフォルトで HTTPS 化されているのが素晴らしいです。
正直、FF14 の公式サイトとかフォーラムとかが HTTPS 化されていないのが残念。

広告が入らないのも大きな利点です。

[GitHub](https://github.com) の提供するサービスなので、当然ながら、
分散バージョン管理システム Git の恩恵をフルに受けることができます。
過去の変更履歴をたどったり、誤った変更を元に戻したり、
手元で変更を加えて十分に動作確認してから正式に公開したり、
派生版を作ったり、簡単にできます。

個人的に運営している Web サイトは自前の Web サーバで運用していますが、
Git と HTML がわかる人なら GitHub Pages はお手軽でオススメです。


## 雑感

FC2 blog は無料ブログの中ではかなり自由度の高いところだと思いますが、
今後、スクリーンショット画像が増えていくと管理が大変になりそうな予感もあり、
移転することにしました
（あと、HTTPS 化したいとかスマホ対応が微妙とか広告が邪魔とかも理由）。

とりあえず、過去の投稿記事の原稿とかが手元に残っている（Git でバージョン管理できる）
というのは精神衛生上とてもよいです。

ちょっと敷居が高いかもしれませんが、オススメです。

ご質問とかあればお気軽にご連絡ください。
連絡先はサイドバーに書いてあります。
もちろんゲーム内でコンタクトしていただいても OK です。
