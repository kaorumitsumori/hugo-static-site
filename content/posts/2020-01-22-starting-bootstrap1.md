---
title: Bootstrapで0から簡単なホームページをつくる手順【ヘッダーとクローバルナビをつくる】
author: KAORU
type: post
date: 2020-01-22T04:03:52+00:00
url: /starting-bootstrap1/
featured_image: /wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.22.07.png
categories:
  - Front-end development
  - Programming
tags:
  - bootstrap
  - css
  - html
  - wordpress

---
<a rel="noreferrer noopener" aria-label=" (新しいタブで開く)" href="https://getbootstrap.com/" target="_blank">Bootstrap</a>とは、スマホ、タブレット、PC、どのスクリーンサイズにも対応しているレスポンシブサイトをつくるための、HTML, CSS, JavaScriptコードのテンプレート集のようなものです。  
  
ウェブサイトでよく使われるボタンやフォーム、縦向きに割けられているデザインなどのコードが、<a rel="noreferrer noopener" aria-label=" (新しいタブで開く)" href="https://getbootstrap.com/" target="_blank">Bootstrap</a>ではそのまま利用できます。  
  
また、文字の色を変える、適当なmarginを入れる、x個のカラムに分ける、などのよく使われるスタイルに対応したクラス名があらかじめ設定されています。HTMLを書くときには、そのクラス名を記述するだけでCSSを書くことなくスタイルを設定できます。

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.26.39-327x1024.png" alt="" class="wp-image-1090" width="266" height="834" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.26.39-327x1024.png 327w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.26.39-96x300.png 96w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.26.39-490x1536.png 490w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.26.39.png 574w" sizes="(max-width: 266px) 100vw, 266px" /></figure>
</div>

今回はBootstrapを使って、このようなページのHTMLをコーディングします。

  * index.htmlを準備し、Bootstrapを紐付ける
  * ヘッダーとクローバルナビをつくる
  * [メインコンテンツをつくる][1]
  * [フッターをつくる][2]

完成したテーマは[こちら][3]。

## index.htmlを準備し、Bootstrapを紐付ける

まずはどのエディターでもいいので、index.htmlを準備しましょう。同じ階層にimgと名付けたファイルも用意し、そのなかに何かしらの画像を置いておきます。

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.00.51-1024x734.png" alt="" class="wp-image-1081" width="315" height="225" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.00.51-1024x734.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.00.51-300x215.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.00.51-768x550.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.00.51.png 1326w" sizes="(max-width: 315px) 100vw, 315px" /></figure>
</div>

  
次に[Bootstrap][4]のトップページの&#8221;Get started&#8221;というところから、”Starter template”のコードをコピーしてindex.htmlに貼り付けます。

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.22.28-1024x608.png" alt="" class="wp-image-1083" width="587" height="349" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.22.28-1024x608.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.22.28-300x178.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.22.28-768x456.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.22.28-1536x912.png 1536w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.22.28.png 1926w" sizes="(max-width: 587px) 100vw, 587px" /></figure>
</div>

<pre class="wp-block-code"><code>
&lt;!doctype html>
&lt;html lang="en">
  &lt;head>
    &lt;!-- Required meta tags -->
    &lt;meta charset="utf-8">
    &lt;meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    &lt;!-- Bootstrap CSS -->
    &lt;link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">

    &lt;title>Hello, world!&lt;/title>
  &lt;/head>
  &lt;body>
    &lt;h1>Hello, world!&lt;/h1>

    &lt;!-- Optional JavaScript -->
    &lt;!-- jQuery first, then Popper.js, then Bootstrap JS -->
    &lt;script src="https://code.jquery.com/jquery-3.4.1.slim.min.js" integrity="sha384-J6qa4849blE2+poT4WnyKhv5vZF5SrPo0iEjwBvKU7imGFAV0wwj1yYfoRSJoZ+n" crossorigin="anonymous">&lt;/script>
    &lt;script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous">&lt;/script>
    &lt;script src="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js" integrity="sha384-wfSDF2E50Y2D1uUdj0O3uMBJnjuUD4Ih7YwaYd1iqfktj0Uod8GCExl3Og8ifwB6" crossorigin="anonymous">&lt;/script>
  &lt;/body>
&lt;/html></code></pre>

<link>タグによってBootstrapと紐付けられているので、あらかじめ設定されているクラスを使うことで、スタイルを付与できます。  
Hello, world!は好きな文字列に変えてもよいです。

## ヘッダーとクローバルナビをつくる

次に下のコードを<body>の直下に書き、<h1>も下のように<div>のなかに動かします。

<pre class="wp-block-code"><code> 
&lt;header>
　 &lt;div>
      &lt;h1>Hello, world!&lt;/h1>
　 &lt;/div>
&lt;/header></code></pre>

ヘッダーはこれでOKです。  
つぎにクローバルナビを作ります。クローバルナビとはこういうののことです。

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.29.31-1024x76.png" alt="" class="wp-image-1084" width="585" height="43" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.29.31-1024x76.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.29.31-300x22.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.29.31-768x57.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.29.31-1536x115.png 1536w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.29.31.png 1634w" sizes="(max-width: 585px) 100vw, 585px" /></figure>
</div>

Bootstrapの検索フォームでnavbarと入れると、こちらにいきます。<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.31.16-1024x726.png" alt="" class="wp-image-1085" width="577" height="409" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.31.16-1024x726.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.31.16-300x213.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.31.16-768x544.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.31.16-1536x1089.png 1536w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.31.16-2048x1451.png 2048w" sizes="(max-width: 577px) 100vw, 577px" /></figure> 

画面にあるcopyによってコードを取得し、</header>の直下にペーストしましょう。

<pre class="wp-block-code"><code>
&lt;header>
　 &lt;div>
      &lt;h1>Hello, world!&lt;/h1>
　 &lt;/div>
&lt;/header>
&lt;!-- Global navi  -->
&lt;nav class="navbar navbar-expand-lg navbar-light bg-light">
  &lt;a class="navbar-brand" href="#">Navbar&lt;/a>
  &lt;button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    &lt;span class="navbar-toggler-icon">&lt;/span>
  &lt;/button>

  &lt;div class="collapse navbar-collapse" id="navbarSupportedContent">
    &lt;ul class="navbar-nav mr-auto">
      &lt;li class="nav-item active">
        &lt;a class="nav-link" href="#">Home &lt;span class="sr-only">(current)&lt;/span>&lt;/a>
      &lt;/li>
      &lt;li class="nav-item">
        &lt;a class="nav-link" href="#">Link&lt;/a>
      &lt;/li>
      &lt;li class="nav-item dropdown">
        &lt;a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          Dropdown
        &lt;/a>
        &lt;div class="dropdown-menu" aria-labelledby="navbarDropdown">
          &lt;a class="dropdown-item" href="#">Action&lt;/a>
          &lt;a class="dropdown-item" href="#">Another action&lt;/a>
          &lt;div class="dropdown-divider">&lt;/div>
          &lt;a class="dropdown-item" href="#">Something else here&lt;/a>
        &lt;/div>
      &lt;/li>
      &lt;li class="nav-item">
        &lt;a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled&lt;/a>
      &lt;/li>
    &lt;/ul>
    &lt;form class="form-inline my-2 my-lg-0">
      &lt;input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
      &lt;button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search&lt;/button>
    &lt;/form>
  &lt;/div>
&lt;/nav></code></pre>

するとこのようになります。<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.44.56-1024x134.png" alt="" class="wp-image-1086" width="572" height="74" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.44.56-1024x134.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.44.56-300x39.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.44.56-768x101.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-18.44.56.png 1494w" sizes="(max-width: 572px) 100vw, 572px" /></figure> 

次に以下のように各所を変更します。

<pre class="wp-block-code"><code>
&lt;header>
　 &lt;div>
      &lt;h1>Hello, world!&lt;/h1>
　 &lt;/div>
&lt;/header>
&lt;!-- Global navi  -->

&lt;!-- 背景色を暗くする(bg-darkで)  -->
&lt;nav class="navbar navbar-expand-lg navbar-light bg-dark">

&lt;!-- divで囲い、class="container"をつける  -->
&lt;div class="container">

&lt;!-- 文字を明るくする(text-white)、ほかのメニュー項目も同様  -->
  &lt;a class="navbar-brand text-white" href="#">Navbar&lt;/a>

&lt;!-- ボタンの背景を明るくする(bg-white)  -->
  &lt;button class="navbar-toggler bg-white" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    &lt;span class="navbar-toggler-icon">&lt;/span>
  &lt;/button>
  &lt;div class="collapse navbar-collapse" id="navbarSupportedContent">
    &lt;ul class="navbar-nav mr-auto">
      &lt;li class="nav-item active">
        &lt;a class="nav-link text-white" href="#">Home &lt;span class="sr-only">(current)&lt;/span>&lt;/a>
      &lt;/li>
&lt;!-- 上と同様のメニュー項目を複製する  -->
      &lt;li class="nav-item active">
        &lt;a class="nav-link text-white" href="#">Home &lt;span class="sr-only">(current)&lt;/span>&lt;/a>
      &lt;/li>
      &lt;li class="nav-item active">
        &lt;a class="nav-link text-white" href="#">Home &lt;span class="sr-only">(current)&lt;/span>&lt;/a>
      &lt;/li>
      &lt;li class="nav-item active">
        &lt;a class="nav-link text-white" href="#">Home &lt;span class="sr-only">(current)&lt;/span>&lt;/a>
      &lt;/li>

&lt;!-- これ以降のメニュー項目は削る〜  -->
      &lt;li class="nav-item">
        &lt;a class="nav-link" href="#">Link&lt;/a>
      &lt;/li>
      &lt;li class="nav-item dropdown">
        &lt;a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          Dropdown
        &lt;/a>
        &lt;div class="dropdown-menu" aria-labelledby="navbarDropdown">
          &lt;a class="dropdown-item" href="#">Action&lt;/a>
          &lt;a class="dropdown-item" href="#">Another action&lt;/a>
          &lt;div class="dropdown-divider">&lt;/div>
          &lt;a class="dropdown-item" href="#">Something else here&lt;/a>
        &lt;/div>
      &lt;/li>
      &lt;li class="nav-item">
        &lt;a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled&lt;/a>
      &lt;/li>
&lt;!-- 〜ここまで削る  -->

    &lt;/ul>

&lt;!-- 以下のformも削る  -->
    &lt;form class="form-inline my-2 my-lg-0">
      &lt;input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
      &lt;button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search&lt;/button>
    &lt;/form>
&lt;!-- 〜ここまで削る  -->

  &lt;/div>
&lt;/div>
&lt;/nav></code></pre>

項目の名前を適当に変えれば以下のようにできあがります。

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.14.06-1024x132.png" alt="" class="wp-image-1087" width="574" height="73" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.14.06-1024x132.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.14.06-300x39.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.14.06-768x99.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.14.06-1536x197.png 1536w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.14.06.png 1790w" sizes="(max-width: 574px) 100vw, 574px" /></figure>
</div>

レスポンシブデザインなので、縮めるとこのように表示されます。

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.14.58-1024x223.png" alt="" class="wp-image-1088" width="569" height="123" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.14.58-1024x223.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.14.58-300x65.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.14.58-768x167.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.14.58.png 1132w" sizes="(max-width: 569px) 100vw, 569px" /></figure>
</div>

続きは<a href="https://kaorumitsumori.com/starting-bootstrap2/" target="_blank" rel="noreferrer noopener" aria-label="こちら (新しいタブで開く)">こちら</a>です！

 [1]: https://kaorumitsumori.com/starting-bootstrap2/
 [2]: https://kaorumitsumori.com/starting-bootstrap3/
 [3]: http://kaorumitsumori.com/MySimple_html/index.html
 [4]: https://getbootstrap.com/