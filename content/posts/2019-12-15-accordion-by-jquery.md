---
title: jQueryでアコーディオンのように動くコンテンツを作る
author: KAORU
type: post
date: 2019-12-15T08:14:35+00:00
url: /accordion-by-jquery/
featured_image: /wp-content/uploads/2019/12/ac-1.gif
categories:
  - Front-end development
  - Programming
tags:
  - css
  - html
  - jquery
  - toppicking

---
このようにコンテンツが収納される仕組みをつくる。

## HTMLの構造

<pre class="wp-block-code"><code>
&lt;dl>
	&lt;dt>Step.1&lt;/dt>
	&lt;dd>&lt;p>This is a sample.&lt;/p>&lt;/dd>
	&lt;dt>Step.2&lt;/dt>
	&lt;dd>&lt;p>This is a sample.&lt;/p>&lt;/dd>
	&lt;dt>Step.3&lt;/dt>
	&lt;dd>&lt;p>This is a sample.&lt;/p>&lt;/dd>
&lt;/dl></code></pre>

  * definition listの中に、definition termとdefinition descriptionのセットを3つ入れる

## CSSの構造

<pre class="wp-block-code"><code>
*{
	margin:0;
	padding:0;
	border:0;
}
dl{
	width:800px;
	margin:50px auto;
}
dt{
	line-height:35px;
	font-size:large;
	text-indent:3em;
	font-weight:bold;
	color:white;
	height:35px;
	background:url("images/background.jpg");
}
dt.over{
	background:url("images/background-over.jpg");
	cursor:pointer;
}
dt.selected{
        background:url("images/background_selected.jpg");
	cursor:default;
	color:black;
}
dd{
	height:300px;
	background:#D4D0C8;
}
dd p{
	text-indent:1em;
	padding:20px;
}</code></pre>

  * 23~32行目、後でjQueryによって付与されるclassである.overと.selectedの挙動を設定

## JavaScript（jQuery）の構造

<pre class="wp-block-code"><code>
$(function(){
	$("dd:not(:first)").css("display","none");
	$("dt:first").addClass("selected");
	$("dl dt").click(function(){
		if($("+dd",this).css("display")=="none"){
			$("dd").slideUp("slow");
			$("+dd",this).slideDown("slow");
			$("dt.selected").removeClass("selected");
			$(this).addClass("selected");
		}
	}).mouseover(function(){
		$(this).addClass("over");
	}).mouseout(function(){
		$(this).removeClass("over");
	});
});</code></pre>

  * 3行目、始めのdd以外は消し去る
  * 4行目、始めのddにclass=&#8221;selected&#8221;を付与
  * 6~8行目、クリックしたdtのすぐ後にあるddがdisplay:noneなら、ddをすべてslideUp（閉じ）、クリックしたdtのすぐ後にあるddはslideDown（開く）
  * 12行目~、カーソルを合わせたdtの背景（薄い黒に変色）とカーソルのマーク（指の形になる）を、class=&#8221;over&#8221;を移動させることで変化させる