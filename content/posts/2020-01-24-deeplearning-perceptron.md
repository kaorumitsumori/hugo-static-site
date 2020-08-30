---
title: 【ゼロからDeepLearningをつくる】Pythonでパーセプトロンをつくる
author: KAORU
type: post
date: 2020-01-24T13:55:00+00:00
url: /deeplearning-perceptron/
featured_image: /wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.41.png
categories:
  - Data science
  - Programming
tags:
  - deeplearning
  - python

---
パーセプトロンとは<a rel="noreferrer noopener" aria-label="Frank Rosenblatt (新しいタブで開く)" href="https://ja.wikipedia.org/wiki/%E3%83%95%E3%83%A9%E3%83%B3%E3%82%AF%E3%83%BB%E3%83%AD%E3%83%BC%E3%82%BC%E3%83%B3%E3%83%96%E3%83%A9%E3%83%83%E3%83%88" target="_blank">Frank Rosenblatt</a>が考案したアルゴリズムで、ニューラルネットワークの起源でもあり、いくつかの信号を入力してそれを１つの信号(1か0)として出力する仕組みです。   
  
シンプルな仕組みですが、パーセプトロンを用いるとコンピュータの多くの処理を実行できます。  
  
コンピュータは理論的にはNAND回路の組み合わせなので、パーセプトロンをコンピュータのように使うには、NAND回路を表現できればいいです。  
  
2つの入力値を「1」か「0」とし、2つの入力値があるパターンにマッチした場合のみ「1」を返して、マッチしなければ「0」を返す仕組みを考えます。下記の4パターンをPythonでつくります。

  * ANDゲート
  * NANDゲート
  * ORゲート
  * XORゲート

## ANDゲート<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.24.57.png" alt="" class="wp-image-1106" width="217" height="216" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.24.57.png 518w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.24.57-300x300.png 300w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.24.57-150x150.png 150w" sizes="(max-width: 217px) 100vw, 217px" /></figure> 

<pre class="wp-block-code"><code>
def AND(x1, x2):
  w1, w2, b = 0.5, 0.5, -0.7
  tmp = x1*w1 + x2*w2 + b
  if tmp &lt;= 0:
    return 0
  else:
    return 1

print(AND(0, 0))
print(AND(0, 1))
print(AND(100, 0))
print(AND(1, 1))

#
0
0
0
1</code></pre>

w1, w2, bのそれぞれについては、適当に設定しました。

## NANDゲート<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.11.png" alt="" class="wp-image-1107" width="221" height="224" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.11.png 512w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.11-297x300.png 297w" sizes="(max-width: 221px) 100vw, 221px" /></figure> 

<pre class="wp-block-code"><code>
def NAND(x1,x2):
  w1, w2, b = -0.5, -0.5, 0.7
  tmp = x1*w1 + x2*w2 + b
  if tmp &lt;= 0:
    return 0
  else:
    return 1

print(NAND(0, 0))
print(NAND(1, 0))
print(NAND(0, 1))
print(NAND(1, 1))

#
1
1
1
0</code></pre>

こちらもw1, w2, bのそれぞれについては、適当に設定しました。

## ORゲート<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.23.png" alt="" class="wp-image-1108" width="217" height="221" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.23.png 496w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.23-294x300.png 294w" sizes="(max-width: 217px) 100vw, 217px" /></figure> 

<pre class="wp-block-code"><code>
def OR(x1,x2):
  w1, w2, b = 0.5, 0.5, -0.2
  tmp = x1*w1 + x2*w2 + b
  if tmp &lt;= 0:
    return 0
  else:
    return 1

print(OR(0, 0))
print(OR(1, 0))
print(OR(0, 1))
print(OR(1, 1))

#
0
1
1
1</code></pre>

またまたw1, w2, bについては、適当に設定しました。

## XORゲート<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.32.png" alt="" class="wp-image-1109" width="224" height="230" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.32.png 488w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.32-293x300.png 293w" sizes="(max-width: 224px) 100vw, 224px" /></figure> 

最後にXORゲートですが、これはほかのパターンのコンビネーションでしか実現できません。なので下記のような構造でつくります。<figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.41.png" alt="" class="wp-image-1110" width="291" height="214" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.41.png 580w, https://kaorumitsumori.com/wp-content/uploads/2020/01/Screen-Shot-2020-01-27-at-22.25.41-300x220.png 300w" sizes="(max-width: 291px) 100vw, 291px" /></figure> 

<pre class="wp-block-code"><code>
def XOR(x1, x2):
  s1 = NAND(x1, x2)
  s2 = OR(x1, x2)
  y = AND(s1, s2)
  return y

print(XOR(0, 0))
print(XOR(1, 0))
print(XOR(0, 1))
print(XOR(1, 1))

#
0
1
1
0</code></pre>

これで4パターンをPythonでつくることができました。