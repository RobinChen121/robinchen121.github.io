---
layout: post
title: Lagrangian sub-gradient method
date: 2014-11-13  09:57:31-0800
categories: ["optimization"]
giscus_comments: true
tags: ["Lagrangian", "sub-gradient"]
related_posts: true
---

To some optimization problems with nonlinear constraints:

$$
\begin{align*}
\min\quad &f(x)\\
s.t. \quad &g(x)\leq 0
\end{align*}
$$

If the nonlinear constraints are difficult to differentiate, the Karush-Kuhn-Tucker (KKT) method cannot be used to solve the problem. In such cases, it is advisable to consider employing the Lagrangian subgradient method. The Lagrangian relaxation model is given by:

$$
\{\min\limits_x~~f(x)+\mu g(x)\}
$$

The dual model of this Lagrangian model is:

$$
\{\max\limits_{\mu}~~f(x)+\mu g(x)\}
$$

For the Lagrange multiplier $$\mu$$, the iterative formula for the subgradient method is:

$$
\mu ^{k+1}=\max\{0,\mu^{k}+s^{k}g(x^{k})\},
$$

where

$$
s^{k}=\lambda^{k}\frac{\widehat{f}-f(x^{k})}{\sum g^{2}(x^{k})}
$$

$$\hat{f}$$ is a feasible solution for $$f$$, and $$\lambda^k\leq 2$$ ($$\lambda$$can be initialized to 2, then updated to its half in each step).

It can be proven that the sequence $$f(x^k)$$ converges to $$f$$ either or converges to a point that $$f(x^k)\geq \hat{f}$$ .

> In practical applications of the subgradient method, it is observed that for some mixed-integer programming problems, especially those with many relaxed inequality constraints, the method may not perform well. The dual gap is too large, and it seems that the parameter settings in the subgradient method rely heavily on empirical knowledge (sometimes combined with branch-and-bound techniques may reach better results).






