---
layout: post
title: "Typora数学公式"
author: "yuruj"
catelog: true
mathjax: true
header-style: text
tags:
  - tips  
---

Typora支持使用Tex/LaTex语法渲染普通数学。渲染过程用MathJax处理

H~2~0 e^2^  ==高亮==

## Math Block（Display Math）

$$
\begin{align*}
y = y(x,t) &= A e^{i\theta} \\
&= A (\cos \theta + i \sin \theta) \\
&= A (\cos(kx - \omega t) + i \sin(kx - \omega t)) \\
&= A\cos \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big) + i A\sin \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big)  \\
&= A\cos \frac{2\pi}{\lambda} (x - v t) + i A\sin \frac{2\pi}{\lambda} (x - v t)
\end{align*}
$$



## Inline Math

f = $\frac{2 \pi}{T}$

$lim_{x \to \infty} \exp(-x) = 0$

## TeX Commands available in Typora

http://docs.mathjax.org/en/v2.6-latest/tex.html#supported-latex-commands

You could add new commands using `\def` or`\newcommand`

## Chemistry Expressions

## Cross Reference

Typora支持TeX样式的引用语法

## 自动编号

Typora支持自动编号数学块

To turn on this feature, please open preferences panel, and enable “Auto Numbering Math Equations” under the “Markdown” section

