---
layout: post
title: Uniform continuous and ordinary continuous
date: 2019-03-26
categories: optimization
giscus_comments: true
tags: ["uniform continuous", "optimization"]
related_posts: true
featured: false
katex: true
toc:
  beginning: true
---

## Uniform continuous

Uniform continuity means: <font color=red> If a function $ f $ is uniformly continuous, then for any two points $ x $ and $ y $ in the domain, as long as $ x $ and $ y $ are sufficiently close, $ f(x) $ and $ f(y)$ will also be sufficiently close. </font>

Another definition using neighborhoods:

- For any real number $ \epsilon > 0 $, there exists a real number $ \delta > 0 $ such that whenever $ \|x - y\| < \delta $, we have $ \|f(x) - f(y)\| < \epsilon $.

The Heine-Cantor theorem states:

- <font color=red>If a function is continuous on a closed interval, then it is also uniformly continuous.</font>

<br>
## Ordinary continuous
{% katexmm %}
The intuitive meaning of ordinary continuity is:
<font color=red>If a function $f$ is continuous, then for any point $x$ in the domain, there exists a sufficiently small neighborhood around $x$ such that $f(x)$ is sufficiently close to the values within this neighborhood.</font>
{% endkatexmm %}

The definition of ordinary continuity by neighborhood:

- For any real number $\epsilon > 0$ and any point $x$ in the domain, there exists a real number $\delta > 0$ such that whenever $\|x - y\| < \delta$, we have $\|f(x) - f(y)\| < \epsilon$, where $$y$$ is any point in the neighborhood of $x$.

<br>
## Difference

From this, we can see:

- In the definition of uniform continuity, $\delta$ only depends on $\epsilon$.
- In the definition of ordinary continuity, $\delta$ depends on both $\epsilon$ and $x$.
- Uniform continuity is a stricter condition than ordinary continuity: a uniformly continuous function is always ordinary continuous, but a ordinary continuous function is not necessarily uniformly continuous.
- The distinction between uniform continuity and continuity is not easy to understand. However, it can be better grasped through a geometric interpretation. For example, consider the function $f(x) = 1/x$. This function is continuous on the interval $(0, 1)$, but it is not uniformly continuous because choosing two points close to 0 that are close to each other does not result in their function values being sufficiently close.
