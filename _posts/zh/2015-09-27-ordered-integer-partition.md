---
layout: post
title: Matlab codes for ordered integer partition
date: 2015-09-27  18:27-0800
categories: ["optimization", "matlab"]
tags: ["matlab", "integer partition", "ordered"]
giscus_comments: true
related_posts: true
---

The integer partition problems found on some websites does not consider order, for example, treating 3, 1 and 1, 3 as the same.

Considering the ordered integer partition problem is equivalent to the staircase problem. However, the online search results for the staircase problem do not provide the arranged outcomes. Below is the MATLAB codes I have written.

```matlab
function hua_fen
n=input('please input a number:\n');
global A B;
num=count(n,n);
A=zeros(num,n);
B=zeros(n,1);
m=1;
global len1 len2;
len1=1;
len2=1;
shu_chu(n,m);
C=zeros(2^(n-1),n); % store the partitioned results
mark=1;
for k=1:num
    temp=pai_lie(nonzeros(A(k,:))');
    [lgh,wth]=size(temp);
    C(mark:mark+lgh-1,1:wth)=temp;
    mark=mark+lgh;
end
end

function num=count(n,m)
    if n==1||m==1
        num=1;
    else
        if n<m
            num=count(n,n);
        end
        if n==m
            num=1+count(n,m-1);
        end
        if n>m
            num=count(n,m-1)+count(n-m,m);
        end
    end
end

function shu_chu(n,m)
global len1 len2 A B;
if n==0
    fprintf('%d',B(1))
    A(len2,1)=B(1);
    for i=2:1:m-1
        fprintf('+');
        fprintf('%d',B(i));
    end
    if m>len1
        fprintf('\n');
        len1=len1+1;
        len2=len2+1;
    else
        fprintf(', ');
        len2=len2+1;
    end
    return;
end

for i=n:-1:1
    if m==1||i<=B(m-1)
        B(m)=i;A(len2,m)=i;
        shu_chu(n-i,m+1);
    end
end
end

function B=pai_lie(A)
    d=length(A);
    B(1,:)=A';
    index=2;
    for i=1:d-1
        for j=i+1:d
            if A(j)~=A(i)
                B(index,:)=[A(1:i-1),A(j),A(i+1:j-1),A(i),A(j+1:d)];
                index=index+1;
            end
        end
    end
end
```
