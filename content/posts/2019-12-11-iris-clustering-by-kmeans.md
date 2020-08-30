---
title: k-means法とアイリスの分類
author: KAORU
type: post
date: 2019-12-11T05:49:28+00:00
url: /iris-clustering-by-kmeans/
featured_image: /wp-content/uploads/2019/12/shubham-sharma-xZer6PPfuxU-unsplash-scaled.jpg
categories:
  - Data science
  - Programming
tags:
  - python

---
k-means法とは、教師なし学習のクラスタリングモデルのうちの一手段である。これは目的変数（y）と説明変数（x）の関係性を探ろうとする手法ではなく、データそのものに潜んだメッセージやインサイトを発見するための手法である。

## k-means法のアルゴリズム

  1. 入力データをプロットし、そこにランダムなn個の点をプロット。それぞれをクラスタ1、クラスタ2、、、クラスタnと名付ける
  2. 入力データのそれぞれについて、n個の点の中で最も近いものを選び、それをグループの重心とする所属クラスタとする
  3. すべての入力データについて所属クラスタが決まったら、それぞれのクラスタの重心（平均）を計算
  4. 3で求めたn個の重心をそれぞれのクラスタの新しい重心点とする
  5. 2.3.4を繰り返し、重心の移動が0になるか、十分に小さくなったら終了<figure class="wp-block-embed-youtube wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio">

<div class="wp-block-embed__wrapper">
  <iframe title="アルゴリズムがデータを分ける様子を可視化した【K-means】【クラスタリング】" width="500" height="281" src="https://www.youtube.com/embed/4F80lCKzpEU?feature=oembed" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div></figure> <figure class="wp-block-embed-youtube wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio">

<div class="wp-block-embed__wrapper">
  <iframe title="Lecture 60 — The k Means Algorithm | Stanford University" width="500" height="281" src="https://www.youtube.com/embed/RD0nNK51Fp8?feature=oembed" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div></figure> 

## アイリスをそれぞれの特徴によって分類する

アイリスという青い花を、その花弁のサイズなどのデータをもとに分類してみる。

<pre class="wp-block-code"><code>
#アイリスのデータセットはsklearnによって用意されている
from sklearn import datasets

from sklearn.preprocessing import StandardScaler
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt</code></pre>

<pre class="wp-block-code"><code>
#データセットを取り込む
iris = datasets.load_iris()

#花弁サイズなどの特徴のデータセットを取り出す
feature = iris.data

#StandardScalerでデータの標準化
scaler = StandardScaler()
features_standardized = scaler.fit_transform(feature)</code></pre>

いくつのクラスタに分類すべきか。今回は答えを見てみると、アイリスの種類は、&#8217;setosa&#8217;, &#8216;versicolor&#8217;, &#8216;virginica&#8217;の3つあるようだ。

<pre class="wp-block-code"><code>
iris.target_names

#
array(&#91;'setosa', 'versicolor', 'virginica'], dtype='&lt;U10')</code></pre>

<pre class="wp-block-code"><code>
#インスタンス化。3種類なので、n_clusters=3とする
cluster = KMeans(n_clusters=3, random_state=0, n_jobs=-1)

#標準化したデータを当てはめる
model = cluster.fit(features_standardized)</code></pre>

<pre class="wp-block-code"><code>
#分類した後の結果
model.labels_.sort()
model.labels_

#
array(&#91;0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
       0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
       0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
       2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
       2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2], dtype=int32)</code></pre>

<pre class="wp-block-code"><code>
#一方でsklearnのデータセットの解答はこちら
iris.target

#
array(&#91;0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
       0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
       0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
       2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
       2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2])</code></pre>

<pre class="wp-block-code"><code>
#一致確認
model.labels_ == iris.target

#
array(&#91; True,  True,  True,  True,  True,  True,  True,  True,  True,
        True,  True,  True,  True,  True, False, False,  True,  True,
        True,  True,  True,  True,  True,  True,  True,  True,  True,
        True,  True,  True,  True,  True, False, False,  True,  True,
        True,  True,  True,  True,  True, False,  True,  True,  True,
        True,  True,  True,  True,  True,  True,  True,  True,  True,
        True,  True, False, False,  True, False, False,  True, False,
        True,  True,  True,  True,  True, False,  True,  True,  True,
       False,  True,  True,  True,  True,  True,  True,  True,  True,
        True,  True,  True,  True, False,  True, False,  True,  True,
        True,  True,  True, False,  True,  True,  True,  True, False,
        True, False, False, False, False, False, False, False, False,
       False, False, False, False, False, False, False, False, False,
       False, False, False, False, False, False, False, False, False,
       False, False, False, False, False, False, False, False, False,
       False, False, False, False, False, False, False, False, False,
       False, False, False, False, False, False])</code></pre>

<pre class="wp-block-code"><code>#正解率は？
np.count_nonzero(model.labels_ == iris.target)/len(model.labels_)

#
0.56</code></pre>