---
layout: post
title: Difference between sup, inf and min, max
date: 2018-07-27  09:57:31-0800
categories: ["optimization"]
giscus_comments: true
tags: ["sup", "inf", "max", "min"]
related_posts: true
thumbnail: assets/img/sup.png
---

In the past, the decision goals for optimizing functions were always either minimizing or maximizing. Recently, while reading papers, I have noticed that in many high-quality papers, the notation "inf" or "sup" is often used.

"inf" is short for infimum, and "sup" is short for supremum.

<font size=4, color=red>Using "inf" or "sup" always ensures the existence of the infimum or supremum of a function, while the minimum or maximum of a function may sometimes not exist.</font>

For example, consider the graph of the function $$f(x)=\sin(x)/x$$:

<p align="center">
  <img src="https://raw.githubusercontent.com/RobinChen121/robinchen121.github.io/master/assets/img/sup.png" />
</p>

Python codes for this picture:

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(-10, 10, 0.1)
plt.plot(x, np.sin(x)/x)

# facecolor generates a hollow circle, s is the size
plt.scatter(0, 1, facecolor = 'none', edgecolor = 'r', s = 100)
plt.show()

```

This function is undefined at $$x=0$$, so its maximum value, or "max," does not exist. However, we can observe that the smallest upper bound of $$f(x)$$ is 1 (any value not less than its maximum value is an upper bound), i.e., $$\sup f(x)=1$$.

* The definition of "sup": The smallest upper bound of a set.

* The definition of "inf": The largest lower bound of a set.
