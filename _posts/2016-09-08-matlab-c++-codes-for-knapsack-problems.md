---
layout: post
title: Matlab and C++ codes for dynamic programming to solve the knapsack problem
categories: ["optimization", "c++", "matlab"]
tags: ["knapsack", "dynamic programming", "c++", "matlab"]
giscus_comments: true
related_posts: true
---

Knapsack Problem Description:

There are five items labeled a, b, c, d, e. Their weights are 2, 2, 6, 5, 4, and their values are 6, 3, 5, 4, 6, respectively. Now, you are given a knapsack with a capacity of 10. How can you maximize the total value of the items in the knapsack? (Assume that multiple instances of each item can be included)

Following the steps to solve dynamic programming problems, let's proceed step by step. Let $$c_i$$ represent the weights of the items, and $$v_i$$ represent their values.

**Stages:**

$$
i=1,2,\dots,5
$$

representing the checking of the $$i_{th}$$ item.

**State variables:**

$$
S_{i}\qquad i=1,2,\dots,5
$$

representing the remaining carrying capacity in the knapsack when examining the $$i_{th}$$ item. To solve a problem using dynamic programming, it is essential to ensure that the state space is finite.
