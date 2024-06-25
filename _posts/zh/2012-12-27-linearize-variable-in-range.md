---
layout: post
title: Linearize a variable have value in one range and 0 otherwise
date: 2022-12-27  23:27-0800
categories: ["optimization"]
giscus_comments: true
tags: ["linear programming", "value in a range", "zero otherwise"]
related_posts: true
---

Occasionally, I encountered a linearization problem: a variable takes one value within a certain range and 0 outside that range. For example,

If $$m_1 \leq x \leq m_2$$, then $$y = x$$; otherwise, $$y = 0$$.

The linearization of this problem is as follows: introduce a binary variable $$z$$ and a sufficiently large constant $$M$$,

$$
\begin{aligned}
x&\geq m_1-zM\\
x&\leq m_2+zM\\
y-x&\geq -zM\\
y-x&\leq zM\\
y&\leq (1-z)M\\
y&\geq -(1-z)M
\end{aligned}
$$
