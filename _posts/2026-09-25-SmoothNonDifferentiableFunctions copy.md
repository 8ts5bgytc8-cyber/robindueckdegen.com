---
layout: post
title: "Continuous Non-Differentiable Functions"
date: 2026-10-13 12:00:00 -0600
tags:
  - Math336
---

To start with, let's go over a basic construction for a class of non-differentiable smooth functions found in Pugh. He begins with the sawtooth function

$$
\sigma(x)=
\begin{cases}
x+2n \quad &x\in[2n,2n+1] \\
2n+2-x \quad & x\in(2n+1,2n+2]
\end{cases}
$$

which is periodic with period 2. We can double this period by multiplying $x$ by four. Now the idea behind the construction is that for $\sigma(x)$ there are non differentiable points at $1+2n$ for each $n$, then after doubling the period there will be non differentiable points at $1/2+n$, and in general for the $k^{th}$ doubling of the period there will be non differentiable points at every $\frac{1+2n}{4^k}$. 

 <!--should plot the discontinuities for 0,1 here-->

Notice how on the interval $[0,1]$ how the points of non-differentiability are the same as those of the binary number $1.111111\ldots$. Indeed, it is not difficult to convince yourself that the non-differentiable points of 

$$
f(x) = \sum_{k=0}^\infty \sigma(4^kx)
$$

will cover the binary expansion of any number. However, it is not yet continuous, as this sum blows up at every point. The solution is to control the amplitude of each term in the summand. Define

$$
\sigma_k(x)= \lambda^k \sigma(4^kx)
$$

with $\lambda\in(0,1)$. Then by the Weirstrauss M test, since this is at most the geometric sum over $\lambda^k$, this now converges at every point and is continuous. We should now look at some approximations of this function so that we can attempt graph it.
