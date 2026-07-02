---
layout: post
title: Some interesting properties of Binomial distribution
date: 2026-07-02 22:29:00-0000
categories: ["statistics", "operational research"]
giscus_comments: true
tags: ["Binomial distribution", "properties"]
related_posts: true
toc:
  beginning: true
---

Recenly during research, I get to know and find some interesting properties about the Binomial distribution. Here I summerize them in this blog.


# Log-concavity, tail property and conditional expectation

>Lemma 1: Let $B \sim \mathrm{Binomial}(b, p)$ be a binomial random variable with parameters $b \in \mathbb{N}_0$ and $p \in [0,1]$. Then the following properties hold:
>
>(a) (*Log-concavity of the survival function*) The survival function (tail probability) of a binomial distribution is log-concave, i.e., for any $k\in \mathbb{N}_0$, the following inequality holds:
>$$
\big(\mathbb{P}(B\geq k+1)\big)^2 \geq \mathbb{P}(B\geq k+2)\cdot\mathbb{P}(B\geq k).
>$$
>
>(b) (*Submultiplicativity of the tail probability*) For any $j, k \in \mathbb{N}_0$, the tail probability satisfies:
>$$\mathbb{P}(B \geq j + k) \leq \mathbb{P}(B \geq j) \cdot \mathbb{P}(B \geq k).
>$$
>
>(c) (*Tail comparison via a smaller binomial*) For any integer $j \in \{0,1,\dots, b\}$ and all $k \in \{0, 1, \dots, b-j\}$, the following inequality holds:
>$$\mathbb{P}(B \geq j + k) \leq \mathbb{P}(B \geq j) \cdot \mathbb{P}(Y \geq k),$$
>where $Y \sim \mathrm{Binomial}(b - j, p)$.
>
>(d) (*Upper bound on conditional expectation*) For any $j \in \{0,1,\dots, b\}$, the conditional expectation of $B$ given that $B > j$ satisfies:$$\mathbb{E}[B \mid B > j] \leq j + 1 + (b - j - 1)p.$$
>
>(e) Upper bound on cumulative tail probability For any $j \in \{0,1,\dots, b\}$, the expectation–probability product satisfies:
>$$
>\sum_{k = j + 1}^b \mathbb{P}(B > k)\le \mathbb{E}[B] \cdot \mathbb{P}(B > j).
$$

*Proof.*

The lemma holds trivially when $p = 0$ or $p = 1$. We now proceed to prove it for $p \in (0,1)$.

Part (a). Let $S(k) := \mathbb{P}(B \ge k)$ denote the survival function and $f(k) := \mathbb{P}(B = k)$ the probability mass function. The inequality is automatically satisfied for $k > b - 2$. Our goal is to show that $S(k)$ is log-concave in $k$ for $k = 0, 1, \dots, b - 2$; that is,$$S(k+1)^2 \ge S(k) \cdot S(k+2).$$Since $S(k) > 0$, this is equivalent to$$\frac{S(k+1)}{S(k)} \ge \frac{S(k+2)}{S(k+1)}.$$Using the identity $S(k) = S(k+1) + f(k)$, we obtain$$\frac{S(k+1)}{S(k)} = \frac{S(k+1)}{S(k+1) + f(k)} = \left(1 + \frac{f(k)}{S(k+1)}\right)^{-1},$$and similarly,$$\frac{S(k+2)}{S(k+1)} = \left(1 + \frac{f(k+1)}{S(k+2)}\right)^{-1}.$$So the desired inequality becomes$$\left(1 + \frac{f(k)}{S(k+1)}\right)^{-1} \ge \left(1 + \frac{f(k+1)}{S(k+2)}\right)^{-1},$$which is equivalent to$$\frac{f(k)}{S(k+1)} \le \frac{f(k+1)}{S(k+2)}, \quad \text{or} \quad f(k+1) S(k+1)\ge f(k) S(k+2).$$Expanding the terms, we write$$f(k+1) S(k+1) - f(k) S(k+2) = f(k+1) f(b) + \sum_{n=k+1}^{b-1} \big[f(k+1) f(n) - f(k) f(n+1)\big].$$We claim that each summand in the sum is non-negative. Indeed, it is straightforward to verify that the PMF (probability mass function) of the binomial distribution is log-concave, so that$$\frac{f(k+1)}{f(k)} \ge \frac{f(k+2)}{f(k+1)}, \quad \forall k.$$For any $n \ge k+1$, it then follows that$$\frac{f(k+1)}{f(k)}\ge \frac{f(n+1)}{f(n)} \quad \implies \quad f(k+1) f(n) \ge f(k) f(n+1),$$showing that each term in the sum is non-negative. Therefore,$$f(k+1) S(k+1) \ge f(k) S(k+2),$$which proves the log-concavity of the survival function:$$S(k+1)^2 \ge S(k) \, S(k+2).$$

Part (b). The inequality is trivial when $j + k > b$, since in that case both sides of the inequality are zero. For other cases, we proceed as follows.By Lemma 1 (a), the survival function $S(k)$ is log-concave and implies that the ratio$$r(k) := \frac{S(k+1)}{S(k)}$$is non-increasing in $k$, i.e.,$$r(k+1) \le r(k), \quad k=0,1,\dots,b-1.$$We express$$\frac{S(j+k)}{S(j)} = \prod_{i=0}^{k-1} r(j+i), \quad \text{and} \quad \frac{S(k)}{S(0)} = \prod_{i=0}^{k-1} r(i).$$Since $r(k)$ is non-increasing and $j+i\geq i$, $r(j+i) \le r(i)$ for all $i$, it follows that$$\frac{S(j+k)}{S(j)} \le \frac{S(k)}{S(0)}.$$But $S(0) = \mathbb{P}(B\geq 0)= 1$, so this becomes:$$S(j+k) \le S(j) \cdot S(k),$$which completes the proof.

Part (c). Define an independent binomial random variable $X \sim \mathrm{Binomial}(j, p)$, and let $Y \sim \mathrm{Binomial}(b - j, p)$. By the additivity of the binomial distribution, we have$$B = X + Y.$$We aim to prove the inequality:$$\mathbb{P}(B \geq j + k) \leq \mathbb{P}(B \geq j) \cdot \mathbb{P}(Y \geq k),$$which is equivalent to:$$\frac{\mathbb{P}(B \geq j + k)}{\mathbb{P}(B \geq j)} = \frac{\mathbb{P}(X + Y \geq j + k)}{\mathbb{P}(X + Y \geq j)} \leq \mathbb{P}(Y \geq k).$$We expand both the numerator and denominator using the law of total probability:$$\frac{\mathbb{P}(X + Y \geq j + k)}{\mathbb{P}(X + Y \geq j)} = \frac{\sum_{i=0}^j \mathbb{P}(X = i) \cdot \mathbb{P}(Y \geq j + k - i)}{\sum_{i=0}^j \mathbb{P}(X = i) \cdot \mathbb{P}(Y \geq j - i)}.$$Define weights:$$\alpha_i := \frac{\mathbb{P}(X = i) \cdot \mathbb{P}(Y \geq j - i)}{\sum_{i=0}^j \mathbb{P}(X = i) \cdot \mathbb{P}(Y \geq j - i)}, \quad i = 0, 1, \dots, j,$$which sum to 1. Then the expression becomes a convex combination of scaled tail probabilities:$$\frac{\mathbb{P}(X + Y \geq j + k)}{\mathbb{P}(X + Y \geq j)} = \sum_{i=0}^j \alpha_i \cdot \frac{\mathbb{P}(Y \geq j + k - i)}{\mathbb{P}(Y \geq j - i)}.$$Note that for each $i \in \{0,1,\dots,j\}$, we have:$$0 \le j + k - i \le b - j,$$so the expressions involving $Y \sim \mathrm{Binomial}(b - j, p)$ are valid. By applying Lemma 1 (b) to $Y$, we obtain:$$\frac{\mathbb{P}(Y \geq j + k - i)}{\mathbb{P}(Y \geq j - i)} \leq \mathbb{P}(Y \geq k), \quad \forall i.$$Thus,$$\frac{\mathbb{P}(B \geq j + k)}{\mathbb{P}(B \geq j)} \leq \sum_{i = 0}^{j} \alpha_i \cdot \mathbb{P}(Y \geq k) = \mathbb{P}(Y \geq k),$$which completes the proof.

Part (d). Let $Y \sim \mathrm{Binomial}(b - j - 1, p)$, and define $B_2 := j + 1 + Y$, which equals a constant shift of the binomial variable $Y$; that is, $B_2$ is distributed as $j+1+Y$, where $Y\sim\mathrm{Binomial}(b-j-1,p)$.We claim that:$$B \mid B > j \le_{\text{st}} B_2,$$where $\le_{\text{st}}$ denotes stochastic order smaller. By the properties of stochastic ordering (Shaked and Shanthikumar, 2007), this implies that$$\mathbb{E}[f(B \mid B > j)] \le \mathbb{E}[f(B_2)]$$for all non-decreasing functions $f$. In particular, taking $f(x) = x$, we obtain the desired inequality:$$\mathbb{E}[B \mid B > j] \le \mathbb{E}[B_2] = j+1 + (b - j - 1)p.$$To establish the stochastic order, we will show that:$$\mathbb{P}(B \geq k \mid B > j) \leq \mathbb{P}(B_2 \geq k), \qquad \forall k \in \{j+1, \dots, b\}.$$Observe that:$$\mathbb{P}(B \geq k \mid B > j) = \frac{\mathbb{P}(B \geq k)}{\mathbb{P}(B > j)} = \frac{\mathbb{P}(B \geq k)}{\mathbb{P}(B \geq j+1)}.$$Now recall the following inequality by applying part (c) of Lemma 1:$$\mathbb{P}(B \geq k) \leq \mathbb{P}(B \geq j+1) \cdot \mathbb{P}(Y \geq k - j - 1),$$where $Y \sim \mathrm{Binomial}(b - j - 1, p)$. Substituting gives:$$\mathbb{P}(B \geq k \mid B > j) \leq \mathbb{P}(Y \geq k - j - 1) = \mathbb{P}(B_2 \geq k).$$This completes the proof of the stochastic order, and therefore:$$\mathbb{E}[B \mid B > j] \leq \mathbb{E}[B_2] = j + 1 + (b - j - 1)p.$$

Part (e). If $\mathbb{P}(B > j) = 0$, the inequality is trivially satisfied. Otherwise, we first simplify the LHS (left-hand side) of the inequality:$$\begin{aligned}
\sum_{k = j + 1}^b \mathbb{P}(B > k)
&= \sum_{k = j + 1}^b \sum_{i = k + 1}^b \mathbb{P}(B = i) \\
&= \sum_{i = j + 1}^b \sum_{k = j + 1}^{i - 1} \mathbb{P}(B = i) \qquad \text{(by changing the order of summation)}\\
&= \sum_{i = j + 1}^b (i - j - 1) \mathbb{P}(B = i) \\
&= \mathbb{P}(B > j) \cdot \mathbb{E}[(B - j - 1) \mid B > j],
\end{aligned}$$where the last step follows from the definition of conditional expectation:$$\mathbb{E}[B - j - 1 \mid B > j] = \frac{\sum_{i = j + 1}^b (i - j - 1) \mathbb{P}(B = i)}{\mathbb{P}(B > j)}.$$Now consider the RHS (right-hand side):$$\mathbb{E}[B] \cdot \mathbb{P}(B > j) = bp \cdot \mathbb{P}(B > j).$$Thus, the inequality reduces to:$$\mathbb{P}(B > j) \cdot \mathbb{E}[(B - j - 1) \mid B > j]\le bp \cdot \mathbb{P}(B > j).$$Since $\mathbb{P}(B > j)>0$, divide both sides by $\mathbb{P}(B > j)$:$$\mathbb{E}[(B - j - 1) \mid B > j]\le bp.$$Note that:$$\mathbb{E}[B - j - 1 \mid B > j] = \mathbb{E}[B \mid B > j] - (j + 1).$$By part (d) of Lemma 1, $\mathbb{E}[B \mid B > j] \leq j + 1 + (b - j - 1)p$. Thus:$$\mathbb{E}[B - j - 1 \mid B > j] \leq (j + 1 + (b - j - 1)p) - (j + 1) = (b - j - 1)p\leq bp.$$This holds since $b-j-1 \leq b$ and $p\in[0,1]$ and completes the proof. 

■