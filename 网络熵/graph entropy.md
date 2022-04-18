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
> \end{align*}
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



### 四、基于信息熵模块化的社交网络超图划分

**Journal of Network and Computer Applications**

**[4] Hypergraph partitioning for social networks based on information entropy modularity**



#### 1、名词、概念

scaling out：横向拓展。

dyadic：[adj] 二价的，双值的。[n] 双积

mitigate：【adj】减轻的；截止的；【n】减轻；镇静

coincide with：与...相符；不谋而合

bisection：【n】两断；对切；二等分的一半

##### scale-free network

> **无标度网络**。度分布满足**幂律分布**的网络即为无标度网络。互联网、社交网络等网络都具有无标度性或满足幂律分布。1999 年 10 月 15 日的Science 杂志，刊登了 Albert-László Barabási 和 Réka Albert 的文章，提出通过网络生长和偏好依附的模型，可以获得无标度网络，后被称为 B-A 模型。
>
> 无标度网络中大多数节点只与少数节点连接，而少量的节点拥有极其多的节点连接，这种少量节点称为枢纽或集散节点（hub）。**新加入的点更倾向于连接hub节点。**

##### power law distribution

> **幂律分布**。表现为一个变量是另一个变量的幂次方，即$f(x)=ax^{-k}$。
>
> ![img](https://wiki.swarma.org/images/thumb/8/8a/Long_tail.svg/500px-Long_tail.svg.png)
>
> 一个幂律图示例，展示了人气排名的规律。右侧是数量庞大但人气微弱的“长尾”，左侧则是少数“主宰”。 (又称80–20法则)。

##### dyadic graph

> 没找到官方翻译（二价图？并矢图？）。
>
> 定义：
>
> > A graph G is dyadic provided it has a representation v → $S_v$ from vertices v of G to subtrees $S_v$ of a host tree T with maximum degree 3 such that (i) v and w are adjacent in G if and only if $S_v$ and $S_w$ share at least three nodes and (ii) each edge of T is used by exactly two representing subtrees. We show that a connected graph is dyadic if and only if it can be constructed from edges and cycles by gluing vertices to vertices and edges to edges. 

##### Q value

> 最常用的方法，用于评估将网络划分成模块（module）的强度（strength）。
>
> Q值越大，模块内联系越紧密，模块间联系越稀疏。
>
> 公式如下：
> $$
> Q=\sum^k_i(e_{ii}-(\sum^k_ie_{ij})^2)
> $$
> k代表社区个数；$e_{ii}$是社区i内的边数与整个网络中总边数的比值；$e_{ij}$是社区i、社区j之间的边数与整个网络中总边数的比值。
>
> *对于无标度网络，这些方法不太适用。*

#### 2、关于本文

> 研究表明，在很多领域用超图建模比dyadic graph好，比如分区（partition）。举个例子：社交网络用户可以用超图的顶点表示，而多用户操作，例如在一次操作中从多个社交网络（例如 Facebook）朋友中多次收集数据，可以通过超边建模在超图中。
>
> **超图划分**问题，是将超图的顶点划分到k个不相交、非空、等大的分区中，使得连接这些不同分区中顶点的超边数量（称为割）或者割的大小最小。
>
> 例：超图$H=(V,N)$，点$v=\{v_1,v_2,..,v_{14} \}$，超边$H=\{n_1,n_2,..,n_5\}$被分为4个区域$T=\{T_1,T_2,..,T_4\}$，割的大小为4，即$\{n_1,n_2,n_3,n_4\}$。
>
> ![image-20220307173827442](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220307173827442.png)
>
> 
>
>
> 传统的Q value测量模块度的方法不太适用于无标度网络和超图的划分。有以下原因：
>
> 1. 没有充分考虑无标度网络的社区结构。hMETIS 和 khMETIS是最小割超图分区工具，可以在执行最小割时提供load-balancing，但这不一定是具体问题的唯一约束。
> 2. 当社交网络快速增长时，模块化优化算法不能很好地适应不断变化的图结构。这些算法对图结构很敏感。
> 3. 多数超图分区没有考虑到度幂律分布。像*hyperpart（好像是作者以前文章提出的方法）*，使用信息熵平等对待每个节点，显然不能反映无标度网络的度分布特征。
>
> 本文就集各家之长，由于熵的分布规律与顶点度分布相吻合，使用基于信息熵计算的Q值来描述无标度网络的社区结构，并指导min-cut超图划分过程，产生高保真划分结果。
>
> 这个方法作者命名为**EQHyperpart**。
>
> 
>
> 本文顺带提了一下当前常见的社区检测方法：
>
> 1. minimun-betweenness
> 2. clustering centrality
> 3. random walk
> 4. eigenvectors of matrices
> 5. target function optimization
> 6. density of edge connection
>
> 注重检测速度以及重叠社区检测并且是运用信息论的方法：
>
> 1. minimum description length(MDL)
> 2. mutual information
> 3. information bottle

#### 3、Q and EQ

> 本文提出的度量方法。
>
> **E**：反映无标度网络特征的信息熵
>
> **EQ**：基于超图中Q值的模块化
>
> 
>
> **本文用到的熵：**
>
> * 社交网络熵，基于顶点的度而产生
>
> > 顶点i的“重要性”（就一概率而已）：$I_i=\frac {d_i} {\sum^N_{i=1} d_i}$，N为网络中顶点的数量，$d_i$为顶点i的度。
> >
> > 那么网络的熵即为：$E=-\sum^N_{i=1}I_i \log(I_i)$
>
> * 社区结构熵（Community Structure Entropy，CSE）
>
> > 由无标度网络的特性，一个社区的重要性，比如数量，决定了新节点加入的概率。
> >
> > CSE定义为**条件熵**$H(Y|X)$，在社区Y已存在的情况下，衡量顶点X的不确定性或者无序的情况。
> > $$
> > \begin{aligned}
> > H(Y|X) & = -\sum^N_{i=1} \sum^M_{j=1}P(x_i,y_i)\log(P(y_j|x_i))\\
> > &=-\sum^N_{i=1}\sum^M_{j=1}P(y_j|x_i)P(x_i)\log(P(y_j|x_i))
> > \end{aligned}
> > $$
> > 社区变量$Y=(y_1,y_2,..,y_{|y|})$，
> >
> > 顶点变量$X=(x_1,x_2,..,x_{|x|})$，
> >
> > N为所有顶点数，M为所有社区数，
> >
> > $P(x_i,y_j)=P(y_j|x_i)P(x_i)$是**联合概率**（joint probability）。
> >
> > $P(x_i)$表示顶点i的”重要性“，上文有提到；
> >
> > $P(y_j|x_i)$表示社区j包含顶点i的概率，即$P(y_j|x_i)=\frac {m_j}{N}$,社区j的节点数占全网节点数的比例。
> >
> > 因此，计算CSE可用如下公式：
> > $$
> > \begin{aligned}
> > E_{CS} = -\frac {\sum^N_{i=1,Z_{{ij}=1}} \sum^M_{j=1}d_i*(\frac {m_j} {N}*\log(\frac {m_j} {N}))}{\sum^N_{i=1}d_i}
> > \end{aligned}
> > $$
> > 其中$Z_{ij}$是分配矩阵（assignment matrix），如果顶点i被分配到社区j，则$Z_{ij}=1$，否则等于0。
>
> * 社区间熵（inter-community entropy，ICE）
>
> > 用于反映社区间的不确定性。
> >
> > 经典的超图多级分区框架由三个阶段组成：粗化（coarsening）、分区（partitioning）、去粗化（uncoarsing）。
> >
> > 通过使用一些启发式算法合并顶点和/或边来粗化超图。 在极端情况下，顶点级超图可以粗化为社区级超图。 受此启发，社区可以被视为粗化后的超顶点（super-vertices），社区之间的关联可以被认为是社区之间的割超边（cut hyperedge）。
> >
> > ICE定义如下：
> > $$
> > E_{IC}=-C*(\frac 1 M)*\log(\frac 1 M)
> > $$
> > 其中C是当前超图建模网络的 K-1 cut size，M是社区总数。
>
> 最后，EQ定义如下：
> $$
> EQ=E_{CS}-(E_{IC})^2
> $$

#### 4、EQHyperpart algorithm

> 为避免局部最优解，按照模拟退火的想法进行改进；并定义了Micro cut降低在分区时进入局部最优解的概率，即当在最高增益移动候选中存在平局时，可以应用Micro cut，或者在计算移动增益时代替 K -1 cut size。
>
> ![image-20220313163615892](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220313163615892.png)
>
> ![image-20220313172750334](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220313172750334.png)

#### 5、实验

> * 三个方面进行评估：scalability、several adopted metrics、auto-tradeoff ability
> * 四个数据集，其中三个真实世界网络（Karate club、Dolphin social network、American College Football），Facebook的一部分数据。
> * 环境：C++、Windows 2008 server、Intel Xeon 2.0Ghz、8G RAM。
>
> **评价scalability**：用查询成本节省率（query cost saving rate）$R_{CS}$评价。
>
> > $C_{init}$：网络初始状态的的平均查询成本
> >
> > $C_{grown}$：按照网络增长的机制，当网络规模到达1000，重新计算平均查询成本
> > $$
> > R_{CS}=\frac{C_{init}-C_{grown}}{C_{init}}
> > $$
> > ![image-20220313211221108](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220313211221108.png)
>
> **serveral adopted metrics**：
>
> * K-1 cut size within balance constraints
>
>   >展示了不同平衡水平下的 K-1 cut size。 观察到 EQHyperpart 分区器优于加权网络中的其他竞争算法，因为基于熵的 Q 值是为非均匀分布式无标度网络设计的。 具体来说，EQHyperpart-MC 在Micro cut的帮助下显着减小了 K-1 cut size。 hMETIS 和 hyperpart 遗漏了一些数据，因为它们无法在某些平衡级别要求下产生分区结果。
>   >
>   >![image-20220313213019150](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220313213019150.png)
>
> * Modularity features retainment ability
>
>   > 采用信息检索系统中的典型指标，包括召回率(recall rate)、准确率(precision)和F-score作为评价指标。
>   >
>   > 分区partition：$t \in T$
>   >
>   > 自然分化的社区natural community：$c\in C$
>   >
>   > $\alpha(c,T)$:正确分配给 c 的顶点数
>   >
>   > $\beta(c,T)$:错误分配给 c 的顶点数
>   >
>   > $\gamma(c,T)$:未正确分配给 c 的顶点数
>   > $$
>   > \begin{align}
>   > R(T) &= \frac{\sum_c\alpha(c,T)}{\sum_c\alpha(c,T)+\gamma(c,T)} \\
>   > P(T) &= \frac{\sum_c\alpha(c,T)}{\sum_c\alpha(c,T)+\beta(c,T)} \\
>   > F1 &=\frac {2*P(T)*R(T)}{P(T)+R(T)} 
>   > \end{align}
>   > $$
>   >
> 	>
> 	> ![image-20220314154613361](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220314154613361.png)
> 	>
> 	> ![image-20220314154640796](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220314154640796.png)
> 	>
> 	> 实验效果还行，但对于有重叠社区的检测效果一般，因为设计算法的时候没有考虑这些。
> 	
> * Tradeoff between modularity and cut size
>
>   > $FS_i$：F-Score value
>   >
>   > $CS_i$：K-1 cut size
>   >
>   > $TO_i$：tradeoff value
>   >
>   > $i$：unbalance level
>   >
>   > $|E|$：number of edges of dataset
>   >
>   > $a,b$：weighting coefficients, a+b=1
>   > $$
>   > TO_i=a*FS_i*100+b(1-\frac{CS_i}{|E|})*100
>   > $$
>   > ![image-20220314163517695](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220314163517695.png)
>   >
>   > 结果显示平均tradeoff value比其他三个要好。
>
> **Auto-tradeoff partitioning**：
>
> > 通常是注重减小 k-1 cut size和unbalance factor。本文认为modularity retaining ability也很重要。
> >
> > $FS_{auto}$：F-Score value
> >
> > $CS_{auto}$：k-1 cut size
> >
> > $UB_{auto}$：unbalance factor value
> >
> > $|E|$：number of edges of the dataset
> >
> > $UB_{max}$：max unbalance factor
> >
> > $a,b,c$：weighting coeffcients, a+b+c=1
> > $$
> > TO_{auto}=a*FS_{auto}*100+b*(1-\frac{CS_{auto}}{|E|})*100+c*(1-\frac{UB_{auto}}{UB_{max}})*100
> > $$
> > ![image-20220314200129936](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220314200129936.png)
> >
> > *原文：总之，EQHyperpart 在没有任何平衡约束的情况下产生了令人满意的结果。 换句话说，我们已经验证了 EQHyperpart 的自动权衡分区能力的有效性。*
>
> **execution time:**
>
> 由于同一数据集上不同不平衡级别的分区时间相似，我们计算了每个数据集上每个分区器的平均值，并相对于 khMETIS 的运行时间进行了归一化。
>
> > ![image-20220314201123241](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220314201123241.png)



### 五、基于信息熵的复杂网络中影响节点识别

**Influential Nodes Identification in Complex Networks via Information Entropy**

*Guo C, Yang L, Chen X, et al. Influential nodes identification in complex networks via information entropy[J]. Entropy, 2020, 22(2): 242.*

源码：https://github.com/YangLiangwei/Influential-nodes-identification-in-complex-networks-via-information-entropy

#### 1、名词概念

compartmental: [adj]区划的，分为若干部分的

copiously: [adv]充裕地、丰富地

attenuation：[n]衰减；稀释；弱化

##### rich club phenomenon

> 重要的节点趋向于相互重叠。相关论文：Colizza, V.; Flammini, A.; Serrano, M.; Vespignani, A. Detecting rich-club ordering in complex networks.
> Nat. Phys. 2006, 2, 110–115.

##### three degrees of influence(TDI) theory

> 该理论说明，个人的社会影响只在一个相对较小的范围内。

#### 2、传播模型

> 衡量复杂网络中一组节点的影响的最佳方法是通过对现实生活网络数据的**传播动态过程**。如：
>
> **SIR model**, susceptible infected recovered model；
>
> 本文采用SIR模型客观评价算法选择的节点的传播能力。
>
> SIR 模型中的每个节点都可以分为三种状态之一，即易感节点 (S)、感染节点 (I) 和恢复节点 (R)。具体过程：
>
> 1. 开始，选择一些节点作为已感染状态节点，其他节点为易感染状态。
>
> 2. 每次迭代，已感染节点随机选取一个邻居节点，感染概率为$\mu$。
>
> 3. 同时，已感染节点恢复概率为$\beta$，并且不会再被感染。
>
> 经过足够多次的迭代后，到达平稳状态，不再有感染。
>
> 感染率：$\lambda = \frac{\mu}{\beta}$;
>
> SIR传播阈值：$\mu_c=\frac{\langle k \rangle}{\langle k \rangle^2 - \langle k \rangle }$, $\langle k \rangle$为网络的平均度；
>
> 设置$\mu =  1.5\mu_c$；$\mu$太小，影响范围小或者根本不能传播，而$\mu$太大，几乎所有的方法都会影响整个网络，没有比较意义。

#### 3、EnRenew Algorithm

> 顶点v的信息熵的计算公式：
> $$
> E_v = \sum_{u\in\Gamma_v}H_{uv}=-\sum_{u\in\Gamma_v}p_{uv}\log(p_{uv})
> $$
> 其中$p_{uv}=\frac{d_u}{\sum_{l\in\Gamma_v}d_l}$（*u是v的邻居，即u的度除以顶点v所有邻居顶点的度*）, $\Gamma_v$表示顶点v的邻居，$d_u$表示顶点u的度，$H_{uv}$表示顶点u到顶点v的传播能力。（使用的是自然对数）
>
> 
>
> ![image-20220325215445056](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220325215445056.png)
>
> ![image-20220326193456031](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220326193456031.png)
>
> **该算法挑选出一组传播者。该算法考虑到了网络的聚集现象，没有简单的使用顶点度来衡量。**
>
> $\frac{1}{2^l-1}$：衰减因子，离点v越远，对v的影响越小。
>
> $E_{\langle k \rangle}=-\langle k \rangle \cdot \frac{1}{\langle k \rangle} \cdot \log(\frac{1}{\langle k \rangle})$：*也不懂为什么要这么写，直接 log不就完事了？*
>
> **时间复杂度**：
>
> 三个阶段：initialization、selection and renewing。n, m ,r分别代表顶点数、边数、初始感染的顶点数
> $$
> \begin{array}{}
> &O(m+n)+O(r\log n)+O(r \langle k \rangle^2)\\
> &=O(m+n+r\log n +\frac{rm^2}{n^2})
> \end{array}
> $$
> 若是稀疏网络，$r\ll n$，近似于O(n)。

#### 4、评判传播效果

> $$
> F(t) = \frac{n_{I(t)}+n_{R(t)}}{n}
> $$
>
> $n_{I(t)}$、$n_{R(t)}$分别代表t时刻被感染和已恢复的顶点。$F(t)$越大，传播越广；t越小，传播越快。
> $$
> F(t_c) = \frac{n_{R(t_c)}}{n}
> $$
> $F(t_c)$表示达到稳定状态时的传播规模。该值越大，初始所选的顶点传播能力越强。
> $$
> L_S=\frac{1}{|S|(|S|-1)}\sum_{u,v\in S,u\neq v}l_{u,v}
> $$
> $L_S$表示初始感染点集S中顶点的平均最短路径长度。$L_S$越大，初始感染点越分散。$l_{u,v}$表示u到v的最短路径，如果u、v不相连，则距离为$D_{GC}+1$，$D_{GC}$是连通分量的直径。

#### 5、参数 l 的确定

> 在renewing the information entropy时，通过参数 l 可以改变顶点的影响范围。l=1，只影响到其邻居，以此类推。
>
> 总体来看，l=2时效果比较好。
>
> ![image-20220326215330559](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220326215330559.png)
>
> *p 是初始感染节点的比率。*

#### 6、实验比较

> ![image-20220327172638582](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220327172638582.png)
>
> 比较最终的感染规模。本文的算法超过其他的benchmark方法。
>
> 
>
> ![image-20220327172725442](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220327172725442.png)
>
> 比较传播速度。本文的算法在相同时间传播的范围更广。
>
> 
>
> ![image-20220327172744211](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220327172744211.png)
>
> 比较不同传播条件下的最终效果。基本上还行，表明本文算法对不同传播条件有着更强的泛化能力（generalization ability）。
>
> 
>
> ![image-20220327172808390](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220327172808390.png)
>
> 比较$L_S$。除了最后一个，其他的值都明显比其他算法的大。说明本算法趋向选取分散分布的点。


#### 7、我的看法
> 如果初略的看一下，感觉效果还不错。仔细看完本文+源代码，发现有些也没讲清楚就糊弄过去了。
>
> 1. 计算$H_{uv}$，那么这个$H_{uv}$是表示哪个点呢？u还是v?如果是u，那换一个邻居H的值就变了。看了源代码，作者说和做是两回事。
>
> 2. 像all_degree，没理解错的话是度总和，直接就简单的等于“图中所有顶点-1”，这在简单图上是成立的，但问题是这些数据集是简单图吗？
> 3. 平均度的计算，也没指明是怎么计算的。看了源代码才知道是$\frac{edge\times 2} {node}$; E\<k\>的计算在文章中也写得云里雾里;



### 六、使用节点熵和分区熵的模因算法用于网络中的社区检测

**Memetic algorithm using node entropy and partition entropy for community detection in networks**

*Žalik K R, Žalik B. Memetic algorithm using node entropy and partition entropy for community detection in networks[J]. Information Sciences, 2018, 445: 38-49.*



#### 1、名词概念

memetic: [n]模因；通过人类的模仿能力完成复制，在人际之间传播的信息；*与基因、信息论等概念有关*。

convergence: [n]趋同；汇集，相交；会聚区；收敛

locus: [n]轨迹；地点，所在地；基因座，基因位点；位点；

> 生物学和遗传算法中的术语，指某个基因或某个具有调控作用的DNA序列，在染色体上所处的特定位置。示意图如下：
>
> ![](https://bkimg.cdn.bcebos.com/pic/3801213fb80e7bec53715811252eb9389a506b92?x-bce-process=image/watermark,image_d2F0ZXIvYmFpa2U4MA==,g_7,xp_5,yp_5/format,f_auto)

chromosome：[n] 染色体；

agglomerative：[adj] 会凝聚的；凝结的

##### binary tournament  selection:

> 遗传算法中的一个选择策略，tournament selection，锦标赛选择。策略很直观，在整个种群中抽取 n 个个体，让他们进行竞争，抽取其中最优的个体。参加锦标赛的个体个数称为tournament size。**当 n=2**时，便是最常用的大小，称为binary tournament selection。下图展示了 n=3 的tournament selection：
> ![img](https://pic2.zhimg.com/80/v2-b4ea072ab4e6bc195daa9c4ed90c7495_720w.png)

#### 2、关于本文

> 本文的算法是由遗传算法（genetic algorithm）改进而来，用于进行社区检测。
>
> 遗传算法的执行框架：
>
> ![img](https://pic1.zhimg.com/80/v2-2f174fefc2d84caa6b9ed054b679b1c8_720w.png)
>
> 
>
> 很多基于模块度优化（modularity optimization）的方法，存在**resolution limit**的问题，即无法检测到小社区。
>
> 遗传算法作为一种全局搜索技术是有效的，但它们需要相对较长的时间才能收敛到全局最优

#### 3、问题定义

* 图G，n个顶点，m条边。

* $A_{ij}$：图G的邻接矩阵。

* $C_i$：表示社区，$C_i\in G$。社区内紧密（$E_{C_i}^{in} = \sum_{i,j\in C_i}A_{ij}$）,社区间稀疏（$E^{out}_{C_i}=\sum_{i\in C_i,j\notin C_i}A_{ij}$）。

* 模块度Q：挑选符合社区定义的 "最佳" 的社区。
  $$
  Q=\sum_{C_i \in P}\frac{E_{C_i}^{in}}{m}-(\frac{2*E_{C_i}^{in}+E_{C_i}^{out}}{2*m})^2
  $$
  
* 顶点熵：$\Gamma_i$是顶点 i 的邻居；deg(i)是顶点i的度；来自社区 C 的节点引起的节点熵部分为$NE_C$; 
  $$
  NE(i)=-\frac{\sum_{j\in \Gamma_i}p_i^j\log (p_i^j)}{\log (deg(i))};\\ 
  NE_C=-\frac{\sum_{i\in C,j\in \Gamma_i}p_i^j\log(p_i^j)}{\log (deg(i))}\\
  p_i^j = \frac {1}{deg(j)}
  $$
  

#### 4、NE-NET

*遗传算法，涉及一些生物学概念*

> * 每个染色体由n个基因组成，每个基因通过包含分配节点的**社区标签**或者一个邻居的**索引值**，来表示图的一个节点。
>   假设从 1 开始的节点序列号，基因 i 对应于节点 $n_i$ 。
>
> * 进化算法中常用的染色体表示是**基于组(group based)**的表示。染色体的每个基因都包含其所属组的值。
>   在基于基因座的相邻表示中，每个基因都包含一个节点邻居的索引。
>   在基于相邻基因座的表示中，所有具有基因的节点及其相邻基因形成一个社区，而在**基于组**的表示中，所有由具有**相同社区标签值的基因**表示的节点形成一个社区。**本文使用基于组的表示**。
> * 按照适者生存和优胜劣汰的原理，逐代（generation）演化产生出越来越好的近似解，在每一代，根据问题域中个体的适应度（fitness）大小选择（selection）个体，并借助于自然遗传学的遗传算子（genetic operators）进行组合交叉（crossover）和变异（mutation），产生出代表新的解集的种群。

**交叉算子(Crossover operators)**

> 交叉算子主要定义了遗传算法的性能。交叉从父染色体继承良好的社区并添加新的社区。
>
> *类似于同源染色体的联会*
>
> ![](https://upload-images.jianshu.io/upload_images/10386940-38df5ee1440b2fbc.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/264/format/webp)
>
> * Uniform crossover，均匀交叉：使用随机生成的二进制向量（vector）。对于二进制向量中的值为 0，解基因取自第一个染色体，二进制向量的值为 1 则取自第二个染色体。
> * two-point crossover, 两点交叉：选定两个节点，交换这两个基因(簇标识符)。
>
> 均匀交叉和两点交叉产生非常随机的后代时效率很低，但它们快。
>
> **本文的方法：**
>
> ==由于==模块化比例最高的社区和社区的节点数，比模块化程度最高的社区增加了整个分区的模块化程度，
>
> ==因此==通过模块化和分配给社区的节点数的**比值**对两个父染色体的社区进行排序。尝试在后代中形成与父母相同的社区，但仅来自未分配给之前形成的任何社区的节点。
>
> **具体怎么交叉的，以下为示例：** *(原文的图不太正确，估计作者也没认真校对)*
>
> ![image-20220411205557630](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220411205557630.png)
>
> ![](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220411201622264.png)
>
> 从Table 1 可知，父母1(Parent 1)含有社区2、5、15、25，父母2(Parent 2)含有社区1、7、9，顶点 "11"属于社区1， Fig.1 (b)中标识错误，都圈出来了。
>
> ![image-20220411202408375](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220411202408375.png)
>
> ![image-20220411202733575](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220411202733575.png)
>
> Table 2 展示了具体的交叉过程。step2 时，漏了 "30" 这个点。模块度与顶点数的比值，经排序后如上所示。step3 时，Parent 2 的社区7中的点都已经在之前的步骤中分配了，就顺延到下一个候选，即Parent 2 的社区1。step5 执行完成后，所有点已使用，交叉过程结束。最后 step6 进行微调，由于有小社区9，且经过计算，只有将社区9与社区15合并后模块度增大，因此合并社区9和社区15。

#### 5、算法

![image-20220410154422079](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220410154422079.png)

> * step1: 初始化，影响最终解的质量和收敛速度。一般不知道解的信息，因此使用染色体基因的**随机初始化**来生成候选解(初始种群)。
>   最初，代表图节点的每个基因都被放置在初始种群中所有个体的不同社区中。*(即没有重叠)*
>   用基因索引($X^i_p=i;i=1,2,..,n$)作为社区标签。
>   对于 n 个基因中每个基因 i 的所有染色体，算法为图中的每个节点 i 随机选择一个邻居节点 k 并设置 $x^i_p = k$ 。因此每个基因都包含其邻居之一的索引(1,...,n)。
>   然后随机选择每个个体的每个基因，并将其分配到与带有标签 $x_i^j$ 的索引的基因**相同**的社区中。
>
> * step2：计算初始种群$P_0$ 的每条染色体的模块度值。
>
> * step3：按比例克隆到种群 $P_{t-1}$ 形成第一个后代种群。 然后遗传算子对后代种群进行提炼，并将新的遗传物质引入后代种群。使用**Binary Tournament Selection**进行选择。
>   变异算子不是完全随机的，是基于邻居的。当随机生成的概率小于$p_m$是发生，将该基因的社区标签换成它其中一个邻居的标签。
>
>   交叉算子，继承具有最高模块化比率和节点数的最佳社区。来自父母双方的所有社区都按照模块化比率和分配给社区的节点数进行排序。首先在后代中创建社区，该社区等于具有最高比率的社区，然后具有次优比率的社区，依此类推，直到后代中的所有节点都分配给一个社区。
>
> * step4：子染色体按一下两个步骤进行修改。
>
>   4.1. 合并社区增加模块度。交叉算子会产生一些小社区，这些社区可以与真实社区进行合并以增加模块度。为了一次合并多对社区，使用与**多步贪婪凝聚算法 (Multi-Step Greedy agglomerative algorithm, MSG)** 相同的标准，在每次迭代时，模块化是在每对连通社区合并后计算的。当模块化变化最大(greatest)和积极(positive)时，两个社区合并，并且第一个社区和第二个社区都不会导致与任何其他社区的最高模块化变化。
>   4.2. 重新分配节点。每个社区边界上的每个节点都可以移动到一个邻居社区。 在此步骤中，将未分配到具有最大节点熵的社区的每个节点移动到该社区。
>
> * step5：模型选择。首先，形成一个组合种群 $R_t = P_t + P_o$ 。 每个解都被分配了一个Rank（1 是最好的水平，2 是次优的水平，依此类推）等于它的非支配水平(**nondomination level**)。 然后，根据非支配对总体 $R_t$ 进行排序。
>   计算所有非支配个体的**拥挤距离值**，并选择前 N 个个体作为新种群。 主导种群(dominant population)被更新。 重复步骤 2 中的所有步骤，直到迭代次数达到 $g_{max}$ 。*(来源于这篇论文中的方法，引用量高。K. Deb , A. Pratap , S.A. Agarwal , T. Meyarivan , A fast and elitist multiobjective genetic algorithm: NSGA-II, IEEE Trans. Evol. Comput. 6 (2) (2002) 182–197 .)*



**分区熵(Partition entropy)和算法E-Net**

> 使用分区熵而不是模块化函数来避免分辨率限制(resolution limit)并识别所有重要的良好分离的社区，而不管社区的大小。算法E-Net就是一个小改进，避免出现resolution limit。
>
> **本文认为，整个图G具有最大的信息，社区检测视为信息丢失的过程。**
>
> 分区熵测量每个社区的无序程度。 社区的元素越相似，社区越有序，社区的熵越少。
> $$
> entropy_c= \left\{
> \begin{aligned}
> &n_c*(-sim_c*\log(sim_c)),\quad when \ sim_c>0 \\
> &n_c*(1.0-(-sim_c)*\log(-sim_c)),\quad when \ sim_c<0
> \end{aligned}
> \right\}
> $$
> $n_c$为社区C的顶点数；$sim_c$为社区的顶点相似度；
> $$
> sim_c=\frac{In_c-Out_c}{2*(In_c+Out_c)};\\
> In_c=\sum_{i,j\in C}(A_{ij});\\
> Out_c=\sum_{i\in C,j\notin C}(A_{ij})
> $$
> $In_c$和$Out_c$分别表示社区C内部和外部的边。
>
> Partition entropy: k为分区P的社区数。
> $$
> entropy_P=\frac{\sum_{i=1}^kentropy_{C_i}}{k}
> $$



#### 6、我的看法

> 还是要有点GA算法的基础才能看明白，有些地方作者默认你都懂，导致我看得费劲。
>
> 但是有些地方作者还是不讲清楚，像算法step5，用了NSGA-II的方法，也不讲清楚具体的目标函数是什么。
>
> 实验结果就不放上来了，总体来说比一般的遗传算法强；大部分情况下比 Louvian 算法**强一点点**，少部分情况 Louvian算法反超一点。





### 七、一种基于内聚熵的社交网络影响力最大化动态算法

**A dynamic algorithm based on cohesive entropy for influence maximization in social networks**

*Li W ,  Zhong K ,  J  Wang, et al. A Dynamic Algorithm based on Cohesive Entropy for Influence Maximization in Social Networks[J]. Expert Systems with Applications, 2020, 169(2):114207.*

#### 1、名词概念

pervasive：[adj]弥漫的，普遍的、遍布的

discrepancy: [n]差异；不符

hinge: [n] 铰链；合叶；枢纽；关键；

##### IC model(Independent Cascade Model)

>独立级联模型，是一个影响力模型。
>节点有两个状态：
>
>* 未激活：节点未收到消息。
>* 激活：节点收到消息并且能够传播给他们的邻居。
>
>在 t 时刻被激活的节点在 t+1 时刻**仅有一次**机会去激活其邻居。例如顶点 v 在 t 时刻被激活，则对于 v 的任何邻居 w，w在 t+1 时刻被激活的概率是 $P_{vw}$。
>
>![](https://img-blog.csdnimg.cn/20200519193809968.png#pic_center)
>
>==特点==：
>
>- 以发送者为中心（ sender-cen-tered)。当一个结点被激活后，它试图去激活它的所有邻接结点；
>- 一个结点独立地激活其所有的邻接结点（不一定都被激活)；
>- 信息扩散的过程随信息的级联过程（ cascading process）而变。网络中的信息扩散过程**不确定**了。

##### LT model(Linear Threshold Model)

> 线性阈值模型，也是一个影响力模型，有激活和未激活状态。
>
> * 在任意时刻，激活的节点都可以影响未被激活的点。
> * 每个节点都有激活阈值。
> * 如果影响程度超过该节点的阈值，则这个节点被激活。
>
> ==特点==：
>
> - 以接收者为中心(receiver-centered)，通过观察一个结点的所有邻接结点，根据该结点的阈值决定是否可以激活该结点;
> - 结点的激活依赖于一个结点的全部邻接结点;
> - 一旦给定线性阈值模型中的阈值，网络中的信息扩散过程也就**确定**了。

#### 2、关于本文

> 有利用到**相对熵，JS散度**来确定顶点的相似度。

##### cohesive entropy

> 本文提出的一个方法，衡量两个节点之间关于相邻区域信息分布的相似性。
>
> ![image-20220416203521295](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220416203521295.png)
>
> ![image-20220416203402709](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220416203402709.png)
>
> 以Fig 1为例。顶点 i 的相邻区域的概率 $p(i,l)=\frac {D_{local}(l)}{\sum_{b=1}^m D_{local}(b)}$,
> $N_{local}^3=[1,2,3,4,5]$,相对应的度为$[2,1,4,2,1]$。
> 则$DI_{local}^3=[\frac{2}{10},\frac{1}{10},\frac{4}{10},\frac{2}{10},\frac{1}{10}]$。**为之后计算JS散度做准备。**
>
>
> 节点 i 和节点 j 的cohesive entropy的计算公式如下：
> $$
> \begin{aligned}
> &CE_{ij}=1-\frac{r_{ij}}{\max(r_{ij})}\\
> 
> &r_{ij}=D_{kl}(DI^i_{local}||DI^j_{local})+D_{kl}(DI^j_{local}||DI_{local}^i)\\
> 
> &D_{kl}(DI_{local}^i||DI_{local}^j)=\sum_{b=1}^B P(i,b)\ln \frac{P(i,b)}{P(j,b)}
> \end{aligned}
> $$
> 其中 $B=\min(D(i)+1,D(j)+1)$，以确保两个概率分布的大小相同。

#### 3、算法

##### 基于内聚熵的社区重叠传播算法(Community overlap propagation algorithm based on cohesive entropy)

> 该算法由COPRA改进过来。COPRA的主要概念是节点所属的社区由邻居的社区分布决定，即一个节点与所有相邻节点的距离及其影响程度相同。**缺点**：然而现实中，节点的影响程度是不同的。 密友之间分享信息的概率远高于普通朋友之间分享信息的概率，受影响的用户也信任其他有相似偏好的用户。
>
> 本文**CECOPA**算法：
>
> ![image-20220416213335237](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220416213335237.png)
>
> t 是一个阈值，用于限制满足条件的系数的最小值。该算法输出社区结构(community structure)，为之后挑选种子节点做准备。
>
> 
>
> ==aggregation bridge==:本文定义的一个概念。每个社区是一个aggregation area，社区重叠的区域就是aggregation bridge，记为$N_{hinge}=\cup_{i=1}^p Community^i_{bridge}$，是一个集合。
>
> 其中$Community_{bridge}^i$表示在社区 i 中的**顶点集**同时落于**6个及以上**的社区。*( 为什么是6个？六度分离的概念concept of the six degree )*
>
> ==aggregation focus==：每个社区的不重叠节点形成社区的集中聚集区。在这区域中，拥有最高度中心性(degree of centrality)的顶点与该区域中的其他顶点有着最紧密的连接。记为$N_{core}=\cup_{i=1}^p argmax_{v\in c_i}D(v)$。
>
> 示例如下：顶点8和16的度为6，构成了聚合桥{8,16}。
>
> ![image-20220417221550846](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220417221550846.png)
>
> 由于示例中的网络较小，因此聚合桥的标准降低为跨多个社区节点的最适中的节点。 在现实的网络中，一般都存在满足聚合网桥要求的节点。
>
> 对于每个社区，aggregation focus为：$N_{core}^1=\{3,4\},N_{core}^2=\{12\}$。第三个社区，排除重叠顶点，剩余的顶点度都为1，因此没有，但这种情况在大型网络中并不常见。
>
> 挑选候选种子集的算法**TKRCS, Candidate seed Set based on Two Key Regions**：
>
> ![image-20220417222845363](H:\school_materal_temp\硕士\MK笔记\网络熵\graph entropy.assets\image-20220417222845363.png)
>
> 

