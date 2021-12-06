# 奇异值分析

[>>前往教程目录](guide-matrix.md)

[TOC]

## 基础知识的补充

### 矩阵范数

$$
\|A\|=\max _{x} \frac{\|A x\|}{\|x\|}
$$

$$
\left\|A^{-1}\right\|=\max _{y} \frac{\left\|A^{-1} y\right\|}{\|y\|}=1 / \min _{y} \frac{\|y\|}{\left\|A^{-1} y\right\|}=1 / \min _{x} \frac{\|A x\|}{\|x\|}
$$

### 关于扰动对求逆的影响

足够近的扰动可以保持可逆矩阵的“可逆”性（可以通过特征值函数的连续性来说明）

### 酉矩阵

$$
A^H A = AA^H =E
$$

其中上角标H表示共轭转置矩阵。

### 奇异值

设 $A$ 为 $m*n$ 阶 矩，$q=\min(m, n)$，$A^HA$ 的 $q$ 个非负特征值的算术平方根叫作 $A$ 的奇异 值。 奇异值分解是线性代数和矩阵论中一种重要的矩阵分解法，适用于信 号处理和统计学等领域。

## 数值稳定性与条件数

在介绍数值稳定性之前，我们先来定义一下什么叫良性问题和病态问题，我们先给出定义。

良性问题：$f\left(d^{*}\right) \rightarrow f(d) \quad \text { as } \quad d^{*} \rightarrow d$

病态问题：$f\left(d^{*}\right) \nrightarrow f(d) \quad \text { as } \quad d^{*} \rightarrow d$

在扰动理论中，称求解 $f(d)$ 的某种算法 $f^*$ 是数值稳定的，若它引入的对扰动的敏感度不会比原问题本身的敏感度大。即若 $f^*(\sim f)$是稳定的，则$f\left(d^{*}\right) \rightarrow f(d) \quad \text { as } \quad d^{*} \rightarrow d$

良态问题与算法稳定性可以保证“少量”扰动问题的解接近于无扰动问题的解。

### 数值稳定性

数值稳定性（数学表示）：我们考察 $Ax = b$ 这个方程，通过研究方程的解向量 $x$ 如何受系数矩阵 A 和系数向量 b 的元素微小变化(扰动)的影响，将得到描述矩阵A的一个重要特征的数值，称为条件数(condition number)。

矩阵的条件数：$\kappa(A)=\|A\|\left\|A^{-1}\right\|$

注，条件数同时描述了对向量的拉伸和压缩能力。即，使得向量发生形变的能力。条件数越大，向量在变换后可能发生变化的越大。

### 条件数在线性方程稳定上扮演的角色

- 我们先看对**向量 $b$** 的扰动的影响：

$$
\begin{aligned} & \boldsymbol{A}(\boldsymbol{x}+\delta \boldsymbol{x})=\boldsymbol{b}+\delta \boldsymbol{b} \\ \Rightarrow & \delta \boldsymbol{x}=\boldsymbol{A}^{-1} \delta \boldsymbol{b} \\ \Rightarrow &\|\delta \boldsymbol{x}\| \leqslant\left\|\boldsymbol{A}^{-1}\right\|\|\delta \boldsymbol{b}\| \end{aligned}
$$

另外我们有 $\|b\|=\|A x\| \leqslant\|A\|\|x\|$

综上两个不等式，我们可以轻松得到：
$$
\frac{\|\delta x\|}{\|x\|} \leqslant\left(\|A\|\left\|A^{-1}\right\|\right) \frac{\|\delta b\|}{\|b\|}
$$
由上面这个不等式可以看出，当条件数为10时，观测值如果变化100%， 会导致解最多变化1000%。
$$
\frac{1}{\kappa(A)} \frac{\|\delta b\|}{\|b\|} \leq \frac{\|\delta x\|}{\|x\|} \leq \kappa(A) \frac{\|\delta b\|}{\|b\|}
$$
首先，矩阵的条件数唯一决定了线性方程的解受观测值的噪声的影响程度，条件数越大，x受噪声影响越严重，这意味着，x的变化率越偏离b的变化率(注意，并非只有x变化率远大于b的变化率才叫偏离， 变化率过小的情况也叫偏离，比如无论b怎么变化，x都纹丝不动)。其次，条件数对稳定性的衡量不受尺度影响，整体放缩任意的比例都不会影响该不等式的结果，因为受噪声影响程度是通过变化率来衡量的， 与绝对大小无关。

- 对**矩阵 $A$** 的扰动的影响：

$$
(\boldsymbol{A}+\delta \boldsymbol{A})(\boldsymbol{x}+\delta \boldsymbol{x})=\boldsymbol{b}
$$

展开得到：$\delta x=-\boldsymbol{A}^{-1} \delta \boldsymbol{A}(\boldsymbol{x}+\delta \boldsymbol{x})$

取范数得到：$\|\delta x\|=\|\boldsymbol{A}^{-1} \delta \boldsymbol{A}(\boldsymbol{x}+\delta \boldsymbol{x})\|$

由范数的性质得到不等式：
$$
\begin{array}{c}\|\delta \boldsymbol{x}\| \leqslant\left\|\boldsymbol{A}^{-1}\right\|\|\delta \boldsymbol{A}\|\|\boldsymbol{x}+\delta \boldsymbol{x}\| \\ \frac{\|\delta \boldsymbol{x}\|}{\|x+\delta \boldsymbol{x}\|} \leqslant\left(\|\boldsymbol{A}\|\left\|\boldsymbol{A}^{-1}\right\|\right) \frac{\|\delta \boldsymbol{A}\|}{\|\boldsymbol{A}\|}\end{array}
$$
考虑向量 $b$ 和矩阵 $A$ 的扰动的综合影响知：解向量 $x$ 的相对误差 $\delta x$ 与数值$\|A\| \|A^{-1}\|$ 成正比。

因此有了这个条件数的定义：矩阵的条件数：$con d(A)=\|A\|\left\|A^{-1}\right\|$

条件数刻画了求解线性方程时，误差经过矩阵A的的传播扩大为解向量误差的程度，因此是衡量线性方程数值稳定性的一个重要指标。注意，条件数的定义中并未指定矩阵范数的类型，可以为矩阵的任一从属范数。因此，**其大小依赖于范数类型的选择**。

### 条件数的性质

1. $\operatorname{cond}(A) \geq 1$，特别的如果 A 为正交矩阵或者酉矩阵，则 $\operatorname{cond}(A) = 1$。
2. $\operatorname{cond}(aA) = \operatorname{cond}(A) ,(a \neq 0)$
3. $\operatorname{cond}(A^HA) = [\operatorname{cond}(A) ]^2$
4. 正交(酉)变换不改变条件数

$$
\operatorname{cond}(QA) = \|QA\|\|(QA)^{-1}\| = \|A\|\|A^{-1}\|\operatorname{cond}(A)
$$

在线性方程中，病态方程一般是指系数矩阵条件数“很大”的线性方程。此时，对于一个接近真实 b 的 $b^*$，由于条件数很大，所以与 $b^*$ 对应的解就会远离对应于 b 的真实解。

对上面这个问题，也就是求解病态方程，我们也有方法解决：

- 对病态方程使用正交变换或者正交分解(如QR分解、奇异值分解、特征值分解等)。
- 然而，解决这类病态问题更为有效的方法却是总体最小二乘法，其基础即为奇异值分解。

## 奇异值分解

### 奇异值分解定理

...

### 关于奇异值分解定理的证明

...

### 关于奇异值分解的几点解释

...

矩阵奇异值的内在含义：$n \times n$ 矩阵 $A$ 至少有一个零奇异值 $\rightarrow$  $rank(A)\leq
n-1$ $\rightarrow$ 矩阵 $A$ 奇异。推而广之，一个非正方的矩阵如果有零奇异值，则说明这个长方矩阵一定不是列满秩或行满秩的。这种情况称为矩阵的秩亏缺，它相对于矩阵的满秩是一种奇异现象。总之，无论是正方还是长方矩阵，零奇异值都刻画矩阵的奇性，而最小奇异值一定程度上代表着矩阵接近奇异的程度。

### 奇异值的性质

...

## 奇异值和其他矩阵概念的关系

### 和范数

...

### 和行列式

...

### 和条件数

...

### 和特征值

...

## 奇异值分解的应用

### 静态系统的建模

...

### 图像压缩

一幅图像的 $n \times n$ 个像素可以用 $n \times n$ 矩阵 $A$ 表示。假定 $A=U\Sigma V^T$，其中，奇异值按照从大到小的顺序排列。如果从中选择 $k$ 个大奇异值以及与这些奇异值对应的左和右奇异向量逼近原图像，便可以共使用k(2n+1)个数值代替原来的 $n\times  n$ 个图像数据。这 $k(2n+1)$ 个被选择的新数据是矩阵 $A$ 的前 $k$ 个奇异值、$n \times n$ 左奇异向量矩阵 $U$ 的前 $k$ 列和 $n \times n$ 右奇异向量矩阵 $V$ 的前 $k$ 列的元素。

在接收端，接收到奇异值 $\sigma_1,\sigma_2,\cdots,\sigma_k$，和对应的左奇异向量和右奇异值向量后，可以通过截尾的奇异值分解公式：
$$
\widehat{A} = \sum^k_{i = 1}\sigma_i u_iv_i^T
$$
近似重构出原图像。因此，我们在图像存储与传输的过程中，就无需使用 $n\times n$ 个原始数据，而只需要储与传输 $k(2n + 1)$ 个有关奇异值和奇异向量的数据即可。显然，$k$ 越小，则压缩效率越高。

我们称 $\rho = \frac{n^2}{k(2n+1)}$ 为图像的压缩比。

若 $k$ 值偏小，即压缩比 $\rho$ 偏大，则重构的图像的质量有可能不能令人满意。反之，过大的 $k$ 值又会导致压缩比过小，降低图像压缩和传送的效率。因此，需要根据不同种类的图像，选择合适的压缩比，以兼顾图像传送效率和重构质量。
