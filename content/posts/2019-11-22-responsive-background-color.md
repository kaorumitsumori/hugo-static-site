---
title: '[レスポンシブ基礎] 画面の幅ごとに背景色を変える方法'
author: KAORU
type: post
date: 2019-11-22T06:19:10+00:00
url: /responsive-background-color/
featured_image: /wp-content/uploads/2019/12/15.gif
siteorigin_page_settings:
  - 'a:6:{s:6:"layout";s:7:"default";s:10:"page_title";b:1;s:15:"masthead_margin";b:1;s:13:"footer_margin";b:1;s:16:"display_masthead";b:1;s:22:"display_footer_widgets";b:1;}'
categories:
  - Front-end development
  - Programming
tags:
  - css
  - html

---
パソコンだけでなくスマホやタブレットなど、スクリーンのサイズごとにコンテンツの配置を見やすく変化させるデザインのことを、レスポンシブデザインという。  
今回はレスポンシブデザインの基礎として、画面幅の変化にしたがって背景色も変化する仕組みを作ってみる。

<pre class="wp-block-code"><code>&lt;!-- 以下HTMLコード -->
&lt;body>
&lt;/body>


/*以下CSSコード*/

/*A.幅が801px以上のとき*/
body{
background:yellow;}

/*B.幅が800px〜601px以上のとき*/
@media screen and (max-width: 800px){
body{
background:green;}
}

/*C.幅が600px以下のとき*/
@media screen and (max-width: 600px){
body{
background: pink;}
}</code></pre>

@media screen and (条件の指定){CSSの記述}というように書けばよい。  
max-widthとは最大幅という意味であり、条件が適応されるときの上限幅を指定できる。

「 A.幅が801px以上のとき」には @media screen and を書いていないが問題ない。これは「B.幅が800px〜601px以上のとき」と「C.幅が600px以下のとき」

反対に、min-widthで幅の下限によって条件を指定することもできる。min-widthの場合は、記述の順が反対になることに注意。max-widthでもmin-widthでも使いやすい方を選べばよい。

<pre class="wp-block-code"><code>/*min-widthを使ったCSSコード*/

/*A.幅が600px以下のとき*/
body{
background:pink;}

/*B.幅が800px〜601px以上のとき*/
@media screen and (min-width: 601px){
body{
background:green;}
}

/*C.幅が801px以上のとき*/
@media screen and (min-width: 801px){
body{
background: yellow;}
}</code></pre>