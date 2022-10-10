## Rumor correction maximization problem in social networks

**社会网络中的谣言纠正最大化问题**

Zhang Y, Yang W, Du D Z. Rumor correction maximization problem in social networks[J]. Theoretical Computer Science, 2021, 861: 102-116.

#### 1、名词、概念

Admittedly：[adv]诚然；无可否认

malicious：[adj]恶毒的

Containment：[n]遏制

leaflets：[n]传单

stifler：[n]扼杀者

monotone：[n]单调；[adj]单调的

##### 集合函数（set function）

> 有限集合$V=\{1,2,..,n\}$，集合函数 $f:2^V \rightarrow \mathbb{R}$。
> 
> $2^V$是集合 V 的幂集，是 V 的所有子集组成的集合。
> 
> 由于V的每个元素在它的子集里都有**选或者不选**两种可能，因此有$2^{|V|}$个元素。
> 
> 即该函数的意思是，可以把 V 的子集映射到实数。

##### 次模函数 submodular function

> "边际效用递减" 的形式化说法
> 
> 对于给定一个集合函数$f:2^V \rightarrow R$，若$S\subseteq V$，那么在S中增加一个元素所增加的收益要小于等于在 S 的子集中增加一个元素所增加的收益。
> 
> 即对于函数 f，若$A\subseteq B \subseteq V \ and \ e\in V-B$，则$f(A\cup\{e\})-f(A) \ge f(B \cup \{e\})-f(B)$。

##### 无偏估计 unbiased estimation

> 无偏估计是用样本统计量来估计总体参数时的一种无偏推断。
> 
> 例如：总体平均数未知，但知道部分样本，可计算出样本平均值。样本平均值不一定等于总体平均值，但这种估算方法没有系统上的偏差。即样本平均数是总体平均数的无偏估计。

#### 2、关于本文

> 谣言遏制问题**（Rumor Containment problem）**实际上与**影响最大化问题(Influence Maximization)**息息相关。
> 
> 但谣言遏制问题是限制谣言的影响。下图中灰色的顶点是已感染的节点，白色顶点是未感染的顶点。如果只选一个顶点去阻止，那么选 u 这个顶点是最好的选择，可以纠正更多的被感染的点。对于 v 点，选它可以激活更多点，对于影响最大化问题来说是最佳选择。==突发奇想：能不能像森林防火一样挖一条 “防火带”，阻止谣言的传播？==
> 
> ![](rumor%20control.assets/image-20220519212932695.png)
> 
> 本文选取两种顶点集，来研究Rumor Correction Maximization problem，这两个集合分别为：seed nodes、boost nodes。
> 
> boost nodes：当boost nodes提前收到相关信息时，它们更有可能成为采用者(adopter)。然而，如果没有邻居的影响，它可能不会成为采用者。
> 
> **举个例子**：一家公司与其他公司竞争一个市场。它不仅可以为一些有影响力的用户提供免费的样品，也可以为一些个人提供传单。此外，传单的成本要比免费样品低得多。这家公司希望通过这两种策略获得最大的利润。
> 
> 在这种情况下，把拥有免费样品的用户视为seed nodes，把拥有传单的用户视为boost nodes。
> 
> 假设社会网络中存在两种信息，即谣言和真相，在社会网络中传播。我们假设谣言的传播过程已经停止，并且知道感染性节点。在给定预算的情况下，RCM问题要求种子节点和助推节点都能最大化预期的修正节点数量。

#### 3、传播模型

> **Boosting Independent Cascade (BIC) model**
> 
> 给定一个网络G=(V, E)，对于每条边$e_{uv}$有两种影响概率：$p_{uv}$ 和  $p_{uv}^\prime(p^\prime_{uv}\ge p_{uv})$。
> 
> 顶点有3种状态：infectious（如谣言接收者）、active（如真相接收者）、inactive。
> 
> 假设传播谣言的过程已经结束，令感染性节点的集合为R。给定一组真相节点 T，一组加速节点（boost nodes）B，则具体过程如下：
> 
> * t=0时刻，激活真相节点集 T。
> * $t \ge 1$时，每个新激活的顶点 u 只有一次机会去影响它的邻居（out-neighbor） v。如果 v 是boost node，它的邻居（in-neighbor）u 激活 v 的概率为 $p_{uv}^\prime$。否则，u 影响 v 的概率为$p_{uv}$。在 t 时刻以后，u 就不能再去影响其他顶点。
> * 循环上述过程，直至没有新的节点被激活。

#### 4、问题定义

> 给定感染顶点集R，真相集合T，加速节点集B，令$f_R(T,B)$为纠正顶点集R中的顶点数。因此有这样的问题：如何选择T和B，使$f_R(T,B)$在有限的预算下达到最大。称该问题为 Rumor Correction Maximization（RCM）problem。
> 
> 当T已知，目标函数的计算是#P-hard；
> 
> 给定R和T，找到大小为 k 的B，使得$f_R(T,B)$最大化，是NP-hard的问题，即Boosting Rumor Correction Maximization（BRCM）problem是NP-hard。
> 
> 且不同的B、T组合会有不同的结果，有指数级的情况。
> 
> **证明BRCM是NP-hard:**
> 
> ![image-20220523155117977](rumor%20control.assets/image-20220523155117977.png)
> 
> 从集合覆盖进行规约。设$U=\{u_1,u_2,..,u_n\}$为所有节点（全集），$S=\{S_1,S_2,..S_m\}$为子集合的集合。
> 
> 让节点 t 是真相集 T 的单子种子节点，谣言集$R=\{a_1,..,a_m,b_1,..,b_n\}$。
> 
> 点$a_i$对应集合$S_i$，点$b_j$对应点$u_j$。
> 
> 若$u_j\in S_i$，那么就有一条有限边从 $a_i$ 指向 $b_j$；
> 
> 我们观察到，集合覆盖问题等同于看这个图中是否有一个包含k个节点的boost set B，使得 $f_R(T,B)\ge n+k$。
> 
> *顶点* $a_i$ *就相当于 boost node set，也是谣言节点，因此有 f 大于等于 n+k*。

#### 5、近似算法

生成一个随机k-PRR(k-Potentially Reverse Reachable graph)图

> * 给定一个图G=(V,E)，一个点$r\in R$，整数k。
> 
> * 先构建一个确定的图$G^\prime$且对应每条边上的影响传播$e_{uv}\in E$。
> 
> * **live**:在$G^\prime$中，边$e_{uv}$是 live，对应的概率为$p_{uv}$。
> 
> * **live-upon-boost**：在$G^\prime$中，边$e_{uv}$是 live-upon-boost，对应的边的概率为$p^\prime_{uv}-p_{uv}$。
> 
> * **blocked**：在$G^\prime$中，边$e_{uv}$是 blocked，对应的边的概率为$1-p^\prime_{uv}$。
> 
> * **k-PRR graph:** 是$G^\prime$的子图，包含介于 T 和 r 之间的顶点的所有路径，且都是 non-blocked 的边，每条路径至多 k 个 live-upon-boost 边。
> 
> * 如果 r 是从 R 中随机选取的，就称其为 random k-PRR graph。
> 
> * 称一条路径是 *live*：当这条路径上的边都是 live 的。
> 
> * 称一条路径是 *live-upon-boost*：该路径不是 live，但这条路径上的边是 live 或者是 live-upon-boost。
>   下图是一个 7个点6条边的图。r 是感染点，真相节点$T=\{t_1,t_2,t_3\}$。其中 live、live-upon-boost 和 block 边分别用实线、虚线、带x的点线表示。方框中表示一个 2-PRR图，路径 $t_1$到 r 是 *live-upon-boost*。
>   
>   ![image-20220521162853236](rumor%20control.assets/image-20220521162853236.png)
> 
> * $d[v]$：所有点 v 至 点 r 的路径中，live-upon-boost 边的数量的最小值。
> 
> * $N^+(v)$：顶点 v 的 in-neighbors。
> 
> * $N^-(v)$：顶点 v 的out-neighbors。
> 
> * 如果边$e_{uv}$是 live-upon-boost，$weight[e_{uv}]=1$，否则$weight[e_{uv}]=0$。
> 
> * *就是使用了广度优先的方法，更新 d[u] 的值，并且其小于 k 时，将边放入 g 中。*
> 
> ![image-20220521165316540](rumor%20control.assets/image-20220521165316540.png)

假设真相集T是已知的，并且k-PRR图的数量θ足够大。使用贪心算法获得次模下界$f_R^-(T,B)$的近似解。在每个迭代中，它选择具有最大边际覆盖率的节点。之后的算法3会调用该算法。

> * $\Phi_g=\{v\in V:I^-_g(\{v\})-I^-_g(\emptyset)=1\}$：即对于$v \in \Phi_g$，g 为 k-PRR图，存在一条 live upon boosting v的路径。
> * 用$\mathcal{G}$表示k-PRR 图的集合，$|\mathcal{G}|=\theta,\mathcal{G}=\{g_1,g_2,..,g_\theta\}$，相应的有$\Phi=\{\Phi_{g_1},\Phi_{g_2},..,\Phi_{g_\theta}\}$
> 
> ![image-20220521170723355](rumor%20control.assets/image-20220521170723355.png)

为了最小化运行时间，使用一个近似的解决方案。其基本思想见于算法3。它首先根据k-PRR图创建两个集合$\Phi_1$和$\Phi_2$。接下来，根据Algorithmm2得到一个集合$B_L$，它是$\Phi_1$的最大覆盖集合。接下来，使用集合$B_L$的下限和最优解$B^∗_L$的上限之间的分数来计算近似比率。下限和上限分别由$\Phi_2$和$\Phi_1$产生。如果比率小于$1 -1/e -\epsilon$，它就向$\Phi_1$和$\Phi_2$插入新的集合。否则，它返回结果。

> ![image-20220521201856817](rumor%20control.assets/image-20220521201856817.png)
> 
> ![image-20220524111704596](rumor%20control.assets/image-20220524111704596.png)
> 
> ![image-20220522111615067](rumor%20control.assets/image-20220522111615067.png)
> 
> ![image-20220524105625756](rumor%20control.assets/image-20220524105625756.png)

整合影响反向采样（Influence Reverse Sampling，RIS）技术和三明治近似（sandwich approximation，SA）策略得到算法4。使用算法3，我们首先得到一个k-size 的结点集$B_L$。此外，我们只用$\Psi_1$和$\Psi_2$来代替算法3中的$\Phi_1$和$\Phi_2$。然后，我们可以有其他节点集$B_U$。我们选择在$\Psi_1$中具有最大覆盖率的 top k 节点作为原始问题的解决方案$B_O$。最后，在$B_O$、$B_L$和$B_U$三个集合中，我们返回具有最大估计的谣言修正的集合作为最终解决方案。

> ![image-20220521202903654](rumor%20control.assets/image-20220521202903654.png)

在大多数情况下，我们不知道seed nodes和boost nodes的确切数量。因此，我们希望研究在seed 和 boost 上分配预算的策略。给定一个参数$\alpha \in [0, 1]$，我们在下文中提出最小种子选择（MSS）问题。该参数代表了真相集 T 所纠正的感染性节点的最小部分。MSS问题试图给出真相集 T 的最小尺寸，使 T 能够纠正至少 $\alpha-|R|$ 个感染节点。

> RR：Reverse Reachable。
> 
> S：RR集的集合。
> 
> $\Lambda_S(T)$：T 所覆盖的 S 中的 RR集的比例。是对$f_R(T)$的无偏估计(unbiased estimation)。
> 
> ![image-20220522113033011](rumor%20control.assets/image-20220522113033011.png)
> 
> ![image-20220521204443720](rumor%20control.assets/image-20220521204443720.png)

## Containment of rumor spread in complex social networks

**遏制复杂社会网络中的谣言传播**
Yang L, Li Z, Giua A. Containment of rumor spread in complex social networks[J]. Information Sciences, 2020, 506: 113-130.

#### 1、名词概念

prevalence：[n]流行，流行程度

heterogeneity:[n]异质性

counterexample：[n]反例

##### 纳什均衡 Nash equilibrium

> 又称非合作博弈均衡。在一个博弈过程中，无论对方的策略选择如何，当事人一方都会选择某个确定的策略，则该策略被称作支配性策略。如果两个博弈的当事人的策略组合分别构成各自的支配性策略，那么这个组合就被定义为纳什均衡。　　
> 
> 一个策略组合被称为纳什均衡，当每个博弈者的均衡策略都是为了达到自己期望收益的最大值，与此同时，其他所有博弈者也遵循这样的策略。
> 
> 典型情况：囚徒困境

#### 2、关于本文

> 两种策略：
> 
> 1. 网络中断（删除某些重要的点、边）：<mark>实际应用中不太可行</mark>。干扰网络结构对控制者来说不太可能。删除关键节点是一种审查形式，可能违反道德标准。
> 
> 2. 平衡策略（释放正确信息来抵消负面影响）：该策略是本文所采取的。
> 
> 传播模型：
> 
> 传统的传播模型不太适用于存在竞争性信息传播的情况。通常假设竞争者的播种策略已经固定，并且是已知的。在所有竞争者都可能调整其战略的情况下，人们从博弈论的角度提出了纳什均衡分析。
> 
> **“我们不研究竞争性影响最大化问题，而是通过选择一组合适的节点，在检测到谣言后传播真相，来解决谣言传播最小化的问题。”**(讲这么久才说)
> 
> 对于其他人提出的谣言、真相同时传播的模型，有的是优先接收谣言，有的是优先接收真相，接收的概率不是0就是1，**不太符合实际情况**。
> 
> 此外，所有提到的竞争性扩散模型都假定，一旦一个人被一种类型的信息激活，他/她就会永远保持这种状态，永远不会改变他/她的想法。这个假设对与购买行为相关的产品采用很有效，因为购买行为通常不容易逆转，但对信息传播或意见形成却不适用，因为人们对某一政治活动或新闻事件的态度会根据从网络上收集到的新信息而改变。
> 
> <mark>本文基于线性阈值模型进行改进：</mark>
> 
> Linear Threshold model with One Direction state Transition (LT1DT for short)
> 
> 1. 两种阈值：influence threshold和decision threshold，分别用于激活inactive node和转化rumor activated node。
> 
> 2. 允许对已经接受谣言的节点进行重新考虑（成为真相节点），但不允许对已经接受真相的节点进行重新考虑。
> 
> <mark>采用平衡策略的最小化谣言传播问题是NP-hard</mark>
> 
> 提出了一个启发式算法*ContrId*，并于pagerank 和 贪心法进行比较。
> 
> <mark>研究接近效应</mark>
> 
> 在谣言节点周围放置真相节点的效果。

#### 3、传播模型

> Linear Threshold model with One Direction state Transition (LT1DT for short)
> 
> * **LT1DT网络N是一个4元组（4-tuple），$(G(V,E),W,\theta,\theta^R)$。**
> 
> > $G(V,E)$是一个有向图；
> > 
> > 函数$\theta,\theta^R$是$V\rightarrow(0,1]$的映射，为$u\in V$中的点分配阈值，influence threshold $\theta_u\in(0,1]$(被影响的概率)，decision threshold $\theta_u^R\in(0,1]$(被影响后发生改变的概率)；
> > 
> > 函数$W$是$V\times V\rightarrow (0,1]$的映射，为图中的边分配权重，$W(u,v)\in(0,1]$,
> 
> 
> 
> $$
> \left\{
\begin{aligned}
&W(u,v)=0,(u,v)\notin V \\
&\sum_{u\in V}W(u,v)=1,\text{for all }v\in V
\end{aligned}
\right.
> $$
> 
> 
> 
> 
> * **扩散动力（diffusion dynamic）**
> 
> > 每个节点有3种状态：inactive、R-active（adopting R）、T-active（adopting T），一个转移状态：influenced。*（R、T代表两种观点、事物，如谣言和真相）*
> > 
> > $S_R$：表示t=0时接收R的顶点集。
> > 
> > $\phi_t^T$：表示t时刻接收T的顶点集。
> > 
> > $\Phi_t^T=\bigcup_{k=0}^t\phi^T_k$：表示$[0,t]$这段时间内接收T的顶点集。
> > 
> > $\phi_t^{R\rightarrow T}$：表示t时刻从R-active转变为T-active的顶点集。
> > 
> > $\Phi_t^R=\bigcup_{k=0}^t\phi_k^R /\bigcup_{k=0}^t\phi_t^{R\rightarrow T}$:表示t时刻，在$[0,t]$这段时间内接收R且没发生转变的顶点集。
> > 
> > $\Phi_t=\Phi_t^T\cup \Phi_t^R$：在t时刻为激活状态的顶点集，$\Phi_0=S_R\cup S_T$。
> 
> ![](assets/2022-08-28-20-58-05-image.png)
> 
> * **激活流程（activation process）**
> 
> > influence stage：未激活的点u的已激活的入邻居（active in-neighbors）权重之和，大于等于$\theta_u$，那么点u就变为 influenced。*(决定是否进入激活状态)*
> 
> $$
> \text{u is influenced}\Leftrightarrow \sum_{v\in N_u^{in}\cap\Phi_{t-1}}W(v,u)\ge \theta_u
> $$
> 
> $$
> u\in \phi_t^R \Leftrightarrow 
\frac{\sum_{v\in N^{in}_u \cap \Phi_{t-1}^R}W(v,u)}
{\sum_{v\in N^{in}_u \cap \Phi_{t-1}}W(v,u)} \ge \theta_u^R
> $$

> > decision stage：顶点 u 的 R-active in-neighbors 的权重之和比上顶点u的 active in-neighbors 的权重之和，大于等于\theta_u^R，那么顶点u就会接收 R。**否则接收T**，u\in \phi_t^T。
> > 
> > **~~发现一个问题：假设 node A 达到了 influence threshold，其邻居都是 R-active，没有 T-active。但没有达到 decision threshold，即 node A 会接收 T。但这合理吗？其周围没有 T-active邻居，却能变成 T-active？~~** (感觉又没问题了。。。)
> 
> * **系统动态分析(Analysis of the system’s dynamics)**
> 
> > $\Phi_R^*(S_R,S_T)$：最终（稳定状态）接收 R 的顶点集合 *(相当于一个集合函数 )*。
> > 
> > $\Phi_T^*(S_R,S_T)$：最终（稳定状态）接收 T 的顶点集合 *(相当于一个集合函数 )*。
> > 
> > $\Phi^*(S_R,S_T)$：最终处于激活状态的顶点集合 *(相当于一个集合函数)*。
> > 
> > **上述的表达式是关于初始种子节点的选取对最终激活节点的影响。**
> > 
> > 给定了$S_R$，那么$|\Phi^*(S_R,S_T)|$和$|\Phi_T^*(S_R,S_T)|$就是关于$S_T$递增的,单调的；但对于$|\Phi_R^*(S_R,S_T)|$而言，就不一定是递减的，是非单调的，因为增加 T 的种子节点并不一定能减少 R 的扩散。
> > 
> > ![](assets/2022-08-29-20-51-27-image.png)
> > 
> > 上图展示了一个反例。
> > 
> > 设$S_R=\{1\},W(u,v)=\frac{1}{|N_v^{in}|}$,$\theta_2,\theta_3 \in (0.5,1],\theta_5 \in (0,0.5),\theta_2^R,\theta_3^R\in(0,0.5),\theta_5^R\in(0.5,1]$
> > 
> > 不设置T时：$\Phi_R^*(S_R,\emptyset)=\{1,2,5,6\}$；
> > 
> > 设置 $S_T=\{6\}$时：$\Phi_R^*=\{1,2\},\Phi_T^*=\{5,6\}$，减小了 R 的扩散；
> > 
> > 设置 $S_T=\{4\}$时：$\Phi_R^*=\{1,2,5,6,3\}，\Phi_T^*=\{4\}$,节点3从节点4获得额外的影响，但因为decision threshold，采用了 R，扩大了R的影响。

#### 4、问题定义

> * 谣言最小化传播(Minimizing rumor spread,MRS)
> 
> > 谣言遏制的问题是选择一组合适的节点来传播真相，以尽量减少最终接受谣言的节点数量。
> > 
> > *给定 LT1DT 模型，谣言种子节点 $S_R$。给定整数 ，在 $V/S_R$中找到真相种子节点 $S_T=X$,满足$|S_T|\le k$，使得最终 R 接收者数量最小。*
> 
> $$
> \begin{array} {}
\min |\Phi_R^*(S_R,X)| \\
\text{s.t. } X \subseteq V/S_R \\
|X|\leq k
\end{array}
> $$

> * 从最大覆盖问题(Maximum Coverage Problem,MCP)归约到本问题。
> 
> > $MCP\le MRS$
> > 
> > 按照MCP的定义构建了一个MRS的实例。
> > 
> > **MCP**:集合 $O=\{o_1,o_2,\dots,o_q\}$ 含有 q 个元素, 集合的集合$\mathcal{X}=\{X_1,X_2,...,X_p\}$,其中$X_i$是元素为$o_j\in O$的集合。给定一个正的常数 $l$，找到一个 $\mathcal{X}^\prime \subset \mathcal{X}$, 满足$|\mathcal{X}^\prime|\le l$, 使得$|\bigcup_{X_i\in \mathcal{X}^\prime}X_i|$覆盖 $O$ 中的元素数量最大。
> 
> $$
> \begin{array}{}
\max |\bigcup_{X_i\in \mathcal{X}^\prime}X_i| \\
\text{s.t. } \mathcal{X}^\prime \subset \mathcal{X} \\
|\mathcal{X}^\prime|\le l
\end{array}
> $$
> 
> 归约证明：
> 
> ![](assets/2022-08-30-15-36-15-image.png)
> 
> 给定MCP的一个实例$\mathcal{I}=(O,\mathcal{X},l,\lambda)$,相应地构建一个MRS实例$\mathcal{M}=(V,E,\theta,\theta^R,W,S_R,k,\rho)$。
> 
> 编号从0开始（图示是从 1 开始，可能原文有误），为每个子集 $X_i\in \mathcal{X}$ 添加一个节点 $u_i$, 为$O$中的每个元素添加一个节点$o_j$,以及一个特殊节点 x 。
> 
> 然后将 x 连接到每个节点$o_j$，并为每个$o_j∈X_i$添加一条边$(u_i,o_j)$。
> 
> 以节点$o_3$为例，它至少有3条入射边(来自$u_1,u_2,u_p$)，这意味着$o_i$至少存在于相应的子集$X_1 , X_2 , X_p$中。
> 
> 每个节点 $o_i$ 给定了相同的influence threshold $\theta_{o_i}=1/q$ 和 decision threshold $\theta_{o_i}^R = \frac{d_{o_i}}{q-1}$, 正整数$d_{o_i}$为元素$o_i$所属的子集$X_i$的数量。
> 
> 从节点x到节点$o_i$的弧的权重被设定为1/q，即$W(x,o_i)=1/q$。从$u_j$到$o_i$的弧的权重是同质的，设置为$（1 -1 /q ）/d_{o_i}$，即$W(u_j,o_i)=(1-1/q)/d_{o_i}$。然后，对于每个$o_i$，从x和$u_j$传入的权重之和为1。
> 
> 最后设置$S_R=\{x\},k=l,\rho=q-\lambda+1$。
> 
> <mark>证明：</mark>
> 
> 假设$\mathcal{X}^*$是实例$\mathcal{I}$的一个解，$|\mathcal{X}^*|\le l$，能够覆盖$O$中至少$\lambda$个元素。我们可以选择对应于子集$X_j∈\mathcal{X}^∗$的所有节点$u_j$作为真相种子集$S_T$,因此$|S_T|=k=l$。
> 
> 因为$\mathcal{X}^*$可以覆盖$O$中至少$\lambda$个$o_i$元素,即$O$中至少有$\lambda$个节点相信真相。这是因为对于任何被覆盖的$o_i$，让$d^∗_{o_i}$为$o_i$所属的子集$X_j∈\mathcal{X}^∗$的数量，那么我们有$1 ≤d^∗_{o_i} ≤d_{o_i}$。
> 
> 那么，来自谣言和真相的总影响为$1/q+d^*_{o_i}(\frac{1-1/q}{d_{o_i}})\ge \theta_{o_i}=1/q$。来自其R-active邻居的权重之和为1/q。因此$o_i$会相信真相，因为
> 
> $$
> \frac{1/q}{1/q+d^*_{o_i}(\frac{1-1/q}{d_{o_i}})}
\le \frac{1/q}{1/q+\frac{1-1/q}{d_{o_i}}}
= \frac{d_{o_i}}{d_{o_i}+q-1}
< \theta^R_{o_i}= \frac{d_{o_i}}{q-1}
> $$

> 因此，在MRS问题中，T-final adopter set的基数至少是λ+ k，R-final adopter set的cardinality最多是ρ= q -λ+ 1。
> 
> **反之**，假设$S_T^*$是实例$\mathcal{M}$的一个解，即，$|S^∗_T| = k$，这样R-final adopter 集的基数最多为$\rho$。这意味着T-final adopter集合的基数至少是$q-(\rho-1)+k$。那么$\mathcal{X}^∗$可以是一个子集$X_i$的集合，对应于那些$u_i∈S^∗_T$。因此，$\mathcal{X}^∗$的大小为k，因为根据假设，$l = k$，并且至少可以覆盖$O$中的$q -\rho+ 1$个元素。

#### 5、启发式算法

> 根据选择 truth seed 的搜索空间，它们可以分为两类，无约束(unconstrained)和有约束(constrained)。
> 
> **unconstrained:** 可在$V/S_R$中根据具体的判定，选择任意点作为 truth seed。
> 
> * MinGreedy
> 
> > ![](assets/2022-08-30-21-37-50-image.png)
> 
> > 在每个迭代中，将最大限度地减少谣言传播的节点u添加到真相种子集$S_T$中（第5行）。
> > 
> > 在每个迭代中，对于每个候选节点$w∈V/S_R$，需要计算相应的final adopter集合，这可能需要检查每个节点是否被激活，这可以在$O ( nd )$ 的时间内完成。因此，MinGreedy的时间复杂性为$O ( kdn^2 )$。
> 
> * PageRank
> 
> $$
> \textbf{p}=(1-\gamma)\hat A \textbf{p} + \frac{\gamma}{n} \textbf{1}
> $$

> > [知乎文章](https://zhuanlan.zhihu.com/p/137561088#:~:text=PageRank%E7%AE%97%E6%B3%95%E7%9A%84%E5%9F%BA%E6%9C%AC%E6%83%B3%E6%B3%95%E6%98%AF%E5%9C%A8%E6%9C%89%E5%90%91%E5%9B%BE%E4%B8%8A%E5%AE%9A%E4%B9%89%E4%B8%80%E4%B8%AA%E9%9A%8F%E6%9C%BA%E6%B8%B8%E8%B5%B0%E6%A8%A1%E5%9E%8B%EF%BC%8C%E5%8D%B3%E4%B8%80%E9%98%B6%E9%A9%AC%E5%B0%94%E5%8F%AF%E5%A4%AB%E9%93%BE%EF%BC%8C%E6%8F%8F%E8%BF%B0%E9%9A%8F%E6%9C%BA%E6%B8%B8%E8%B5%B0%E8%80%85%E6%B2%BF%E7%9D%80%E6%9C%89%E5%90%91%E5%9B%BE%E9%9A%8F%E6%9C%BA%E8%AE%BF%E9%97%AE%E5%90%84%E4%B8%AA%E7%BB%93%E7%82%B9%E7%9A%84%E8%A1%8C%E4%B8%BA%E3%80%82,%E5%9C%A8%E4%B8%80%E5%AE%9A%E6%9D%A1%E4%BB%B6%E4%B8%8B%EF%BC%8C%E6%9E%81%E9%99%90%E6%83%85%E5%86%B5%E8%AE%BF%E9%97%AE%E6%AF%8F%E4%B8%AA%E7%BB%93%E7%82%B9%E7%9A%84%E6%A6%82%E7%8E%87%E6%94%B6%E6%95%9B%E5%88%B0%E5%B9%B3%E7%A8%B3%E5%88%86%E5%B8%83%EF%BC%8C%E8%BF%99%E6%97%B6%E5%90%84%E4%B8%AA%E7%BB%93%E7%82%B9%E7%9A%84%E5%B9%B3%E7%A8%B3%E6%A6%82%E7%8E%87%E5%80%BC%E5%B0%B1%E6%98%AF%E5%85%B6PageRank%E5%80%BC%EF%BC%8C%E8%A1%A8%E7%A4%BA%E7%BB%93%E7%82%B9%E7%9A%84%E9%87%8D%E8%A6%81%E5%BA%A6%E3%80%82)
> > 
> > 使用 teleportation model 计算PageRank value。（即对于没有出度的点，使其出度的概率为1，如下图中的 m 点）
> > 
> > ![](assets/2022-08-31-20-28-12-ab8839d4a4c31921787bfe3e170bcea7_985935-20200206231904537-329829314.png)
> > 
> > 带重启的随机游走,每一步选择相邻节点，或者开始节点,重启概率 $\gamma=0.15$。$\textbf{p}$ 为 PageRank向量，$\sum_{i=1}^n p_i=1$，$p_i$为节点 i 的pagerank value。$\textbf{1}$为所有分量为 1 的向量。*(文章没有给初始的 P，但我感觉每个点的初始值应该相同，即 1/N，N为顶点总数。)*
> > 
> > ![](assets/2022-08-31-16-33-31-image.png)
> > 
> > $\hat A(i,j)=A(i,j)/(\textbf{1}^T A(:,j))$ 。$\hat A$是邻接矩阵 A 的缩放,即对应元素除以该列之和，也就是<mark>百分比，就是个状态转移矩阵</mark>。原文（如上图）对$\hat A$的定义感觉不太严谨，因该加个括号。
> > 
> > PageRank在$V/S_R$中选择了 k 个具有最高pagerank值的节点作为真相种子。
> > 
> > 由于缩放的邻接矩阵$\hat A$是一个稀疏矩阵，每行平均有d个非零元素（所谓的网络平均度），矩阵和向量的乘法可以在 $O ( nd )$ 的时间内完成。
> > 
> > 因此，pagerank值的计算需要时间$O(n(d+1)I)$，其中I是p收敛到合理近似值的迭代次数。最终需要选 k 个真相点，因此时间复杂度为$O(n(d+1)I+nk)$。
> 
> * ContrId
> 
> > PageRank完全取决于网络结构。作者提出了一种新的启发式方法ContrId（Contributors Identification），它基于谣言传播的动态，试图识别哪些节点对谣言传播贡献最大（称为贡献者），并中断谣言从谣言种子传播到其余网络的重要路径。
> > 
> > 在 $t_v$ 时刻被激活的节点 v 的 contribution ，定义为其在任何 $t > t_v $ 被激活的外邻的数量。
> > 
> > 首先模拟谣言传播，谣言种子集$S_R$，真相种子集$S_T=\emptyset$，记录从$1\sim T_s$每一步激活的节点集，$T_s$为网络进入最终稳定状态的时刻。令$L$为最长 simple path 的长度，有$T_s \le L$，因为扩散过程至多 L steps。对于每个点 $v\in \phi_t^R$，有
> 
> $$
> Ctr(v)=|(\cup_{i=t+1}^{T_s}\phi_i^R)\cap N_v^{out}|
> $$
> 
> > 对于 inactive 节点，贡献设置为 0 。
> 
> **Constrainted**：约束版本（称为ProxMinGreedy、ProxPageRank和ProxContrId），将搜索空间限制在谣言种子集的附近。
> 
> $S_R-\text{proximity space}$：$\mathcal{N}^{out}(S_R)=(\cup_{v\in S_R}N_v^{out})$
> 
> 其思路是阻断从谣言种子到剩余网络的有影响力的路径。
> 
> * ProxMinGreedy
> 
> > 每次迭代中，在$\mathcal{N}^{out}(S_R)$中选最大限度地减少谣言传播的节点u添加到真相种子集$S_T$中，共选k个点。算法还是algorithm 1，只是第5行换成：
> 
> $$
> u=\mathop{argmin}\limits_{i\in \mathcal{N}^{out}(S_R)}
|\Phi_R^*(S_R,S_T\cup \{i\})|
> $$

> * ProxPageRank
> 
> > 同PageRank，只是在$\mathcal{N}^{out}(S_R)$中选k个PageRank value最高的点作为 truth seed。
> 
> * ProxContrId
> 
> > 同 ContrId，只是在$\mathcal{N}^{out}(S_R)$选 k 个 Ctr 值最高的点作为 truth seed。
> 
> ![](assets/2022-09-01-17-00-54-image.png)

#### 6、实验

> 数据集：2个合成网络、2个真实网络
> 
> * 合成网络：
> 
> > scale-free network:采用 Barabási-Albert model *(A.L. Barabási , R. Albert , Emergence of scaling in random networks, Science 286 (5439) (1999) 509–512 .)* 生成500个顶点的网络。
> > 
> > Small-world network：小世界网络是指大多数节点与其他节点没有联系，但某一节点的邻居有可能相互联系的网络。此外，网络中的大多数节点可以通过几步或几跳到达任何其他节点。通过采用Watts-Strogatz模型[(详情)](https://wiki.swarma.org/index.php/WS%E5%B0%8F%E4%B8%96%E7%95%8C%E6%A8%A1%E5%9E%8B_Watts%E2%80%93Strogatz_model) *(D.J. Watts , S.H. Strogatz , Collective dynamics of ’small-world’ networks, Nature 393 (6684) (1998) 4 40–4 42 .)*，并将规则格子的平均度数设定为4，重布线概率$β=0.2$，生成了一个有500个节点的小世界网络。
> > 
> > ![](assets/2022-09-01-20-23-29-7f08b0c5862a3505b1ea66b1553713a4_Algorithm-of-Watts-Strogatz-model-which-can-be-tuned-by-parameter-p-0-1.png)
> 
> * 真实网络
> 
> > NetScience、US-power
> 
> ![](assets/2022-09-01-20-49-51-image.png)
> 
> * 参数
> 
> > 权重 $W(u,v)=1/|N_v^{in}|$; $\theta_u,\theta_u^R$ 在$(0,1]$间均匀随机(uniformly at random);$|S_R|=3$,$|S_T|\in[1,10]$。
> 
> * 结果
> ![](assets/2022-09-01-21-07-01-image.png)
> ![](assets/2022-09-01-21-11-28-image.png)
> 
> ![](assets/2022-09-01-21-28-19-image.png)
> 
> ![](assets/2022-09-01-21-35-08-image.png)
> 
> 综合以上结果图，就效果而言，有$\text{Greedy}\ge \text{ContrId} \ge \text{PageRank}$，PageRank更适合用于影响最大化的问题。
> 
> * 运行时间
> 
> ![](assets/2022-09-01-21-36-40-image.png)
> 
> * 放缩性
> 
> ![](assets/2022-09-01-21-41-23-image.png)

#### 7、未来的研究思路

> 1. 由于人类活动的异质性，影响从一个人传播到他的朋友可能有一定的时间延迟，而且个人之间的影响也可能随着时间的推移而衰减。
> 
> 2. 另一个有趣的话题或趋势是分析有符号的社会网络(signed social network)中的扩散动态，即弧线(arc)与正(positive)或负(negtive)符号相关的网络。社会个体有可能与他们的朋友（与正弧连接）做出相同的决定，而与他们的敌人（与负弧连接）做出相反的决定。



## Fast controlling of rumors with limited cost in social networks
**以有限的成本快速控制社交网络中的谣言**
Yao X, Gu Y, Gu C, et al. Fast controlling of rumors with limited cost in social networks[J]. Computer Communications, 2022, 182: 41-51.

#### 1、名词概念

extent: [n] 程度，范围，长度
conduct: [n] 开展，指挥，举办
contagion: [n] 传染
state-of-the art: [n] 最先进的事物 [adj]最先进的
acnode：[n] 孤立点
  ##### 优化问题（optimization problem）
>  优化问题的本质是要选择一组变量或参数，满足一系列有关的约束条件下，使设计目标达到最优值。
>  最优化问题一般由三个要素构成：
>  1. 决策变量（decision variable）:  $x=(x_1,x_2,...,x_n)^T \in R^n$,表示在最优化问题中要求解的变量。
>  2. 目标函数（object function）：$f:R^n \rightarrow R$, 表示需要最大化或最小化的表达式。是最终需要优化的函数，同样也是决策变量 x 的函数。
>  3. 约束条件（constraint）: $c_i:R^n \rightarrow R$, 表示需要满足的==等式==条件或者==不等式==条件。

##### sharp-p 问题（#-p）
> 在计算复杂性理论中，复杂性类#P（"sharp P"，或者， "number P " 或 "hash P"）是与集合NP中的决策问题相关的计数问题的集合。
> 换言之，对于一个NP问题，不是去问有没有，而是问有多少，就会转化为一个 sharp-p 问题。[来源](https://www.douban.com/group/topic/12959835/?_i=4886251Q6j1nw_)


#### 2、关于本文
>谣言控制可以分成 3 类：
>1. 移除用户之间的联系以阻断谣言。*( Removing associations between users to block rumors)*
>2. 封禁被（谣言）影响的用户。*( Blocking influential users)*
>3. 传播真相来澄清谣言。*( Spreading truth to clarify rumors)*
>
>**但大多数研究都只采用一种方法来控制谣言。**
>本文提到**对不同的人采用不同的方法**，如：
>* 接收谣言又传播谣言者，封。
>* 容易被谣言影响者，给他真相或者阻断它接受信息。
>* 不容易被谣言影响者，只需打个标签(tag)，跟踪后续。
>
>因此对用户进行分类。怎么分？文章提出`contact coefficient`对用户进行分类。
>一些标记：
>![](assets/Pasted%20image%2020220929205905.png)

#### 3、其他
> 1. C.J. Kuhlman 等人提到了移除edge来阻止谣言扩散。
> 	Kuhlman C J, Tuli G, Swarup S, et al. Blocking simple and complex contagion by edge removal[C]//2013 IEEE 13th International Conference on Data Mining. IEEE, 2013: 399-408.  [链接](https://ieeexplore.ieee.org/document/6729524)
>2. G. Tong 等人提出随机近似算法 randomized approximation algorithm，说是比现有的方法在时间上更快。
>   Tong G, Wu W, Guo L, et al. An efficient randomized algorithm for rumor blocking in online social networks[J]. IEEE Transactions on Network Science and Engineering, 2017, 7(2): 845-854. [链接](https://ieeexplore.ieee.org/abstract/document/8194896)
>

#### 4、传播模型
>基于独立级联模型的改进——多概率独立级联模型(multi-probability independent cascade model，MPIC)
>顶点的状态有2种：True or False
>$$
>\left\{
>	\begin{aligned}
>	&\text{True},v \text{ is influenced by rumors} \\
>	&\text{False},v \text{ is not influenced by rumors}
>	\end{aligned}
>\right.
>$$
>
>顶点分成 5 类：$H_i(i\in\{1,2,3,4,5\})$
>* $H_5$：表示删除用户账户的集合。
>* $H_4$：表示传播真相的集合。
>* $H_3$：阻断获取信息的集合。
>* $H_2$：标记用户的集合。
>* $H_1$：不需要采取行动的集合。
>
>处于$H_5$中的用户无法接受/传播谣言，其他处于$H_1 \sim H_4$的用户可以被谣言影响，只是概率不同。
>由于$H_5$直接删号了，因此对于$H_1 \to H_4$，共有4种阻断影响率(blocking influence rates)，用$\alpha_i(i\in \set{1,2,3,4})$表示。
>**定义：**$0\le \alpha_1 <\alpha_2 <\alpha_3 <\alpha_4 <p_{(u,v)} \le 1$。其中$p_{(u,v)}$表示在不采取任何措施时，点u对点v的影响概率。采取措施后的概率如下：
>![](assets/Pasted%20image%2020220928170156.png)
>
>
>传播过程如下：
>1. t=0 时，k 个点为谣言节点(True nodes)，其他 (n-k)个点为 False nodes，分属于各自的类别。
>2. $t\ge 1$时，u 在 t 时刻被谣言影响，那么它可以通过影响概率 $g_{(u,v)}$ 去影响邻居 v。如果 u 成功影响了，那么 v 在 t+1 时刻成为 True node，并且它的 v 状态就不会再发生改变了。否则 v 只能被 t 时刻之后的其他 rumor 节点影响。
>3. 最后，没有节点可以再被影响。
>
>**具体例子如下：**
> 总共 9个点，初始时 $v_5,v_9$ 为True node。
> 假设每条边的影响概率为 $p_{(u,v)}=1$，令 $\alpha_1=0.1,\alpha_2=0.2,\alpha_3=0.3,\alpha_4=0.4$。
> $H_{t,i}$ 表示 t 时刻属于 $H_i$ 的用户的*集合*。
> 假设$H_{0,1}=\set{v_2,v_7},H_{0,2}=\set{v_3,v_8},H_{0,3}=\set{v_1,v_6},H_{0,4}=\set{v_4},H_{0,5}=\set{v_5,v_9}$。
> * t = 0 时，$v_5,v_9$ 会以 ($1-\alpha_4=0.6$)的概率去影响 $v_4$ ; $v_5$ 会以 ($1-\alpha_3=0.7$) 的概率去影响 $v_1$ 和 $v_6$ 。
> * t = 1 时，$v_4,v_6$ 被 $v_5$ 成功激活, 删掉 $v_5,v_9$ ，令$H_{1,5}=\set{v_4,v_6}$ 。令 $H_{1,2}=\set{v_2,v_7},H_{1,3}=\set{v_3,v_8}$，$H_{1,1}=\set{v_1},H_{1,4}=\emptyset$ 。因为 $v_1$ 是孤立点，不会去影响其他点；而 $v_6$ 将尝试以概率 ( $1-\alpha_3=0.7$) 去影响 $v_3,v_8$ 。
> * t = 2 时，$v_8$ 被 $v_6$ 成功影响，删掉 $v_4,v_6$ ，
>   令$H_{2,5} = \set{v_8},H_{2,3}=\set{v_7},H_{2,1}=\set{v_1,v_2,v_3},H_{2,2}=H_{2,4}=\emptyset$ 。 $v_8$ 将尝试以概率 ( $1-\alpha_3=0.7$) 去影响 $v_7$ 。
>   * t = 3 时，$v_7$ 没有被 $v_8$ 影响，删除 $v_8$ ，此时再没有点可被影响，传播结束。
>![](assets/Pasted%20image%2020220928163716.png)
>
>**那么用户是怎么分类的？** 接触系数 *contact coefficient*
> t 时刻点  $v_j$  的接触系数定义如下：
> $$
> \beta_{t,j} = \omega_1 x +\omega_2 y + \omega_3 z + \omega_4 \lambda
>$$
>  $\omega_1 \sim \omega_4$  为给定的权重系数，x 表示节点 $v_j$ 的第一跳的 True node 数量，y 为第二跳的 True node 数量，z 为第三跳 True node 数量。对于第四跳或更多，$\lambda$ 定义为:
>  $$
>  \lambda = \left\{
>  \begin{aligned}
>  & 0, \text{ no True node in it's 4th or more hops} \\
>  & 1, \text{ have True node in it's 4th or more hops}
>  \end{aligned}
>  \right.
>  $$
>  这个 *“跳数”* 就是走几步能到的点。如果 $v_j$ 是一个孤立的点，则$\beta_{t,j}=0$ 。
>  
>  有了这个评价指标，要界定区分边界。令 $\theta_1,\theta_2,\theta_3(0\le \theta_1 < \theta_2 < \theta_3)$ 为分界点，==其中一个目标就是找到分界点。==分类规则如下：
>  ![](assets/Pasted%20image%2020220929201200.png)
>  **具体例子如下：**
>  黑点表示 True node 。设 $\omega_1 =2 ,\omega_2=1,\omega_3=0.5,\omega_4=0.1,\theta_1 = 0.9,\theta_2 = 1.9,\theta_3 = 3.5$ 。
>  * t = 0 时，$v_5,v_9$ 为 True node，则$H_{0,5} = \set{v_5,v_9}$ 。
>    $\beta_{0,4} = \omega_1\cdot 2 + \omega_2 \cdot 0 +\omega_3 \cdot 0 + \omega_4 \cdot 0 = 2\times 2=4$  ;
>    $\beta_{0,1}=\beta_{0,6} = 2 \times 1 +1 \times 1 = 3$ ; *( 这里原文中写错了 )*
>    $\beta_{0,3}=\beta_{0,8} = 1,5$ ;
>    $\beta_{0,2}=\beta_{0,7} = 0.6$ .
>    分类结果如图 (a-3)所示。因此有$H_{0,1}=\set{v_2,v_7},H_{0,2}=\set{v_3,v_8},H_{0,3}=\set{v_1,v_6},H_{0,4}=\set{v_4},H_{0,5}=\set{v_5,v_9}$ 。
>    
>  ![](assets/Pasted%20image%2020220929201326.png)

#### 5、问题定义
> **快速控制谣言问题（Fast Controlling Rumor problem, FCR）**:
> >给定 n 个点的图 G ，k 个 True nodes，影响概率 $p_{(u,v)}$ , 阻断影响率  $(\alpha_1,\alpha_2,\alpha_3,\alpha_4)$，开销 $(C_1,C_2,C_3,C_4,C_5)$，找到分界点 $\theta_1,\theta_2,\theta_3$，在预算 $C_{\text{total}}$ 内使得 $\tau$ 最小。
> 实际开销 $H_{\theta_1\theta_2\theta_3(\text{cost})}$ ，是指从时间0到时间𝑡采取不同措施的成本之和。
> ![](assets/Pasted%20image%2020220929211347.png)

#### 6、算法
> **Withdraw Bedeckung-Greedy Algorithm，WB-GA**
> ![](assets/Pasted%20image%2020220930104815.png)
> 概括一下：目标是找$\theta_1,\theta_2,\theta_3$ 。
> 1. 对接触系数相同的点进行降序排序。
> 2. 随机选择$\theta_1,\theta_2,\theta_3$ ，需要满足一些条件。
> 3. 如果 $H_{\theta_1\theta_2\theta_3(\text{cost})} \le C_{\text{total}}$，则输出$\theta_1,\theta_2,\theta_3$ 。（case 1）
> 4. 否则，case2。在成本约束下，将具有相同接触系数的节点，连续的放入$H_4,H_3,H_2 \text{ 至 } H_1$ 的集合中，如果开销小于 $C_{total}$ ，则将 $H_4$ 中==最小==接触系数的点放入 $H_3$ 中；将 $H_1$ 中接触系数==最大==的点放入 $H_2$ 中，直到有更好的解。最后，节点$H_1$，$H_2$和 $H_3$  的最大接触系数，就分别为$\theta_1$，$\theta_2$ 和 $\theta_3$ 。
> 
> 计算 $H_{\theta_1\theta_2\theta_3(\text{cost})}$ ：
> ![](assets/Pasted%20image%2020221004162824.png)
> 还是以 fig1 为例：
> 1. t=0 时
>    $$
>    \begin{aligned}
>    \text{cost}_0 &= C_1\cdot |H_{0,1}|+C_2\cdot |H_{0,2}|+C_3\cdot |H_{0,3}|+C_4\cdot |H_{0,4}|+C_5\cdot |H_{0,5}| \\
>    & = 2C_1+2C_2+2C_3+C_4+2C_5
>    \end{aligned}
>  $$
> 2. t=1 时，删除了 True node
>    $$
>    \begin{aligned}
>    \text{cost}_1 &= C_1\cdot |H_{1,1}|+C_2\cdot |H_{1,2}|+C_3\cdot |H_{1,3}|+C_5\cdot |H_{1,5}| \\
>    &= C_1+2C_2+2C_3+2C_5
>    \end{aligned}
>  $$
>  3. t=2 时
>     $$
>     \begin{aligned}
>     \text{cost}_2 &= C_1 \cdot|H_{2,1}|+C_3 \cdot|H_{2,3}|+C_5 \cdot|H_{2,5}| \\
>     &=3C_1+C_3+C_5
>     \end{aligned}
>  $$
>  4. t=3 时，没有更多的 True node ，传播停止了，$\text{cost}_3 = 0$ ，因此
>     $H_{\theta_1\theta_2\theta_3\text{(cost)}} = \text{cost}_0+\text{cost}_1+\text{cost}_2 = 6C_1+4C_2+5C_3+2C_4+5C_5$


#### 7、实验
> 数据集来自 SNAP。
> ![](assets/Pasted%20image%2020221004210115.png)
> 两个图的密度分别为 0.001, 0.0002 。
> edge 的概率可以统一设置为 𝑝(𝑢,𝑣)=0.05 或 𝑝(𝑢,𝑣)=0.1 或其他值。 *( 出处来自笔记中的第一篇论文，谣言纠正最大化 )*
> 
> 其他参数：
> ![](assets/Pasted%20image%2020221004211026.png)
> 对于每种算法，用1000次蒙特卡洛来估计谣言的预期传播时间（𝜏）和受谣言影响的预期节点数的结果。
> 
> **用于比较的算法：(文章这里写的很简略模糊，之后也没有具体解释)**
> 1. Proximity。启发式算法，赋予顶点index值，选择和分类有最高 index 值的rumor nodes。
> 2. Degree。基于顶点度进行挑选和分类。
> 3. IMRank。通过计算基于排名的边际影响传播(marginal influence spread)，和排名之间的相互作用，来选择和分类顶点。
> 4. Unblocking。啥也不干。
> 
> **结果图如下：**
> 随着初始rumor nodes 的增加(k 的增加)，都展现出上升趋势，但WB-GA上升的幅度不大。图 Fig 4，当 k<800 时，WB-GA算法的扩散时间小于其他算法；k=800时，可以推断，WB-GA效果不好，因为初始谣言节点太多，而且在实践中，𝑘通常很小。
> 原文说：*“我们可以推断，𝑘越小，我们的算法的性能就越好。”*
> ![](assets/Pasted%20image%2020221005170815.png)
> ![](assets/Pasted%20image%2020221005173036.png)
> ![](assets/Pasted%20image%2020221005172724.png)
> 
> 
> 当𝑘相同时，算法WB-GA的实际成本要比其他算法高。这是因为设定的其他算法的 $H_i$ 的数量很少。
> ![](assets/Pasted%20image%2020221005203334.png)
> 
> 在不同的数据集下，WB-GA在不同的𝑝(𝑢,𝑣)下的运行时间，它包括1000次蒙特卡罗模拟的运行时间。
> ![](assets/Pasted%20image%2020221005203356.png)



## Minimizing rumor influence in multiplex online social networks based on human individual and social behaviors
基于人的个体和社会行为，尽量减少多人在线社交网络中的谣言影响
Hosni A I E, Li K, Ahmad S. Minimizing rumor influence in multiplex online social networks based on human individual and social behaviors[J]. Information Sciences, 2020, 512: 1458-1480.

#### 1、名词概念

word-of-mouth: [n]口碑
herd mentality: [n]从众心理
oscillation:[n]震荡
eye-catching: [adj] 吸引眼球的
latent:[adj]潜在的
partial derivative: [n] 偏导数
manifest:[v]显示，表明；[adj]明显的，显而易见的；[n]旅客清单，载货清单
neutral:[adj]中立的，中性的

#### 2、关于本文
> 主要工作：
> 1. 提出一个新的谣言传播模型 HISBmodel，综合考虑了人类的个人和社会行为。
> 2. 提出 "真理运动策略（truth campaign strategy）"，来最小化谣言的影响。
> 3. 通过实验证明，该策略平均减少了 69%的可能被谣言影响的人。
> 
> 文章将现有的研究方法分为两类：
> 1. 宏观方面（Macroscopic approaches）：
>    主要是基于Epidemic模型[(文章链接)](https://www.nature.com/articles/2041118a0)来研究谣言传播的问题。最近的研究集中在人类个体和社会行为的作用上；这些研究调查了不同人类因素在谣言传播过程中的影响。有几项工作侧重于研究人类的个体行为，如遗忘和记忆 ，犹豫不决 ，不完整的阅读，以及个体的教育 。其他的工作集中在人类社会行为的影响上，如信任机制，羊群心态，以及社会强化在网络行为传播中的作用。这些工作研究了不同因素在不同类型网络中的影响，如 "无标度网络" 和 "小世界网络" 。他们认为，所有的用户都具有不可区分的特征，具有相同的影响他人的能力。此外，在人类行为和人类互动中观察到的超出我们想象的多样性和复杂性被忽略了，这使得对谣言传播这样的现象进行建模具有挑战性。**此外，谣言的传播和流行病的传播是不同的**，因为个人在这里可以选择在任何时候退出谣言的传播过程；但是在流行病中，感染过程是相对被动的。最后，由于其研究问题的宏观性，用Epidemic模型研究RIM问题具有挑战性。
> 2. 微观方面（Microscopic approaches）：多年来，在微观方法中提出了几个模型，例子包括：
>    * 概率模型，如著名的独立级联（IC）和线性阈值（LT）模型，或Galam模型[(文章)](https://www.sciencedirect.com/science/article/abs/pii/S0378437102015820?via%3Dihub)；
>    * 自然启发（nature-inspired）的模型，如能量模型（energy model）[(文章)](https://www.sciencedirect.com/science/article/abs/pii/S0378437113009680?via%3Dihub)；
>    * 推理的概率模型(probabilistic models of inference)[(文章)](http://proceedings.mlr.press/v28/gomez-rodriguez13.html)；
>    * 状态转换模型（state transition models）[(文章)](https://academic.oup.com/comnet/article-abstract/6/2/215/4060524?redirectedFrom=fulltext)
>    这个方向的研究主要集中在设计限制谣言传播的策略上，其中对传播模型的关注很少。此外，这些模型仍然缺乏一些重要的细节，因为它们未能捕捉到某些方面，如个人意见的传播。
>    最后，这些策略都是在封闭世界的假设下提出的；**然而，个人经常加入多个OSN，其中的谣言会同时在多个网络中传播。** 因此，所提出的RIM方法不能直接应用于多路OSN的传播；此外，据我们所知，很少有[文章](https://link.springer.com/chapter/10.1007/978-3-030-04224-0_9)研究多路OSN中的这个问题。
>    

##### 简谐阻尼运动

##### 生存理论



#### 3、传播模型
##### 多重在线社交网络（online social networks，OSN）的表示
> 简单来说，一个人可能同时使用多个社交网络，因此信息不单单只在一个网络上传播。
> **定义：** 多重OSNs，有 n 个网络，用集合 $\mathbb{G}^n = (I,G^n)$ 表示，其中 $I=(V,C)$ 表示用户的集合。对于 $i\in I$ 中的每个用户，用点 $v\in V$ 与特点集合 $c\in C$ 表示，其中特点定义为用户所响应的谣言。$G^n = \set{G_1 = (V,E_1),G_2 = (V,E_2),...,G_n = (V,E_n)}$ ，具体示例见下图。
> ![](assets/Pasted%20image%2020221008110018.png)
##### 个人对谣言表述的行为(Individual behavior toward a rumor formulation)
> ==三大因素：== 
> 1. 个人背景知识(individual's background knowledge, IBK)。关于谣言了解的越多，即 IBK 越高，越快失去对谣言的兴趣。
> 2. 犹豫机制（hesitating mechanism，HM）。一个人在传播谣言之前，最终会拥有一个潜伏期。这与个人对复兴的谣言的怀疑程度相对相关。
> 3. 遗忘-记忆（forgetting-remembering，FR）因素。谣言可能被OSN中的其他信息所掩盖，个人可以停止并重新开始传播该谣言。
> 
> 作者研究发现：**个体对谣言的吸引在偏离平衡位置时类似于一个振荡系统。**
> ![](assets/Pasted%20image%2020221008155006.png)
> IBK现象如上图(a)所示；HM现象如上图(c)所示；FR现象如上图(b)所示。
> 因此定义个人对谣言的吸引力为：
> $$
> A(t)=A_{int}e^{-\beta t}\cos(\omega t+\delta)
> $$
> 其中 A(t) 为个人在 t 时刻对谣言的吸引力；$A_{int}$ 为初始的谣言吸引力；$\beta$ 表示 IBK；$\omega$ 表示 FR 因素；$\delta$ 表示对谣言来源的信任程度，即HM。
> 
> 文章提出了一个命题：*谣言在网络中的影响对 FR和 HM因素的依赖性越来越大，而对 IBK 因素和谣言影响的依赖性却越来越小。*
> 具体证明过程就不写了，大致就是**求偏导数**。
> 令：
> $$
> \phi(\omega,\beta,\delta) = \int_0^\infty A_{int}e^{-\beta t}|\sin(\omega t + \delta)|dt,\quad \text{for } \beta>0
> 
> $$
> 一通推导后有：
> $$
> \phi(\omega,\beta,\delta)=A_{int}\frac{\omega e^{\frac{\delta}{\omega}}(e^{\frac{-\beta\pi}{\omega}}+1)}{(\beta^2+\omega^2)(1-e^{\frac{-\beta\pi}{\omega}})}
> $$
> ![](assets/Pasted%20image%2020221008212533.png)
> 上图证实了 $\phi( \omega, \beta, \delta)$ 的峰值是在 β 值较低、ω 和 δ 值较高时达到的。此外，我们可以看到 β 对下降趋势有更大的影响，这与关于IBK在传播过程中的重要性的假设相一致。
> 最后，为了方便，将个人对谣言的吸引力记为： #公式2
> $$
> A(t)=A_{int}e^{-\beta t}|\sin(\omega t+\delta)|\tag{2}
> $$

##### 个人观点表述（Individual opinion formulation）
> 个人对同一谣言的认定不同，个人可以确认、反驳、质疑或讨论感兴趣的事项。
> 本文通过一个加法模型来评估个人 v 对谣言的态度： #公式3 
> $$
> B_v(t)=\sum_{u\in \mathbb{N}^v}\sum_{j=1}^n \frac{B_u(t-1)}{j},\quad \text{for } t>0 \tag{3}
> $$
> 其中 $\mathbb{N}^v$ 为 点 v 的邻居们，n 表示点 v 从一个邻居处收到的谣言的次数。
> 不同值对应不同态度：
> $$
> B_v \in
> \left\{
> \begin{aligned}
> &[-\infty,0],\text{ denial}\\
> &[0,10],\text{ neutral}\\
> &[10,20],\text{ questioning}\\
> &[20,+\infty],\text{ supporting}
> \end{aligned}
> \right.
> $$
> [文章](https://www.sciencedirect.com/science/article/pii/S0378437115010328)中提出，大多数人是从众心理，盲目跟从他人观点；然而，当个人**不止一次**收到相同的信息时，由于信息冗余，它对他们的影响可能没有最初那么大。

##### 谣言传播规则（Rumor transmission rules)
> 确立一下谣言是怎么在多重OSN上传播的。
> 分三部分：什么时候传播谣言？什么时候接收？选择那个网络？
> 因此有了网络选择概率、谣言发送概率、谣言接收概率。
> 对于第 k 层网络，点 u 向 v 传播谣言的概率为： #公式1
> $$
> \begin{align*}
> p_{u,v}^k(t) = p_u^k \cdot p_u^{send}(t) \cdot p_{v,u}^{acc} \tag{1}
> \end{align*}
> $$
> *网络选择概率*：与顶点的度有关，一个节点的入度代表了在OSN中的权威。其中 $d_{in}^i(u)$ 表示点 u 在 $\mathbb{G}^n$ 中的第 i 层的入度。
> $$
> p_u^k=\frac{d_{in}^k(u)}{\sum_{i=1}^n d_{in}^i(u)}
> $$
> *谣言发送概率：* 人为因素很大，即之前分析的。
> $$
> p_u^{send}(t) = e^{-\beta t}|\sin(\omega t + \delta)|
> $$
> *谣言接收概率：* 由于名人效应，度大的点不容易被影响。因此设计了一个平衡权重概率。其中 P 是在传播过程中设置的概率参数。
> $$
> p_{v,u} = \frac{1}{1+\frac{d_{in}^k(v)}{d_{in}^k(u)}}\cdot P
> $$

##### HISBmodel 传播流程
> 给定一个 $\mathbb{G}^n=(I,G^n)$。
> * t=0 时，给定一组传播者，在不同层中传播，并将不同的 “信念（belief）” 随机分配给这些点。其余点的状态为 “无知（ignorant）”。
> * 在传播过程中，一个无知点满足 #公式1 ，那么它就成为传播者，并服从对谣言的行为，如 #公式2 所示。
> * 在每个时刻，一个人接收谣言后，根据 #公式3 ，更新它对谣言的态度。
> * 一个人可以接受一个以上的谣言。但是，他们对每个被接受的谣言只能传播一次。当传播者对谣言的兴趣减弱时，就不再参与传播过程。
> * 最后，当谣言 “流行度恶化（rumor popularity deteriorates）” 时，传播过程就会结束。进一步定义如下：
>   $$
>   R(t) = \sum\limits_{i=1}^n R_i(t) \quad \text{where} \quad R_i(t)=\sum\limits_{v\in V}A_v(t)\cdot d_{in}^i(v)
>   $$
>   其中 $R_i(t)$ 是每层中所有个体的累积吸引力。

### 4、谣言影响最小化
> **问题定义：** 考虑多路 OSN，$\mathbb{G}^n = (I,G^n)$ 。假设在时刻 $t_{det}$ 时，在网络的第i层检测到一个谣言。目标是选择 k 个个体来发起真相运动，以使相信谣言的个体数量最小。

##### 解决方法（算法）
> 当谣言被检测到时，将顶点 V 分成两个集合：$V=V_{B^+} \cup V_{B^-}$ 。其中 $V_{B^-}$ 表示持负面态度的个体的集合，$V_{B^+}$ 表示剩余的集合。
> 目标是从 $V_{B^+}$ 中选择 k 个最有影响力的节点来宣传，防止个人采用该谣言。提出了一个加法生存模型，其中节点 u 被激活的概率是由 #公式1 表示的传播概率**之和**。因此，节点被一个节点 v 感染的概率如下：
> $$
> \begin{aligned}
>  h_v(t) &= \sum\limits_{i=1}^n \sum\limits_{u\in \mathbb{N}_i^v} p^i_{u,v}(t) \\
>  &= p_v^{\text{send}}(t)\sum\limits_{i=1}^n \sum\limits_{u\in \mathbb{N}_i^v}p_v^i p_{v,u}^{\text{acc}}
>  \end{aligned}
> $$
> 