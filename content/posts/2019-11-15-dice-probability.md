---
title: サイコロを1億回ふってそれぞれの目がでる確率を計算してみた
author: KAORU
type: post
date: 2019-11-15T14:26:55+00:00
url: /dice-probability/
siteorigin_page_settings:
  - 'a:6:{s:6:"layout";s:7:"default";s:10:"page_title";b:1;s:15:"masthead_margin";b:1;s:13:"footer_margin";b:1;s:16:"display_masthead";b:1;s:22:"display_footer_widgets";b:1;}'
page_type:
  - default
categories:
  - Data science
  - Programming
tags:
  - python

---
サイコロをふったときのそれぞれの目がでる確率を、PythonのNumpyというライブラリを使って計算してみた。

<pre class="wp-block-code"><code>#Numpyというライブラリをnpという名前で読み込む
import numpy as np

#サイコロの目（1〜6）を設定する
dice = np.arange(1,7)

#diceは配列の形式になる
array([1, 2, 3, 4, 5, 6])

#サイコロをふる回数nは1億（10の8乗）回
n = 10 ** 8

#1億回ふって出た目を順に並べる
result = np.random.choice(dice, n)

#resultも配列の形式
array([5, 2, 6, 1, 5, .... 6, 3])

#たとえば3がresultの中にいくつあるかをカウントするときは
#lenを以下のように使う
len(result[result == 3])

#resultの中の3の個数
16664506

#よって確率はこれで計算できる
len(result[result == 3]) / n

#for文でそれぞれの目の確率pを一度に計算する
for x in range(1,7):
  p = len(result[result == x]) / n
  print('Probability of ',x,' is ',p)

#結果
Probability of 1 is 0.16664859
Probability of 2 is 0.1667152
Probability of 3 is 0.16664506
Probability of 4 is 0.16670248
Probability of 5 is 0.16663413
Probability of 6 is 0.16665454</code></pre>

こんな感じで、1億回もふるとどれもほぼ同じ確率になる。  
ちなみに10,000回、100回のときの結果は以下のようになった。

<pre class="wp-block-code"><code>#サイコロを10,000回ふったとき（n = 10 ** 4）
Probability of  1  is  0.1633
Probability of  2  is  0.164
Probability of  3  is  0.1748
Probability of  4  is  0.1691
Probability of  5  is  0.1646
Probability of  6  is  0.1642

#サイコロを100回ふったとき（n = 10 ** 2）
Probability of  1  is  0.2
Probability of  2  is  0.1
Probability of  3  is  0.18
Probability of  4  is  0.14
Probability of  5  is  0.14
Probability of  6  is  0.21</code></pre>

試行回数を減らすと、それぞれの確率のばらつきが目立つ。  
このように試行回数が増えると、確率や平均値などが理論値に近づくことを「大数の法則」という。