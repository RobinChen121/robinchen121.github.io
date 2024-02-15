---
layout: post
title: Draw animated hear by Python
date: 2023-11-08  20:30-0800
categories: python-practice
giscus_comments: true
tags: animated-heart, Python,
related_posts: true
featured: true
---

Stumbled upon a dynamic heart-shaped graph implemented by someone using MATLAB on a Chinese TikTok video, I got inspired to recreate it using Python. So I explored two different implementation approaches, and the result is as follows:

```python
import matplotlib.pyplot as plt
import numpy as np


# type %matplotlib qt to shown figure in a separate window
x = np.linspace(-1.8, 1.8, 1000)
alpha = 1

while alpha <= 21:
    plt.xlim(-3, 3)
    plt.ylim(-2, 4)
    y = abs(x)**(2/3) + 0.9*np.sqrt(3.3 - x**2)*np.sin(alpha*(np.pi)*x)
    plt.plot(x, y)

    plt.text(-1.6, 3, r'$f(x)=x^{2/3}+0.9(3.3-x^2)^{1/2}\sin(\alpha\pi x)$')
    alpha_s = str(round(alpha, 2))
    tx = plt.text(-0.5, 2.5, r'$\alpha=$' + alpha_s)
    plt.pause(0.02) # pause 0.02 s
    if alpha <= 20:
        alpha += 0.1
        plt.clf() # clear the current picture
    else:
        break
```
