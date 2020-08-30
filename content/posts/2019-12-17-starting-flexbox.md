---
title: 【基礎はこれだけ】CSSのFlexboxの使い方
author: KAORU
type: post
date: 2019-12-17T03:31:00+00:00
url: /starting-flexbox/
featured_image: /wp-content/uploads/2019/12/3.gif
categories:
  - Front-end development
  - Programming
tags:
  - css
  - html
  - sidepicking

---
基本的にHTMLで書いたものは、上から下に積み下がるように順に、左寄せで配置されていきます。  
これを真ん中に置いたり、ひとつ前のコンテンツの横並びに置いたり、あるいは等間隔で横に並べて置きたいときもありますよね。

そうした配置はCSSのfloatでも実現できるのですが、「Flexbox」というCSSでも可能です。しかもFlexbox = Flexible Boxの名の通り、フレキシブルでわりと簡単に希望のレイアウトを組めます。

<pre class="wp-block-code"><code>
#HTML
&lt;div class="container">
  &lt;div class="box box-1">1&lt;/div>
  &lt;div class="box box-2">2&lt;/div>
  &lt;div class="box box-3">3&lt;/div>
  &lt;div class="box box-4">4&lt;/div> 
  &lt;div class="box box-5">5&lt;/div>
  &lt;div class="box box-6">6&lt;/div>
  &lt;div class="box box-7">7&lt;/div>
  &lt;div class="box box-8">8&lt;/div>
  &lt;div class="box box-9">9&lt;/div>  
&lt;/div></code></pre>

<pre class="wp-block-code"><code>
#CSS
.box {
  font-size: 48px;
  color: white;
  padding: 10px;
  text-align:center;
  font-weight: bold;
  box-sizing: border-box;}

.box-1 {
  background: #e51400;}
.box-2 {
  background: #fa6800;}
.box-3 {
  background: #f0a30a;}
.box-4 {
  background: #e3c800;}
.box-5 {
  background: #a4c400;}
.box-6 {
  background: #60a917;}
.box-7 {
  background: #00aba9;}
.box-8 {
  background: #1ba1e2;}
.box-9 {
  background: #aa00ff;}</code></pre>

上記のようにHTMLとCSSを書くと、このようになります。<figure class="wp-block-image size-large">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/1.gif" alt="" class="wp-image-910" /></figure> 

つぎに、親要素である.containerに下記のように加えるだけでfloat:leftのような配置にすることができます。

<pre class="wp-block-code"><code>
.container {
  display:flex;}</code></pre><figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/2.gif" alt="" class="wp-image-911" width="290" height="74" /></figure> 

さらに、親要素である.containerにflex-direction:**を加えると、子要素の並ぶ向き（縦か横か）や順番を設定することができます。  
またflex-wrap:**によって、画面が小さくなったときにはみ出した子要素を下の段に落とすこともできます。

<pre class="wp-block-code"><code>
.container {
  display:flex;

#向きは横向きで反対向き
  flex-direction: row-reverse; 

#はみ出した要素を下の段に落とす
  flex-wrap:wrap;}</code></pre><figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/3.gif" alt="" class="wp-image-912" width="341" height="88" /></figure> 

このように親要素に加えるセレクターは以下のように各種あります。<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/4-1-1024x518.png" alt="" class="wp-image-913" width="576" height="291" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/4-1-1024x518.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/4-1-300x152.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/4-1-768x389.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/4-1-1536x777.png 1536w, https://kaorumitsumori.com/wp-content/uploads/2019/12/4-1-2048x1036.png 2048w" sizes="(max-width: 576px) 100vw, 576px" /></figure> 

また、子要素に書くタイプのセレクターもあります。<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/5-2-985x1024.png" alt="" class="wp-image-914" width="333" height="346" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/5-2-985x1024.png 985w, https://kaorumitsumori.com/wp-content/uploads/2019/12/5-2-289x300.png 289w, https://kaorumitsumori.com/wp-content/uploads/2019/12/5-2-768x798.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/5-2.png 1426w" sizes="(max-width: 333px) 100vw, 333px" /><figcaption>子要素に書くセレクター</figcaption></figure> 

  * align-self：垂直方向の揃え。ex）.box-1 { align-self: flex-start;}
  * order：順序を指定。ex）.box-1 { order: 2;}
  * flex-grow：伸びる比率。ex）.box-1 { flex-grow: 2; }
  * flex-shrink：縮む比率。ex）.box-1 { flex-shrink: 2; }
  * flex-basis：ベース幅の指定。ex）.box-1 { flex-basis: 200px; }
  * flex：flex-grow、flex-shrink、flex-basisをまとめて指定。ex）.box-1 { flex: 0 1 200px; }

<blockquote class="wp-block-quote">
  <p>
    <a rel="noreferrer noopener" aria-label=" (新しいタブで開く)" href="https://www.webcreatorbox.com/tech/css-flexbox-cheat-sheet" target="_blank">CSS Flexboxのチートシートを作ったので配布します</a>
  </p>
</blockquote>

また、こちらの記事が抜群にわかりやすいので見てみてください。