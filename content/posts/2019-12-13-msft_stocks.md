---
title: マイクロソフト株の金融指標をPythonで可視化する
author: KAORU
type: post
date: 2019-12-13T06:00:00+00:00
url: /msft_stocks/
featured_image: /wp-content/uploads/2019/12/candle-825x426.jpg
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
[アップルの株価の日ごとの変動をヒストグラムにしてみた][1]が、ほかの金融指標についてもmatplotlibやseabornなどのライブラリを使って表現できる。  
  
今回はマイクロソフト（ティッカーシンボルはMSFT）株のデータをimportして実行してみる。

  * 出来高と終値をプロット
  * 移動平均線
  * ローソクチャート

<pre class="wp-block-code"><code>
#各種ライブラリを準備する
import pandas as pd
from pandas import Series, DataFrame
import numpy as np

#可視化のためライブラリ
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style('whitegrid')

#金融データを読み込むためのライブラリ
from pandas.io.data import DataReader
import pandas_datareader as pdd

#Pythonで日付と時刻を扱うためのライブラリ
from datetime import datetime

#ローソクチャートのためのライブラリ
from plotly.offline import init_notebook_mode, iplot
from plotly import figure_factory as FF</code></pre>

<pre class="wp-block-code"><code>
#30年間の時間を設定
end = datetime.now()
start = datetime(end.year - 50, end.month, end.day)

#マイクロソフト株のデータを取得
MSFT = pdd.DataReader('MSFT', 'yahoo', start, end)

type(MSFT)
#
pandas.core.frame.DataFrame

MSFT.head()</code></pre><figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/msft.jpg" alt="" class="wp-image-729" width="483" height="176" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/msft.jpg 891w, https://kaorumitsumori.com/wp-content/uploads/2019/12/msft-300x110.jpg 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/msft-768x281.jpg 768w" sizes="(max-width: 483px) 100vw, 483px" /></figure> 

## 出来高と終値をプロット

<pre class="wp-block-code"><code>
#出来高を図示
plt.figure(figsize=(10,4))
plt.plot(MSFT&#91;'Volume'])
plt.legend=True</code></pre><figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/vol.jpg" alt="" class="wp-image-730" width="474" height="201" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/vol.jpg 906w, https://kaorumitsumori.com/wp-content/uploads/2019/12/vol-300x128.jpg 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/vol-768x327.jpg 768w" sizes="(max-width: 474px) 100vw, 474px" /></figure> 

<pre class="wp-block-code"><code>
#終値を図示
plt.figure(figsize=(10,4))
plt.plot(MSFT&#91;'Adj Close'])
plt.legend=True</code></pre><figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/adj.jpg" alt="" class="wp-image-731" width="465" height="202" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/adj.jpg 924w, https://kaorumitsumori.com/wp-content/uploads/2019/12/adj-300x131.jpg 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/adj-768x335.jpg 768w" sizes="(max-width: 465px) 100vw, 465px" /></figure> 

## 移動平均線

移動平均を求めるには次の関数を使う。  
rolling(window=ma).mean()

<pre class="wp-block-code"><code>
#10, 20, 50, 150日ごとの平均値を算出する
distance_day = &#91;10, 20, 50, 150]

#DataFrameにそれぞれの数字を入れる列を作成し、
#各平均値をあてはめる
for x in distance_day:
    column_name = "MA {}".format(str(ma))
    MSFT&#91;column_name] = MSFT&#91;'Adj Close'].rolling(window=x).mean()

MSFT.head(10)</code></pre><figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/madata.jpg" alt="" class="wp-image-732" width="523" height="207" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/madata.jpg 992w, https://kaorumitsumori.com/wp-content/uploads/2019/12/madata-300x119.jpg 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/madata-768x306.jpg 768w" sizes="(max-width: 523px) 100vw, 523px" /><figcaption> &#8221;MA 10&#8221;の10行目から数字が現れ始めている</figcaption></figure> 

<pre class="wp-block-code"><code>#移動平均線を図示
MSFT&#91;&#91;'MA 10','MA 20','MA 50','MA 150']].plot(subplots=False,figsize=(20,5))</code></pre><figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/rolling_line-1024x270.jpg" alt="" class="wp-image-734" width="505" height="132" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/rolling_line-1024x270.jpg 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/rolling_line-300x79.jpg 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/rolling_line-768x203.jpg 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/rolling_line.jpg 1197w" sizes="(max-width: 505px) 100vw, 505px" /></figure> 

## ローソクチャート

<pre class="wp-block-code"><code>
#Colaboratoryの場合、この関数を使う
def configure_plotly_browser_state():
  import IPython
  display(IPython.core.display.HTML('''
        &lt;script src="/static/components/requirejs/require.js">&lt;/script>
        &lt;script>
          requirejs.config({
            paths: {
              base: '/static/base',
              plotly: 'https://cdn.plot.ly/plotly-latest.min.js?noext',
            },
          });
        &lt;/script>
        '''))</code></pre>

<pre class="wp-block-code"><code>
#ローソクチャートの設定
candle = FF.create_candlestick(MSFT.Open, MSFT.High, MSFT.Low, MSFT.Close, dates = MSFT.index)

iplot(candle)</code></pre><figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/candle-1024x374.jpg" alt="" class="wp-image-735" width="499" height="182" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/candle-1024x374.jpg 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/candle-300x110.jpg 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/candle-768x281.jpg 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/candle.jpg 1166w" sizes="(max-width: 499px) 100vw, 499px" /></figure>

 [1]: https://kaorumitsumori.com/appl-stock-price/