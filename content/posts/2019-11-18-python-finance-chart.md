---
title: Pythonを使ってビットコインのチャートっぽいものを再現してみた
author: KAORU
type: post
date: 2019-11-18T11:47:21+00:00
url: /python-finance-chart/
featured_image: /wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-20.23.27.png
siteorigin_page_settings:
  - 'a:6:{s:6:"layout";s:7:"default";s:10:"page_title";b:1;s:15:"masthead_margin";b:1;s:13:"footer_margin";b:1;s:16:"display_masthead";b:1;s:22:"display_footer_widgets";b:1;}'
page_type:
  - default
categories:
  - Data science
  - Programming
tags:
  - finance
  - python

---
PythonにはMatplotlibというライブラリがある。これはグラフなどを使って、データをわかりやすく可視化するためのもので、棒グラフ、円グラフ、ヒストグラムなどの形態で見える化できる。  
今回は完全にランダムな数字を使って、ビットコインなんかの金融データのチャートを再現してみる。

<pre class="wp-block-code"><code>#matplotlib.pyplotをpltという名付けでインポート
import matplotlib.pyplot as plt

#numpyをnpという名付けでインポート
import numpy as np

#ランダムに数字を生成できるrandomというnumpyの機能をインポート
from numpy import random</code></pre>

Matplotlib、数値計算のライブラリであるNumpy、それとNumpyの機能のひとつで乱数を発生させるrandom関数をインポートした。  
寄り道してrandom関数についてちょこっと説明。

<pre class="wp-block-code"><code>#randnを使うと正規分布(平均0、標準偏差1)の乱数を発生させられる
#100個発生させるなら下記
n = random.randn(100)

#nは配列形式になっている
array(&#91;-2.14971193, -2.09685556, -2.0439992 , -1.99114283, -1.93828646,
        -1.8854301 , -1.83257373, -1.77971737, -1.726861  , -1.67400463,
        -1.62114827, -1.5682919 , -1.51543554, -1.46257917, -1.40972281,
        -1.35686644, -1.30401007, -1.25115371, -1.19829734, -1.14544098,
        -1.09258461, -1.03972824, -0.98687188, -0.93401551, -0.88115915,
        -0.82830278, -0.77544641, -0.72259005, -0.66973368, -0.61687732,
        -0.56402095, -0.51116458, -0.45830822, -0.40545185, -0.35259549,
        -0.29973912, -0.24688275, -0.19402639, -0.14117002, -0.08831366,
        -0.03545729,  0.01739908,  0.07025544,  0.12311181,  0.17596817,
         0.22882454,  0.28168091,  0.33453727,  0.38739364,  0.44025   ,
         0.49310637,  0.54596274,  0.5988191 ,  0.65167547,  0.70453183,
         0.7573882 ,  0.81024457,  0.86310093,  0.9159573 ,  0.96881366,
         1.02167003,  1.07452639,  1.12738276,  1.18023913,  1.23309549,
         1.28595186,  1.33880822,  1.39166459,  1.44452096,  1.49737732,
         1.55023369,  1.60309005,  1.65594642,  1.70880279,  1.76165915,
         1.81451552,  1.86737188,  1.92022825,  1.97308462,  2.02594098,
         2.07879735,  2.13165371,  2.18451008,  2.23736645,  2.29022281,
         2.34307918,  2.39593554,  2.44879191,  2.50164828,  2.55450464,
         2.60736101,  2.66021737,  2.71307374,  2.76593011,  2.81878647,
         2.87164284,  2.9244992 ,  2.97735557,  3.03021194,  3.0830683 ,
         3.13592467]),

#ヒストグラムでnを観察する
plt.hist(n,bins=100)</code></pre>

100個だから少なくてわかりにくいけど、nは正規分布(下図)<figure class="wp-block-image">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-19.57.40.png" alt="" class="wp-image-82" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-19.57.40.png 728w, https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-19.57.40-300x204.png 300w" sizes="(max-width: 728px) 100vw, 728px" /></figure> 

さすがに10,000個も乱数を発生させると、よく見る正規分布らしい形状になる。(下図)  
あと当然だけど、数が多いほど偏差1の範囲を逸脱する件数もかなり多いのが個人的にはおもしろい。<figure class="wp-block-image">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-20.01.02.png" alt="" class="wp-image-83" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-20.01.02.png 754w, https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-20.01.02-300x195.png 300w" sizes="(max-width: 754px) 100vw, 754px" /></figure> 

<p class="has-text-align-left">
  ほかにもrandom関数では、いろんな条件で乱数を発生させられる。正規分布だけでなく、一様分布、ベータ分布、ガンマ分布。平均値や標準偏差や出現範囲も自由に設定できる。<br />さて話が逸れたが、金融データのチャートを再現するためのx軸とy 軸の値を設定していく。
</p>

<pre class="wp-block-code"><code>#x軸は0~10,000の自然数の配列
x = np.arange(10001)

#y軸は正規分布(平均0、標準偏差1)の乱数をランダムに並べ、
#それまでの和を順に並べた配列
#.cumsum()でそれまでの和を計算できる
y = np.random.randn(10001).cumsum()

#xとyを順番に対応させ、折れ線グラフにしてみる
plt.plot(x, y)
plt.grid(True)</code></pre><figure class="wp-block-image">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-20.23.27-1024x317.png" alt="" class="wp-image-87" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-20.23.27-1024x317.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-20.23.27-300x93.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/11/Screen-Shot-2019-11-18-at-20.23.27-768x238.png 768w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure> 

結果が上の図だけど、ぼくはこれをはじめて見たときぶっちゃけ感動した。

FXなどのトレーダーの界隈では、値が上がっている流れのときに上昇トレンド(反対は下落トレンド)とか言ったりする。買いが買いを呼んだり、あるいは上昇トレンドが続くと、利益を確定させるための売りなどがトリガーになって下落トレンドに反転する。当然逆も然りだ。基本的に金融データの値動きでは、ミクロでもマクロでも、このシーソーゲームの応酬が起きている。

つまり何が言いたいかと言うと、リアルワールドの値動きでは人間のselfishな思惑が織り込まれてあのようなチャートの形態になっているのにも関わらず、そのような思惑の入り込まないランダムでできたチャートと、ほとんど変わらない形をしているのだ。上昇トレンドや下落トレンドらしきものも、ミクロでもマクロでもあるっぽく見える。  
一人ひとりのプレイヤーが考えていることって、あまりにも多様すぎて全体から見たらランダムみたいなものでしょ？って言われている気がした。トレードだけでなくいろんなことにおいて。

もしかすると、きちんと定量的に調べたら違いがあるのかもしれない。リアルのチャートでは、たとえば1秒ごとの増減の差分が正規分布になるとは思えない、なんとなくだけど。（[検証したら正規分布になることが判明した][1]）どちらにしてもすこぶるおもしろいし、もっと深堀りしてみたいと思った。

&nbsp;

 [1]: https://kaorumitsumori.com/appl-stock-price/