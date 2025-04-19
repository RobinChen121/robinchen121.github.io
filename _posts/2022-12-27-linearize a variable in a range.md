---
layout: post
title: Linearize a variable in a range
date: 2012-12-27  20:30-0800
categories: ["optimization"]
giscus_comments: true
tags: [“linerization”, “range”]
related_posts: true
toc:
  beginning: true
---



Occasionally, I encountered a linearization problem where a variable takes one value in a certain region and another value elsewhere, i.e.,  

- If $ m_1 \leq x \leq m_2 $, then $ y = x $; otherwise, $ y = 0 $.  

The linearization of this problem is as follows:  
- Introduce a binary variable \( z \) and a sufficiently large constant \( M \).  

\[
\begin{aligned}
x&\geq m_1-zM\\
x&\leq m_2+zM\\
y-x&\geq -zM\\
y-x&\leq zM\\
y&\leq (1-z)M\\
y&\geq -(1-z)M
\end{aligned}
\]