# CommunityGAN: Community Detection with Generative Adversarial Nets
生成对抗网络的社区检测算法

# Pre
GAN(Generative Adversarial Network)

**AGM(Affiliation Graph Model)**：对密集重叠的社区结构进行建模的框架。对顶点-社区对分配一个非负因数，表示顶点对社区的隶属程度。一个顶点到所有社区的隶属关系构成表示向量

# Abstract
- 图的表示学习被用于社区检测，但只能用节点嵌入的聚类算法检测社区
- 聚类算法无法检测重叠社区
- **CommunityGAN**：解决重叠社区检测和图的表示学习
- 区别于传统的图嵌入，CommunityGAN的嵌入表示节点对社区的隶属强度
- 使用GAN优化嵌入

# Keywords
- 社区检测
- 图表示学习
- 生成式对抗网络

# Introduction
- **社区发现Community Detection**：节点分组，属性相似或功能相同
- **图嵌入Graph Embedding**：将图的每个节点表示为低维向量
- 深度学习算法Skip-gram, Convolutional Network进展很大
- 引入GAN(Generative Adversarial Nets)
- 成果有利于链接预测、推荐和节点分类
- 重叠密集的社团嵌入存在很多限制
- 一般来说，向量的相互距离比较有用，而单个向量没有意义
- 检测社区的直接方法是在向量空间使用聚类算法
- 一个顶点可能属于多个社区，聚类算法无法处理

Community GAN
- 用于解决重叠的社区检测和图表示学习
- **输入**：关系网络
- **输出**：顶点对社区的从属关系以及关系强度
![输入输出](https://github.com/EyreYoung/Notes/blob/master/Paper/img/Figure1.png)

- **AGM(Affiliation Graph Model)隶属图模型**：一个可以对密集重叠的社区结构进行建模的框架。它为每个顶点-社区对分配一个非负因数，该非负因数表示该顶点对社区的隶属程度。
因此，从一个顶点到所有社区的隶属关系的强度构成了它的表示向量。

生成和鉴别社区检测的图案
- 生成器：生成顶点子集`s`，组成特定图案
- 鉴别器：鉴别子集`s`是否是真的图案
- 最终目标：生成器生成的图案无法被鉴别

论文贡献
- 组合AGM和GAN来实现优秀性能的GAN和顶点-社团的AGM表示
- 研究正确标记数据中的图案分布并分析它如何帮助提升社区检测的质量
- 提出一种图案生成的实现Graph AGM，使用计算方法生成最可能的图案

实验结果
- 解决密集重叠问题
- motif级的生成器和鉴别器
- 使用五个数据集，在社区检测和群体预测上评估CommunityGAN
- 社区检测和图形表示上，CommunityGAN优于最新方法
- F1-Score上得分比基线高7.9%到21%
- 3-派系和4-派系预测任务上，AUC分数分别提高到0.99和0.956
- 特有的嵌入方法、对抗学习、motif级别的优化

# Related Work
**Community Detection**
- 设计社团度量指标如模块度并进行优化
- 采用生成模型来描述图的生成，并且可以通过将图拟合到此类模型来推断社区
- 在图邻接矩阵上采用矩阵分解算法来输出顶点和社团之间的关系

**Graph representation learning**
- DeepWalk显示图形中的随机游动类似于自然语言中的文本序列，采用Skip-gram(词表示学习模型)来学习顶点表示
- Node2vec通过提出一种有偏的随机游走算法进一步扩展了DeepWalk的概念，该算法在生成采样的顶点序列时提供了更大的灵活性
- LINE首先学习保留一阶和二阶接近度的顶点表示
- GraRep应用在图上定义的不同损失函数来捕获图的不同k阶接近度和全局结构特性
- GraphGAN提出了一个统一的对抗学习框架，该框架自然地从图上捕获结构信息以学习图表示
- ANE利用GAN作为正则化器来学习稳定而强大的特征提取器

**Unified framework for graph representation learning andcommunity detection**
- Wang设计了模块化的非负矩阵分解算法，以保留顶点相似性和社区结构。但是，由于矩阵分解的复杂性，该模型无法应用于许多包含数百万个顶点的真实世界图 
- Cavallari设计了一个框架，解决社区嵌入，社区检测和节点嵌入

# Empirical Observation
数据集
- LiveJournal，Orkut和Youtube 在线社交网络
- DBLP 协作网络
- Amazon 产品网络
![数据集统计数据](https://github.com/EyreYoung/Notes/blob/master/Paper/img/Table1.png)

问题
- 社区如何组成motif
- 社区重叠的情况下图案生成有哪些变化

步骤
- 从社区中取2/3/4个点，判断是否能组成motif，获得一个社区中生成motif的概率

- 将这个概率与整个网络的概率相比较，本文主要关注的motif是2/3/4-派系

- motif的出现与社区结构关联性很大
![顶点采样出现派系的概率](https://github.com/EyreYoung/Notes/blob/master/Paper/img/Table2.png)

- 两个顶点同属的社区越多，它们越可能是2-派系（有边相连）

- 本文发现3-派系、4-派系也存在这种情况，处于社区重叠中的顶点连接比单个社区中的更加紧密

![顶点采样出现派系的概率](https://github.com/EyreYoung/Notes/blob/master/Paper/img/Figure2.png)

# Methodology
CommunityGAN框架
研究图：$\mathcal{G} = (\mathcal{V}, \mathcal{E}, \mathcal{M})$

节点集合：$\mathcal{V} = \{v_1,...,v_V\}$

节点间的边：$\mathcal{E} = \{e_{ij}\}_{i,j=1}^V$

$\mathcal{G}$中的motif集合：$\mathcal{M}$

包含某节点的所有motif集合：$\mathcal{M}(v_c)$

生成器Generator：$G(s|v_c;\theta_G)$

鉴别器Discriminator：$D(s,\theta_D)$

![所有符号](https://github.com/EyreYoung/Notes/blob/master/Paper/img/Table3.png)

$$\min\limits_{\theta_G}\max\limits_{\theta_D}V(G,D) = \sum_{c=1}^V(E)$$



