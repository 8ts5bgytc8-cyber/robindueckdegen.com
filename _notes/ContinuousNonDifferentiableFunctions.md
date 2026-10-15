---
layout: post
title: "Takagi Curves"
date: 2026-09-13 12:00:00 -0600
tags:
  - Math336
---

![A gif I made which graphs the blancmange curve as the precision increases.]({{ '/assets/Images/ContinuousNonDifferentiableFunctions/iterations.gif' | relative_url }})


I initially began by investigating a continuous non differentiable curve detailed in Pugh's Real Mathematical Analysis. He defines 

$$
\sigma_k(x)= (\frac{3}{4})^k \sigma(4^kx), \qquad f(x) = \sum_{k=0}^\infty \sigma_k(x)
$$

Where

$$
\sigma(x)=
\begin{cases}
x-2n \quad &x\in[2n,2n+1] \\
2n+2-x \quad & x\in(2n+1,2n+2]
\end{cases}
$$

which is periodic with period 2, and $\sigma_k$ has a period of $\frac{2}{4^k}$. I decided to change the period multiple from $4^k$ to $2^k$, as I liked the connections with binary expansions of numbers, and change the $\frac{3}{4}$ to a simple $\lambda$ to make the construction more general. However, as it turns out this type of function is actually called a Takagi curve, and the special case of these where $\lambda=1/2$ is called the Blanchemange curve. 

 Since in the case we desire to investigae we only double $x$, i.e. we have

$$
\sigma_k(x)= \lambda^k \sigma(2^kx), \qquad f(x) = \sum_{k=0}^\infty \sigma_k(x)
$$


 we also only halve the period for each increase in $k$. Now for $\sigma(x)$ there are non differentiable points at $1\pm 2n$ for each $n$, then after doubling there will be non differentiable points at $\frac{1+2n}{2}$, and in general for the $k^{th}$ doubling there will be non differentiable points at every $\frac{1+2n}{2^k}$. Notice how on the interval $[0,1]$ how the points of non-differentiability are the same as those of the binary number $x.xxxxxx\ldots$. Indeed, it is not difficult to convince yourself that the non-differentiable points of 

$$
f(x) = \sum_{k=0}^\infty \lambda^k \sigma(2^kx)
$$

The main thing to note here is that we can use the Weirstrauss M test to show that so long as $\lambda<1$, the series will converge. This is because each $\sigma(2^kx)$ is at most one, and therefore the series is at most geometric. Since each $\sigma_k$ is continuous, the limit is continuous as well. However we cannot set $\lambda<1$ arbitrarily without losing the non differentiability condition. For instance, if $\lambda<\frac{1}{2}$ then in fact, as we will see, $f(x)$ is smooth at uncountably many points.  

For the first, note that for any given $k$ the slope of $\sigma_k$ is positive for any $x\in(\frac{n}{2^{k-1}},\frac{2n+1}{2^k})$, and negative for $x\in(\frac{2n+1}{2^k},\frac{n+1}{2^{k-1}})$. Since the slope of $\sigma_k$ is $\pm (2\lambda)^k$, it must be that $x$ being a member of the first means that $\sigma_k(x)$ has slope $(2\lambda)^k$, and $x$ in the second range means $\sigma_k(x)$ has slope $-(2\lambda)^k$. Because the above intervals are nested and decreasing, if $\sigma_k$ is smooth at $x$, it must be that $\sigma_l$ is smooth at $x$ for $l<k$. It follows that for any partial sum $f_m= \sum_{k=0}^{m} \sigma_k(x)$ the slope of any $x$ such that $x$ is in an interval of one of the above forms. Therefore, the derivative of $f_m$ at $x$ has the form

$$
D_{m} = \sum_{k=0}^{m} \pm (2\lambda)^k. 
$$

Now since the above sum is at most geometric, and the geometric sum is a cauchy sequence, it follows that the above is also a cauchy sequence and therefore converges. The intersection of these intervals corresponds with the set of all numbers which have no finite binary expansion, which is an uncountable set. 

Now given $x\in (\frac{n}{2^{k-1}},\frac{2n+1}{2^k})\cup (\frac{2n+1}{2^k},\frac{n+1}{2^{k-1}})$ with binary expansion $y_1y_2y_3\ldots y_nx_0.x_1x_2x_3\ldots x_k \ldots$, if $x_0=0$, then $\sigma_0$ has a positive slope, and $x_0=1$ means that $\sigma_0$ has a negative slope, and so on. Therefore the signs of each term in the sum $D_m$ are determined by the binary expansion of $x$. 

We can see how the function starts out looking relatively smooth when $\lambda<1/2$, then as we further increase $\lambda$ we see the function becomes increasingly divergent.

<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/amplitude.gif' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">


However, it should also be noted how suspiciously smooth the curve becomes very early in the animation. In fact if $\lambda=\frac{1}{4}$, $f$ converges to $x^2$. We can see this more clearly by graphing the derivative next to the graph of the function, and slowing down the change in $\lambda$
<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/derivative.gif' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">


I won't go into the details for how to prove that $f$ converges to $x^2$ here, but it is noteworthy for the investigation of this function. The remainder of what I would like to investigate about this function are the integral, the derivative, and connections with different functional bases, further I would like to mention the self similar properties of this curve. For graphing the function I wrote the following code:

```python
def sawtooth(h,n,iter):
    y = np.linspace(-1,1,2**n)
    y = 1-np.abs(y)
    for k in range(1,iter):
        y_k = np.linspace(-2**-k,2**-k,2**(n-k))
        y_k = h**k*(1-2**k*np.abs(y_k))
        for j in range(1,2**n):
            y[j-1] = y[j-1] + y_k[j%2**(n-k)-1]
    return y
```

It works by considering each sawtooth an absolute value function, then adding them up in the correct way to obtain $f$. The any other code can be found on my github here: <a href="https://github.com/Rdueckd/AppliedProjects/tree/main/AnalysisExperiments/NowhereDifferentiable">github</a>.

We can see by varying the number of iterations next to the derivative of the function that there is a rather visually obvious connection to the derivative of the Blancmange curve, and the Haar basis:

<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/DerivativeIter.gif' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">

We should therefore be able to show that Takagi curves are actually the integral of some sum of Haar functions. Now if we integrate one more time we can see that the integral of Takagi curves actually appear to be quite smooth:

<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/integral.gif' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">

<!--Should replace the above graph with varying over iterations-->

Then it seems that we can naturally move between the Haar basis, the sawtooth 'basis', which we should show is in fact a basis, and some basis of smooth functions via integration and differentiation. 

<!--use fourier transform at this point-->

The final aspect of this function which I wanted to point out was that it is self similar. I want to show that the Blancmange curve is self similar around any point with a repeating decimal expansion, and that general takagi curves have self similarity with some linear error. 

<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/zoom.gif' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">
