---
title: アップル過去50年の株価をPythonで解析してみた
author: KAORU
type: post
date: 2019-12-03T14:16:03+00:00
url: /appl-stock-price/
featured_image: /wp-content/uploads/2019/12/frame.png
page_type:
  - default
update_level:
  - high
categories:
  - Data science
  - Programming
tags:
  - finance
  - python
  - sidepicking

---
[乱数を発生させるNumpyのrandom関数を利用して、金融データのチャートを再現してみた][1]が、これを作るとき、時々刻々の変動幅が標準偏差1の正規分布になるようにランダムに出力している。

しかしランダムに出力したにも関わらず、このように現実のチャートに非常に近しい形をしているのが不思議だった。  
「もしかして株価などの現実の金融データも、一定時間ごとの変動幅が正規分布になっているのでは？」と思ったので、アップルの株価を使って検証してみることにした。

<div class="wp-block-image">
  <figure class="aligncenter is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-20.23.27-1024x317.png" alt="random_walk" class="wp-image-87" width="540" height="168" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-20.23.27-1024x317.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-20.23.27-300x93.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-20.23.27-768x238.png 768w" sizes="(max-width: 540px) 100vw, 540px" /><figcaption>ランダムの賜物だが、現実のチャートに非常に近しい</figcaption></figure>
</div>

  1. pandasを使って株価をimportする
  2. 日ごとの変化率(%)を計算する
  3. ヒストグラムを描く

## pandasを使って株価をimportする

<pre class="wp-block-code"><code># 必要なライブラリをimport
import pandas_datareader as pdd
from datetime import datetime

end = datetime.now()
start = datetime(end.year - 50, end.month, end.day)

#Yahooからアップル(AAPL)の株価データを取得
data = pdd.DataReader('AAPL', 'yahoo', start, end)

type(data)
#pandas.core.frame.DataFrame

data.head()</code></pre><figure class="wp-block-image is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/frame-1024x395.png" alt="" class="wp-image-395" width="494" height="190" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/frame-1024x395.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/frame-300x116.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/frame-768x297.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/frame-320x124.png 320w, https://kaorumitsumori.com/wp-content/uploads/2019/12/frame.png 1028w" sizes="(max-width: 494px) 100vw, 494px" /></figure> 

## 日ごとの変化率(%)を計算する

<pre class="wp-block-code"><code>#pct_change()を使って1日ごとの終値の変化率をパーセンテージ化し、
#結果を列としてdataに追加する
data&#91;'Daily Change Rate'] = data&#91;'Adj Close'].pct_change()

data&#91;'Daily Change Rate']
#Date
#1980-12-12         NaN
#1980-12-15   -0.052174
#1980-12-16   -0.073394
#1980-12-17    0.024752
#1980-12-18    0.028986
#                ...   
#2019-11-26   -0.007809
#2019-11-27    0.013432
#2019-11-29   -0.002203
#2019-12-02   -0.011562
#2019-12-03   -0.017830
#Name: Daily Change Rate, Length: 9827, dtype: float64

type(data&#91;'Daily Change Rate'])
#pandas.core.series.Series</code></pre>

## ヒストグラムを描く

<pre class="wp-block-code"><code>＃いよいよ結果を図示してみる。まずは変化率をプロット
data&#91;'Daily Change Rate'].plot(figsize=(24,8), linestyle='--', marker='o')</code></pre>

<div class="wp-block-image">
  <figure class="alignleft is-resized"><img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/plo-1024x329.png" alt="" class="wp-image-396" width="494" height="159" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/plo-1024x329.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/plo-300x96.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/plo-768x247.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/plo-320x103.png 320w, https://kaorumitsumori.com/wp-content/uploads/2019/12/plo.png 1252w" sizes="(max-width: 494px) 100vw, 494px" /></figure>
</div>

<pre class="wp-block-code"><code>#ヒストグラムを描く
data&#91;'Daily Change Rate'].hist(bins=200, range = (-0.2, 0.2))</code></pre><figure class="wp-block-image is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/data.png" alt="" class="wp-image-397" width="448" height="293" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/data.png 582w, https://kaorumitsumori.com/wp-content/uploads/2019/12/data-300x196.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/data-320x209.png 320w" sizes="(max-width: 448px) 100vw, 448px" /></figure> 

見事な正規分布になっている。  
つまり金融データの一定時間ごとの増減は 、 短期的に見ればランダムで決まっており、 増減の確率はほぼ1/2ずつだということになる。

 [1]: https://kaorumitsumori.com/python-finance-chart/