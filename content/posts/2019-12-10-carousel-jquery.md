---
title: jQueryでカルーセルを作る方法
author: KAORU
type: post
date: 2019-12-10T04:25:15+00:00
url: /carousel-jquery/
featured_image: /wp-content/uploads/2019/12/14.gif
categories:
  - Front-end development
  - Programming
tags:
  - css
  - html
  - jquery
  - sidepicking

---
アマゾンの商品紹介などでよく使われる表示方法。  
上のアニメーションの場合、リスト化したサムネイル画像を４枚づつグループ化し、そのグループごとに横移動させる仕組みになっている。<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/box-1024x350.jpg" alt="" class="wp-image-619" width="637" height="218" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/box-1024x350.jpg 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/box-300x103.jpg 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/box-768x263.jpg 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/box.jpg 1202w" sizes="(max-width: 637px) 100vw, 637px" /></figure> 

## HTMLの構造

<pre class="wp-block-code"><code>
&lt;div id="carouselWrap">
			&lt;p id="carouselPrev">&lt;img src="./images/btn_prev.gif" alt="前へ">&lt;/p>
			&lt;p id="carouselNext">&lt;img src="./images/btn_next.gif" alt="次へ">&lt;/p>
			&lt;div id="carousel">
				&lt;div id="carouselInner">
					&lt;ul class="column">
						&lt;li>&lt;a href="#">&lt;img src="./images/photo1_thum.jpg" alt="">&lt;/a>&lt;/li>
						&lt;li>&lt;a href="#">&lt;img src="./images/photo2_thum.jpg" alt="">&lt;/a>&lt;/li>
						&lt;li>&lt;a href="#">&lt;img src="./images/photo3_thum.jpg" alt="">&lt;/a>&lt;/li>
						&lt;li>&lt;a href="#">&lt;img src="./images/photo4_thum.jpg" alt="">&lt;/a>&lt;/li>
					&lt;/ul>
					&lt;ul class="column">
						&lt;li>&lt;a href="#">&lt;img src="./images/photo5_thum.jpg" alt="">&lt;/a>&lt;/li>
						&lt;li>&lt;a href="#">&lt;img src="./images/photo6_thum.jpg" alt="">&lt;/a>&lt;/li>
						&lt;li>&lt;a href="#">&lt;img src="./images/photo7_thum.jpg" alt="">&lt;/a>&lt;/li>
						&lt;li>&lt;a href="#">&lt;img src="./images/photo8_thum.jpg" alt="">&lt;/a>&lt;/li>
					&lt;/ul>
					&lt;ul class="column">
						&lt;li>&lt;a href="#">&lt;img src="./images/photo9_thum.jpg" alt="">&lt;/a>&lt;/li>
						&lt;li>&lt;a href="#">&lt;img src="./images/photo10_thum.jpg" alt="">&lt;/a>&lt;/li>
						&lt;li>&lt;a href="#">&lt;img src="./images/photo11_thum.jpg" alt="">&lt;/a>&lt;/li>
						&lt;li>&lt;a href="#">&lt;img src="./images/photo12_thum.jpg" alt="">&lt;/a>&lt;/li>
					&lt;/ul>
					&lt;ul class="column">
						&lt;li>&lt;a href="#">&lt;img src="./images/photo13_thum.jpg" alt="">&lt;/a>&lt;/li>
						&lt;li>&lt;a href="#">&lt;img src="./images/photo14_thum.jpg" alt="">&lt;/a>&lt;/li>
						&lt;li>&lt;a href="#">&lt;img src="./images/photo15_thum.jpg" alt="">&lt;/a>&lt;/li>
						&lt;li>&lt;a href="#">&lt;img src="./images/photo16_thum.jpg" alt="">&lt;/a>&lt;/li>
					&lt;/ul>
				&lt;/div>
			&lt;/div>
&lt;/div></code></pre>

  * li要素でサムネイル画像を囲む
  * ul要素４グループをひとまとめにする（div#carouselInner でグループ化）
  * div#carouselでさらに４つのグループをまとめる
  * btn\_prev.gifでnextボタンとbtn\_next.gifでprevボタンを作成
  * これらのボタンとdiv#carouselをまとめたものが# carouselWrap

## CSSの構造

<pre class="wp-block-code"><code>
*{
	margin:0;
	padding:0;}

#carouselWrap{
	margin:100px auto;
	width:620px;
	height:135px;
	padding:5px;
	background:url("./images/background.gif");
	position:relative;}

#carouselPrev{
	position:absolute;
	top:65px;
	left:-8px;
	cursor:pointer;}

#carouselNext{
	position:absolute;
	top:65px;
	right:-8px;
	cursor:pointer;}

#carousel{
	width:100%;
	height:100%;
	overflow:hidden;}

#carouselInner ul.column{
	width:605px;
	height:105px;
	padding:15px 0 15px 15px;
	list-style-type:none;
	float:left;}

#carouselInner ul.column li{
	float:left;
	margin-right:10px;
	display:inline;}

#carouselInner ul.column li img{
	border:none;}</code></pre>

  * #carouselWrapは幅と高さを決める。ここはカルーセルの枠部分デザイ ン。背景に適当な画像を入れる
  * #carouselWrapの子要素ではpositionを使うので、 position:relative;を設定
  * #carouselPrevと#carouselNextはpositionで配置
  * #carouselは親要素と高さと幅を合わせるために、widthと heightを100%とする。また子要素が横に大きくはみ出す設計なので、こ こにoverflow:hiddenを設定
  * ul.column liはfloatで横並びに<figure class="wp-block-image size-large">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/css.jpg" alt="" class="wp-image-624" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/css.jpg 861w, https://kaorumitsumori.com/wp-content/uploads/2019/12/css-300x102.jpg 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/css-768x262.jpg 768w" sizes="(max-width: 861px) 100vw, 861px" /></figure> 

  * 画面の幅、140px*4=560px
  * liのマージン、10px*4=40px
  * 最後の右の余白、5px
  * 必要な合計幅、560+40+15+15=605px 

## JavaScript（jQuery）の構造

<pre class="wp-block-code"><code>
$(function(){
	$("#carouselInner").css("width",620*$("#carouselInner ul.column").length+"px");
	$("#carouselInner ul.column:last").prependTo("#carouselInner");
	$("#carouselInner").css("margin-left","-620px");
	
	$("#carouselPrev").click(function(){
		$("#carouselNext,#carouselPrev").hide();
		$("#carouselInner").animate({
			"margin-left" : parseInt($("#carouselInner").css("margin-left"))+620+"px"
		},"slow","swing" , 
		function(){
			$("#carouselInner").css("margin-left","-620px");
			$("#carouselInner ul.column:last").prependTo("#carouselInner");
			$("#carouselNext,#carouselPrev").show();
		});
	});
	
	$("#carouselNext").click(function(){
		$("#carouselNext,#carouselPrev").hide();
		$("#carouselInner").animate({
			"margin-left" : parseInt($("#carouselInner").css("margin-left"))-620+"px"
		},"slow","swing" , 
		function(){
			$("#carouselInner").css("margin-left","-620px");
			$("#carouselInner ul.column:first").appendTo("#carouselInner");
			$("#carouselNext,#carouselPrev").show();
		});
	});
	
});</code></pre>

  * 3行目、#carouselInnerのwidthを設定。ul.columnの数が増えても自動で計算される
  * $(&#8220;#carouselInnerul.column&#8221;).lengthでul 要素の数が算出される
  * 4行目、最後に位置するul要素を.prependTo() を使用して先頭に移動させる
  * これで常に最後の要素が先頭に移動するようになる
  * 5行目、マイナスのマージンをかけて最後のulを左に移動させて最初のul を表示させる
  * 7行目、$(&#8220;#carouselPrev&#8221;).click(function(){ではbtn_prev.gifボタンがクリックされたら実行。イ ベント処理が終了するまで.hide()を使用してボタンは非表示に。スライド中にボタンが押されないようにするた め
  * 9行目、parseInt($(&#8220;#carouselInner&#8221;).css(&#8220;margin-left&#8221;)+620+&#8221;px&#8221;によって.animate()でmargin-leftに620pxプラスして#carouselInnerを右に動かす
  * 12行目、コールバック関数で、先に動 かしたばかりの#carouselInnerを再びmargin-left: -620pxへ。つぎの処理のため
  * 14行目、$(“#carouselInner ul.column:last&#8221;).prependTo(&#8220;#carouselInner&#8221;);で最後のものを先頭に移動。ただし、ここでは先頭の&#8221;#carouselInnerを表示しておきたいのでmargin-left: -620pxにする
  * 15行目、すべての処理が終わったら消しておいたボタンを再表示
  * 19行目、btn_nextも同様の処理をする