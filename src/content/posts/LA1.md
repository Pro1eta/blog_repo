---
title: 几个简单的秩不等式
published: 2024-03-04
description: '几个简单的秩不等式及其证明'
image: ''
tags: [线性代数]
category: '课程笔记'
draft: false 
lang: ''
---







# 前言

这是初学线代时整理的，实践证明，当初学的有多认真，现在忘得就有多快（

---

# 正文

  >**命题**
  >设 $A$, $B$ 为 $n$ 阶方阵，$AB=0$​ ，则有
  >$$
  >rank(A) + rank(B)\le n
  >$$
  >

**分析**
线性映射基本定理的简单应用。

**证明**
$AB=0$ 说明 $B$ 的每一列都被 $B$ 映成零向量，从而 $span(B) \in Ker(A)$​ ，那么有
$$
rank(B)=dimSpan(B) \leq dimKer(A)
$$
由线性映射基本定理可得
$$
rank(A) + rank(B)\le dimSpan(A) +dimKer(A)=n
$$
于是得证。

****

  >**命题**
  >设 $A$, $B$ 为 $m \times n$，$n \times p$ 矩阵，则有
  >$$
  >rank(AB) \leq  min\{rank(A), rank(B)\}
  >$$
  >

**分析**
所谓的“秩越乘越小”。可以通过矩阵乘法运算得到这个结论，这里我们考虑另一种办法。

**证明**
$AB$ 乘一个列向量 $\alpha$ 可以看作两步。第一步， $B$ 乘 $\alpha$；第二步，$A$ 再乘 $B\alpha$ 。

第一步可以看作映射：
$$
\sigma_1:\mathbb{F}^{p}\to\mathbb{F}^{n}, \begin{bmatrix}
  x_1\\
  \vdots\\
  x_p
  \end{bmatrix}
 \mapsto
 B\begin{bmatrix}
  x_1\\
  \vdots\\
  x_p
  \end{bmatrix} 
$$
第二步可以看作映射，这一步的像集也就是 $Im(AB)$ ：
$$
\sigma_2:Span(B)\to\mathbb{F}^{m}, \begin{bmatrix}
  x_1\\
  \vdots\\
  x_n
  \end{bmatrix}
 \mapsto
A \begin{bmatrix}
  x_1\\
  \vdots\\
  x_m
  \end{bmatrix} 
$$
所以
$$
rank(AB)=dim(Span(A\big|_{Im(B)}))
$$
由于
$$
Span(A\big|_{Im(B)})\subset Span(A)
$$
从而 $$rank(AB) \leq rank(A)$$
由于转置运算不改变矩阵的秩，所以 $$rank(AB)=rank(B^TA^T) \leq rank(B^T)=rank(B)$$
整理即有 $rank(AB) \leq  min\{rank(A), rank(B)\}$

****

  >**命题(Sylvester不等式)**
  >设 $A$, $B$ 为 $n$ 阶方阵，$AB=0$ ，则有
  >$$
  >rank(AB) \ge rank(A)+rank(B)-n
  >$$
  >



**分析** 
与上一个不等式的证明思路类似。

**证明**
即证明
$$
n - rank(A) \ge  rank(B) - rank(AB)
$$
发现
$$
左边 = dimKer(A)\geq右边=dimKer(A|_{Im(B)})
$$
从而得到了证明。

****

  >**命题**
  >设 $A$, $B$ 为 $m \times p$，$m \times q$ 矩阵，则有
  >$$
  >rank(A+B) \leq  rank(A|B)\leq rank(A)+rank(B)
  >$$
  >

**分析** 
将矩阵看作列向量组，然后观察它们的关系

**证明**
显然 $A+B$ 的列向量组可以被 $A|B$ 线性表出，故 $rank(A+B) \leq rank(A|B)$，

设 $A,B$ 的极大无关组分别是 $(\alpha_1,\alpha_2,\dots,\alpha_s)$，$(\beta_1,\beta_2,\dots,\beta_k)$ ，

那么 $rank(A|B) = rank(\alpha_1,\alpha_2,\dots,\alpha_s,\beta_1,\beta_2,\dots,\beta_s) \leq s+k=rank(A)+rank(B)$，

于是得到了证明。

****

  >**命题**
  >设 $A$, $B$ 为 $s \times n$，$l \times m$ 矩阵，则有
  >$$
  >rank \begin{pmatrix}
  >A&O \\
  >O&B\\
  >\end{pmatrix}
  >= rank(A)+rank(B)
  >$$
  >

**分析**
证明思路与上一题一致

**证明**
设 $A,B$ 的极大无关组分别是 $(\alpha_1,\alpha_2,\dots,\alpha_j)$，$(\beta_1,\beta_2,\dots,\beta_k)$ ，所以
$$
rank \begin{pmatrix}
  A&O \\
   O&B\\
   \end{pmatrix}=rank \begin{pmatrix}
  \begin{pmatrix}
   \alpha_1\\
   0\\
   \end{pmatrix}，\begin{pmatrix}
   \alpha_2\\
   0\\
   \end{pmatrix}，\dots,
    \begin{pmatrix}
   \alpha_j\\
   0\\
   \end{pmatrix},  
     \begin{pmatrix}
   0\\
   \beta_1\\
   \end{pmatrix}，\begin{pmatrix}
   0\\
   \beta_2\\
   \end{pmatrix}，\dots,
    \begin{pmatrix}
   0\\
   \beta_k\\
   \end{pmatrix}
   \end{pmatrix}
$$
由定义立得右边的向量组线性无关，所以
$$
rank \begin{pmatrix}
   A&O \\
   O&B\\
   \end{pmatrix}
    = j+k=rank(A)+rank(B)
$$
这样就证明了这个等式。

****

  >**命题**
  >设 $A,B,C$ 为 $s \times n,l \times m,s \times m$ 矩阵，则有
  >$$
  >rank \begin{pmatrix}
  >A&O \\
  >C&B\\
  >\end{pmatrix}
  >\ge rank(A)+rank(B)
  >$$
  >

**分析**
证明思路与上一题没差多少

**证明**
设 $A,B$ 的极大无关组分别是 $(\alpha_1,\alpha_2,\dots,\alpha_j)$，$(\beta_1,\beta_2,\dots,\beta_k)$ ，所以
$$
rank \begin{pmatrix}
  A&O \\
   C&B\\
   \end{pmatrix} \ge rank \begin{pmatrix}
  \begin{pmatrix}
   \alpha_1\\
   c_1\\
   \end{pmatrix}，\begin{pmatrix}
   \alpha_2\\
   c_2\\
   \end{pmatrix}，\dots,
    \begin{pmatrix}
   \alpha_j\\
   c_j\\
   \end{pmatrix},  
     \begin{pmatrix}
   0\\
   \beta_1\\
   \end{pmatrix}，\begin{pmatrix}
   0\\
   \beta_2\\
   \end{pmatrix}，\dots,
    \begin{pmatrix}
   0\\
   \beta_k\\
   \end{pmatrix}
   \end{pmatrix}
$$
这是因为由定义立即知右边的向量组线性无关，而且 $(\begin{pmatrix} 
   \alpha_1\\
   c_1\\
   \end{pmatrix}，\begin{pmatrix}
   \alpha_2\\
   c_2\\
   \end{pmatrix}，\dots,
    \begin{pmatrix}
   \alpha_j\\
   c_j\\
   \end{pmatrix})$ 不一定会张成 $Span
   \begin{pmatrix}
   A\\C
   \end{pmatrix}$，从而就不难得到
$$
rank \begin{pmatrix}
   A&O \\
   C&B\\
   \end{pmatrix}
    \ge rank(A)+rank(B)
$$
