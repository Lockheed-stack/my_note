# 网络熵



### [1]Şahin Bünyamin. New network entropy: The domination entropy of graphs[J]. Information Processing Letters,2022,174:

### 起源

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



### 关于本文

> 支配（domination）也是图的一个重要的属性。
>
> Haynes等人证明，图的这些不变的属性，在树中，对图的微小变化是十分敏感的。
>
> 基于以上种种原因，作者定义了一个基于支配集的图熵的度量。
>
> 要得到熵，作者使用了图的支配多项式（domination polynomials）。
>
> 除了一些众所周知的支配多项式之外，我们还定义了细分星图的支配多项式。 此外，我们将支配熵与基于匹配、独立集、顶点度和给出的 21 个图的自同构组的图熵度量进行了比较。 这 21 个五阶图根据其拓扑复杂度进行排序。



### 名词、概念



cardinality：[n] 基数；集合的势

subdivide:





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



##### 总支配数$\gamma_t(G)$

> 用于表示图 G 的总支配数，它是具有最小阶数的总支配集的基数



##### 支配多项式domination polynomial，$D(G,x)$

> $D(G, i)$ 表示基数为 i 的 G 的支配集族，$d_i$ 表示 $D(G, i)$ 的基数，使得 $d_i(G) =|D(G, i)|$。
> $$
> D(G,x) = \sum ^{V(G)}_{i=\gamma(G)} d_i(G)x^i
> $$
>
> 例子：
>
> 考虑路径图 $P4:v1v2v3v4$。 为了支配图$P_4$，取支配其他两个顶点的两个顶点就足够了。 因此$\gamma(P_4) =2$。  $P_4$ 的总支配集是 $\{v2, v3\}$ 并且 $γ_t(P_4) =2$。 基数为 2 的 $P_4$ 的支配集是 $D(G, 2) =\{ \{v1, v3\}, \{v1, v4\}, \{v2, v3\}, \{v2, v4\} \}$且$d——2(G) =4$  . 此外，基数为3的$P_4$的支配集为$D(G, 3) = \{\{v1, v2, v3\}, \{v1, v2, v4\}, \{v1, v3, v4\}, \{v2, v3, v4  \}\}$，$d_3(G) =4$。 最后，基数为 4 的 $P_4$ 的支配集是 $D(G, 4) =\{v1, v2, v3, v4\} $和 $d_4(G) =1$。
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
> > $γ_s$ 来表示支配集的总数，该符号与图的总支配数 $γ_t$ 是一个意思。很明显，$γ_s$ 等于图 G 的支配多项式的**系数之和**。
>
> 



##### 图熵

> 设 G 是一个图，$f:S\rightarrow R_+$ 是定义在 $S=\{s_1, s_2, ..., s_k\}$ 上的信息泛函，使得 S 是 G 的一组元素。定义如下(log以2为底)：
> $$
> \begin{align*}
> I_f(G) &= -\sum ^k_{i=1} \frac {f(s_i)} {\sum^k_{j=1}f(s_j)} \log(\frac {f(s_i)} {\sum^k_{j=1}f(s_j)}) \\
> 
>        &=\log (\sum^k_{i=1}{f(s_i)})-\frac {\sum ^k_{i=1}f(s_i)\log f(s_i)} {\sum^k_{j=1}f(s_j)}
> \end{align*}
> $$
> 



##### 支配熵

> 对图 G ，$|V| =n$ 且没有孤立的顶点，我们引入信息泛函使得 $f := d_i(G)$，其中$d_i(G)=|D(G,i)|$。
>
> ![image-20211121200204211](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20211121200204211.png)
>
> *划线部分怎么理解？什么意思？*
>
> 





### 一些图的支配熵

> 假设$H_1$和$H_2$是两个连通图，$H=H_1∪H_2$分别是$H_1$和$H_2$的不相交并集。 我们得到:
> $$
> \begin{align*}
> I_{dom} = \log (\sum^n_{i=\gamma(H)}{d_i(H)})-\frac 1 {\sum ^n_{i=\gamma(H)}d_i(H)}\sum^n_{i=1}d_i(H)\log(d_i(H))
> \end{align*}
> $$
> 这样可得$γ(H)=γ(H_1)+γ(H_2)$和$d_i(H) =\sum^i_{j=γ(H_1)}d_j(H_1)d_{i−j}(H_2)$.



> 完全图$K_n$，可得：
> $$
> I_{dom}(K_n)=\log(2^n-1)-\frac 1 {2^n-1}\sum^n_{i=1}C^i_n \log(C_n^i)
> $$
> 



> 星图$S_n$，可得：
> $$
> I_{dom}(S_n)=\log(2^{n-1}+1)-\frac 1 {2^{n-1}+1}(\sum^{n-3}_{i=1}C^i_{n-1}\log(C^i_{n-1}))-\frac {n\log n} {2^{n-1}+1}
> $$



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
> 

