---
layout: post
title: Proof for the continuity of a min function
date: 2019-01-10  21:27-0800
categories: ["optimization"]
tags: ["continuity proof"]
giscus_comments: true
related_posts: true
---

Assume a min real function is defined below:

$$
f(x)=\min\limits_{x\leq y\leq h(x)}g(y)
$$

$$g(x)$$ is continuous. $$x\geq 0, h(x)=ax+b, a\geq 1, b\geq 0$$. Prove $$f(x)$$ is continuous.

_Proof _

For any $$x_0$$ in the domain of $$f(x)$$, we must prove that for any $$\epsilon>0$$, there exists $$\delta>0$$, such that when $$\|x-x_0\|<\delta$$,

$$
|f(x)-f(x_0)|<\epsilon
$$

Because $$g(x)$$ is continous, for any $$\epsilon_1>0$$, there exits $$\delta_1$$, when $$\|x-x_0\|<\delta_1$$,

$$
|g(x)-g(x_0)|<\epsilon_1\tag{1}
$$

$$g(x)$$ is also continous on $$x=h(x_0)$$. There exists $$\delta_2$$, when $$\|h(x)-h(x_0)\|<\delta_2$$,

$$|g(h(x))-g(h(x_0))|<\epsilon_2\tag{2}$$

For any two number $$x_1, x_2$$ in the domain $$[x_0-\delta, x_0+\delta]$$, let $$\delta\leq \delta_1$$, we can get

$$
\begin{aligned}
|g(x_1)-g(x_2)|&=|g(x_1)-g(x_0)+g(x_0)-g(x_2)|\\
&\leq |g(x_1)-g(x_0)|+|g(x_0)-g(x_2)|<2\epsilon_1
\end{aligned}\tag{3}
$$

For any two number $$x_1, x_2$$ in the domain $$[x_0-\delta, x_0+\delta]$$, because $$h(x)=ax+b$$,

$$
\begin{aligned}
a(x_0-\delta) +b\leq h(x_1)\leq a(x_0+\delta)+b\\
a(x_0-\delta) +b\leq h(x_2)\leq a(x_0+\delta)+b
\end{aligned}
$$

When $$\delta\leq \delta_2$$, then $$h(x_1), h(x_2)\in[h(x_0)-\delta_2, h(x_0)+\delta_2]$$, by Eq. (2), we can get

$$
\begin{aligned}
|g(h(x_1))-g(h(x_2))|&=|g(h(x_1))-g(h(x_0))+g(h(x_0))-g(h(x_2))|\\
&\leq |g(h(x_1))-g(h(x_0))|+|g(h(x_0))-g(h(x_2))|<2\epsilon_2
\end{aligned}\tag{4}
$$

Assume

$$
\begin{align*}
g(y^\ast_{0})&=\min\limits_{x_0\leq y\leq h(x_0)}g(y)\\
g(y^\ast_{\Delta})&=\min\limits_{x_0-\delta\leq y\leq h(x_0+\delta)}g(y)
\end{align*}
$$

For any $$x\in [x_0-\delta, x_0+\delta]$$,

$$
g(y^\ast_{x})=\min\limits_{x\leq y\leq h(x)}g(y)
$$

Apparently, $$g(y^\ast_{\Delta})\leq g(y^\ast_{x}), g(y^\ast_{\Delta})\leq g(y^\ast_0)$$.

And $$f(x)=g(y^\ast_x), f(x_0)=g(y^\ast_0)$$.

So,

$$
\begin{aligned}
|f(x)-f(x_0)|&=|g(y^\ast_x)-g(y^\ast_0)| \\
&= |g(y^\ast_x)-g(y^\ast_\Delta)+g(y^\ast_\Delta)-g(y^\ast_0)|\\
&\leq |g(y^\ast_x)-g(y^\ast_\Delta)|+|g(y^\ast_0)-g(y^\ast_\Delta)|
\end{aligned}\tag{5}
$$

According the location of $$y^\ast_\Delta$$, there are three cases possible for $$\| g(y^\ast_x)-g(y^\ast_\Delta) \|$$ :

(a). $$y^\ast_\Delta= y^\ast_x$$, if $$y^\ast_\Delta\in [x, h(x)]$$.

In this case, $$\| g(y^\ast_x)-g(y^\ast_\Delta) \|=0$$.

(b). $$y^\ast_\Delta\in [x-\delta, x]\subset [x_0-\delta, x_0+\delta]$$.

In this case, let $$\delta\leq \delta_1, \| g(y^\ast_x)-g(y^\ast_\Delta) \|\leq \| g(x)-g(y^\ast_\Delta) \|<2\epsilon_1$$. (because of Eq. (3))

(c). $$y^\ast_\Delta\in [h(x), h(x_0+\delta)]\subset [h(x_0-\delta), h(x_0+\delta)]$$.

In this case, let $$\delta\leq \delta_2$$,

$$\| g(y^\ast_x)-g(y^\ast_\Delta) \|\leq \| g(h(x))-g(y^\ast_\Delta) \|<2\epsilon_2$$ (according to Eq. (4)).

Therefore, from the three cases, when $$\delta\leq\min\{\delta_1, \delta_2\}$$, we can get

$$
| g(y^\ast_x)-g(y^\ast_\Delta) |<\max\{2\epsilon_1, 2\epsilon_2\}
$$

Because $$g(y^\ast_0)$$ is a special situation of $$g(y^\ast_x)$$ when $$x=x_0$$, there is also

$$
|g(y^\ast_0)-g(y^\ast_\Delta)|<\max\{2\epsilon_1, 2\epsilon_2\}
$$

Eq. (6) can be written to be:

$$
|f(x)-f(x_0)|<2\max\{2\epsilon_1, 2\epsilon_2\}
$$

Let $$\max\{\epsilon_1, \epsilon_2\}=\epsilon$$, we can get

$$
| f(x) - f(x_0) | < \epsilon
$$

The continuity of $$f(x)$$ is proved.

<p style="text-align:right;font-size:30px">&#9633;</p>
