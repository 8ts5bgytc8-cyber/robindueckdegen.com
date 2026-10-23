---
layout: post
title: "A Modification to the Weirstrauss Function"
date: 2026-09-13 12:00:00 -0600
---


<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/iterations.gif' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">

I initially began by investigating a continuous non differentiable curve detailed in Pugh's Real Mathematical Analysis[^pugh]. He defines 

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

which is periodic with period 2, and $\sigma_k$ has a period of $\frac{2}{4^k}$. I decided to change the period multiple from $4^k$ to $2^k$, as I liked the connections with binary expansions of numbers, and change the $\frac{3}{4}$ to a simple $\lambda$ to make the construction more general. Therefore, we define $\sigma_k$ by

$$
\sigma_k(x)=
\begin{cases}
\lambda^k(2^kx-2n) \quad &x\in[2n/2^k,(2n+1)/2^k] \\
\lambda^k(2n+2-2^kx) \quad & x\in((2n+1)/2^k,(2n+2)/2^k]
\end{cases}
$$


The construction found in Pugh is, as Pugh states, "due to Weirstrauss"[^pugh]. After the adaptations I applied, as it turns out, this construction is very closely related to what are called blancmange curves, and a special case called the Takagi curve[^lagrias].

With these specific constructions in mind, the below will be the construction we will use for the rest of this document:

$$
\sigma_k(x)= \lambda^k \sigma(2^kx), \qquad f(x) = \sum_{k=0}^\infty \sigma_k(x)
$$

We also only halve the period for each increase in $k$. Now for $\sigma(x)$ there are non differentiable points at $1\pm 2n$ for each $n$ (as well as at every integer), then after doubling there will be non differentiable points at $\frac{1+2n}{2}$, and in general for the $k^{th}$ doubling there will be non differentiable points at every $\frac{1+2n}{2^k}$. This will all be important information for the non differentiability of this curve, but first we should establish its continuity.

The main thing to note here is that we can use the Weirstrauss M test to show that so long as $\lambda<1$, the series will converge [^pugh]. This is because each $\sigma(2^kx)$ is at most one, and therefore the series is at most geometric. Since each $\sigma_k$ is continuous, the limit is continuous as well. However we cannot set $\lambda<1$ arbitrarily without losing the non differentiability condition. For instance, if $\lambda<\frac{1}{2}$ then in fact, as we will see, $f(x)$ is differentiable at uncountably many points.  

To see this, note that for any given $k$ the slope of $\sigma_k$ is positive for any $x\in(\frac{n}{2^{k-1}},\frac{2n+1}{2^k})$, and negative for $x\in(\frac{2n+1}{2^k},\frac{n+1}{2^{k-1}})$. Since the slope of $\sigma_k$ is $\pm (2\lambda)^k$, it must be that $x$ being a member of the first means that $\sigma_k(x)$ has slope $(2\lambda)^k$, and $x$ in the second range means $\sigma_k(x)$ has slope $-(2\lambda)^k$. Because the above intervals are nested and decreasing, if $\sigma_k$ is differentiable at $x$, it must be that $\sigma_l$ is differentiable at $x$ for $l<k$. It follows that for any partial sum $f_m= \sum_{k=0}^{m} \sigma_k(x)$ the slope of any $x$ such that $x$ is in an interval of one of the above forms. Therefore, the derivative of $f_m$ at $x$ has the form

$$
D_{m} = \sum_{k=0}^{m} \pm (2\lambda)^k. 
$$

Which should be a Cauchy sequence, though I have yet to put in the time to actually show that it actually is. Making the reasonable assumption that it is, the intersection of the intervals where the derivative of $f_m$ is defined corresponds with the set of all numbers which have no finite binary expansion, which is an uncountable set. It should be the case then that for $\lambda<1/2$, that $f$ is differentiable on the set of all non-dyadic numbers.

Now given $x\in (\frac{n}{2^{k-1}},\frac{2n+1}{2^k})\cup (\frac{2n+1}{2^k},\frac{n+1}{2^{k-1}})$ with binary expansion $y_1y_2y_3\ldots y_nx_0.x_1x_2x_3\ldots x_k \ldots$, if $x_0=0$, then $\sigma_0$ has a positive slope, and $x_0=1$ means that $\sigma_0$ has a negative slope, and so on. We might infer that the signs of each term in the sum $D_m$ are determined by the binary expansion of $x$, I believe that this is probably the case. 

As to non differentiability, we know that at the very least the non-dyadic numbers will be non differentiable, and since every dyadic number is non differentiable, it follows that all points along the curve will be non differentiable. 

We can see how the function starts out looking relatively smooth when $\lambda<1/2$, then as we further increase $\lambda$ we see the function becomes increasingly divergent.

<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/amplitude.gif' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">


However, it should also be noted how suspiciously smooth the curve becomes very early in the animation. In fact if $\lambda=\frac{1}{4}$, $f$ converges to $2x-x^2$. We can see this more clearly by graphing the approximate derivative next to the graph of the function, and slowing down the change in $\lambda$

<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/derivative.gif' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">


I won't go into more detail on this convergence, but it is a noteworthy property of this function, and is visually quite obvious from the approximate derivative on the right hand side of the above graph. The remainder of what I would like to investigate about this function are the integral, the 'piecewise derivative' and connections with the Haar basis. I would also like to mention the self similar properties of this curve. For graphing the function I wrote the following code:

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

and it generates graphs like the one below:

<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/combined.png' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">

It works by considering each sawtooth an absolute value function, then adding them up in the correct way to obtain $f$. Any other code can be found on my github here: <a href="https://github.com/Rdueckd/AppliedProjects/tree/main/AnalysisExperiments/NowhereDifferentiable">github</a>. It should be noted that are some differences between the above code and what can be found on my github as I improved the code for efficiency, but it works essentially the same. All of the code for each of the animated graphs included here can also be found there. 

We can see by varying the number of iterations of the approximated curve next to the approximate derivative of the function that there is a rather visually obvious connection to the Haar basis. For the derivative I wrote the following:

```python
def derive(y):
    yprime = np.gradient(y, 2 / (len(y) - 1))
    return yprime
```

I graphed the approximated function on the left with its derivative on the right for $\lambda = 0.5$, as this made viewing the connection to the Haar basis the easiest:

<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/DerivativeIter.gif' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">


The relationship between the Haar basis and the sawtooth functions which the Weirstrauss function is made up of is detailed in section 4 of Bell here[^bell], but I go through it in sufficient detail for our puposes below. Because it is convenient with our domain, and the construction of our function, we will define 

$$
\chi_{n,k}(x) = 
\begin{cases}
1 \quad &x\in[2n/2^k,(2n+1)/2^k] \\
-1 \quad & x\in((2n+1)/2^k,(2n+2)/2^k] \\
0 \quad \text{otherwise}
\end{cases}
$$

To be the $(n,k)^{th}$ Haar function. We will also define the $(n,k)^{th}$ sawtooth to be

$$
\sigma_{n,k}(x) = 
\begin{cases}
\lambda^k(2^kx-2n) \quad &x\in[2n/2^k,(2n+1)/2^k] \\
\lambda^k(2n+2-2^kx) \quad & x\in((2n+1)/2^k,(2n+2)/2^k] \\
0 \quad \text{otherwise}
\end{cases}
$$

Now, consider the derivative of each individual function of the piecewise, it is clear that after taking these derivatives we should obtain an element of the Haar basis, and integrating any Haar basis element, we should similarly obtain a sawtooth. Define $\sigma_{n,k}'(x)$ to be the derivative of each individual function of the piecewise, then 

$$
\sigma_{n,k}'(x) = 
\begin{cases}
\lambda^k2^k \quad &x\in[2n/2^k,(2n+1)/2^k] \\
-\lambda^k2^k \quad & x\in((2n+1)/2^k,(2n+2)/2^k] \\
0 \quad \text{otherwise}
\end{cases}
= \lambda^k2^k\chi_{n,k}(x)
$$

Now, such an operation should be approximately equal to the numerical approximation of the derivative. This is because the numerical approximation takes the difference between successive points and then divides that by the number of points. My functions rely on there being an even number of points, so we only need to concern ourselves with when our array defining the sawtooth contains an even number of points. Let $\Delta x$ be the difference between any two successive points, and $N$ be the length of the array. The $n^{th}$ entry in the array for our approximated derivative will be 

$$
d_n = \frac{a_{n+1}-a_{n}}{\Delta x}
$$

Then because the points are evenly spaced, the approximated derivative should be essentially exact for any $n$ which is less than $N/2$, or greater than $N/2$. However, at exactly $N$, because of how ```numpy.linspace``` works and how I've constructed my arrays, the value on the left should be greater than the value on the right, and so despite $\lambda^k2^k$ being in between these points, the slope at that section will be negative. However, this ends up being negligable.   

Now by our definitions of $\sigma_{n,k}'(x)$ and $\chi_{n,k}(x)$, since the Haar basis is orthogonal

$$
\frac{1}{2}\int_0^2 \sigma_{n,k}'\chi_{r,s} dx = \delta_{n,r}\delta_{k,s} \lambda^k 
$$

It now makes sense to find the decomposition of each approximate derivative of our approximated curve. I wrote the following code to this end

```python
def haardecomp(y):
    m = len(y).bit_length()-1 # y must be lenght 2^n
    Hk = np.ones(len(y))
    Hk[1 << m-1:] -= 2
    lambdas = np.zeros((m,m))
    r = 1

    for n in range(0,m):
        yH = y.reshape(-1,1 << m-n) * Hk[::r] # multiply each section of y by the appropriate Haar basis element
        for k in range(0, n+1):
            lambdas[n,k] = np.sum(yH[k]) / (2**m-1) # integrate
        r = r << 1
    return lambdas
```

Which produces a matrix of the following form:

$$
\begin{pmatrix}
1          &   0         & 0          & \cdots & 0 \\
\lambda    & \lambda     & 0          & \cdots & 0 \\
\lambda^2  & \lambda^2   & \lambda^2  & \ddots & \vdots \\
\vdots     & \vdots      & \vdots     & \ddots & 0 \\
\lambda^{n-1} & \lambda^{n-1} & \lambda^{n-1} & \cdots & \lambda^{n-1}
\end{pmatrix}
$$

Really the diagonal is all that matters in this case, but I opted to keep the full matrix as I may want to use this code to decompose other functions in the future, and the number of computations are small enough that it only takes a hundred or so milliseconds to run anyways. Setting $\lambda=0.5$, we can see that it produces the correct values

<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/figure4Haar.png' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">

Setting $\lambda = 0, 75$, we can see that the error increases with lambda

<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/figure7Haar.png' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">

Notice as well that our earlier identity for the derivative between non differentiable points, $D_m$, matches with this new construction in terms of the Haar basis as 

$$
\sum_{k=0}^{m} \sum_{n=0}^k \chi_{n,k}(x) = \sum_{k=0}^{m} \pm (2\lambda)^k = D_{m} 
$$

For a given $x$.

The final aspect of this function which I wanted to point out was that it is self similar. I want to show that the Takagi curve is self similar around any point with a repeating decimal expansion, and that general blancmange curves have self similarity with some linear error. Below is linked an animated zoom into a section of the Takagi curve.

<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/zoom.gif' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">

I refer to [^lagrias] for calculations and identities relating to the self similarity of our curve with the note that their function $<<x>>$ is related to  $\sigma$ via

$$
\sigma(x) = <<\frac{1}{2} x>>
$$


<!--Now if we integrate one more time we can see that the integral of our curve actually appears to be quite smooth:

<img
  src="{{ '/assets/Images/ContinuousNonDifferentiableFunctions/integral.gif' | relative_url }}"
  style="display: block; margin: 1em auto; width: 700px; max-width: 100%; height: auto;">-->

## References

[^pugh]: Charles C. Pugh, *Real Mathematical Analysis*, 2nd ed. (Springer, 2015), Chapter 4, §7, pp. 254–255. https://doi.org/10.1007/978-3-319-17771-7.

[^bell]: Jordan Bell, *C[0,1]: The Faber–Schauder Basis, the Riesz Representation Theorem, and the Borel σ-Algebra* (2015). https://jordanbell.info/LaTeX/mathematics/CK/CK.pdf.

[^lagrias]: Jeffrey C. Lagarias, “The Takagi Function and Its Properties,” in *Functions in Number Theory and Their Probabilistic Aspects*, RIMS Kôkyûroku Bessatsu B34 (2012). https://arxiv.org/abs/1112.4205.

[^hong]: Don Hong, Jianzhong Wang, and Robert Gardner, "Orthonormal Wavelet Bases," Chapter 7 in *Real Analysis with an Introduction to Wavelets and Applications* (Academic Press, 2005), pp. 209–269. https://doi.org/10.1016/B978-012354861-0/50007-5.
