---
title: 乘法逆, 线性同余方程, 扩展欧几里得算法, 费马小定理
published: 2024-09-17
tags: [数论, 离散数学]
category: 课程笔记
description:
draft: false
---

出于行文方便, 变量如果无特殊说明(一般是我忘记加说明或者懒得加), 都是整数或者正整数. 相信你也不难根据上下文判别.

## 乘法逆

我们知道有限域是一种代数结构，它包含有限个元素，并且定义了加法与乘法运算。有限域中的每一个非零元素都有一个乘法逆元。比如 $x * y = 1$, 我们说 $y$ 是 $x$ 的乘法逆元。

举个栗子，比如假定一个 `unsigned char` 数组 `arr[k]` 中每一个元素属于有限域(0x00至0xff), 并通过如下的方式加密:

```cpp
for (int j = 0; j < ; ++j)
	arr[j] = arr[j] * 17 + 113;
```

解密时**不能**出现 `/17`, 整数除法将会损失数据. 试一试容易知道 17 在 mod 256 下的乘法逆是 241, 因此解密算法:

```cpp
for (int j = 0; j < ; ++j)
	arr[j] = (arr[j] - 113) * 241;
```

在数不大的情况下, 可以试出乘法逆. 但问题是有没有一种更一般的方法去求得乘法逆呢? 在有限域下, 对于一个线性同余方程
$$
ax \equiv 1(\mathrm{mod} \ b)
$$
我们说 $x$ 是 $a$ 的逆元, 记为 $a^{-1}$.

它其实等价于(为什么是这样?)
$$
ax + by = 1\, \ (x,y \in \mathbb{Z})
$$
只要我们解出 $x$, 也就得到了乘法逆, 当然, 也顺便把 $y$ 解出了. 我们进一步分析这个方程.

- 如果 $a$ 与 $b$ 是互素的, 那么根据贝祖定理, 我们能解出唯一的 $(x,y)$:

$$
\exists ! x,y\in\mathbb{Z} \ \  \  s.t. \ \ \ ax + by = \gcd(a,b)=1
$$

- 如果 $a$ 与 $b$ 不是互素的, 此时根据 $ax \equiv 1(\mathrm{mod} \ b)$ 的条件:

$$
ax+by = 1\\
\Rightarrow \gcd(a,b)(\frac{ax}{gcd(a,b)}+\frac{by}{gcd(a,b)})=1
$$

注意到左边两个因子的绝对值都大于等于 1, 其中 $\gcd(a,b)>1$, 产生矛盾. 因此 $ax \equiv 1(\mathrm{mod} \ b)$ 仅在 $a$ 与 $b$ 互素时有解. 我们实际上是在解方程：
$$
ax + by = \gcd(a,b)
$$
下面我们介绍一下解这个方程的一个一般算法.

## 扩展欧几里得算法

根据贝祖定理
$$
\exists ! x,y\in\mathbb{Z} \ \  \  s.t. \ \ \ ax + by = \gcd(a,b)
$$
下面给出**扩展欧几里得算法**, 这实际上是在解出上面的式子所提到的 $x,y$:

```cpp
int ex_gcd(int a, int b, int& x, int& y) {
  if (b == 0) {
    x = 1;
    y = 0;
    return a;
  }
    
  // 欧几里得算法的迭代形式
  int d = ex_gcd(b, a % b, x, y);
    
  // 从欧几里得算法的后一步走向前一步, 通过每一步商和余数的线性组合来求出x, y  
  int temp = x;
  x = y;
  y = temp - a / b * y;
  return d;
}
```

为什么是这样? 我指的是最后一段代码:

```cpp
  int temp = x;
  x = y;
  y = temp - a / b * y;
```

对于欧几里得算法, 在下相信你对它的过程是非常熟练和清晰的, 比如, 求 $\gcd(a,b)$ 是如下的一种过程, 其中的 $q_i$ 无关紧要:
$$
\begin{align*}
a &= bq_1 + r_1 \\
b &= r_1q_2 + r_2 \\
r_1 &= r_2q_3 + r_3 \\
\vdots \\
r_{n-2} &= r_{n-1}q_n + r_n \\
r_{n-1} &= r_n q_{n+1} + 0	\\
r_n &
\end{align*}
$$
于是 $\gcd(a,b) = r_n$. 

最后一步得到 $r_n$ 之后, 设 $x=1,y=0$, 回退到上一步, 计算后得到 $x=0,y=1$, 于是
$$
0\cdot r_{n-1} + 1\cdot r_n = r_n
$$
实际上, 对于欧几里得算法中任何相邻的两步
$$
\begin{align*}
r_{k-2} &= r_{k-1}q_k + r_k \\
r_{k-1} &= r_k q_{k+1} + r_{k+1}	\\
\end{align*}
$$
如果
$$
xr_{k-1}+yr_{k} = r_n
$$
代入化简, 使得只剩下 $r_{k-1}, r_k, r_n$，
$$
\begin{align*}
r_{k-2} &= (r_k q_{k+1} + r_{k+1})q_k+r_k					\\
yr_{k-2} &= y(r_k q_{k+1} + r_{k+1})q_k+yr_k					\\
yr_{k-2} &= y(r_k q_{k+1} + r_{k-1} - r_k q_{k+1})q_k+yr_k	\\
yr_{k-2} &+ (x-yq_k)r_{k-1} = r_n
\end{align*}
$$
也即是
$$
yr_{k-2} + (x-y\lfloor \frac{r_{k-2}}{r_{k-1}} \rfloor)r_{k-1} = r_n	
$$
于是
$$
x'=y , \ y' = x-y\lfloor \frac{r_{k-2}}{r_{k-1}} \rfloor
$$
逐步计算即可得到最终结果. 至此, 相信你已经完全掌握了扩展欧几里得算法.

## 线性同余方程

我们定义线性同余方程形同
$$
ax \equiv m(\mathrm{mod}\,b),\, m>0
$$
其中 $x$ 是变量。我们曾经得到过 $a^{-1}$, 我们将上述方程左右同乘 $a^{-1}$, 不难证明出
$$
x \equiv ma^{-1}(\mathrm{mod}\,b)
$$
此即为线性同余方程的解法. 所以重点是求 $a$ 的逆元. 前面我们已经讨论过 $\gcd(a,b)=1$ 的情况. 但是, 如果 $a$ 与 $b$ 不互素呢?$ax \equiv1(\mathrm{mod} \, m)$ 无解, 一定意味着 $ax \equiv m(\mathrm{mod}\,b)$ 无解吗?

实际上, 当 $\gcd(a,b) \neq 1$ 时, 我们可以进一步讨论. 

- 如果此时 $m \,|\gcd(a,b)$, 稍稍想想就能明白原来的线性同余方程等价于

$$
a'x \equiv m'(\mathrm{mod}\,b')
$$

 其中 $a',m',b'$ 都是

## 费马小定理

等待补充

## 实战

等待补充
