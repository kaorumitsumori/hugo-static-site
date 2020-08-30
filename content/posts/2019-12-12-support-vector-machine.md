---
title: サポートベクターマシンを使ってガンの判別をする
author: KAORU
type: post
date: 2019-12-12T03:47:21+00:00
url: /support-vector-machine/
featured_image: /wp-content/uploads/2019/12/sv-825x367.jpg
categories:
  - Data science
  - Programming
tags:
  - python

---
サポートベクターマシン（Support Vector Machine）とは、データ群をdivide、分類する境界線を、境界線の周りのデータに接しないスペースが最大になるように引く手法である。（マージンに接するようなデータのことをサポートベクトルという。）

実際には、直線によって完全に分類できることは少ないので、ソフトマージンという手法を使う。  
ソフトマージンでは、境界線とデータがなるべく離れており、誤判別はなるべく少なくするような境界線を引く。

このとき、誤判別に対する許容度をCというパラメーターにより決める必要がある。このようにモデルの構築時に、人間によって設定する定数をハイパーパラメーターという。ハイパーパラメーターはモデルの精度に影響を与える。

サポートベクターマシンモデルをインスタンス化するときにCを設定できるが、設定せずともデフォルト値C=1として進められる。Cが大きいほど誤判別に対して厳しいモデルとなり、∞に大きいときはハードマージンと呼ばれる。

## SVCとLinearSVC

SVC（SVM Classification）は標準的なソフトマージンのサポートベクターマシン（SVM）。 一方、LinearSVCは直線で分離するSVM。直線で分離できないときはソフトマージンを使う。

## SVMでガンの判別をする

<pre class="wp-block-code"><code>
import numpy as np
import numpy.random as random
import scipy as sp
import pandas as pd
from pandas import Series, DataFrame

import matplotlib.pyplot as plt
import matplotlib as mlp
import seaborn as sns

import sklearn
from sklearn.svm import LinearSVC

#訓練データとテストデータを分けるライブラリ
from sklearn.model_selection import train_test_split

#データの読み込み
from sklearn.datasets import load_breast_cancer
cancer = load_breast_cancer()</code></pre>

sklearnには、各種のデータセットが格納されているので、今回はガンのデータを読み込む

<pre class="wp-block-code"><code>
from sklearn.datasets import load_breast_cancer
cancer = load_breast_cancer()</code></pre>

<pre class="wp-block-code"><code>
type(cancer)
#
sklearn.utils.Bunch

#辞書形式のように、下記の項目ごとに数字が格納されている
cancer.keys()
#
dict_keys(&#91;'data', 'target', 'target_names', 'DESCR', 'feature_names', 'filename'])dict_keys(&#91;'data', 'target', 'target_names', 'DESCR', 'feature_names', 'filename'])</code></pre>

<pre class="wp-block-code"><code>
#各特徴量にラベルを貼り、Pandasに変換する
cancer_pd = pd.DataFrame(cancer.data,columns=cancer.feature_names)
cancer_pd.head()</code></pre><figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/setsumei.jpg" alt="" class="wp-image-707" width="535" height="146" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/setsumei.jpg 801w, https://kaorumitsumori.com/wp-content/uploads/2019/12/setsumei-300x82.jpg 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/setsumei-768x211.jpg 768w" sizes="(max-width: 535px) 100vw, 535px" /></figure> 

<pre class="wp-block-code"><code>
#目的変数もPandasに変換しておく
cancer_tg = pd.DataFrame(cancer.target)</code></pre>

### SVMモデルにデータを当てはめる

<pre class="wp-block-code"><code>
#訓練データとテストデータに分ける
xtrain, xtest, ytrain, ytest = train_test_split(
    cancer_pd, cancer_tg, stratify = cancer.target, random_state=0)

#LinearSVCモデルをインスタンス化、Cは1とする
model = LinearSVC(C=1)
model.fit(xtrain, ytrain)

#決定係数は？
print('R2(train):{:.3f}'.format(model.score(xtrain, ytrain)))
print('R2(test):{:.3f}'.format(model.score(xtest, ytest)))

#
R2(train):0.852
R2(test):0.902</code></pre>