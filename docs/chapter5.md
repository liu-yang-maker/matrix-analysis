# 子空间方法

[>>前往教程目录](guide-matrix.md)

[TOC]

## 子空间一般理论

线性空间定义：设 $V$ 是一个非空集合，其元素用向量 $x,y,z$ 等表示；$K$ 是一个数域



## 列空间、行空间与零空间

### **基本子空间**

对于矩阵 $A \in C^{m \times n}$，其 m 个行向量和 n 个列向量分别记做
$$
\begin{aligned} \boldsymbol{r}_{1} &=\left[a_{11}, a_{12}, \cdots, a_{1 n}\right] \\ \boldsymbol{r}_{2} &=\left[a_{21}, a_{22}, \cdots, a_{2 n}\right] \\ & \vdots \\ \boldsymbol{r}_{m} &=\left[a_{m 1}, a_{m 2}, \cdots, a_{m n}\right] \end{aligned}
$$

$$
\boldsymbol{a}_{1}=\left[\begin{array}{c}a_{11} \\ a_{21} \\ \vdots \\ a_{m 1}\end{array}\right], \quad \boldsymbol{a}_{2}=\left[\begin{array}{c}a_{12} \\ a_{22} \\ \vdots \\ a_{m 2}\end{array}\right], \quad \cdots, \quad \boldsymbol{a}_{n}=\left[\begin{array}{c}a_{1 n} \\ a_{2 n} \\ \vdots \\ a_{m n}\end{array}\right]
$$

那么矩阵 $A = [a_1,a_2,\cdots,a_n] \in C^{m \times n}$ 的列空间定义为列向量的所有线性组合的集合：
$$
\begin{aligned} \operatorname{Col}(\boldsymbol{A}) &=\operatorname{Span}\left\{\boldsymbol{a}_{1}, \boldsymbol{a}_{2}, \cdots, \boldsymbol{a}_{n}\right\} \\ &=\left\{\boldsymbol{y} \in \mathbb{C}^{m}: \boldsymbol{y}=\sum_{j=1}^{n} \alpha_{j} \boldsymbol{a}_{j}: \alpha_{j} \in \mathbb{C}\right\} \end{aligned}
$$
同理，矩阵 A 的行空间定义为其复共轭行向量的所有线性组合的集合：
$$
\begin{aligned} \operatorname{Row}(\boldsymbol{A}) &=\operatorname{Span}\left\{\boldsymbol{r}_{1}^{*}, \boldsymbol{r}_{2}^{*}, \cdots, \boldsymbol{r}_{m}^{*}\right\} \\ &=\left\{\boldsymbol{y} \in \mathbb{C}^{n}: \boldsymbol{y}=\sum_{i=1}^{m} \beta_{i} \boldsymbol{r}_{i}^{*}: \beta_{i} \in \mathbb{C}\right\} \end{aligned}
$$
我们还需要给出下面几个定义：

- 矩阵 $A \in C^{m \times n}$ 的值域：

$$
\operatorname{Range}(\boldsymbol{A})=\left\{\boldsymbol{y} \in \mathbb{C}^{m}: \boldsymbol{A} \boldsymbol{x}=\boldsymbol{y}, \quad \boldsymbol{x} \in \mathbb{C}^{n}\right\}
$$

- 矩阵 $A \in C^{m \times n}$ 的零空间（也叫核）：

$$
\operatorname{Null}(\boldsymbol{A})=\operatorname{Ker}(\boldsymbol{A})=\left\{\boldsymbol{x} \in \mathbb{C}^{n}: \boldsymbol{A} \boldsymbol{x}=\mathbf{0}\right\}
$$

- 复矩阵 $A_{m \times n}$ 的的共轭转置 $A^H$ 的零空间定义为：

$$
\operatorname{Null}\left(\boldsymbol{A}^{\mathrm{H}}\right)=\operatorname{Ker}\left(\boldsymbol{A}^{\mathrm{H}}\right)=\left\{\boldsymbol{x} \in \mathbb{C}^{m}: \boldsymbol{A}^{\mathrm{H}} \boldsymbol{x}=\mathbf{0}\right\}
$$

- 零空间的维数称为 $A$ 的零化维度或零度：

$$
\operatorname{nullity}(\boldsymbol{A})=\operatorname{dim}[\operatorname{Null}(\boldsymbol{A})]
$$

我们称这四个为矩阵 $A$ 的四个基本子空间：列空间、行空间、零空间 $\operatorname{Null}(\boldsymbol{A})$ 和 $\operatorname{Null}(\boldsymbol{A}^{\mathrm{H}})$。

### 四个基本子空间之间的关系

### 子空间的基的构造







## 子空间方法

### 信号子空间与噪声子空间

假设观测信号的模型：
$$
\boldsymbol{x}(t)=\sum_{i=1}^{r} s_{i}(t) \boldsymbol{a}\left(\omega_{i}\right)+\boldsymbol{w}(t)=\boldsymbol{A} \boldsymbol{s}(t)+\boldsymbol{w}(t)
$$
其中：

- 随机信号向量
- 信号混合矩阵
- 对信号 $s_i$ 的响应向量
- 加性噪音向量

### MUSIC方法

### 求解方程 $X = AS$













