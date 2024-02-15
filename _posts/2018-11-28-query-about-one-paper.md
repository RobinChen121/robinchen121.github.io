---
layout: post
title: A query about one paper
date: 2018-11-28  20:30-0800
categories: paper-reading
giscus_comments: true
description: I read the paper "Dynamic Inventory Management with Cash Flow Constraints" from Xiuli Chao, et. al (2008).  The proofs in this paper are very lengthy and complex. During the deductions of the proofs by myself, there is a query that I can not understand.
tags: dynamic programming, cash-flow inventory, query about paper
related_posts: true
---

Recently, I am reading the paper "Dynamic Inventory Management with Cash Flow Constraints" from Xiuli Chao, et. al (2008). The proofs in this paper are very lengthy and complex. During the deductions of the proofs by myself, there is a query that I can not understand.

Among the proof for Theorem 2 in the appendix, it wrote:

$$
\begin{aligned}
\tilde{V}_n(x, R)=&~V_n(x, S)\\
=&~ V_n(x, R-cx)\\
=&~ \max_{x\leq y\leq R/c}\pi_n(y, R)\\
=&~ \max_{x\leq y\leq R/c}E\left[\tilde{V}_{n+1}((y-D)^+, ~(p-c)\min\{y, D\}+(1+d)R-dcy)\right]
\end{aligned}
$$

In the last term, I can not understand why it is $(p-c)\min\\{y, D\\}$, because on page 761, it wrote:

$$
\pi_n(y, R)=E\left[V_{n+1}((y-D)^+, ~p\min\{y, D\}+(1+d)(R-cy))\right]
$$

So, I think the last term should be:

$$
\max_{x\leq y\leq R/c}E\left[\tilde{V}_{n+1}((y-D)^+, ~(p-c)\min\{y, D\}+(1+d)R-dcy-cy+c\min\{y, D\})\right]
$$

Why is $y=\min\\{y, D\\}$? This may affect the main conclusions of this paper. In the extension paper of Xiting Gong et. al (2014), I also noted the same problem. In page 188, the author wrote:

$$
\pi_n(y, R)=E\left[\tilde{V}_{n+1}((y-D)^+, ~(p-c)\min\{y, D\}+\phi(R-cy))+cy\right]
$$

I do not know why it is $(p-c)\min\\{y, D\\}$, either. Is it the error of this paper or my incorrect understanding?

I also do some numerical tests for the numerical examples in the paper. I note that the authors do not give the value of initial capital in the numerical example. My results by stochastic dynamic programming seems not to conincide with the results in the paper. Moreover, in the numerical setting, mean demand and variance are both 10, which is too big and can cause negative demand values.

Given the above query, I decide to quit perusing this paper. But the conclusion of the paper about the optimal ordering policy is right: a base-stock policy for the cash contrained problem. But its computation for the base-stock level may exit some bug.

> Note: after asking some other academics two years later, the proofs in this paper are right but there are some small bugs in the numerical testing (no initial cash is given in the numerical cases and there are some possible errors in the pictures).

<!-- more -->
