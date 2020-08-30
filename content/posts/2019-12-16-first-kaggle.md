---
title: Kaggleに初挑戦した話【結果は16221位/16862人】
author: KAORU
type: post
date: 2019-12-16T14:30:07+00:00
url: /first-kaggle/
featured_image: /wp-content/uploads/2019/12/97percent.png
categories:
  - Competition
  - Data science
  - Programming
tags:
  - kaggle
  - python

---
[Signate][1]に続き、<a rel="noreferrer noopener" aria-label="Kaggle (新しいタブで開く)" href="https://www.kaggle.com/" target="_blank">Kaggle</a>にも挑戦してみた。  
将来はバウンティハンター（賞金稼ぎ）になったり、コンペティションがきっかけで職が決まったり、友達ができたらいいなと思っている。

トライしたのは、Signateと同じタイタニックの問題。<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-19.09.26-1024x571.png" alt="" class="wp-image-869" width="527" height="293" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-19.09.26-1024x571.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-19.09.26-300x167.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-19.09.26-768x428.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-19.09.26-1536x856.png 1536w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-19.09.26-2048x1141.png 2048w" sizes="(max-width: 527px) 100vw, 527px" /><figcaption>[Titanic: Machine Learning from Disaster][2]</figcaption></figure> 

<pre class="wp-block-code"><code>
#必要なライブラリをインポート
import numpy as np
import pandas as pd

from sklearn.model_selection import train_test_split

#必要なデータセットをインポート
train = pd.read_csv('train.csv')
test = pd.read_csv('test.csv')
gender_submission = pd.read_csv('gender_submission.csv')</code></pre>

試しにデータの中身を見てみる。  
ちなみにウェブサイトにデータの説明があるので、こちら。<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-22.45.29-1-1024x808.png" alt="" class="wp-image-886" width="491" height="387" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-22.45.29-1-1024x808.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-22.45.29-1-300x237.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-22.45.29-1-768x606.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-22.45.29-1.png 1364w" sizes="(max-width: 491px) 100vw, 491px" /></figure> 

<pre class="wp-block-code"><code>
train.groupby('Sex')&#91;'Survived'].mean()
#
Sex
female    0.742038
male      0.188908
Name: Survived, dtype: float64

train.groupby('Pclass')&#91;'Survived'].mean()
#
Pclass
1    0.629630
2    0.472826
3    0.242363
Name: Survived, dtype: float64

train.groupby('Embarked')&#91;'Survived'].mean()
#
Embarked
C    0.553571
Q    0.389610
S    0.336957
Name: Survived, dtype: float64

age_range = &#91;0, 10, 20, 30, 40, 50, 80]
age_range_cut = pd.cut(train.Age, age_range)
train&#91;'Age_range'] = age_range_cut
pd.value_counts(age_range_cut)
#
(20, 30]    230
(30, 40]    155
(10, 20]    115
(40, 50]     86
(50, 80]     64
(0, 10]      64
Name: Age, dtype: int64

train.groupby('Age_range')&#91;'Survived'].mean()
#
Age_range
(0, 10]     0.593750
(10, 20]    0.382609
(20, 30]    0.365217
(30, 40]    0.445161
(40, 50]    0.383721
(50, 80]    0.343750
Name: Survived, dtype: float64</code></pre>

男性よりも女性のほうが、Pclass（Ticket class）はハイグレードのほうが、Embarked（乗り込み港）はCherbourg、年齢は10歳未満、次に30代の人が比較的生存率が高かったようだ。

次にデータの加工を始める。

<pre class="wp-block-code"><code>
#性別とEmbarked（乗り込み港）は、文字列データなので、train, testともに量的データに変換する
#念の為、生存率が低かったものから大きい数字を割り当てるように揃える
train&#91;'SexIndex'] = train&#91;'Sex'].map(lambda x: 1 if x =='male' else 0)
train&#91;'EmbarkedIndex'] = train&#91;'Embarked'].map(lambda x: 2 if x == 'S' else 1 if x == 'Q' else 0)

test&#91;'SexIndex'] = test&#91;'Sex'].map(lambda x: 1 if x =='male' else 0)
test&#91;'EmbarkedIndex'] = test&#91;'Embarked'].map(lambda x: 2 if x == 'S' else 1 if x == 'Q' else 0)</code></pre>

<pre class="wp-block-code"><code>
#特徴量が量的データだけのDataFrameを作る
x = train&#91;&#91;'Pclass', 'SexIndex', 'Age', 'SibSp', 'Parch', 'Fare', 'EmbarkedIndex']]
y = train&#91;'Survived']

#欠損値は平均値で代替する
x.fillna(x.mean(),inplace=True)

#欠損値はなくなった
x.isnull().sum()
#
Pclass           0
SexIndex         0
Age              0
SibSp            0
Parch            0
Fare             0
EmbarkedIndex    0
dtype: int64

#testデータでも同様の下ごしらえをする
X = test&#91;&#91;'Pclass', 'SexIndex', 'Age', 'SibSp', 'Parch', 'Fare', 'EmbarkedIndex']]
X.fillna(x.mean(),inplace=True)</code></pre>

ようやく、モデルの作成と学習を始める。  
今回は勾配ブースティングを使ってみる。

<pre class="wp-block-code"><code>
from sklearn.ensemble import GradientBoostingRegressor

#x,yを訓練データとテストデータに分ける
xtrain, xtest, ytrain, ytest = train_test_split(
    x, y, random_state=1)

#インスタンス化
GradientBoost = GradientBoostingRegressor(random_state=0) 
GradientBoost.fit(xtrain, ytrain)

GradientBoost.score(xtest, ytest)
#
0.381950933876793</code></pre>

すこぶる低い正答率だけど、このまま続ける。

<pre class="wp-block-code"><code>
#学習したモデルをもとに、生存率の予想値の配列をつくる
Y_pred = GradientBoost.predict(X)

#Y_predをもとにcsvを出力する
submission = test&#91;&#91;'PassengerId']]
submission&#91;'Survived'] = list(map(int, Y_pred))
submission.to_csv('submission.csv', index=False)</code></pre>

いよいよ、その結果をこちらにアップロードする。<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-23.22.09-1024x668.png" alt="" class="wp-image-887" width="423" height="276" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-23.22.09-1024x668.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-23.22.09-300x196.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-23.22.09-768x501.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-23.22.09-1536x1001.png 1536w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-23.22.09.png 1942w" sizes="(max-width: 423px) 100vw, 423px" /><figcaption>アップロードはこちらから</figcaption></figure> 

その結果がこちら。<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-19.02.12-1024x113.png" alt="" class="wp-image-888" width="420" height="46" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-19.02.12-1024x113.png 1024w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-19.02.12-300x33.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-19.02.12-768x85.png 768w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-19.02.12-1536x169.png 1536w, https://kaorumitsumori.com/wp-content/uploads/2019/12/Screen-Shot-2019-12-16-at-19.02.12.png 1940w" sizes="(max-width: 420px) 100vw, 420px" /><figcaption>【結果は16221位/16862】</figcaption></figure> 

トップ97%にランクインw  
無事にアップロードし、ランキングボードにとりあえず乗れたのでOKとしようか。

 [1]: https://kaorumitsumori.com/signate-titanic/
 [2]: https://www.kaggle.com/c/titanic