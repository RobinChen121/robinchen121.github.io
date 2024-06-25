---
layout: post
title: Matlab and C++ codes for dynamic programming to solve the knapsack problem
date: 2016-09-08  13:20-0800
categories: ["optimization", "c++", "matlab"]
tags: ["knapsack", "dynamic programming", "c++", "matlab"]
giscus_comments: true
related_posts: true
toc:
  beginning: true
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

**Decision Variables:**

$$
x_{i}\qquad i=1,2,\dots,5
$$

representing how many of the $$i_th$$ item are included.

**State Transition Equation:**

$$
S_{i+1}=S_{i}-c_{i}x_{i}
$$

**Optimal Profit Function:**

$$
\mathop{f}(S_{i})
$$

Represents, when examining the $$i_{th}$$ item, the maximum value achievable by including items $$i, i+1,\dots,5$$ in the knapsack with remaining capacity $$S_i$$.

**Optimal Profit Function Transition Equation:**

$$
\mathop{f}\limits_{c_{i}x_{i}\leq S_{i}}(S_{i})= \begin{cases} v_{i}x_{i}+f(S_{i+1})\quad &i=1,2,\dots 4\ v_{i}x_{i}\quad &i=5 \end{cases}
$$

Once the optimal transition equation is obtained, the problem can be solved. It can be solved by backward induction. However, it is also possible to solve it using forward induction, but it requires a change in the definition of the optimal profit function.

### matlab codes

```matlab
function Knapsack
c=[2 2 6 5 4];v=[6 3 5 4 6];
f=zeros(5,11);x=zeros(5,11);xx=zeros(5,1);
for i=5:-1:1
    for S=0:10
        if i==5
            f(i,S+1)=v(i)*floor(S/c(i));
            x(i,S+1)=floor(S/c(i));
        else
            xMax=floor(S/c(i));
            ff=zeros(xMax+1,1);
            for k=0:xMax
                ff(k+1)=v(i)*k+f(i+1,S-c(i)*k+1);
            end
            [f(i,S+1),index]=max(ff);
            x(i,S+1)=index-1;
        end
    end
end
[optValue,index]=max(f(1,:));
xx(1)=x(1,index);
tempS=index;
fprintf('optimal solution:%d\n',optValue);
for i=2:5
    xx(i)=x(i,tempS-c(i-1)*xx(i-1));
    tempS=tempS-c(i-1)*xx(i-1);
end
for i=1:5
    fprintf('put %d item%d in the bag\n',xx(i),i);
end

end
```

### c++ codes

```c++
#include"stdio.h"
#include"stdlib.h"


int * Max(int *arr, int n)
{
	int *a=(int *)malloc(2*sizeof(int));
	a[0]=0;a[1]=0;
	for (int i=0;i<n;i++)
	{
		if (arr[i]>a[0])
		{
			a[0]=arr[i];a[1]=i;
		}
	}
	return a;
}

void main()
{
	static const int c[5]={2,2,6,5,4};
	static const int v[5]={6,3,5,4,6};

	int f[5][11];
	int x[5][11];
	int itemNum[5];

	for (int i=5;i>0;i--)
		for (int S=0;S<11;S++)
		{
			if (i==5)
				{
					f[i-1][S]=v[i-1]*(S/c[i-1]);
					x[i-1][S]=S/c[i-1];
				}
			else
			{
				int xMax=S/c[i-1];
				int * ff= (int *)malloc(sizeof(int)*(xMax+1));
				for(int k=0;k<=xMax;++k)
					ff[k]=v[i-1]*k+f[i][S-c[i-1]*k];
				int *a=Max(ff,xMax+1);
				f[i-1][S]=a[0];x[i-1][S]=a[1];
				free(a);
				free(ff);
			}
		}

	int *temp=f[0];
	int *maxValue=Max(temp,11);
	int tempS=maxValue[1];
	itemNum[0]=x[0][tempS];
	for (int i=1;i<5;++i)
	{
		itemNum[i]=x[i][tempS-c[i-1]*itemNum[i-1]];
		tempS-=c[i-1]*itemNum[i-1];
	}
	printf("the optimal solution is: %d\n",maxValue[0]);
	for(int i=0;i<5;i++)
		printf("put %d item%d in the bag\n",itemNum[i],i+1);
	free(maxValue);
}
```
