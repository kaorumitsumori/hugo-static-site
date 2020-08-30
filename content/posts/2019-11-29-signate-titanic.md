---
title: SIGNATEに初トライ。「タイタニックの生存予測」問題にチャレンジしてみた
author: KAORU
type: post
date: 2019-11-29T05:12:09+00:00
url: /signate-titanic/
featured_image: /wp-content/uploads/2019/11/Image_by_addesia-from_Pixabay.jpg
page_type:
  - default
categories:
  - Competition
  - Data science
  - Programming
tags:
  - python
  - sidepicking
  - signate

---
[SIGNATE][1]というウェブサイトがある。データサイエンスのコンペ（競争）サイトであり、そこではさまざまな問題が出題されている。参加者は与えられたデータをダウンロード、解析し、正解にもっとも近いモデルをつくることを競う。

このように聞くと、 [SIGNATE][1]は凄腕のデータサイエンティストやプログラマーが技術を競う場所で、ハードルが高そうだなと感じられるかもしれない。ぼくもPythonを学び始めてからまだたったの２ヵ月。いつか参加できたらいいな、くらいに思っていた。

ふと覗いてみると、練習問題として「タイタニックの生存予測」なるものが用意されており、気分転換に手を付けてみたらわりとおもしろかった。

<pre class="wp-block-code"><code>#まずはpandasをインポート
import pandas as pd

#与えられたデータを読みこむ
train = pd.read_table('train.tsv')
test = pd.read_table('test.tsv')
sample_submit = pd.read_table('sample_submit.tsv')

#試しに出力してみる
train.head(10)</code></pre><figure class="wp-block-image">

<img src="https://kaorumitsumori.com/wp-content/uploads/2019/11/a.png" alt="" class="wp-image-164" srcset="https://kaorumitsumori.com/wp-content/uploads/2019/11/a.png 591w, https://kaorumitsumori.com/wp-content/uploads/2019/11/a-300x162.png 300w, https://kaorumitsumori.com/wp-content/uploads/2019/11/a-320x173.png 320w" sizes="(max-width: 591px) 100vw, 591px" /></figure> 

survivedは生還結果（1が生還、0が死亡）、pclassは客室のクラス（1,2,3の順に高級クラス）、sibspは乗船していた兄弟や配偶者の数、parchは乗船していた両親や子供の数、embarkedは乗船した港の頭文字である。

まずは、男女別で生存率を比較してみた。

<pre class="wp-block-code"><code>train.groupby('sex')&#91;'survived'].mean()

sex
female    0.775641
male      0.200692</code></pre>

なんと男性は20％、女性は77％の生存率だった。男女で差はないか、あっても男性のほうが高いとぼくは思っていた。真逆の結果だった。

タイタニック号はイギリス発の航海だった。乗客はレディファーストを重んじていたのだろうか。ぼくがそんな瀬戸際の状況にいたら、自分の命よりほかの誰かの命を優先することができるだろうか。たぶんNOだ。

それにしても顕著な差がでている。乗客の敬虔なポリシーがここまではっきりと数字に現れるとは畏怖する。数字をみて涙ぐんだのは初めてだ。

つぎに年齢別で生存率を比べてみる。まずは年齢をグループ分けする。

<pre class="wp-block-code"><code>age_range = &#91;0, 10, 20, 30, 40, 50, 80]
age_range_group = pd.cut(train.age, age_range)

#もとのデータに「age_range」という列を追加
train&#91;'age_range'] = age_range_group</code></pre>

<pre class="wp-block-code"><code>#年齢別グループの人数を調べる
pd.value_counts(age_range_cut)

(20, 30]    113
(30, 40]     83
(10, 20]     60
(40, 50]     45
(0, 10]      33
(50, 80]     26</code></pre>

21歳以上30歳未満の人数が113人ともっとも多い。  
そして、このグループごとの生存率を出力する。（男女別の結果からこちらの結果も想像がつく。計算結果を見るのが少し怖い。）

<pre class="wp-block-code"><code>train.groupby('age_range')&#91;'survived'].mean()

age_range
(0, 10]     0.575758
(10, 20]    0.450000
(20, 30]    0.389381
(30, 40]    0.469880
(40, 50]    0.311111
(50, 80]    0.423077</code></pre>

やはり、10歳未満の子どもの生存率がもっとも高い。  
最後にほかの条件での生存率を一気に計算する。

<pre class="wp-block-code"><code>for x in &#91;'pclass', 'sex', 'sibsp', 'parch', 'embarked', 'age_range']:
 print(train.groupby(x)&#91;'survived'].mean())

pclass
1    0.685185
2    0.443299
3    0.258333

sex
female    0.775641
male      0.200692

sibsp
0    0.351171
1    0.576577
2    0.571429
3    0.333333
4    0.000000
5    0.000000
8    0.000000

parch
0    0.357576
1    0.642857
2    0.428571
3    0.600000
4    0.000000
5    0.333333

embarked
C    0.594937
Q    0.410256
S    0.350769

age_range
(0, 10]     0.575758
(10, 20]    0.450000
(20, 30]    0.389381
(30, 40]    0.469880
(40, 50]    0.311111
(50, 80]    0.423077</code></pre>

  * pclassとは客室のクラスであるが、客室のグレードが高いほど生存率が高い。
  * sibsp,parchについて、家族が同乗していない人よりも同乗している人のほうが生存率が高い。
  * embarkedについて、乗船した港によってはっきりと生存率に差がある。

今回はここまで。それぞれの人の属性によって個別の生存確率の計算ができるはず。解析に引き続きトライしていこうと思う。

 [1]: https://signate.jp/