# 最小二乘法

[>>前往教程目录](guide-matrix.md)

[TOC]

## 最小二乘法

最小二乘法(又称最小平方法)是一种数学优化技术。它通过最小化误差的平方和寻找数据的最佳函数匹配。在统计学中，利用最小二乘法可以简便地求得未知的数据，并使得这些求得的数据与实际数据之间误差的平方和为最小。

很多工程应用问题都可以归结为线性方程 $Ax = b$ 的求解。其中，$A$ 和 $b$ 为已知，但可能同时或其中一个有误差。独立方程的个数可能少于、等于或多于未知向量x的维数(欠定、适定、超定方程)。

问题：求最佳解 $x^*$ 使得对应的方程两边的误差向量的某种范数最小化：
$$
\left\|A x^{*}-b\right\|_{p} \leqslant\|A x-b\|_{p}
$$

1. 当p= 1时，该问题称为最小绝对偏(least absolute deviation, LAD)问题；
2. 当p=2时，该问题称为线性最小二乘(linearleast-squares)问题；
3. 当p= $\infty$时，该问题称为Chebyshev或最小最大(minimax)问题。

其中的无穷范数的定义为：
$$
\|y\|_{\infty}=\max \left(\left|y_{1}\right|,\left|y_{2}\right|, \cdots,\left|y_{n}\right|\right)
$$
故最小最大问题即为使方程两边误向量的最大误元素最小化。

求解的其近似解的方法就是最小二乘，我们介绍普通最小二乘、数据最小二乘和总体最小二乘三种。

（1）普通最小二乘(OLS, Ordinary Least Squares)：假定仅向量 $b$ 有误 $e$，且每一个误差元素服从零均值、等方差的独立高斯分布。
代价函数：
$$
J(x) = \|e\|_2^2 = e^Te = (A x-b)^{T}(A x-b)
$$
OLS准则：使方程两边的误平方和最小。

（2）数据最小二乘(DLS, Data Ieast Squares)：假定仅数据矩阵 $A$ 有误差，且每一个误差元素服从零均值、等方差的独立高斯分布，则x的最优解为：
$$
\boldsymbol{x}^{*}=\arg \left\{\min \|\boldsymbol{E}\|_{F}^{2}\right\} \quad \text { s.t. } \quad \boldsymbol{b} \in \operatorname{Range}(\boldsymbol{A}+\boldsymbol{E})
$$
考虑拉格朗日函数，再对矩阵 $E$ 求导，易得：
$$
J(\boldsymbol{x})=\|\boldsymbol{E}\|_{F}^{2}=\operatorname{tr}\left(\boldsymbol{E} \boldsymbol{E}^{T}\right)=\frac{(\boldsymbol{A} \boldsymbol{x}-\boldsymbol{b})^{T}(\boldsymbol{A} \boldsymbol{x}-\boldsymbol{b})}{\boldsymbol{x}^{T} \boldsymbol{x}}
$$
（3）总体最小二乘(TLS, Total Least Squares)：假定数据矩阵 $A$ 和向量 $b$ 分别有误差矩阵 $E$ 和误差向量 $e$，并且每一个误差元素都服从零均值、等方差的高斯分布，则 $x$ 的解由优化问题：
$$
\min \|[\boldsymbol{E}, \boldsymbol{e}]\|_{F}^{2} \quad \text { s.t. } \quad \boldsymbol{b}+\boldsymbol{e} \in \operatorname{Range}(\boldsymbol{A}+\boldsymbol{E})
$$
即：
$$
J(x)=\frac{\left[\begin{array}{c}
x \\
-1
\end{array}\right]^{T}[A, b]^{T}[A, b]\left[\begin{array}{c}
x \\
-1
\end{array}\right]}{\left[\begin{array}{c}
x \\
-1
\end{array}\right]^{T}\left[\begin{array}{c}
x \\
-1
\end{array}\right]}
$$
总结：线性矩阵方程 $Ax =b$ 的三种最小二乘问题及其代价函数：
$$
J(x)=\left\{\begin{array}{ll}
(A x-b)^{T}(A x-b)& \text { 普通最小二乘 } \\
\frac{(A x-b)^{T}(A x-b)}{x^Tx}
& \text { 数据最小二乘 }\\
\frac{
{\left[\begin{array}{c}
x \\
-1
\end{array}\right]^{T}[A, b]^{T}[A, b]\left[\begin{array}{c}
x \\
-1
\end{array}\right]} }{1+x^{T} x}& \text { 总体最小二乘 }
\end{array}\right.
$$

### 普通最小二乘方法

在条件 $Ax=b+\Delta b$ 约束下 $\min_{x,\Delta b} \|\Delta b\|$ 

最小二乘方法的基本思想：用尽可能小的校正项 $\Delta b$ 去扰动 $b$，使得 $b十\Delta b$ 满足 $Ax=b+\Delta b$，从而补偿存在于数据向量 $b$ 中的噪声。

最小二乘方法的实质：当测量 $b$ 无噪声时，有 $Ax_0=b_0$。此时 $x_0$ 给出准确解。但实际观测值往往存在误差，即 $b= b_0-e$。因此 $Ax_0=b$ 不再成立。现在我们用一个尽可能小的 $\Delta b$ 去抗劫 $b$，即 $b+\Delta b$，目的是抵消掉 $e$，即 $b+\Delta b = b_0 - e+\Delta b \rightarrow b_0$。从而使得 $Ax=b+\Delta b$ 成立。在这个意义上得出的 $x$ 即为最小二乘解。

代价函数：
$$
\phi(\boldsymbol{x})=\|\Delta \boldsymbol{b}\|_{2}^{2}=\|\boldsymbol{A} \boldsymbol{x}-\boldsymbol{b}\|_{2}^{2}
$$
我们对它求导，并令其为零向量，即：
$$
\frac{\mathrm{d} \phi}{\mathrm{d} x}=-2 \boldsymbol{A}^{\mathrm{T}} \boldsymbol{b}+2 \boldsymbol{A}^{\mathrm{T}} \boldsymbol{A} \boldsymbol{x}=0
$$
则解 $x$ 必然满足：
$$
\boldsymbol{A}^{\mathrm{T}} \boldsymbol{A} \boldsymbol{x}=\boldsymbol{A}^{\mathrm{T}} \boldsymbol{b}
$$
当矩阵 $A_{m \times n}$ 具有不同的秩时，该方程的解分成两种情况：

1. $rank(A) = n$

   此时 $A^T A$ 非奇异，所以方程有唯一的解：$x=(A^T A)^{-1}A^Tb$，此即为最小二乘解。在参数估计理论中，称这种可以唯一确定的未知参数 $x$ 是(唯一)可辨识的。

2. $rank(A)<n$
   此时，方程 $Ax = b$ 存在无穷多个解。显而易见，虽然数据向量 $b$ 可以提供有关 $Ax$的某些信息，但是却无法区别对应于相同 $Ax$ 值的各个不同的未知参数向量 $x$。因此，称这样的参数向量是不可辨识的。更一般地，如果某参数的不同值给出在抽样空间上的相同分布，则称该参数是不可辨识的。

**Gauss-Markov定理**

我们考虑线性方程组 $A \theta = b+e$，其中 $A \in R^{m \times n},\theta \in R^{n \times 1}$ 分别是常数矩阵和未知数向量，$b \in R^{m \times 1}$ 存在随机误差向量 $e = [e_1,e_2,\cdots,e_m]^T$，满足 $E(e) = 0,cov(e) = E(ee^H) = \sigma^2 I$.

则当且仅当 $rank(A) = n$，$\theta$ 存在最优无偏估计 $\hat{\theta}$ 
$$
\hat{\boldsymbol{\theta}}=\left({A}^{\mathrm{H}} \boldsymbol{A}\right)^{-1}{A}^{\mathrm{H}} \boldsymbol{b}
$$
其方差 $\operatorname{var}(\hat{\boldsymbol{\theta}}) \leqslant \operatorname{var}(\tilde{\boldsymbol{\theta}})$. $\tilde{\boldsymbol{\theta}}$ 是 $A \theta = b+e$ 的任意其他解。

证明：...（暂略）

## 总体最小二乘

最小二乘：
$$
Ax = b+e
$$
总体最小二乘：

基本思想：不仅用扰动向量e去干扰数据向量b，而且用干扰矩阵E同时去干扰数据矩阵A，以便校正A和b两者内存在的扰动(误差)并使两个扰动的范数平方保持最小。
$$
\begin{aligned}
(\boldsymbol{A}+\boldsymbol{E}) \boldsymbol{x}=\boldsymbol{b}+\boldsymbol{e} & \Rightarrow([-\boldsymbol{b}, \boldsymbol{A}]+[-e, \boldsymbol{E}])\left[\begin{array}{l}
1 \\
\boldsymbol{x}
\end{array}\right]=0 \\
& \Rightarrow(\boldsymbol{B}+\boldsymbol{D}) z=0 \\
& \Rightarrow \min _{D, \boldsymbol{x}}\|\boldsymbol{D}\|_{\mathrm{F}}^{2} \\
& \text { s.t. }(\boldsymbol{b}+\boldsymbol{e}) \in \operatorname{Range}(\boldsymbol{A}+\boldsymbol{E})
\end{aligned}
$$

## 约束总体最小二乘(选)

..（暂略）

## 结构总体最小二乘(选)

..（暂略）

