---
layout: post
title: Proof for the continuity of an recursive function
categories: ["paper reading"]
tags: ["paper reading"]
giscus_comments: true
related_posts: true
---

Recently I am reading one paper "Shaoxiang Chen, M. Lambrecht. XY Band and (s, S) Policies. Research Paper, 1990, No. 9011, ETEW, KU Leuven." Its proofs for the continuity of a recurisive function is very impressive for me.

The recursive function is:

$$
\begin{aligned}
&f_n(x)=\min
\begin{cases}
L(x)+\displaystyle\int f_{n+1}(x-t)\phi(t)dt\\
\min\limits_{x\leq y\leq  x+B}K-cx+L(y)+\displaystyle\int f_{n+1}(y-t)\phi(t)dt
\end{cases}\\
&f_{N+1}(x)=0
\end{aligned}
$$

An assumption: $$L(y)$$ is a continuous function on $$x$$.

$$\textit{Proof}.$$

The proof is by induction. Apparently $$f_{N+1}(x)$$ is continuous. Assume $$f_{n+1}(x)$$ is continuous, now we prove the continuity of $$f_n(x)$$.

- $$V(x)=L(x)+\displaystyle\int f_{n+1}(x-t)\phi(t)dt$$ is continous
- $$U(x)=K-cx+\min\limits_{x\leq y\leq  x+B}L(y)+\displaystyle\int f_{n+1}(y-t)\phi(t)dt$$ is also continuous. (the proof is very similar to my another blog)
- min function of two continuous functions is also continuous.

Therefore, $$f_n(x)$$ is continuous on $$x$$.
