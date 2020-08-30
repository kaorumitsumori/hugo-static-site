---
title: 毒キノコを判別するモデルを決定木で構築する
author: KAORU
type: post
date: 2019-12-05T06:21:45+00:00
url: /poisonous-mushroom-decision-tree/
featured_image: /wp-content/uploads/2019/12/1.png
categories:
  - Data science
  - Programming
tags:
  - python

---
キノコの形状、色、におい、生息地などの属性から、食用キノコか毒キノコかを判別するモデルを決定木（Decision Tree）を使って作ってみる。

  1. データをダウンロードし、加工する
  2. 説明変数を選び、ダミー変数に変換（get_dummies）する
  3. 決定木でモデルを作り、決定係数で精度を確認する

## データをダウンロードし、加工する

<pre class="wp-block-code"><code>url = 'http://archive.ics.uci.edu/ml/machine-learning-databases/mushroom/agaricus-lepiota.data'
a = requests.get(url).content
mr = pd.read_csv(io.StringIO(a.decode('utf-8')), header=None)

#試しに5列を表示
mr.head()</code></pre><figure class="wp-block-image is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/1.png" alt="" class="wp-image-420" width="526" height="148" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/1.png 962w, https://kaorumitsumori.com/wp-content/uploads/2019/12/1-300x85.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/1-768x216.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/1-960x271.png 960w" sizes="(max-width: 526px) 100vw, 526px" /></figure> 

このままだと、列の名前が0~22の数字になっており、なんの属性なのかまったくわからない。

<pre class="wp-block-code"><code>#列の名前を追加する
mr.columns = 
&#91;'classes','cap_shape','cap_surface','cap_color','odor','bruises',
                             'gill_attachment','gill_spacing','gill_size','gill_color','stalk_shape',
                             'stalk_root','stalk_surface_above_ring','stalk_surface_below_ring',
                             'stalk_color_above_ring','stalk_color_below_ring','veil_type','veil_color',
                             'ring_number','ring_type','spore_print_color','population','habitat']

mr.head()</code></pre><figure class="wp-block-image is-resized">

<img class="wp-image-421 alignnone" src="https://kaorumitsumori.com/wp-content/uploads/2019/12/2-1024x190.png" alt="" width="532" height="99" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/2-1024x190.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/2-300x56.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/2-768x142.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/2.png 1194w" sizes="(max-width: 532px) 100vw, 532px" /></figure> 

列の名前を付与することができた。  
各列の項目は以下を指している。

<pre class="lang:default decode:true">classes | 毒キノコか否か（毒キノコ=p, 食用キノコ=e）
cap-shape | 傘形状（ベル型=b, 円錐型=c, 饅頭型=x, 扁平型=f, コブ型=k, 凹んだ扁平型=s）
cap-surface | 傘表面（繊維=f, 溝=g, 鱗片=y, 滑らか=s）
cap-color | 傘の色（ブラウン=n, バフ=b, シナモン=c, グレー=g, グリーン=r, ピンク=p, パープル=u, レッド=e, ホワイト=w, イエロー=y）
odor | 臭気（アーモンド=a, アニス=l, クレオソート=c, フィッシュ=y, ファウル=f, ミューズイ=m, なし=n, 辛味=p, スパイシー=s）
bruises | 斑点（斑点あり=t, 斑点なし=f）
gill-attachment | ひだの付き方（直生=a, 垂生=d, 離生=f, 凹生=n）
gill-spacing | ひだの間隔（近い=c, 過密=w, 長い=d）
gill-size | ひだのサイズ（広い=b, 狭い=n）
gill-color | ひだの色（ブラック=k, ブラウン=n, バフ=b, チョコレート=h, グレー=g, グリーン=r, オレンジ=o, ピンク=p, パープル=u, レッド=e, ホワイト=w, イエロー=y）
stalk-shape | 柄の形状（広がり=e, 先細り=t）
stalk-root | 柄の根（球根=b, クラブ=c, カップ=u, 等しい=e 根茎形態=z, 根=r, 無し=？）
stalk-surface-above-ring | 柄表面-上記リング（繊維状=f, 鱗片状=y, 絹毛=k, 滑らか=s）
stalk-surface-below-ring | 柄-表面下のリング（繊維状=f, 鱗片状=y, 絹毛=k, 滑らか=s）
stalk-color-above-ring | 柄の色-上記リング（ブラウン=n, バフ=b, シナモン=c, グレー=g, オレンジ=o, ピンク=p, 赤=e, 白=w, 黄色=y）
stalk-color-below-ring | 柄-カラーリング下（ブラウン=n, バフ=b, シナモン=c, グレー=g, オレンジ=o, ピンク=p, 赤=e, 白=w, 黄色=y）
veil-type | つぼの種類（内皮膜=p, 外皮膜=u）
veil-color | つぼの色（ブラウン=n, オレンジ=o, ホワイト=w, イエロー=y）
ring-number | つばの数（none=n, one=o, two=t）
ring-type | つばの種類（クモの巣状=c, 消失性=e, 炎のような=f, 大きな=l, 無し=n, 垂れた=p, 鞘=s, 環帯=z）
spore-print-color | 胞子の色（ブラック=k, ブラウン=n, バフ=b, チョコレート=h, グリーン=r, オレンジ=o, パープル=u, ホワイト=w, イエロー=y）
population | 集団形成方法（大多数=a, 群れを成して=c, 多数=n, 分散=s, 数個=v, 孤立=y）
habitat | 生息地（牧草=g, 葉=1, 牧草地=m, 小道=p, 都市=u, 廃棄物=w, 森=d）</pre>

つぎに、行と列の数と、欠損値について調べる。

<pre class="wp-block-code"><code>print('data form : {}'.format(mr.shape))
print('data defection : \n{}'.format(mr.isnull().sum()))</code></pre>

<pre class="wp-block-code"><code>#Output

data form : (8124, 23)
data defection :
0     0
1     0
2     0
3     0
4     0
5     0
6     0
7     0
8     0
9     0
10    0
11    0
12    0
13    0
14    0
15    0
16    0
17    0
18    0
19    0
20    0
21    0
22    0
dtype: int64</code></pre>

形状は縦8124行、横23列、各列の欠損値の数は全て0であることが分かる。

## 説明変数を選び、ダミー変数に変換する（get_dummies）

今回は、下記の4つの説明変数を利用することにする。

  * &#8216;cap_surface&#8217;, 傘表面（繊維=f, 溝=g, 鱗片=y, 滑らか=s）
  * &#8216;odor&#8217;, 臭気（アーモンド=a, アニス=l, クレオソート=c, フィッシュ=y, ファウル=f, ミューズイ=m, なし=n, 辛味=p, スパイシー=s）
  * &#8216;bruises&#8217;, 斑点（斑点あり=t, 斑点なし=f）
  * &#8216;habitat&#8217;, 生息地（牧草=g, 葉=1, 牧草地=m, 小道=p, 都市=u, 廃棄物=w, 森=d）

<pre class="wp-block-code"><code>#4つの説明変数を0 or 1で表現できるようにダミー変数にする
mrd = pd.get_dummies(mr&#91;&#91;'cap_surface', 'odor', 'bruises', 'habitat']])

#目的変数も定量化（0 or 1）する
mrd&#91;'poisonous'] = mr&#91;'classes'].map(lambda x: 1 if x =='p' else 0)
mrd.head()</code></pre><figure class="wp-block-image is-resized">

<img class="wp-image-422" src="https://kaorumitsumori.com/wp-content/uploads/2019/12/3-1024x173.png" alt="" width="537" height="91" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/3-1024x173.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/3-300x51.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/3-768x130.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/3.png 1224w" sizes="(max-width: 537px) 100vw, 537px" /></figure> 

つぎに、斑点なし（bruises_f）と有毒キノコ（poisonous）の件数のバランスを試しに確認してみる。

<pre class="wp-block-code"><code>mrd.groupby(&#91;'bruises_f', 'poisonous'])&#91;'poisonous'].count().unstack()</code></pre><figure class="wp-block-image is-resized">

<img class="wp-image-425" src="https://kaorumitsumori.com/wp-content/uploads/2019/12/5-1.png" alt="" width="195" height="130" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/5-1.png 308w, https://kaorumitsumori.com/wp-content/uploads/2019/12/5-1-300x201.png 300w" sizes="(max-width: 195px) 100vw, 195px" /></figure> 

どうやら、斑点なし（bruises_f=1）の食用キノコ（poisonous=0）の件数は0のようだ。

## 決定木でモデルを作り、決定係数で精度を確認する

<pre class="wp-block-code"><code>from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import  train_test_split

#xに説明変数、yに目的変数を設定
x = mrd.drop('poisonous', axis=1)
y = mrd&#91;'poisonous']

#x.yそれぞれをトレーニング用、テスト用とに分ける
xtrain, xtest, ytrain, ytest = train_test_split(x, y, random_state=1)

#entropyというアルゴリズムを使って、5層まで分岐を繰り返す決定木モデルを作成
mode = DecisionTreeClassifier(criterion='entropy', max_depth=5, random_state=1)

#そのモデルにトレーニング用x,yを当てはめ、x,y間の関数をつくる
mode.fit(xtrain, ytrain)

#その関数を使った結果の正答率（R2）をトレーニング用、テスト用それぞれで算出
print('R2 of Train data : {:.3f}'.format(mode.score(xtrain, ytrain)))
print('R2 of Test data : {:.3f}'.format(mode.score(xtest, ytest)))</code></pre>

<pre class="wp-block-code"><code>#Output

R2 of Train data : 0.997
R2 of Test data : 0.994</code></pre>

これはトレーニング用x,yをもとにした関数が、テスト用x,yに当てはめても99%以上の正当率を出しており、さらにトレーニング用、テスト用それぞれでの正当率にほぼ乖離がないということを示している。

トレーニング用、テスト用それぞれの正当率での乖離具合は、過学習の度合いを表現している。今回は過学習をしていない良いモデルを作成できたと言える。