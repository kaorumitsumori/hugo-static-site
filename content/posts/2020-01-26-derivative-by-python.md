---
title: 数値微分をPythonで実装する方法
author: KAORU
type: post
date: 2020-01-26T06:13:03+00:00
url: /derivative-by-python/
featured_image: /wp-content/uploads/2020/01/myfig-1.png
categories:
  - Data science
  - Programming
tags:
  - python
  - toppicking

---
たとえば10分間で2km走ったとすれば、スピードは0.2km/分ですが、これはあくまで10分間の平均のスピードです。  
  
微分をするというのは「ある瞬間」の変化の量を計算するということです。この10分間を1分間、1秒、0.01秒と限りなく小さくすることでこれを近似的に計算できます。

「ある瞬間」の変化量、微分は次の数式で定義されます。 $$ \frac{df(x)}{dx}=lim_{h\to0}\frac{f(x+h)-f(x)}{h} $$ 

## 解析的な微分と数値微分 $$ \frac{d}{dx}x^2=2x $$ 

高校で勉強したこのような微分を「解析的な微分」という一方で、限りなく小さな数字を用いて近似的に微分することを「数値微分」といいます。

## 数値微分の問題点A

数値微分をPythonで表現してみます。

<pre class="wp-block-code"><code>
def numerical_diff(f, x):
    h = 1e-50
    return (f(x+h) - f(x)) / h</code></pre>

限りなく小さな値として、h=1e-50（10の-50乗）を用いていますが、これでは**丸め誤差**が問題になります。

<pre class="wp-block-code"><code>np.float32(1e-50)

#
0.0</code></pre>

つまり、このように細かすぎる値を用いると小数点のいくつか以降は省略されてしまい、思うような結果を得ることができません。  
なのでこれは、h=1e-8（10の-8乗）というそこそこ小さな値を用いて解決します。

## 数値微分の問題点B $$ \frac{df(x)}{dx}=lim_{h\to0}\frac{f(x+h)-f(x)}{h} $$ 

今回のこの数式では、(x+h)とxの間の傾きを計算していますが、数値微分においてはhを無限に0に近づけられないために、結果に誤差が生じてしまいます。

この誤差を減らす工夫として、(x+h)と(x-h)の差分を用いて計算するという方法があります。つまり下記のように計算します。 $$ \frac{df(x)}{dx}=lim_{h\to0}\frac{f(x+h)-f(x-h)}{2h} $$ 

## 数値微分のサンプル

問題点A,Bを踏まえると、下記のようにPythonで記述できます。

<pre class="wp-block-code"><code>
def numerical_diff(f, x):
    h = 1e-8
    return (f(x+h) - f(x-h)) / 2h</code></pre>

この関数を用いて、実際に次の三次関数を数値微分してみます。 $$ y=x^3+5x^2+3x $$ 

<pre class="wp-block-code"><code>
import numpy as np
import matplotlib.pylab as plt

def numerical_diff(f, x):
    h = 1e-8 # 0.00000001
    return (f(x+h) - f(x-h)) / (2*h)

def function_1(x):
    return x**3 + 5*x**2 + 3*x 

def tangent_line(f, x):
    d = numerical_diff(f, x)
    print(d)
    y = f(x) - d*x
    return lambda t: d*t + y
     
x = np.arange(-50.0, 50.0, 0.1)
y = function_1(x)
plt.xlabel("x")
plt.ylabel("f(x)")

#x=30で微分する
tf = tangent_line(function_1, 30)
y2 = tf(x)

plt.plot(x, y)
plt.plot(x, y2)
plt.show()

#
3003.000165335834</code></pre><figure class="wp-block-image size-large is-resized">

<img src="https://kaorumitsumori.com/wp-content/uploads/2020/01/myfig.png" alt="" class="wp-image-1217" width="364" height="243" srcset="https://kaorumitsumori.com/wp-content/uploads/2020/01/myfig.png 432w, https://kaorumitsumori.com/wp-content/uploads/2020/01/myfig-300x200.png 300w" sizes="(max-width: 364px) 100vw, 364px" /></figure> 

3003.000165335834と出力されていますが、これは解析的に微分したときのx=30の接線の傾斜3003と非常に近しい結果です。