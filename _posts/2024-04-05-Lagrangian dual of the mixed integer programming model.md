---
layout: post
title: Lagrangian dual of the mixed integer programming model
date: 2024-04-05
categories: optimization
giscus_comments: true
tags: ["Lagrangian dual", "Lagrangian relaxation", "MIP", "Integer programming"]
related_posts: true
toc:
  beginning: true
---

In one paper, I encountered a dual problem of a mixed-integer programming model, which was very interesting. I found that the Lagrangian dual is very powerful. This blog post records and summarizes it.

<br>
## 1. Mixed-Integer Programming

For a mixed-integer programming problem:

$$
\begin{aligned}
\max\quad &cx\\
\text{s.t.}\quad & Ax\leq b\\
& x_j\in\mathbb{Z},\quad j=1,2,\dots, p\\
 &x_i\geq 0\quad~~ i=1,2,\dots, n
\end{aligned}
$$

where $ p\leq n $. Let the feasible solution set of the problem be $S$. All parameters are rational numbers. There is a very important property: <font color="red">When $S$ is non-empty, i.e., the mixed-integer programming problem has a solution, it is equivalent to a linear programming problem:</font>

$$
\begin{aligned}
\max\quad &cx\\
\text{s.t.}\quad & x\in \text{conv}(S)
\end{aligned}
$$

<font color="red">where $\text{conv}(S)$ denotes the convex hull of the set $S$.</font>The geometric meaning of this property seems relatively easy to understand: the optimal solution of a mixed-integer programming problem is always achieved at some vertex of the convex hull (a polyhedron) of its feasible region. 

Strict proofs can be found in the reference of Section 2.

<br>
## 2. Lagrangian Dual of Mixed-Integer Programming

If the constraints of the mixed-integer programming problem are divided into two parts:

$$
\begin{aligned}
\max\quad &cx\\
\text{s.t.}\quad & A_1x\leq b_1\\
&A_2x\leq b_2\\
& x_j\in\mathbb{Z},\quad j=1,2,\dots, p\\
 &x_i\geq 0\quad~~ i=1,2,\dots, n
\end{aligned}
$$

Assuming we relax the first set of constraints, we get a Lagrangian relaxation model:

$$
\begin{aligned}
\max\quad &cx+\lambda(b_1-A_1x)\\
\text{s.t.}\quad & A_2x\leq b_2\\
& x_j\in\mathbb{Z},\quad j=1,2,\dots, p\\
 &x_i\geq 0\quad~~ i=1,2,\dots, n\\
 &\lambda\geq 0
\end{aligned}
$$

Let the domain of this Lagrangian relaxation model be $Q$. Since the relaxation model is an upper bound of the original problem, the optimal solution of the original problem is the smallest upper bound. Thus, the Lagrangian dual model of the original problem can be expressed as:

$$
\min_{\lambda\geq 0}\max_{x\in Q} \{cx+\lambda(b_1-A_1x)\}
$$

It can be proven that this Lagrangian dual model is equivalent to: [^1]

$$
\max\{cx\mid A_1x\leq b_1, x\in\text{conv}(Q)\}
$$

This property is quite magical. The Lagrangian dual originally requires solving a maximization function followed by a minimization function, but this property simplifies it to solving just a maximization function.

<br>
## 3. An Example
Let $x_0$ be a known constant. The original problem is:


$$
\begin{align*}
\min\limits_{y,z}\quad &y\\
\text{s.t.}\quad &1.5y\geq x_0\\
&z=x_0 \tag{1}\\
&0\leq z\leq 2\\
&y\in\{0,1,2\}
\end{align*}
$$

Introducing a penalty parameter $\pi$, relaxing constraint (1), and utilizing the above property, we get the dual model:


$$
\begin{aligned}
\max\limits_{\pi}\min\limits_{y,z}\quad &y-\pi(z-x_0)\\
\text{s.t.}\quad &1.5y\geq x_0\\
&(y,z)\in\text{conv}(Q)\\
\end{aligned}
$$


where $Q$ is the set $\\{(y,z)\mid 0\leq z\leq 2, y\in\\{0,1,2\\}\\}$, which actually consists of two line segments and one point. The convex hull $\text{conv}(Q)$ is a right triangle containing these two line segments and the point.

When $x_0=1$, the optimal solution of the original problem is 1, and the optimal solution of the dual problem is $1/1.5=2/3$.

&nbsp;
&nbsp;

---
References:

[^1]: Conforti, Michele, et al. Integer programming. Springer International Publishing, 2014, pp: 322-323.