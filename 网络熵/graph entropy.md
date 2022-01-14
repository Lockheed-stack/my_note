# 网络熵



### 一、新网络熵：图的支配熵

**Information Processing Letters**

**[1]Şahin Bünyamin. New network entropy: The domination entropy of graphs[J]. Information Processing Letters,2022,174:**

### 1.起源

> 熵entropy：香农在1948年提出的概念。
>
> 图熵graph entropy：Rashevsky在1955年提出的概念。用于衡量顶点相对于顶点度的等效类的划分。



> **介绍一下用熵来衡量某些拓扑结构的优势**
>
> **以前：**化学、物理、生物的分子拓扑结构，通过一个拓扑指数（topological indices）来展示不同分子的差异。以下是一些拓扑指数：
>
> 1. Wiener index：维纳指数等于图中每对顶点之间总距离的二分之一。
> 2. Hosoya index：Hosoya 指数等于匹配总数。
> 3. Merrifield-Simmons index：Merrifield-Simmons 指数等于独立集的总数 。
>
> 存在的问题：它们通常与分子的相对分子特性相关，但相同的指标不能对不同的分子有很高的区分能力。
>
> 
>
> **后来：**运用信息论中的熵，提出了信息指数（information indices）。结果表明，信息指数比各自的拓扑指数对分子有更大的区分能力。
>
> 
>
> **再后来：**Dehmer 介绍了一些新的图顶点<u>信息泛函</u>（information functionals，更准确地说，信息泛函基于导出的概率分布量化图的结构信息）。
>
> 然后就出现了很多图熵度量（graph entropy measure），基于图的一些不变的属性，如顶点数、边数、顶点的度序列、顶点的<u>度幂</u>（degree powers），还有基于匹配和独立集的。



### 2.关于本文

> 支配（domination）也是图的一个重要的属性。
>
> Haynes等人证明，图的这些不变的属性，在树中，对图的微小变化是十分敏感的。
>
> 基于以上种种原因，作者定义了一个基于支配集的图熵的度量。
>
> 要得到熵，作者使用了图的支配多项式（domination polynomials）。
>
> 除了一些众所周知的支配多项式之外，我们还定义了细分星图的支配多项式。 此外，我们将支配熵与基于匹配、独立集、顶点度和给出的 21 个图的自同构组的图熵度量进行了比较。 这 21 个五阶图根据其拓扑复杂度进行排序。



### 3.名词、概念



cardinality：[n] 基数；集合的势

subdivide: [vi]细分；[vt]把...细分





##### star graph

> n阶星图$S_n$，或者称为“n-star”，是一个n个节点的**树**，其中一个节点的度为n-1，剩下的n-1个节点的度为1。因此星形图 $S_n$ 与完全二部图 $K_{1,n-1}$ 同构。
>
> ![img](https://mathworld.wolfram.com/images/eps-gif/StarGraphs_1001.gif)

##### double star graph

>双星图，是由两个星图联合以及连接他们中心的线组成的图形。
>
>
>
>n阶双星图$S_{p,q}$，由$S_{1,p} \ and \ S_{1,q}$组成，$n=p+q+2$。

##### subdivided star graph

>细分的星图$S^*_k$，由星图$S_{k+1}$得来，通过在k个顶点的星图中度为1的顶点上再添加一个点，因此$S_k^*$的阶数等于2k+1。



##### friendship graph

> 友谊图$F_k$，由循环图 $C_3$ 的 k 个副本组成，因此它们都共享一个公共顶点。友谊图$F_k$的阶等于2k+1。



##### 度序列degree sequence

> 假设 $V(G) = \{v_1, .  .  .  , v_n\}$ 和 $deg(v_k ) = d_k$, $k = 1,\dots,n$。 序列 $D(G) = (d_1, d_2, . . , d_n)$ 称为 G 的度序列。



##### 总支配集total dominating set

> 对于图 G 和顶点集 V(G) 的子集 $S^t$，用 $N_G^t[S^t]$ 表示 G 中与 $S^t$ 中的顶点相邻的顶点集（G中的所有点都至少与$S^t$中的一个点相邻）。如果 $N_G^t[S^t]=V(G)$，则称 $S^t$ 是一个总支配集（G 中的顶点）。因为总支配集的成员必须与另一个顶点相邻，所以没有为具有孤立顶点的图定义总支配集。
>
> 总支配集与普通支配集的区别在于，在全支配集 $S^t$ 中，要求 $S^t$ 的成员自身与 $S^t$ 中的一个顶点相邻，而在普通支配集 S 中，  S 的成员可以在 S 本身或与 S 中的顶点相邻。
> ![img](https://mathworld.wolfram.com/images/eps-gif/TotalDominatingSet_1000.gif)



##### 总支配数total domination number，$\gamma_t(G)$

> 用于表示图 G 的总支配数（the total domination number of a graph G），这是最小总支配集的基数（which is the cardinality of a total dominating set with minimum order）。
>
> 例如，在上图所示的彼得森图中，$\gamma(P)=3$，因为集合 $S=\{1,2,9\}$ 是最小支配集（左图），而 $\gamma_t(P)=4$ 因为 $S^t=  \{4,8,9,10\}$ 是最小总支配集（右图）。



##### 支配多项式domination polynomial，$D(G,x)$

> $D(G, i)$ 表示基数为 i 的 G 的支配集族（也是一个集合），$d_i$ 表示 $D(G, i)$ 的基数，使得 $d_i(G) =|D(G, i)|$。
> $$
> D(G,x) = \sum ^{V(G)}_{i=\gamma(G)} d_i(G)x^i
> $$
>
> 例子：
>
> 考虑路径图 $P4:v_1v_2v_3v_4$。 为了支配图$P_4$，取能够支配其他两个顶点的两个顶点就足够了。 因此$\gamma(P_4) =2$。  $P_4$ 的总支配集是 $\{v2, v3\}$ 并且 $γ_t(P_4) =2$。 基数为 2 的 $P_4$ 的支配集是 $D(G, 2) =\{ \{v1, v3\}, \{v1, v4\}, \{v2, v3\}, \{v2, v4\} \}$且$d_2(G) =4$  . 此外，基数为3的$P_4$的支配集为$D(G, 3) = \{\{v1, v2, v3\}, \{v1, v2, v4\}, \{v1, v3, v4\}, \{v2, v3, v4  \}\}$，$d_3(G) =4$。 最后，基数为 4 的 $P_4$ 的支配集是 $D(G, 4) =\{v1, v2, v3, v4\} $和 $d_4(G) =1$。
>
> **因此，$P_4$的支配多项式为$D(G,P_4)=x^4+4x^3+4x^2$。**
>
> 通过这个多项式，可得知$P_4$的总支配集个数是9（4+4+1）。
>
> 
>
> > 由支配多项式，又可推出一个公式：
> > $$
> > \gamma_s(G) = \sum ^{|V(G|}_{i=\gamma(G)}d_i(G)
> > $$
> > $γ_s$ 来表示支配集的总数（We use the notation $γ_s$ to denote the total number of dominating sets.）。**注意，不要和总支配数 $\gamma_t$ 混淆。**很明显，$γ_s$ 等于图 G 的支配多项式的**系数之和**。
>
> 



##### 图熵

> 设 G 是一个图，$f:S\rightarrow R_+$ 是定义在 $S=\{s_1, s_2, ..., s_k\}$ 上的信息泛函，使得 S 是 G 的一组元素。定义如下(log以2为底)：
> $$
> \begin{align*}
> I_f(G) &= -\sum ^k_{i=1} \frac {f(s_i)} {\sum^k_{j=1}f(s_j)} \log(\frac {f(s_i)} {\sum^k_{j=1}f(s_j)}) \\
> &=\log (\sum^k_{i=1}{f(s_i)})-\frac {\sum ^k_{i=1}f(s_i)\log f(s_i)} {\sum^k_{j=1}f(s_j)}
>    \end{align*}
> $$
> 



##### 支配熵

> 对图 G ，$|V| =n$ 且没有孤立的顶点，我们引入信息泛函使得 $f := d_i(G)$，其中$d_i(G)=|D(G,i)|$。
>
> ![image-20211123155608263](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211123155608263.png)
>
> 
>
> 



##### 基于匹配的熵度量(Hosoya index, or Z-index)

>具有 k 条边的匹配数用 $z_k(G)$ 表示。 假设空集是匹配的，并且 $z_0(G) =1$。
>
>图 G 的 Hosoya 指数（或 Z 指数）计算为 $Z(G)=\sum^m_{k=0} Z_k(G)$。
>
>![image-20211123163634021](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211123163634021.png)



##### 基于独立集的熵度量（Merrifield-Simmons index ，or σ-index)

>$\sigma_k(G)$ 表示基数为 k 的独立集合的数量。空集可以认为是一个独立的集，$\sigma_0(G) =1$。
>
>图 G 的 Merrifield-Simmons 指数（或 σ-index）计算为 $\sigma(G)=\sum^n_{k=0}\sigma_k(G)$。
>
>![image-20211123164504706](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211123164504706.png)



##### 基于度幂(degree power)的熵度量

*相关文章：Extremality of degree-based graph entropies*

> 这个度幂degree power，就是字面意思，度的n次方。
>
> ![image-20211123170640782](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211123170640782.png)
>
> 当k=1时，可得到 first-degree entropy。
>
> ![image-20211123170752093](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211123170752093.png)



##### 拓扑信息内容（topological information content）

> ![image-20211123171117903](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211123171117903.png)
>
> *什么是 orbit of G ??*
>
> 答：The equivalence classes of the vertices of a graph G under the action of the automorphisms are called vertex orbits. The equivalence classes of the edges are called edge orbits.
>
> 图 G 的顶点在自同构作用下的等价类称为顶点轨道。 边的等价类称为边轨道。
>
> ![image-20211201205727270](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211201205727270.png)



### 4.一些图的支配熵

> 假设$H_1$和$H_2$是两个连通图，$H=H_1∪H_2$分别是$H_1$和$H_2$的不相交并集。 我们得到:
> $$
> \begin{align*}
> I_{dom} = \log (\sum^n_{i=\gamma(H)}{d_i(H)})-\frac 1 {\sum ^n_{i=\gamma(H)}d_i(H)}\sum^n_{i=1}d_i(H)\log(d_i(H))
> \end{align*}
> $$
> 使得$γ(H)=γ(H_1)+γ(H_2)$和$d_i(H) =\sum^i_{j=γ(H_1)}d_j(H_1)d_{i−j}(H_2)$.  *怎么得来的？*



> 完全图$K_n$，可得：
> $$
> I_{dom}(K_n)=\log(2^n-1)-\frac 1 {2^n-1}\sum^n_{i=1}C^i_n \log(C_n^i)
> $$
>
> 证明：支配多项式$D(G,x)=(1+x)^n-1$，通过二项式展开定理，可得$\gamma_s(G)=2^n-1$，$d_i(G)=C_n^i,1\le i \le n$。**（为什么要减1？答：因为二项式展开的第一项为$C_n^0 1^n \times x^0 =1$，而$d_0(G)=0$，因此这项对于该图来说并不存在，所以要减1）**



> 星图$S_n$，可得：
> $$
> I_{dom}(S_n)=\log(2^{n-1}+1)-\frac 1 {2^{n-1}+1}(\sum^{n-3}_{i=1}C^i_{n-1}\log(C^i_{n-1}))-\frac {n\log n} {2^{n-1}+1}
> $$
> 推导：
>
> 先推导$S_n$的支配多项式（找规律）：
>
> 1. n=1：$d_1(G)=1$
> 2. n=2：$d_1(G)=2,d_2(G)=1$
> 3. n=3：$d_1(G)=1,d_2(G)=3,d_3(G)=1$
> 4. n=4：$d_1(G)=1,d_2(G)=3,d_3(G)=4,d_4(G)=1$
> 5. n=5：$d_1(G)=1,d_2(G)=4,d_3(G)=6,d_4(G)=5,d_5(G)=1$
> 6. ....
>
> 借助杨辉三角，可得以下规律：
>
> <img src="https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211126203351186.png" alt="image-20211126203351186" style="zoom: 50%;" />
>
> 支配多项式的系数为n-1行，所以写成$(1+x)^{n-1}$；
>
> 但这样所有x的幂都少了1，所以再乘一个x，得$x(1+x)^{n-1}$；
>
> 而第n-1个的系数需要加1，因此加一个$x^{n-1}$，得$D(S_n,x)=x^{n-1}+x(1+x)^{n-1}$。
>
> 那么也就易得$\gamma_s(S_n)=\sum^n_{i=\gamma(S_n)=1}d_i(G)=2^{n-1}+1$。
>
> 带入之前的公式，即可得出。



> 双星图$S_{a,b}$，可得：
> $$
> \begin{align*}
> 	I_{dom}(S_{a,b}) =& \log(\gamma_s(S_{a,b}))-\frac 1 {\gamma_s(S_{a,b})}(\sum^{a+b-3}_{i=2}d_i(G)\log(d_i(G))) \\
> 	& -\frac {(C_{a+b-2}^2+a+b-1)\log(C_{a+b-2}^2+a+b-1)+(a+b)\log(a+b)} {\gamma_s(S_{a,b})}
> 	
> \end{align*}
> $$
> 



> 梳子图$E_k$，有n=2k个顶点，可得：
> $$
> I_{dom}(E_k)=\log(3^k)-\frac 1 {3^k} (\sum^{2k}_{i=k} C^k_{i-k}2^{2k-i}\log(C^k_{i-k}2^{2k-i}))
> $$
> ![image-20211122172406930](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211122172406930.png)



> 友谊图$F_k$，有n=2k+1个顶点，可得：
> $$
> \begin{align*}
> 	I_{dom}(F_k) = & \log(3^k+2^{2k}) \\
> 	& -\frac 1 {3^k+2^{2k}}(\sum^{2k}_{i=0}(C_{2k}^{i-1}+C_k^{i-k}2^{2k-i})\log(C_{2k}^{i-1}+C_k^{i-k}2^{2k-i}))
> \end{align*}
> $$
> ![image-20211122172856440](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211122172856440.png)



> 细分的星图$S_k^*$，有n=2k+1个顶点，可得：
> $$
> \begin{align*}
> 	I_{dom}(S_k^*)&=  \log(2\times 3^k-1)\\
> 				  & -\frac 1 {2 \times 3^k-1}((2^k-1)\log(2^k-1)+\sum^k_{i=0}(C^i_k 2^{k-i}+C_k^{i+1}2^{k-i-1})\log(C^i_k 2^{k-i}+C_k^{i+1}2^{k-i-1}))
> \end{align*}
> $$
> <img src="https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211122194947317.png" alt="image-20211122194947317" style="zoom:67%;" />
>
> 推导：*该图的支配多项式是由作者推导出的，其他图的支配多项式别人已经推导出了*
>
> $\because$ 要支配$S_k^*$，那么每个臂（arm）都至少要有一个点在支配集中。
>
> $\therefore \ \gamma(S_k^*)=k$ ，并有以下两种情形：
>
> 1. 在每个臂上，有1个基数为2的集合(取臂上的2个点) ， 2个基数为1的集合(臂上的2个点2选1)，中心点可选可不选，则可得到$(x^2+2x)^k(x+1)=x^k(x+2)^k(x+1)$。
> 2. 满足1的情况下，只有一种情况不是支配集：就是全部由度为1的点组成的集合。因此要把这种情况去除。因而可得$x^k(x+2)^k(x+1)-x^k$。
>
> $\therefore D(S_k^*,x)=\sum^{n=2k+1}_{i=k}d_i(G)x^i=x^k(x+2)^k(x+1)-x^k$。
>
> 



### 5.支配熵与其他熵度量的比较

<img src="https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211123193719860.png" alt="image-20211123193719860" style="zoom: 67%;" />

<img src="https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211123193754648.png" alt="image-20211123193754648" style="zoom: 67%;" />

> 第一个重要结果是图3的$I_{nis}$等于图3的$I_{dom}$。图3是星形图$S_5$。
>
> ![image-20211123210729810](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211123210729810.png)
>
> 感觉作者是不是写错了？应该是蓝线部分相等，才有$I_{nis}=I_{dom}$。

>如表1所示，$I_α$的度量顺序为1.522七次、1.922五次、0.971三次、0.722三次、0两次和1.371一次。 图4和图21是正则图，*它们的自同构群根据它们的对称结构由一个轨道组成(their automorphism groups consist of one orbit based on their symmetry structure，不太懂什么意思)*。 图 21 在 21 图中具有最大的拓扑复杂度度量。 但是，它的 $I_α$ 值为零。

>从表1可以看出，由于图4和图21是正则图，对于n个顶点，它们的first-degree熵等于logn。 
>
>可以看出这些图的拓扑复杂度存在显着差异，可这些图的first-degree熵和拓扑复杂度值之间没有显着相关性。 而且，表中$P_5$的复杂度最小，完全图$K_5$的拓扑复杂度最大。*所以研究一下，用first-degree熵度量$P_n$和$K_n$，看看隐藏着什么秘密or问题。*
>
>`初步观察:`
>
>![image-20211124214505697](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211124214505697.png)
>
>有点规律，但好像又说明不了什么。
>
>`再看看支配熵的表现：`
>
><img src="https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211124215157534.png" alt="image-20211124215157534" style="zoom:80%;" />
>
>$K_n$和$P_n$的$I_{dom}$差异比较明显，对比3~6阶相同图的$I_{fd}$差异。差异是相对明显了，但没有规律。作者也没有继续进行说明。





### 6.结论

1. 我们得到了完全图、星图、双星图、梳状图、友谊图和细分星图的支配熵；
2. 我们定义了细分星图的支配多项式。
3. 我们对21个图表的五个熵度量进行了一些观察。 
4. 我们发现星星的 $I_{dom}$ 和 $I_{nis}$ 是相等的。







----------------------------------

### 二、图的冯诺依曼熵

**Discrete Applied Mathematics**

**[2]Giorgia Minello,Luca Rossi 0004,Andrea Torsello. On the von Neumann entropy of graphs.[J]. J. Complex Networks,2019,7(4):**



#### 1.简介

非空图的冯诺依曼熵提供了一种表征物理系统**量子态信息内容的方法**。

本文利用图参数，给出了非空图的冯诺依曼熵的上下界，并且在到达上下界时，表征出图的性质。

#### 2.名词、概念

##### 厄密特矩阵hermitian matrix

> **共轭conjugate：**复数中的概念。任意复数可表达为$x+iy$，前半部分为实部，后半部分为虚部，$x,y$皆为实数。
>
> 共轭复数，即实数部分相同，虚数部分互为相反数的两个复数。

> **矩阵的共轭转置（conjugate transpose）：**把矩阵转置后，再把每一个数换成它的共轭复数。**记为$A^H$。**

> **厄密特矩阵hermitian matrix：**记矩阵$A=(a_{ij})$，如果$A=A^H$，则矩阵A为hermitian矩阵。
>
> 例子：
> $$
> \begin{array}{**lr**}
> A=\left(
> \begin{matrix}
> 	1&2+i\\
> 	2-i&1
> \end{matrix}
> \right)\\
> 
> A^T=\begin{pmatrix}
> 	1&2-i\\
> 	2+i&1
> \end{pmatrix}\\
> 
> A^H=\begin{pmatrix}
> 	1&2+i\\
> 	2-i&1
> \end{pmatrix}=A
> \end{array}
> $$
> **一些性质：**
>
> 1. 主对角线上的元素都是实数。
> 2. 特征值也是实数。
> 3. 实对称矩阵是厄密特矩阵的特例。

##### 半正定厄密特矩阵positive semi-definite hermitian matrix

>**正定矩阵positive definite matrix：**一个$n\times n$的复数矩阵（complex matrix）$A$，对于所有非零复数向量$x\in C^n$，$x^*$为$x$的共轭转置向量，如果有 $R[x^*Ax]>0$ ，则$A$为正定矩阵。
>
>当A为实数矩阵时，则为$x^TAx>0$。

> **半正定矩阵positive semi-definite matrix：**是正定矩阵的推广。
>
> 设A是n阶方阵，如果对任何非零向量X，都有$x^TAx≥0$​，就称A为半正定矩阵。
>
> [知乎中的一篇关于正定矩阵、半正定矩阵的文章](https://zhuanlan.zhihu.com/p/44860862)

> **半正定厄密特矩阵：**就是厄密特矩阵+半正定。

##### 密度矩阵density matrix

> 在量子力学中，物理系统的状态由一个具有单位迹的半正定厄密矩阵表示，称为密度矩阵。
>
> <img src="https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211207105534572.png" alt="image-20211207105534572" style="zoom:67%;" />
>
> *注：Normalization 归一化。*相关参考文章：[知乎](https://zhuanlan.zhihu.com/p/39448632)；[芝加哥大学](http://home.uchicago.edu/~tokmakoff/TDQMS/Notes/9._Density_Matrix_3-19-09.pdf)


##### 拉普拉斯矩阵Laplacian Matrix

> 在简单图G中，拉普拉斯矩阵$L(G)=D(G)-A(G)$，其中$D(G)=diag(d_1,d_2,...,d_n)$为G的度对角矩阵，$A(G)$为图G的邻接矩阵。
>
> 显然，拉普拉斯矩阵的对角线元素为顶点的度$d_G(v)$。

##### 量子态的冯诺依曼熵  
> 量子态的冯诺依曼熵被定义为与其密度矩阵的**特征值**相关的香农熵。

##### 简单图G的冯诺依曼熵S(G)

> $$
> S(G)=-\sum^n_{i=1} \rho_i\log_2\rho_i
> $$
>
> 对于非空图G，令$\sigma(G)=\frac 1 {d_G}L(G)$，$d_G$为$L(G)$的迹，即图G的度数之和。
>
> $\sigma(G)$是具有单位迹的半正定厄密特矩阵。
>
> 令$\rho_1,\rho_2,...,\rho_n$为$\sigma(G)$的特征值，以非递增的顺序排列*（直接说递减不就行了）*。那么 <u>$ρ_n = 0$</u> 并且 $σ(G)$ 的<u>特征值 0 的重数</u>等于<u>图G 的分量数</u>。
>
> `Question:`为什么$ρ_n = 0$？我试了一下 $P_3$ 的图，确实有一个特征值为0，但一般情况怎么推导证明？
>
> ` Answer:`
>
> 1. 相关文章**M. Fiedler, Algebraic connectivity of graphs, Czechoslovak Math. J. 23 (1973) 298–305.**  
>
> 2. 在这篇文章中提到的：“Any <u>square matrix M with all zero row sums has an eiegnvalue 0 and corresponding eiegnvector is e</u> ($e=(1,1,..,1)^T$)。拉普拉斯矩阵具有这种特点，显然有这结论。
>
> 3. 至于证明，很简单，文章中都懒得证明。这结论的出处肯定不是这篇文章，只是我恰好看到罢了。我自己证明：
>    $$
>    \begin{align}
>    &设矩阵A，A的每行元素之和为a，需证明存在非零向量\alpha，使得A\alpha=\lambda\alpha \\
>    &证:取\alpha=\begin{pmatrix}
>    		1\\1\\1\\ \vdots \\1
>    		\end{pmatrix}
>                         
>    ,可得A\alpha=\begin{pmatrix}
>    			A第一行和\\
>    			A第二行和\\
>    			\vdots
>    			\end{pmatrix}
>    \\
>    &因为A行和相同，等于a，所以A\alpha=\begin{pmatrix}
>    									a\\a\\ \vdots \\ a
>    								\end{pmatrix}
>    								=a\cdot \begin{pmatrix}
>    								1\\1\\ \vdots \\1
>                                    \end{pmatrix}\\
>    &所以A的一个特征值a。
>    \end{align}
>    $$
>    
>
> 
>
> 令$\lambda_1,\lambda_2,...,\lambda_n$为图G的拉普拉斯特征值($L(G)$的特征值)，<u>则$\lambda_{n-1}$为图的代数连通性</u>（*同样在上述的相关文章中提到的，叫做* **Courant's theorem**）。基于上述的定义，显然有$\lambda_i=2m\rho_i$。(*和 $\sigma(G)=\frac 1 {d_G}L(G)$ 有关。也是特征值的性质*。 $m=|E(G)|$，2m就是度数之和)。并有以下关系：
> $$
> \sum^{n-1}_{i=1}\rho_i=tr(\sigma(G))=1
> $$
>
> 
>
>
> 最后为了方便，令$0\log_2 0=0$，得：
> $$
> S(G)=-\sum^{n-1}_{i=1} \rho_i \log_2 \rho_i
> $$
> **一些性质：**
>
> 1. Braunstein等人证明，n个顶点的非空图G，有$0\le S(G) \le \log_2{(n-1)}$。左等式当且仅当 G 有一条边，右等式当且仅当 G 是（同构于）完整图 $K_n$。
> 2. n个顶点，$m\ge1$条边的图，令$Z=Z(G)=\sum_{u\in V(G)}d_u^2$。记$S_n$为n个顶点的星图，Dairyko等人证明，$S(G)\ge-\log_2{\frac {2m+Z} {4m^2}}$。
>
> 
>
> **一些助于理解的文章：**
>
> 1. [矩阵的特征：特征值，特征向量，行列式，trace](https://zhuanlan.zhihu.com/p/25955676)
> 2. [理解矩阵](https://blog.csdn.net/myan/article/details/647511)
> 3. **Recommend:**[线性代数的本质 - 01 - 向量究竟是什么？](https://www.bilibili.com/video/av5987715?from=search&seid=16213828939248415146)



#### 3.一些定理、结论

>





--------------------------------------------------------



### 三、计算正则超图中的独立集

**Journal of Combinatorial Theory, Series A**

**[3]Balogh József,Bollobás Béla,Narayanan Bhargav. Counting independent sets in regular hypergraphs[J]. Journal of Combinatorial Theory, Series A,2021,180:**



#### 1、为什么这篇文章记录在这份笔记中

> 1. 老师给的，说有个巧妙的计算独立集的方法。
> 2. 里面有提到用一个**Kahn的熵** *（An Entropy Approach to the Hard-Core Model on Bipartite Graphs）*方法去验证超图中的一个问题，相当于熵在图中的一个应用了。

#### 2、名词、概念

##### 超图hypergraph

>关于超图的一些基本概念已经记载在“[图论入门](https://gitee.com/Lockheed_LEE/my_note.git)”笔记当中，这里只简单回顾一下：
>
>- k-一致超图 k-uniform hypergraph：每条超边都正好包含 k 个顶点的超图；
>- d-正则超图 d-regular hypergraph：每个顶点的度数都是 𝑑 的超图；
>- <u>顶点集的大小</u>被称为**超图的阶数 order of the hypergraph**。
>- <u>边集的大小</u>被称为**超图的大小 size of the hypergraph**。



##### r-graph

> 本文r-uniform hypergraph的简称。

##### $\mathcal{H^r_d}$

> 在本文表示d-regular r-partite r-graph，d正则、r部分、r一致的超图，**有rd个顶点，$d^2$条边**。

##### the link $\mathcal{L}(v)$

> 在r-graph $\mathcal{G}$中，顶点 v 的链接 $\mathcal{L}(v)$， 是 (r−1)-graph中边的集合 S， 使得 S∪{v} 是 $\mathcal{G}$ 的边。
>
> :question:  "并且其顶点集正是这些边的跨度 "，and whose vertex set is precisely the span of these edges，不太清楚什么意思。
>
> :a:[Mathworld网站](https://mathworld.wolfram.com/GraphEdge.html)中对于“link”的解释：The terms "arc," "branch," "line," "link," and "1-simplex" are sometimes used instead of edge. 所以我感觉就是代表超图的边的意思。

##### Quasi-bipartite hypergraph(拟二部超图、准二部超图)  

> **Quasi-bipartite graph：** *（从Wikipedia上摘抄下来的）*  在图论的数学领域中，如果G中的非末端顶点形成一个独立的集合，即如果每条边都与至少一个末端相关联，则Steiner树问题的一个实例（由无向图G和必须相互连接的末端顶点集合R组成）被称为准二部。这推广了二部图的概念：如果G是二部图，并且R是二部图一侧的顶点集，那么R的集是自动独立的。
>
> > :question: non-terminal vertices非终端顶点是什么？
> > :a:先说 terminal vertex ，它是在有根。树中没有后继的顶点，也被称为叶子节点。那么non-terminal vertices 就是非叶子节点。
>
> **quasi-bipartite hypergraph：**我们说一个 r-graph $\mathcal{G}$ 是quasi-bipartite ，如果它的点可以按以下方式分成A、B两个部分：
>
> 1. G的每条边与A恰好在1个顶点相交。(every edge of G intersects A in exactly one vertex)
> 2. 对于每个$a\in A$，a的连接$\mathcal{L}(a)$是一个匹配。(for each a ∈A, the link L(a) of a is a matching)

#### 3、本文核心

**A brief word about notation: a subset of the vertex set of an r-graph is independent if it induces no edge**

> 对于$r\ge2,d\in \mathbb{N}$，将$\mathcal{H}_d^r$的$d^2$条边进行以下操作：
>
> 1. 标记一个顶点集的子集*(当中的点)*，该子集的阶数为d。
> 2. 剩余的$(r-1)d$个点，划分为d个集合，每个集合$(r-1)$个点。
> 3. 因此可以得到一个(r-1)-uniform matching。
> 4. 最后，将**标记的顶点**和**匹配边**组成的 r-set（r个顶点的集合），放入$\mathcal{H}^r_d$的边集中。
>
> **例子：**
>
> $\mathcal{H}^2_d$：表示完全二部图$K_{d,d}$。
>
> $\mathcal{H}^3_d$：表示图中3d个顶点上的一组三角形，其中d个顶点分别连接到覆盖其他2d个顶点的匹配的所有边的两端。*(英文原文和翻译都看的不是很懂，自己摸索画了一下)*
>
> **具体示例：**
>
> > #### $\mathcal{H}^3_1$：
> >
> > ![image-20211214200230792](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211214200230792.png)
> >
> > 总共3*1=3个点，$1^2$条超边。
> >
> > 顶点集$X=\{v_1,v_2,v_3\}$。
> >
> > 超边集$E=\{e_1\}=\{v_1,v_2,v_3\}$。$e_1$就是图中连接顶点的黑线，忘了标出来。
>
> >#### $\mathcal{H}_2^3$：图分成3个部分，每个部分2个顶点
> >
> >按照上述的说法来画一下
> >
> >step1：
> >
> ><img src="https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211215164415559.png" alt="image-20211215164415559" style="zoom: 67%;" />
> >
> >step2:其中d个点，也就是2个点，取$v_1,v_2$，分别连接到其他2d个点。
> >
> ><img src="https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211215164639373.png" alt="image-20211215164639373" style="zoom:67%;" />
> >
> >step3:按照step2的方式，画完整个图。
> >
> ><img src="https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211215165209830.png" alt="image-20211215165209830" style="zoom:67%;" />
> >
> >总共3*2=6个点，$2^2=4$条超边。
> >
> >蓝、红、棕、绿线分别为$e_1,e_2,e_3,e_4$。
> >
> >顶点集$X=\{v_1,v_2,..,v_6\}$。
> >
> >超边集$E=\{e_1,e_2,e_3,e_4\}=\{\{v_1,v_3,v_4\},\{v_1,v_5,v_6\},\{v_2,v_3,v_4\},\{v_2,v_5,v_6\}\}$。
> >
> >
> >
> >最后将$\mathcal{H}^2_3$和$\mathcal{H}^3_2$对比一下，就清楚多了：
> >
> >![image-20211215170319102](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211215170319102.png)
>
> 
>
> 
>
>
> $ind(\mathcal{G})$: 表示$r-graph \ \mathcal{G}$中独立集的数量。计算公式如下：
> $$
> ind(\mathcal{H}^r_d) = 2^{(r-1)d}+(2^d-1)(2^{r-1}-1)^d
> $$
> **定理：**如果$\mathcal{G}$是d正则、准二部、r一致的n个顶点的图，则
> $$
> ind(\mathcal{G})\le ind(\mathcal{H}^r_d)^{n/rd}
> $$
> **Proof：**
>
> 将G的顶点分为A，B，$A\cup B$表示G的全部顶点。
>
> 令X为随机选中的独立集的特征向量。
>
> 对于顶点集合S，令$X_S$为X的子向量（subvector），该子向量由S中的顶点索引，将$X_{\{v\}}$缩写为$X_v$。*(子向量是什么？搜了一下好像没标准的定义。)*
>
> 则$X=(X_A,X_B)$。令$H(X)$为X的熵，记为：$\log (ind(\mathcal{G}))=H(X)=H(X_B)+H(X_A|X_B)$。
>
> 还可得到$\{V(\mathcal{L}(a)):a\in V\}$是B的d-covering。
>
> 因此，通过Shearer's lemma，可得：
> $$
> H(X_B)\le \frac 1 d \sum_{a\in A}H(X_{V(\mathcal{L}(a))})
> $$
>
>
> 所以$H(X_A|X_B)\le \sum_{a\in A}H(X_a|X_B)=\sum_{a\in A}H(X_a|X_{V(\mathcal{L}(a))})$。
>
> 最后将这些结果合起来，得：
> $$
> H(X)\le \frac 1 d (\sum_{a\in A}H(X_{V(\mathcal{L}(a))})+d \cdot H(X_a|X_{V(\mathcal{L}(a))}))
> $$
>
> 
>
>
> 此时，固定任意一个a($a\in A$)，取集合$I$为G的独立集，$I\subset V(\mathcal{L}(a))$。用$p(I)$表示$X_{V(\mathcal{L}(a))}=I$的概率，和 λ(I) 表示 a 可以添加到 $I$（1 或 2）同时保持 G 中的独立性的方式数。可得：
> $$
> H(X_{V(\mathcal{L}(a))})+d \cdot H(X_a|X_{V(\mathcal{L}(a))})=
> \sum_Ip(I)
> \left(\log (\frac 1 {p(I)})+d \cdot H(X_a|\{X_{V(\mathcal{L}(a))}=I\})
> \right)
> $$
> 又因为$H(X_a|X_{V({\mathcal{L}(a)})}=I)\le \log (\lambda(I))$，可得：
> $$
> \sum_I p(I)
> \left(
> \log \frac 1 {p(I)} +d \cdot \log(\lambda(I))
> \right)
> =\sum_I p(I) \log (\frac {\lambda(I)^d} {p(I)})\le \log (\sum_I {\lambda(I)^d})
> $$
> 注意， $I$ 的范围是在 G 中独立的 $V(\mathcal{L}(a))$ 的子集，可得：
> $$
> \sum_I\lambda(I)^d \le 2^{|V(\mathcal{L}(a))|} +(2^d-1)ind(\mathcal{L}(a))\le 2^{(r-1)d} + (2^d-1)(2^{r-1}-1)^d=ind(\mathcal{H}^r_d)
> $$
> 对于上面的第一个不等式，$V(\mathcal{L}(a))$ 的每个子集对左边的和最多贡献 1，除非它碰巧在 $\mathcal{L}(a)$ 中是独立的，在这种情况下，它贡献了额外的 $2^d−1$。
>
> 要了解为什么上面的第二个不等式成立，首先我们简单地有 $|V(\mathcal{L}(a))| \le (r−1)d$。然后，我们可以使用[熵的次可加性(subadditivity)](https://en.wikipedia.org/wiki/Strong_subadditivity_of_quantum_entropy)再次绑定 $ind(\mathcal{L}(a))$（Shearer's lamma 的平凡情况）：
>
> 用$S_1,S_2,...,S_d$表示 (r-1)-graph $\mathcal{L}(a)$的d条边，从$\mathcal{L}(a)$中随机选择一个独立集的特征向量Y，可得出结论$H(Y)\le \sum^d_{i=1}H(Y_{S_i})$，并且观察到对于每个$1\le i \le d$，$H(Y_{S_i})\le \log(x^{r-1}-1)$产生所需的界限。
>
> 最后，将这些估计放在一起，并使用 $|A|=n/r$ 的事实，因为 G 是 d 正则的，让我们得出结论：
> $$
> H(X)\le \frac n {rd}\log (ind(\mathcal{H}^r_d))
> $$
> 

