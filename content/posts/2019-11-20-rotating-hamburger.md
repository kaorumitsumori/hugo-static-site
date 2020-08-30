---
title: CSSで回転ハンバーガーボタンを作る方法
author: KAORU
type: post
date: 2019-11-20T15:47:02+00:00
url: /rotating-hamburger/
featured_image: /wp-content/uploads/2019/12/h-1.gif
siteorigin_page_settings:
  - 'a:6:{s:6:"layout";s:7:"default";s:10:"page_title";b:1;s:15:"masthead_margin";b:1;s:13:"footer_margin";b:1;s:16:"display_masthead";b:1;s:22:"display_footer_widgets";b:1;}'
page_type:
  - default
categories:
  - Front-end development
  - Programming
tags:
  - css
  - html

---
ウェブサイトの右上とか左上にあって、タップするとメニューが出てくるあの横向きの三本線を、ハンバーガーボタンとか言ったりする。  
今回は、カーソルが合わさったときに✕になり、離せばもとに戻るハンバーガーボタンを作ってみる。さらに、✕になるときの動きをかっこよく回転させてみようと思う。

## まずはハンバーガーボタンの作り方<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-18-at-13.24.57-1024x995.png" alt="" class="wp-image-962" width="123" height="119" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-18-at-13.24.57-1024x995.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-18-at-13.24.57-300x291.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-18-at-13.24.57-768x746.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-18-at-13.24.57.png 1122w" sizes="(max-width: 123px) 100vw, 123px" /></figure> 

まずは上の図のような動きのない三本線を作る。  
ソースコードとともに説明していく。

<pre class="wp-block-code"><code>&lt;!-- 以下HTMLコード -->


&lt;!-- 白いエリアを作る -->
&lt;div class="hamburger">

&lt;!-- 白いエリアの中に3本の線を作る -->
    &lt;span class="top">&lt;/span>
    &lt;span class="middle">&lt;/span>
    &lt;span class="bottom">&lt;/span>

&lt;/div>



/*以下CSSコード*/


/*白いエリアの見た目を作る*/
hamburger {
        width: 54px;
        height: 54px;
        border-radius: 5px;
        background-color:#fff;
/*後に3つのspanを絶対配置するために*/
/*親要素の白いエリアに下記が必要*/
        position: relative;}
    
.hamburger span {
/*下記widthとheightで細い線のようにする*/
        width: 44px;
        height: 2px;
        display: block;
        background: #000;
/*親要素でposition: relativeを指定しているため*/
/*ここでposition: absolute;とすると*/
/*白いエリア内での絶対的な配置を指定できる*/
        position: absolute;
        left: 50%;
        top: 50%;
/*position: absolute;は基本的には左上のポイントを基準に配置されるので*/
/*厳密に白いエリアの中心に配置するために微調整する*/
        margin-left: -22px;
        margin-top: -1px;}
    

.hamburger span {
        transition: all 0.5s;}</code></pre>

transition: all 0.5sの部分は後に説明する`*1`<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-18-at-13.24.30-1024x1008.png" alt="" class="wp-image-963" width="115" height="113" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-18-at-13.24.30-1024x1008.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-18-at-13.24.30-300x295.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-18-at-13.24.30-768x756.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-18-at-13.24.30.png 1118w" sizes="(max-width: 115px) 100vw, 115px" /></figure> 

この時点では一本しか線がない、ように見えるが実は一本しかないのではなく、  
三本の線が同じ位置に重なっているため、一本しかないように見えている。  
次にCSSによって上下に線をずらすことで三本の線にすることができる。

<pre class="wp-block-code"><code>.hamburger .top {
        margin-top: -19px;}
    
.hamburger .bottom {
        margin-top: 19px;}</code></pre>

## 回転させる方法<figure class="wp-block-image size-large">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/h-1.gif" alt="" class="wp-image-964" /></figure> 

擬似クラスの:hoverとtransform: rotateを使う。  
擬似クラスとは、なんらかの条件を満たす場合にのみCSSを発動させる書き方である。  
今回はカーソルが白いエリアに合わさった場合に三本線の動きを発動させたいので:hoverを使う。  
ほかにも:link、:visited、:active、などがある。  
また、transform: rotateで回転の角度を指定できる。transformにはほかにも、translateなどがある。  
下記ソースコードとともに具体的に説明していく。

<pre class="wp-block-code"><code>/*以下CSSコード*/


.hamburger:hover .middle {
/*4つ目の数字(0)で透明にする*/
        background: rgba(255, 255, 255, 0);}
    

.hamburger:hover .top {
/*-405℃回転させる*/
        transform: rotate(-405deg);
/*上にずらしていた線を中心に戻す*/
        margin-top: 0px;}
    

.hamburger:hover .bottom {
/*405℃回転させる*/
        transform: rotate(405deg);
/*上にずらしていた線を中心に戻す*/
        margin-top: 0px;}</code></pre>

transition: all 0.5s;の部分について説明する。`*1`  
カーソルが合ったときのときの動きを擬似クラス:hoverで指定したが、この動きが何秒かけて実行されるのかを指定する必要がある。それを動きが起こる要素に、擬似クラスでないCSSで指定しておいた。この場合、指定した動きが0.5秒で等速で実行される。allとは指定した動きすべてという意味。

これによって、カーソルが合わさったときにハンバーガーボタンをかっこよく回転させることができた。