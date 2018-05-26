---
layout: post
title: 【约束非线性优化】拉格朗日乘子法与KKT条件.
categories:
tags: 8数值计算与最优化
keywords:
description:
order: 7200
---

拉格朗日乘子法（Lagrange Multiplier)是解决有约束条件的优化问题的重要方法  


## 问题
回忆非线性最优化的问题表达形式
### 无约束优化问题
$\min f(x)$  
[另一篇文章]


### 等式约束优化问题
$\min f(x)$,   
s.t. $h_i(x) = 0; i =1, ..., n $  

可以用拉格朗日乘子法解决  

### 不等式约束优化问题

$\min f(x)$,   
s.t. $g_i(x) <= 0; i =1, ..., n$  
$h_i(x) = 0; i =1, ..., n $  

常用KKT条件

## 等式约束优化问题
## 一个看似可行的方案

考察这样的问题：  
目标函数$f(x)=f(x_1,x_2,...x_{m+p})$  
约束条件:$$\left \{ \begin{array}{ccc}
g_1(x)=g_1(x_1,x_2,...x_{m+p})\\
.........\\
g_p(x)=g_p(x_1,x_2,...x_{m+p})\\
\end{array}\right.$$  


当然要求$$rank \left [ \begin{array}{ccc}
\dfrac{\partial g_1}{\partial x_1}&...&\dfrac{\partial g_1}{\partial x_{m+p}}\\
...&.....&...\\
\dfrac{\partial g_p}{\partial x_1}&...&\dfrac{\partial g_p}{\partial x_{m+p}}\\
\end{array}\right]=p$$  

移动变量位置，使得$$rank \left [ \begin{array}{ccc}
\dfrac{\partial g_1}{\partial x_1}&...&\dfrac{\partial g_1}{\partial x_p}\\
...&.....&...\\
\dfrac{\partial g_p}{\partial x_1}&...&\dfrac{\partial g_p}{\partial x_p}\\
\end{array}\right]=p$$  


那么，可以解出$$\left \{ \begin{array}{ccc}
x_{m+1}=\psi_1 (x_1,x_2,...x_m)\\
...\\
x_{m+p}=\psi_p (x_1,x_2,...x_m)\\
\end{array}\right.$$  

带入目标函数，得到  
$\phi((x_1,...,x_m)=f(x_1,...,x_m,\psi_1 (x_1,x_2,...x_m),...,\psi_p (x_1,x_2,...x_m))$(1-1)  
这就转化为无约束最优化问题。  


**然而，显示的解出约束变量几乎是不可能的**  

## 拉格朗日乘子法

引入辅助函数  
$F(x,\lambda)=f(x)+\sum_{r=1}^p \lambda_r g_r(x)$  
其中，$x=(x_1,...x_{m+p})$  


如果a是极值，那么存在$\lambda$，使得$(a,\lambda)$是$F(x,\lambda)$的临界点  
也就是说$$\left \{ \begin{array}{ccc}
\dfrac{\partial F}{\partial x_k}=0\\
\dfrac{\partial F}{\partial x_k}=g_r=0\\
\end{array}\right.$$  

### 证明提要  


#### （必要条件）  

用到(1-1)式  
$\phi((x_1,...,x_m)=f(x_1,...,x_m,\psi_1 (x_1,x_2,...x_m),...,\psi_p (x_1,x_2,...x_m))$在a取临界点  
$g_r(x_1,...,x_m,\psi_1 (x_1,x_2,...x_m),...,\psi_p (x_1,x_2,...x_m))=0$是恒等式  


上式分别取偏导数，分别得到甲式和乙式。乙式与$\lambda$线性组合加到甲式上。(略)  


得到：  
$\dfrac{\partial f}{\partial x_i}+\sum\limits_{r=1}^p \lambda_r \dfrac{\partial g_r}{\partial x_i}+\sum\limits_{j=1}^p(\dfrac{\partial f}{\partial x_{m+j}}+\sum\limits_{r=1}^p\lambda_r \dfrac{\partial g_r}{\partial x_{m+j}})\dfrac{\partial \psi_j}{\partial x_i}=0$(1-2)  


选择$\lambda$,可以使得  
$\dfrac{\partial f}{\partial x_{m+j}}+\sum\limits_{r=1}^p\lambda_r \dfrac{\partial g_r}{\partial x_{m+j}}=0$(1-3)  
带回(1-2)，得到：  
$\dfrac{\partial f}{\partial x_i}+\sum\limits_{r=1}^p \lambda_r \dfrac{\partial g_r}{\partial x_i}=0$(1-4)  

(1-3)与(1-4)就是拉格朗日条件。  

#### (充分条件)
$a+h,a$在可行域上M，$g(a+h)-g(a)=0$二阶展开，带入$f(a+h)-f(a)$后，可以找到取极值的条件。  

## Lagrange对偶性

从上面知道，对于优化问题：  
$\min f(x)$,   
s.t. $g_i(x) <= 0; i =1, ..., n$  
$h_i(x) = 0; i =1, ..., n $  


对应的Lagrange函数是$L(x,\lambda,v)=\sum\limits_{i=1}^m\lambda_i f_i(x)+\sum\limits_{i=1}^p v_ih_i(x)$  


那么Lagrange对偶函数是$g(\lambda,v)=\inf\limits_x L(x,\lambda,v)$  

<!--
### 性质
1. 即使原问题不是凸的，对偶函数也是凹函数
-->


## 参考资料


http://www.jianshu.com/p/96db9a1d16e9
