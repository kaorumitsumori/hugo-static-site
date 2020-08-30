---
title: Bootstrapで0から簡単なホームページをつくる手順【メインコンテンツをつくる】
author: KAORU
type: post
date: 2020-01-23T04:01:08+00:00
url: /starting-bootstrap2/
featured_image: /wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.26.39-copy.png
categories:
  - Front-end development
  - Programming
tags:
  - bootstrap
  - css
  - html
  - wordpress

---
<a rel="noreferrer noopener" aria-label=" (新しいタブで開く)" href="https://kaorumitsumori.com/starting-bootstrap1/" target="_blank">前回</a>はヘッダーとクローバルナビをつくったので、今回はメインコンテンツをコーディングします。  
メインコンテンツは下の画像のように、3列のピックアップ記事と2列（メイン記事とサイドバー）の構成にします。

完成したテーマは[こちら][1]。

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-19.26.39-1-433x1024.png" alt="" class="wp-image-1129" width="386" height="913" /></figure>
</div>

<pre class="wp-block-code"><code>
   &lt;!-- まずはmainタグをつくり、背景色を設定(bg-light) -->
   &lt;main class="bg-light">
        &lt;div class="container">

            &lt;!-- ピックアップコンテンツ欄をつくり、rowを付与し、styleをflex-wrapにする-->
            &lt;div class="row py-3">

                &lt;!-- 各コンテンツの幅を12分の4にする(col-md-4 col-12) -->
                &lt;div class="col-md-4 col-12">
                    &lt;div class="bg-white py-3">
                        &lt;!-- Thumbnail -->
                        &lt;div class="pb-3">

                            &lt;!-- 画像の幅を100%にし、高さはauto(img-fluid) -->
                            &lt;img class="img-fluid" src="img/img1.png" alt="">
                        &lt;/div>
                        &lt;!-- Title -->
                        &lt;h2 class="h4 px-3 pb-3">Lorem ipsum dolor, sit amet consectetur adipisicing elit.&lt;/h2>
                        &lt;!-- Button -->
                        &lt;div class="text-center">
                            &lt;a href="#">
                                &lt;div class="d-inline-block border p-3 text-secondary">
                                    Read more
                                &lt;/div>
                            &lt;/a>
                        &lt;/div>
                    &lt;/div>
                &lt;/div>
            &lt;/div>

            &lt;!-- ここからメインのコンテンツ -->
            &lt;div class="row py-3">
                &lt;div class="col-md-8 col-12">
                    &lt;div class="bg-white py-3 text-center mb-3">
                        &lt;!-- Date -->
                        &lt;p>2020/1/22&lt;/p>
                        &lt;!-- Title -->
                        &lt;h2 class="px-3 pb-3 font-weight-bolder">Lorem ipsum dolor sit, amet consectetur!&lt;/h2>
                        &lt;!-- Category -->
                        &lt;p>&lt;a href="">WordPress&lt;/a>&lt;/p>
                        &lt;!-- Thumbnail -->
                        &lt;div class="pb-3">
                        &lt;img class="img-fluid" src="img/img1.png" alt="">
                        &lt;/div>
                        &lt;!-- Desription -->
                        &lt;p class="text-secondary">Lorem, ipsum dolor sit amet consectetur adipisicing elit. Ipsa dolorum nesciunt nulla, culpa earum assumenda, aspernatur illum sit magnam nobis voluptatum non necessitatibus minus perferendis, officiis reprehenderit sed modi cum.&lt;/p>
                        &lt;!-- Button -->
                        &lt;div class="text-center">
                            &lt;a href="">&lt;/a>
                            &lt;div class="d-inline-block border p-3 text-secondary">
                                Read more
                            &lt;/div>
                        &lt;/div>
                    &lt;/div>
                &lt;/div>
                &lt;!-- サイドバー -->
                &lt;div class="col-md-4 col-12">
                &lt;!-- Profile欄 -->
                &lt;div class="container bg-white mb-5 py-5">
                &lt;div class="mx-5">
                &lt;img class="img-fluid rounded-circle" src="img/profile.jpg" alt="profile_icon">
                &lt;/div>
                &lt;div class="text-center">
                    &lt;h4 class="d-inline-block py-3 border-bottom border-info">KAORU MITSUMORI&lt;/h4>
                &lt;/div>
                &lt;p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Nihilo. Lorem ipsum dolor sit amet consectetur adipisicing elit, Nihilo.&lt;/p>
                &lt;/div>
                &lt;!-- Search -->
                &lt;div class="container bg-white mb-5 py-5">
                    &lt;form>
                        &lt;input type="text" class="form-control" placeholder="Search for">
                    &lt;/form>
                &lt;/div>
                &lt;!-- Recommend -->
                &lt;div class="container bg-white mb-5 py-5">
                    &lt;div class="text-center pb-5">
                        &lt;h4 class="d-inline-block py-3 border-bottom border-info">Recommend&lt;/h4>
                    &lt;/div>
                    &lt;div class="pb-5">
                        &lt;!-- Thumbnail -->
                        &lt;div class="pb-3">
                            &lt;img class="img-fluid" src="img/img1.png" alt="">
                        &lt;/div>
                        &lt;!-- Title -->
                        &lt;h5 class="h5">Lorem ipsum dolor sit amet consectetur adipisicing elit. Nihilo. &lt;/h5>
                    &lt;/div>
                &lt;/div>
            &lt;/div>
        &lt;/div>
    &lt;/main>
</code></pre>

<form></form>の部分については、BootstrapでFormと検索し、コードをコピーしてください。

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-28-at-12.55.46-1024x677.png" alt="" class="wp-image-1140" width="567" height="374" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-28-at-12.55.46-1024x677.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-28-at-12.55.46-300x198.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-28-at-12.55.46-768x507.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-28-at-12.55.46-1536x1015.png 1536w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-28-at-12.55.46-2048x1353.png 2048w" sizes="(max-width: 567px) 100vw, 567px" /></figure>
</div>

あとは、ピックアップコンテンツ、メインのコンテンツ、オススメ記事を複製すれば完成です。  
  
また、class=&#8221;row&#8221;のstyle、flex-wrapやがわからなければ、こちらを見てください。

<blockquote class="wp-block-quote">
  <p>
    <a rel="noreferrer noopener" aria-label=" (新しいタブで開く)" href="https://kaorumitsumori.com/starting-flexbox/" target="_blank">【基礎はこれだけ】CSSのFlexboxの使い方</a>
  </p>
</blockquote>

続きは[こちら][2]です！

 [1]: http://kaorumitsumori.com/MySimple_html/index.html
 [2]: https://kaorumitsumori.com/starting-bootstrap3