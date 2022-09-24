# 网络熵

### 一、通过局部信息维度识别复杂网络中的影响者

**Identification of influencers in complex networks by local information dimensionality**

*[1] Wen T, Deng Y. Identification of influencers in complex networks by local information dimensionality[J]. Information Sciences, 2020, 512: 549-562.*

#### 1、名词概念

fractal: [n]分形；[adj]分形的

##### self-similarity

> 如果一个对象在任何尺度上看起来“大致”相同，则称它是自相似的。 分形是一类特别有趣的自相似对象。 具有参数 N 和 s 的自相似对象由幂律描述，例如$N=s^d$，其中$d=\frac{\ln N}{\ln s}$是scaling law的 “维度(dimension)”。*该解释来自于MathWorld。*

##### similarity matrix

> 原文地址：https://deepai.org/machine-learning-glossary-and-terms/affinity-matrix
> 
> 相似度矩阵，也叫做Affinity Matrix。统计学中的技术，用于组织一组数据点之间的相互相似性。
> 
> 相似度度量的典型例子是余弦相似度和 Jaccard 相似度。 这些相似性度量可以解释为两个点相关的概率。 例如，如果两个数据点的坐标接近，那么它们的余弦相似度得分（或各自的“亲和力(Affinity)”得分）将比两个数据点之间有很大空间的数据点更接近 1。

#### 2、关于本文

一些基于中心性（centrality）的方法：

![img](https://ask.qcloudimg.com/http-save/1692602/17i3jd87t8.png?imageView2/2/w/1620)

* degree centrality(DC):
  
  > 度中心性。
  > 
  > $$
  > C_D(i)=\sum_{j=1}^{|N|}e_{ij}
  > $$
  > 
  > 顶点 i 的 DC。
  > 
  > $e_{ij}$表示顶点 i 和 j 之间的边。
  > 
  > 缺点：只关注局部信息，没考虑到全局信息。

* betweenness centrality(BC):
  
  > 中介中心性。
  > 
  > $$
  > C_B(i)=\sum_{s,t\neq i}\frac{g_{st}(i)}{g_st}
  > $$
  > 
  > 顶点 i 的 BC。
  > 
  > 其中$g_{st}$是顶点 s 和顶点 t 之间最短路径的**数目**；$g_{st}(i)$是顶点 s 和顶点 t 之间且经过顶点 i 的最短路径的**数目**。
  > 
  > 缺点：关注了全局信息，但计算复杂度高，限制了在大规模复杂网络中的应用。

* closeness centrality(CC):
  
  > 紧密中心性。某个节点到达其他节点的难易程度。
  > 
  > $$
  > C_C(i)=\frac{1}{\sum^{|N|}_{j=1}\omega_{ij}}
  > $$
  > 
  > 顶点 i 的CC。
  > 
  > 其中$\omega_{ij}$表示顶点 i 到顶点 j 的最短距离；|N| 表示顶点数。
  > 
  > 缺点：同BC。

* eigenvector centrality(EC)
  
  > 特征向量中心性。
  > 
  > $$
  > Ax=\lambda x,x_i=u\sum_{j=1}^{|N|}a_{ij}x_j
  > $$
  > 
  > A是一个相似度矩阵，大小为N*N；顶点 i 的 EC $x_i$是归一化特征向量中属于A的第 i 个条目(entry)；$\lambda$是 A 的最大的特征向量，$u=\frac{1}{\lambda}$；$x_i$是与顶点 i 相连的顶点的相似得分(similarity score)之和。
  > 
  > 缺点：无法用于对称网络。

**Local dimension**

> 跟幂律分布有关。对于半径 r ，已经发现，**到中心节点的最短距离小于 r 的节点数** $N_i(r)$ 遵循幂律，即$N_i(r)\thicksim r^{D_i}$。
> 
> 可以很容易地发现，节点 i 的 $LD\ D_i$ 可以从对数图(log-log plot)的斜率获得:
> $$
> D_i=\frac{d}{d\ln r}\ln N_i(r)
> $$
> d是导数符号。
> 
> 半径 r 从 1 增加到距节点 i 的最短距离 $k_i$ 的最大值，由于复杂网络的离散特性，上式的导数表示如下：
> $$
> D_i = \frac{r}{N_i(r)}\frac{d}{dr}N_i(r)\\
> D_i=r\frac{n_i(r)}{N_i(r)}
> $$
> 其中$n_i(r)$是与central node的最短距离等于 r 的节点数。
> 
> 一个顶点的 LD 值越小，该点的影响力越大，因此对每个点的 LD 值进行排序即可获得重要的顶点。

#### 3、本文的方法

> ![image-20220425155827854](https://cdn.statically.io/gh/Lockheed-stack/my_note/488e4ef3/%E7%BD%91%E7%BB%9C%E7%86%B5/graph%20entropy2.assets/image-20220425155827854.png)
> 
> *box 表示的应该是 "一块区域"。*
> 
> $k_i$是顶点 i 到其他顶点的最短路径中的最大值；$\lceil(k_i/2)\rceil$表示向上取整。
> 
> **local information dimension**：LID $D_{I\_i}$
> 
> $D_{I\_i}=-\frac{d}{d\ln l}I_i(l)$
> 
> 
> d 是导数的符号。l 是 box 的大小。$I_i(l)$是以顶点 i 为中心顶点，大小为 l 的 box 中的信息(information)。
> $I_i(l)=-p_i(l)\ln p_i(l)\\
> p_i(l)=\frac{n_i(l)}{N}$
> 
> $n_i(l)$是这块 box 中的顶点数；N 是总顶点数。
> 
> 因此 LID 可写成如下：
> 
> $$
> \begin{aligned}
D_{I_i} &=-\frac{d}{d\ln l}(-\frac{n_i(l)}{N}\ln \frac{n_i(l)}{N})\\
&=-\frac{d}{d\ln l}(-p_i(l)\ln p_i(l))\\
&=\frac{l}{1+\ln p_i(l)}\frac{d}{dl}p_i(l)\\
&\approx \frac{l}{1+\ln \frac{n_i(l)}{N}}\frac{N_i(l)}{N}
\end{aligned}
> $$
> 
> 其中$N_i(l)$是与中心节点 i 的最短距离**等于** box size l 的节点数；$n_i(l)$是与中心节点 i 的最短距离**小于等于**box size l 的节点数。*跟上面的定义不太一样，但说的是同一件事。*

#### 4、实验

> 6个现实世界网络、5种比较方法(BC,CC,DC,EC,LD)。
> 
> 进行了五个实验：
> 
> 1. 列出前10个节点ID来比较不同措施获得的前10个节点结果的差异
> 2. 基于SI模型的传播显示LID获得的节点的优越感染能力
> 3. 关系图和 Kendall 的 tau 系数显示了不同度量和 SI 模型得到的节点排名的相似性
> 4. 以及不同度量的运行时间，显示了该方法的低计算复杂度。

##### top 10 nodes

> ![image-20220425210818899](https://cdn.statically.io/gh/Lockheed-stack/my_note/488e4ef3/%E7%BD%91%E7%BB%9C%E7%86%B5/graph%20entropy2.assets/image-20220425210818899.png)
> 
> LID 标识的这些唯一节点可能表明传播过程中的重要变化。 从表 2 可以看出，USAir 网络中影响力最大的同一个节点是通过 6 种不同的方法获得的——节点 118。LID 获得的前 10 个节点与 CC 获得的节点相同，分别为 8 和 7 个。 在 LID 与 DC 和 EC 之间分别获得相同的节点。  BC、LD、LID得到的相同top-10节点数少于其他方法，为6个。 美国航空网络的结果表明，其他措施获得的前10个节点中，大部分都是通过LID获得的，这表明了它的相似性和可信度。*以上为原文翻译*

##### SI model

> 每个点有两个状态：infected、susceptible。
