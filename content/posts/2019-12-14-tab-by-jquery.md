---
title: jQueryを使って動的なタブコンテンツを作る方法
author: KAORU
type: post
date: 2019-12-14T14:42:02+00:00
url: /tab-by-jquery/
featured_image: /wp-content/uploads/2019/12/13.gif
categories:
  - Front-end development
  - Programming
tags:
  - css
  - html
  - jquery

---
<a rel="noreferrer noopener" aria-label="yahoo.co.jp (新しいタブで開く)" href="https://www.yahoo.co.jp/" target="_blank">yahoo.co.jp</a>のトップにあるようなアニメーションを、jQueryを使って作ってみる。コンテンツサイズごとに縦の長さも動的に変化させよう。

## HTMLの構造

<pre class="wp-block-code"><code>
&lt;div id="container">
	&lt;ul class="tab">
		&lt;li>&lt;a href="#tab1" class="selected">JavaScript&lt;/a>&lt;/li>
		&lt;li>&lt;a href="#tab2">CSS&lt;/a>&lt;/li>
		&lt;li>&lt;a href="#tab3">HTML&lt;/a>&lt;/li>
		&lt;li>&lt;a href="#tab4">jQuery&lt;/a>&lt;/li>
		&lt;li>&lt;a href="#tab5">XHTML&lt;/a>&lt;/li>
	&lt;/ul>
	&lt;ul class="panel">
		&lt;li id="tab1">This is a sample.&lt;/li>
		&lt;li id="tab2">This is a sample.&lt;/li>
		&lt;li id="tab3">This is a sample.&lt;/li>
		&lt;li id="tab4">This is a sample.&lt;/li>
		&lt;li id="tab5">This is a sample.&lt;/li>
	&lt;/ul>
&lt;/div></code></pre>

まずはタブのラベルをリストで作成し、それぞれのコンテンツもリストで作成する。ラベルはラベルごと、コンテンツはコンテンツごとにリストにしている。

## CSSの構造

<pre class="wp-block-code"><code>
*{
	margin:0;
	padding:0;
}

#container{
	width:500px;
	margin:50px auto;
}

ul.tab{
	padding:0;
}

ul.tab li{
	list-style-type:none;
	width:100px;
	height:40px;
	float:left;
}

ul.tab li a{
	outline:none;
	background:url("./images/tab.jpg");
	display:block;
	color:blue;
	line-height:40px;
	text-align:center;
}

ul.tab li a.selected{
	background:url("./images/tab_selected.jpg");
	text-decoration:none;
	color:#333;
	cursor:default;
}

ul.panel{
	clear:both;
	border:1px solid #9FB7D4;
	border-top:none;
	padding:0;
}

ul.panel li{
	list-style-type:none;
	padding:10px;
	text-indent:1em;
	color:#333;
}</code></pre>

  * .tabのpaddingを0にすることで余計なulの余白を0に
  * ナビのliの幅は100px、高さ40pxとしてfloatで横並びに
  * outline:noneで一部のブラウザでリンクをクリックしたときの点線を消す
  * .selectedがつくとタブの背景画像が変更される

## JavaScript（jQuery）の構造

<pre class="wp-block-code"><code>
&lt;script>
$(function(){
	$("ul.panel li:not("+$("ul.tab li a.selected").attr("href")+")").hide();
	$("ul.tab li a").click(function(){
		$("ul.tab li a.selected").removeClass("selected");
		$(this).addClass("selected");
		$("ul.panel li").slideUp("fast");
		$($(this).attr("href")).slideDown("fast");
		return false;
	});
});
&lt;/script></code></pre>

  * .selected以外のa要素のリンク先のみ表示し、それ以外は hide()でdisplay:noneの状態に
  * .tabのa要素をクリックし、一旦.selectedのクラス名を場所を特定せずに取り去る
  * クリックした対象のa要素に.selectedのクラス名を付ける
  * .panel liを一旦すべて非表示に
  * クリックした対象a要素のリンク先だけを表示