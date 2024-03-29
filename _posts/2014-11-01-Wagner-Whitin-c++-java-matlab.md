---
layout: post
title: C++, Java and Matlab codes for Wagner-Whitin algorithm
date: 2014-11-01  16:52:24-0800
categories: ["c++", "java", "inventory", "matlab"]
tags: ["c++", "java", "lot sizing", "Wagner-Whitin", "matlab"]
giscus_comments: true
related_posts: true
toc:
  beginning: true
---

The Wagner-Whitin algorithm was proposed in Management Science (Wagner and Whitin, 1958) to address the Uncapacitated Lot Sizing Problem (ULSP) in multi-stage batch production without capacity constraints.

The algorithm employs the principles of dynamic programming, and its computational complexity is:

$$
O(N^2),
$$

where $$N$$ is the length of the planning horizon. This algorithm is a polynomial time algorithm. The paper proves two properties satisfied by the optimal solution:

(1) Replenishment is optimal only when initial inventory is zero, i.e., zero inventory ordering policy (Known as the ZIO property), which leads to the development of the dynamic algorithm.

(2) For any period, assuming ordering is done $$m$$ periods in advance, there exists an upper bound on $$m$$. In other words, in the optimal strategy, replenishment should not occur excessively early.

### C++ codes

```c++
#include<iostream>
#include<fstream>

using namespace std;

const int T=12;  // the length of the planning horizon
const double D[T]={10,62,12,130,154,129,88,52,124,160,238,41};
const double s[T]={54,54,54,54,54,54,54,54,54,54,54,54};
const double h[T]={0.4,0.4,0.4,0.4,0.4,0.4,0.4,0.4,0.4,0.4,0.4,0.4};

double min(double *,int); // return to the minimum in an array

template<typename T>
void print(T *,int);

void main()
{
	double cost[T][T]; // the total cost in a production cycle from one period to another period
	double Opt_cost[T];  //optimal total cost from one period to final period T
	int Order[T];  // optimal production plan, binary variables denoting whether to product in each period
	double I[T];  // inventory on hand in each period

	for (int i=0;i<T;i++)
		for (int j=0;j<T;j++)
			cost[i][j]=INT_MAX;  // initializing costs


	// compute costs for difference production cycles and optimal total cost
	for (int i=0;i<T;i++)
	{
		if(i>0)
		{
			double p[T];
			for (int j=0;j<T;j++)
				p[j]=cost[j][i-1];
			Opt_cost[i-1]=min(p,T);
		}

		for (int j=i;j<T;j++)
		{
			double sum=0;
			for (int k=i;k<j+1;k++)
				sum+=D[k];
			double h_sum=0;
			for (int k=i;k<j+1;k++)
			{
				h_sum=h_sum+h[i]*(sum-D[k]);
				sum=sum-D[k];
			}
			if (i>0)
				cost[i][j]=Opt_cost[i-1]+h_sum+s[i];
			else
				cost[i][j]=h_sum+s[i];
		}
	}
	double p[T];
	for (int j=0;j<T;j++)
			p[j]=cost[j][T-1];
	Opt_cost[T-1]=min(p,T);

	// backorder to get optimal production plan
	int i=T-1;
	while (i>=0)
	{
		if (Opt_cost[i]==cost[i][i])
		{
			Order[i]=1;
			i=i-1;
		}
		else
		{
			Order[i]=0;
			int index=i;
			for (int k=0;k<i;k++)
			{
				if (Opt_cost[i]==cost[k][i])
				{
					index=k;
					Order[index]=1;
					break;
				}
			}
			Order[index]=1;
			for (int k=index+1;k<i;k++)
				Order[k]=0;
			i=index-1;
		}
	}

	// get inventory on hand by the optimal production plan
	i=0;
	int index=0;
	while (index<T-1)
	{
		for (int j=i+1;j<T;j++)
		{
			if (Order[j]==1)
			{
				index=j;
				break;
			}
			if (j==T-1&&Order[j]==0)
			{
				index=T;
			}
		}
		double sum=0;
		for (int k=i;k<index;k++)
			sum+=D[k];
		for (int k=i;k<index;k++)
		{
			sum=sum-D[k];
			I[k]=sum;
		}
		i=index;
	}

	cout<<"optimal productoin plan:"<<endl;
	print(Order,T);
	//print(cost,T);
	cout<<"opimtal total cost from each period"<<endl;
	print(Opt_cost,T);
	cout<<"inventory for each period in the optimal production plan"<<endl;
	print(I,T);

}

double min(double *a,int n)
{
	double temp=a[0];
	for (int i=1;i<n;i++)
		if (a[i]<temp)
			temp=a[i];
	return temp;
}

template<typename T>
void print(T *a,int n)
{

	for (int i=0;i<n;i++)
		cout<<a[i]<<" ";
	cout<<endl;
}
```

### Java codes

```java
import java.util.Arrays;

public class SingleItemLS {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int T = 12; // length of the planning horizon
		double[] D = {10,62,12,130,154,129,88,52,124,160,238,41};
		double[] s = {54,54,54,54,54,54,54,54,54,54,54,54};
		double[] h = {0.4,0.4,0.4,0.4,0.4,0.4,0.4,0.4,0.4,0.4,0.4,0.4};

		double[][] cost = new double[T][T]; //the total cost in a production cycle from one period to another period
		double[] OptCost = new double[T]; //optimal total cost from one period to final period T
		int[] Order = new int[T];  // optimal production plan, binary variables denoting whether to product in each period
		double[] I = new double[T]; // inventory on hand at each period

		for (int i = 0; i < T; i++)
			for (int j = 0; j < T; j++)
				cost[i][j] = Double.MAX_VALUE;  // initialize costs


		// compute costs for difference production cycles and optimal total cost
		for (int i = 0; i < T; i++)
		{
			if(i > 0)
			{
				double[] p = new double[T];
				for (int j=0;j<T;j++)
					p[j]=cost[j][i-1];
				OptCost[i-1]= Arrays.stream(p).min().getAsDouble();
			}

			for (int j = i; j < T; j++)
			{
				double sum=0;
				for (int k = i; k < j + 1; k++)
					sum += D[k];
				double hSum = 0;
				for (int k = i; k < j + 1; k++)
				{
					hSum = hSum + h[i]*(sum - D[k]);
					sum = sum - D[k];
				}
				if (i>0)
					cost[i][j] = OptCost[i-1] + hSum + s[i];
				else
					cost[i][j] = hSum + s[i];
			}
		}
		double[] p = new double[T];
		for (int j = 0; j < T; j++)
				p[j] = cost[j][T-1];
		OptCost[T-1] = Arrays.stream(p).min().getAsDouble();

		// backward to get optimal production plan
		int i=T-1;
		while (i>=0)
		{
			if (OptCost[i] == cost[i][i])
			{
				Order[i] = 1;
				i = i-1;
			}
			else
			{
				Order[i] = 0;
				int index = i;
				for (int k = 0; k < i; k++)
				{
					if (OptCost[i] == cost[k][i])
					{
						index = k;
						Order[index] = 1;
						break;
					}
				}
				Order[index] = 1;
				for (int k = index + 1; k < i; k++)
					Order[k] = 0;
				i = index - 1;
			}
		}

		// get optimal inventory at each period by optimal production plan
		i=0;
		int index = 0;
		while (index < T-1)
		{
			for (int j = i + 1; j < T; j++)
			{
				if (Order[j] == 1)
				{
					index = j;
					break;
				}
				if (j == T-1 && Order[j] == 0)
				{
					index = T;
				}
			}
			double sum = 0;
			for (int k = i; k < index; k++)
				sum += D[k];
			for (int k = i; k < index; k++)
			{
				sum = sum - D[k];
				I[k] = sum;
			}
			i = index;
		}

		System.out.println("optimal production plan:");
		System.out.println(Arrays.toString(Order));
		System.out.println("optimal total cost from each period:");
		System.out.println(Arrays.toString(OptCost));
		System.out.println("optimal inventory at each period:");
		System.out.println(Arrays.toString(I));
	}
}
```

### matlab codes

```matlab
function MyWW
% x are binary variabes denoting whether to produce in each period
% y are the production quantities in each period
% I are the inventory in each period
% I0 is the initial inventory

I0=50;
n=8;

% d=randi([5 25],1,n);
% S=randi([20 100],1,n);
% h=randi([5 20],1,n);
% c=randi([10 25],1,n);

d=[9,12,9,25,9,20,20,25];
S=[100,100,100,100,100,100,100,100];
h=[5,5,5,5,5,5,5,5];
c=10*ones(1,n);

x=zeros(1,n);
y=zeros(1,n);
I=zeros(1,n);

C=1e4*ones(n,n); %成本矩阵
opt_cost=zeros(n,1);
initial_I=zeros(n,1);
for i=1:n
    if i>1
        opt_cost=min(C(:,i-1));
    end
    for j=i:n
        if I0>=sum(d(1:j))
            if i==1
                C(i,j)=h(1:j)*(I0-cumsum(d(i:j)))';
            else
                C(i,j)=opt_cost+h(i:j)*(I0-cumsum(d(i:j)))';
            end
        else
            initial_I(i)=I0;
            if i>1
                if I0>sum(d(1:i-1))
                    initial_I(i)=I0-sum(d(1:i-1));
                else
                    initial_I(i)=0;
                end
            end
            prod_amount=sum(d(i:j))-initial_I(i);
            temp_I=initial_I(i)+prod_amount;
            h_sum=h(i:j)*(temp_I-cumsum(d(i:j)))';
            if i>1
                C(i,j)=opt_cost+S(i)+h_sum+c(i)*prod_amount;
            else
                C(i,j)=S(i)+h_sum+c(i)*prod_amount;
            end
        end
   end
end

%back track
j=n;
while j>=1
    [~,index]=min(C(:,j));
    if I0<sum(d(1:index))
        x(index)=1;
        if i>1
            y(index)=sum(d(index:j))-initial_I(index);
        else
            y(index)=sum(d(index:j))-initial_I(index);
        end
    end
    j=index-1;
end
for i=1:n
    if i==1
        I(i)=I0+y(i)-d(i);
    else
        I(i)=I(i-1)+y(i)-d(i);
    end
    fprintf('  %d',I(i));
end
fprintf('\n');
fprintf('production quantity at each period:\n');
for i=1:n
    fprintf('  %d',y(i));
end
fprintf('\n');
fprintf('whether to produce in each period:\n');
for i=1:n
    fprintf('  %d',x(i));
end
fprintf('\n');
end
```
