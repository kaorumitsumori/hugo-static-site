---
title: Bootstrapで0から簡単なホームページをつくる手順【フッターをつくる】
author: KAORU
type: post
date: 2020-01-25T02:48:21+00:00
url: /starting-bootstrap3/
featured_image: /wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-11.22.51.png
categories:
  - Front-end development
  - Programming
tags:
  - bootstrap
  - css
  - html
  - wordpress

---
[前回][1]でメインコンテンツをコーディングしたので、今回はこのようなフッターをつくります。  
フッターは、「About」「Portfolio」「Twitter」の3カラム（列）とコピーライトの黒いバーの構成にします。

完成したテーマは[こちら][2]。

<pre class="wp-block-code"><code>
&lt;footer class="bg-white">
        &lt;div class="container">

            &lt;!-- 以下の3つの列が横並びになるようにdisplay: flex;を付与（class="row"） -->
            &lt;div class="row">

                &lt;!-- Aboutコンテンツ -->
                &lt;div class="col-md-4 col-12">
                    &lt;div class="pb-5">
                        &lt;h4 class="d-inline-block py-3 border-bottom border-info">About&lt;/h4>
                    &lt;/div>
                    &lt;p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Eligendi error hic reprehenderit suscipit iure illum, ut, similique unde blanditiis ullam iusto possimus nulla molestias impedit quibusdam nam asperiores eum. Adipisci!&lt;/p>
                &lt;/div>

                &lt;!-- Portfolioコンテンツ -->
                &lt;div class="col-md-4 col-12">
                    &lt;div class="pb-5">
                        &lt;h4 class="d-inline-block py-3 border-bottom border-info">Portfolio&lt;/h4>
                    &lt;/div>
                    &lt;div class="p-3 border-top border-bottom border-secondary">
                        &lt;a class="text-secondary" href="">kaorumitsumori.com&lt;/a>
                    &lt;/div>
                    &lt;div class="p-3 border-top border-bottom border-secondary">
                        &lt;a class="text-secondary" href="">kaorumitsumori.com&lt;/a>
                    &lt;/div>
                    &lt;div class="p-3 border-top border-bottom border-secondary">
                        &lt;a class="text-secondary" href="">kaorumitsumori.com&lt;/a>
                    &lt;/div>
                &lt;/div>

                &lt;!-- Twitterコンテンツ -->
                &lt;div class="col-md-4 col-12">
                    &lt;div class="pb-5">
                        &lt;h4 class="d-inline-block py-3 border-bottom border-info">Twitter&lt;/h4>
                    &lt;/div>
                    &lt;a class="twitter-timeline" data-lang="en" data-height="600" href="https://twitter.com/kaorumitsumori?ref_src=twsrc%5Etfw">Tweets by kaorumitsumori&lt;/a>
                    &lt;script async src="https://platform.twitter.com/widgets.js" charset="utf-8">&lt;/script>
                &lt;/div>  
            &lt;/div>
        &lt;/div>
        &lt;div class="bg-dark text-white text-center p-3">
            Copyright - KAORU MITSUMORI, 2020 All Right Reserved.
        &lt;/div>
    &lt;/footer></code></pre>

Twitterの埋め込みコードを取得するには、<a href="https://publish.twitter.com" target="_blank" rel="noreferrer noopener" aria-label=" (新しいタブで開く)">こちら</a>からどうぞ。

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-11.40.13-1024x701.png" alt="" class="wp-image-1237" width="488" height="334" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-11.40.13-1024x701.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-11.40.13-300x205.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-11.40.13-768x526.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-11.40.13-1536x1052.png 1536w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-11.40.13-2048x1402.png 2048w" sizes="(max-width: 488px) 100vw, 488px" /><figcaption>ここにアカウントのURLを入力</figcaption></figure>
</div>

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-11.42.39-1024x921.png" alt="" class="wp-image-1238" width="490" height="440" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-11.42.39-1024x921.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-11.42.39-300x270.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-11.42.39-768x691.png 768w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-30-at-11.42.39.png 1474w" sizes="(max-width: 490px) 100vw, 490px" /><figcaption>左の&#8221;Embedded Timeline&#8221;を選び、heightは600にしました。</figcaption></figure>
</div>

また、flexの使い方がイマイチならこちらを見ておくといいかもです！

<blockquote class="wp-block-quote">
  <p>
    <a href="https://kaorumitsumori.com/starting-flexbox/">【基礎はこれだけ】CSSのFlexboxの使い方</a>
  </p>
</blockquote>

  
これで、ヘッダー、メインコンテンツ、フッターが完成しました。

 [1]: https://kaorumitsumori.com/starting-bootstrap2/
 [2]: http://kaorumitsumori.com/MySimple_html/index.html