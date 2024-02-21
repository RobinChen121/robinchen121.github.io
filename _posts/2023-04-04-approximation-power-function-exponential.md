---
layout: post
title: Approximation of power function by exponential function
categories: ["optimization"]
giscus_comments: true
tags: ["python", "power function", "exponential function", "exponential smoothing"]
related_posts: true
thumbnail: assets/img/powerfunction1.png
---

The power function $$(1+x)^\alpha$$ can be approximated by the exponential function $$e^{\alpha x}$$, and even further approximated as $$1+\alpha x$$. This approximation is encountered in the introduction of exponential smoothing methods in a book (Fundamentals of Supply Chain Theory).

### 1. $$(1+x)^{\alpha}\approx 1+\alpha x$$

Expanding $(1+x)^\alpha$ around $x=0$ using Taylor series, we get

$$
(1+x)^\alpha=1+\alpha x+\frac{\alpha(\alpha-1)}{2}x^2+\frac{\alpha(\alpha-1)(\alpha-2)}{6}x^3+\dots
$$

When $$|x|<1$$, the terms $$x^2, x^3,\dots$$ become smaller. If further $$|\alpha x| \ll 1$$ (indicating that $$|\alpha x|$$ is sufficiently smaller than 1), the terms on the right side of the equation become increasingly smaller, and we can omit the later terms. Therefore, $$(1+x)^{\alpha}\approx 1+\alpha x$$.

Although a rigorous proof for these two conditions is not found, it seems reasonable.

### 2. $$(1+x)^{\alpha}\approx e^{\alpha x}$$

This approximation can be obtained through Taylor expansion, as follows:

$$
e{^\alpha x}=1+\alpha x+\frac{\alpha^2}{2}x^2+\frac{\alpha^3}{6}x^3+\dots
$$

When $$|x|$$ is small, $$(1+x)^\alpha$$ is close to $$e^{\alpha x}$$.

In `exponential smoothing methods`, the weighted historical demand value at time $$i$$ is $$\alpha(1-\alpha)^i$$ can be approximated as $$\alpha e^{-\alpha I}$$. The following graphs illustrate the degree of approximation for these two functions.

<p align="center">
  <img src="https://raw.githubusercontent.com/RobinChen121/robinchen121.github.io/master/assets/img/powerfunction1" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/RobinChen121/robinchen121.github.io/master/assets/img/powerfunction2" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/RobinChen121/robinchen121.github.io/master/assets/img/powerfunction3" />
</p>

From the graphs, it is evident that the approximation is quite close, especially when $$\alpha$$ is small.

Code:

```python
import numpy as np
import matplotlib.pyplot as plt


alpha = 0.2
x = np.arange(0, 50)
y1 = [(1 - alpha)**i for i in x]
y2 = [np.exp(-alpha*i) for i in x]

plt.plot(x, y1, label = r'$(1-\alpha)^i$')
plt.plot(x, y2, label = r'$e^{-\alpha i}$')
plt.title(r'$\alpha$ = ' + str(alpha) )
plt.legend()
plt.show()

plt.figure()
alpha = 0.5
x = np.arange(0, 50)
y1 = [(1 - alpha)**i for i in x]
y2 = [np.exp(-alpha*i) for i in x]

plt.plot(x, y1, label = r'$(1-\alpha)^i$')
plt.plot(x, y2, label = r'$e^{-\alpha i}$')
plt.title(r'$\alpha$ = ' + str(alpha) )
plt.legend()
plt.show()

plt.figure()
alpha = 0.8
x = np.arange(0, 50)
y1 = [(1 - alpha)**i for i in x]
y2 = [np.exp(-alpha*i) for i in x]

plt.plot(x, y1, label = r'$(1-\alpha)^i$')
plt.plot(x, y2, label = r'$e^{-\alpha i}$')
plt.title(r'$\alpha$ = ' + str(alpha) )
plt.legend()
plt.show()
```
