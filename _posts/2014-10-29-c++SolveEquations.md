---
layout: post
title: Solve equations by Gaussian Elimination and Doolittle Decomposition in C++
date: 2014-10-29  13:27-0800
categories: c++-practice
giscus_comments: true
tags: c++, solving-equations, Gaussian-Elimination, Doolittle-Decomposition
related_posts: true
---

This is the homework for the "Numerical Analysis" course in Beihang University. After reviewing some codes online, I found most of them typically starting by fixing the number of rows and columns for the matrix. My codes, on the other hand, utilize a two-dimensional dynamic array (dynamic pointer), allowing the input of the number of rows and columns in programming runnning.

```c++
//codey by Chen Zhen, 2014/10/17, Beihang University
//use the dynamic 2D array (dynamic pointer)

#include<iostream>
#include<math.h>
#include<iomanip>
using namespace std;

void Gauss(double **a, double *b,int);//Sequential Gaussian Elimination
void lie_Gauss(double **a, double *b,int);//Partial Pivot Gaussian Elimination
void Doolittle(double **a, double *b,int);//Doolittle Decomposition
void print( double **a, double *b,int);//print equations

void main()
{
	//cout.setf(ios::fixed);
	cout.precision(4);//float precision

	//input matrix A and b
	int n;
	cout<<"please input the column number of the coefficients matirx (or row number since its square matrix):\n";
	cin>>n;
	cin.clear();//the following 3 lines reset input
	while(cin.get()!='\n')
		continue;
	cout<<"please input matirx A:\n";

	//use 2D array
	double **a;
	a=new double *[n];  //memory for the rows
	for (int i=0;i<n;i++)
		a[i]=new double[n];
	for (int i=0;i<n;i++)
	{
		cout<<"the "<< i+1<<"th row";
		for (int j=0;j<n;j++)
			while(!(cin>>a[i][j]))
			{
				cin.clear();
				while(cin.get()!='\n')
					continue;
				cout<<"please input a number";
			}
		cin.clear();
		while(cin.get()!='\n')
			continue;
	}
	cout<<"please input matrix b:\n";
	 double *b=new  double[n];
	for (int j=0;j<n;j++)
		cin>>b[j];
	cin.clear();
	while(cin.get()!='\n')
		continue;

	//store A and b in temple matrixs
	double **temp_a=new double *[n];
	double *temp_b=new double[n];
	for (int i=0;i<n;i++)
		temp_a[i]=new double[n];
	for (int i=0;i<n;i++)
		for (int j=0;j<n;j++)
			temp_a[i][j]=a[i][j];
	for (int i=0;i<n;i++)
		temp_b[i]=b[i];

	//print equations
	print(( double **)temp_a,temp_b,n);

	//chooose a solving algorithm
	cout<<"Please choose an algorithm(represented by a number) to solve:\n";
	cout<<"*************************\n";
	cout<<"1.Sequential Gaussian Elimination\n2.Paritial Pivoting Gaussian Elimination\n";
	cout<<"3.Doolittle Decomoposition\n";
	cout<<"*************************\n";
	int choice;
	while(cin>>choice)
	{
		switch (choice)
		{
		case 1: Gauss(( double **)temp_a,temp_b,n);
			break;
		case 2: lie_Gauss(( double **)temp_a,temp_b,n);
			break;
		case 3:	Doolittle(( double **)temp_a,temp_b,n);
			break;
		case 0: return;
		}
		cout<<"please select an algorithm to solve (number in 1-3), input 0 to exit:\n";
	}

	for (int i=0;i<n;i++)
		delete []temp_a[i];
	delete []temp_a;
	delete []temp_b;
	for (int i=0;i<n;i++)
		delete []a[i];
	delete []a;
	delete []b;
}

void Gauss( double **a,double *b,int n)
{
	double mm;
	double *jie=new double[n];
	for (int k=1;k<n;k++)
	{
		if (a[k-1][k-1]==0)
		{
			cout<<"algorithm is failure"<<endl;
			return;
		}
		for (int i=k+1;i<n+1;i++)
		{
			mm=a[i-1][k-1]/a[k-1][k-1];
			for (int j=k+1;j<n+1;j++)
			{
				a[i-1][j-1]=a[i-1][j-1]-mm*a[k-1][j-1];

			}
			b[i-1]=b[i-1]-mm*b[k-1];
			for (int j=1;j<k+1;j++)
                a[i-1][j-1]=0;
		}
		//print((double**)a,b,n);
	}
	if (a[n-1][n-1]==0)
	{
		cout<<"algorithm is failure"<<endl;
		return;
	}
	cout<<"solutions by Sequential Gaussian Elimination:\n";
	jie[n-1]=b[n-1]/a[n-1][n-1];
	for (int k=n-1;k>0;k--)
	{
		double temp=0;
		for (int j=k+1;j<n+1;j++)
			temp+=a[k-1][j-1]*jie[j-1];
		jie[k-1]=(b[k-1]-temp)/a[k-1][k-1];
	}
	for (int i=0;i<n-1;i++)
		cout<<"x"<<i+1<<" = "<<jie[i]<<endl;
	cout<<"x"<<n<<" = "<<jie[n-1]<<endl;
	cout<<endl;
	delete []jie;
}

void lie_Gauss( double **a,double *b,int n)
{
	for (int k=1;k<n;k++)
	{
		double max=abs(a[k-1][k-1]);
		int lie_hao=k;
		for (int i=k;i<n+1;i++)
			if (abs(a[i-1][k-1])>max)
			{
				max=abs(a[i-1][k-1]);
				lie_hao=i;
			}
		for (int j=k;j<n+1;j++)
		{
			double temp=a[k-1][j-1];
			a[k-1][j-1]=a[lie_hao-1][j-1];
			a[lie_hao-1][j-1]=temp;
		}
		for (int i=k+1;i<n+1;i++)
		{
			double mm=a[i-1][k-1]/a[k-1][k-1];
			for (int j=k+1;j<n+1;j++)
			{
				a[i-1][j-1]=a[i-1][j-1]-mm*a[k-1][j-1];

			}
			b[i-1]=b[i-1]-mm*b[k-1];
			for (int j=1;j<k+1;j++)
                a[i-1][j-1]=0;
		}
	}
	cout<<"solutions by Partial Pivot Gaussian Elimination\n";
	double *jie=new double[n];
	jie[n-1]=b[n-1]/a[n-1][n-1];
	for (int k=n-1;k>0;k--)
	{
		double temp=0;
		for (int j=k+1;j<n+1;j++)
			temp+=a[k-1][j-1]*jie[j-1];
		jie[k-1]=(b[k-1]-temp)/a[k-1][k-1];
	}
	for (int i=0;i<n-1;i++)
		cout<<"x"<<i+1<<" = "<<jie[i]<<endl;
	cout<<"x"<<n<<" = "<<jie[n-1]<<endl;
	cout<<endl;
	delete []jie;
}

void Doolittle(double **a,double *b,int n)
{
	double **u=new double *[n];
	for (int i=0;i<n;i++)
		u[i]=new double[n];
	double **l=new double *[n];
	for (int i=0;i<n;i++)
		l[i]=new double[n];
	double *jie_x=new double[n];
	double *jie_y=new double[n];
	for (int k=1;k<n+1;k++)
	{
		for (int j=k,i=k+1;j<n+1,i<n+1;j++,i++)
		{
			double sum_1=0;
			for (int t=1;t<k;t++)
			{
				sum_1+=l[k-1][t-1]*u[t-1][j-1];
			}
			u[k-1][j-1]=a[k-1][j-1]-sum_1;
			double sum_2=0;
			for (int t=1;t<k;t++)
			{
				sum_2+=l[i-1][t-1]*u[t-1][k-1];
			}
			l[i-1][k-1]=(a[i-1][k-1]-sum_2)/u[k-1][k-1];
		}
		double sum_1=0;
		for (int t=1;t<k;t++)
		{
			sum_1+=l[k-1][t-1]*u[t-1][n-1];
		}
		u[k-1][n-1]=a[k-1][n-1]-sum_1;
	}
	jie_y[0]=b[0];
	for (int i=2;i<n+1;i++)
	{
		double sum=0;
		for (int t=1;t<i;t++)
			sum+=l[i-1][t-1]*jie_y[t-1];
		jie_y[i-1]=b[i-1]-sum;
	}
	jie_x[n-1]=jie_y[n-1]/u[n-1][n-1];
	for(int i=n-1;i>0;i--)
	{
		double sum=0;
		for (int t=i+1;t<n+1;t++)
			sum+=u[i-1][t-1]*jie_x[t-1];
		jie_x[i-1]=(jie_y[i-1]-sum)/u[i-1][i-1];
	}
	cout<<"solutions by Doolittle Decomposition:\n";
	for (int i=0;i<n-1;i++)
		cout<<"x"<<i+1<<" = "<<jie_x[i]<<endl;
	cout<<"x"<<n<<" = "<<jie_x[n-1]<<endl;
	cout<<endl;

	delete []jie_x;
	delete []jie_y;
	for (int i=0;i<n;i++)
		delete []u[i];
	delete []u;
	for (int i=0;i<n;i++)
		delete []l[i];
	delete []l;
}

void print(double **a,double *b,int n)
{
	cout<<"equations:\n";
	cout<<"====================================================\n";
	for (int i=0;i<n;i++)
	{
		for (int j=0;j<n-1;j++)
		{
			cout<<a[i][j]<<" x"<< j+1<<" + ";
		}
		cout<<a[i][n-1]<<" x"<<n<<" = "<<b[i]<<endl;
	}
	cout<<"====================================================\n";
	cout<<endl;
}
```
