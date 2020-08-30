---
title: 【ゼロからDeepLearningをつくる】ニューラルネットワークとパーセプトロン
author: KAORU
type: post
date: 2020-01-27T02:45:02+00:00
url: /neuralnetwork-perceptron/
featured_image: /wp-content/uploads/2020/01/alina-grubnyak-ZiQkhI7417A-unsplash-scaled.jpg
categories:
  - Data science
  - Programming
tags:
  - deeplearning
  - python

---
[Pythonでパーセプトロンをつくる][1]ことができましたが、今度はこのひとつひとつを組み合わせてディープラーニングの仕組みを構築していきます。

そのまえに、ぼくらの脳内にある神経細胞のつくりと仕組みについて知っておいたほうがいいかもです。

  * 脳の神経細胞とニューラルネットワーク
  * ニューラルネットワークをパーセプトロンで模する

## 脳の神経細胞とニューラルネットワーク

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-14.09.14-1024x549.png" alt="" class="wp-image-1274" width="500" height="267" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-14.09.14-1024x549.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-14.09.14-300x161.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-14.09.14-768x412.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-14.09.14.png 1424w" sizes="(max-width: 500px) 100vw, 500px" /><figcaption>脳の神経細胞（ニューロン）</figcaption></figure>
</div>

ヒトの脳にはこのような神経細胞、ニューロンが1,000億個以上あり、1個が1,000個ものニューロンと接続しています。複雑で広大なネットワークが脳のなかには存在しているんですね。

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.06.19-1024x394.png" alt="" class="wp-image-1275" width="525" height="203" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.06.19-1024x394.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.06.19-300x115.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.06.19-768x295.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.06.19-1536x591.png 1536w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.06.19.png 1836w" sizes="(max-width: 525px) 100vw, 525px" /></figure>
</div>

1個のニューロンは、ほかの多数からの信号を受け取り、またほかのニューロンへと信号を伝えていきます。この仕組みは、ニューロンとニューロンの間（シナプス）で受け渡しされる伝達物質（グルタミンやアセチルコリンなど）やその伝達物質を受け取る受容体（受け取ることでゲートを開き、細胞内外でカリウムイオンを通行させ電位差を生む）、ニューロン内外の電位差で生まれる活動電位などによって緻密にできあがっています。

面白いのは、このときほかのニューロンからの信号がどれも平等に扱われているわけではないということです。強めの信号でなければ次の信号に影響しないものがあれば、逆もあります。特定の組み合わせのニューロンからの信号が揃ったときのみ次に信号を伝える、などとローカルルールがたくさんできています。

このローカルルールはもちろんニューロンごとに違い、ヒトの脳内全体となると、個々でまったく異なるネットワーク群ができています。言わずもがな、これが、ヒトの個性やパーソナリティを形作っています。

同じものを見たり聞いたりしたときに幸せを感じるのか悲しく感じるのか、言葉遣いのクセ、記憶していること（得意なこと）がヒトによって異なるのも、ミクロで見れば、ニューロンごとのローカルルールの集合が生み出しているということです。

## ニューラルネットワークをパーセプトロンで模する

ニューロンとニューロンの関係は簡略化するとこのような感じです。

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.10.32-1024x590.png" alt="" class="wp-image-1278" width="340" height="196" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.10.32-1024x590.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.10.32-300x173.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.10.32-768x443.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.10.32-1536x885.png 1536w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.10.32.png 1680w" sizes="(max-width: 340px) 100vw, 340px" /></figure>
</div>

複数の入力に対して、それぞれに異なる加工をして、一つの出力をする仕組みは[前回][1]、Pythonによるパーセプトロンでつくりました。

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.11.10-1024x771.png" alt="" class="wp-image-1279" width="385" height="289" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.11.10-1024x771.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.11.10-300x226.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.11.10-768x578.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.11.10.png 1078w" sizes="(max-width: 385px) 100vw, 385px" /><figcaption>パーセプトロン。複数の入力ごとに異なる掛け算を施して出力</figcaption></figure>
</div> $$ ｙ= \begin{cases} 0\qquad\text{if }(w\_{1}x\_{1}+w\_{2}x\_{2}+b\leq0)\\ 1\qquad\text{if }(w\_{1}x\_{1}+w\_{2}x\_{2}+b>0)\\ \end{cases} \\ w\_{k}=\text{ 入力値 }\\ x\_{k}=\text{ 重み }\\ b=\text{ バイアス }\\ $$ 

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-19.35.32-1024x582.png" alt="" class="wp-image-1346" width="360" height="203" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-19.35.32-300x170.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-19.35.32-768x436.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-19.35.32.png 1384w" sizes="(max-width: 360px) 100vw, 360px" /></figure>
</div>

さらに、入力から出力までのプロセスのひとつとして、活性化関数なるものを加えます。活性化関数によって、各入力をまとめたものをさらに加工します。

これは、下の図のように一層のなかにニューロンを複数設置するのですが、活性化関数を置くことで複数のニューロンを設置する意義を担保するためです。（活性化関数がないと、複数のニューロンによる出力の合計を、一つのニューロンで表現できてしまいます。）

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.11.23-1024x771.png" alt="" class="wp-image-1280" width="395" height="298" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.11.23-1024x771.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.11.23-300x226.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.11.23-768x578.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-15.11.23.png 1358w" sizes="(max-width: 395px) 100vw, 395px" /><figcaption>ひとつひとつの丸がニューロンでありパーセプトロン</figcaption></figure>
</div>

次回から、パーセプトロンを何個も組み合わせて模擬的にニューラルネットワークをPythonでつくります。

 [1]: https://kaorumitsumori.com/deeplearning-perceptron/