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
- 社区发现Community Detection：节点分组，属性相似或功能相同
- 图嵌入Graph Embedding：将图的每个节点表示为低维向量
- 深度学习算法Skip-gram, Convolutional Network进展很大
- 引入GAN(Generative Adversarial Nets)
- 成果有利于链接预测、推荐和节点分类
- 重叠密集的社团嵌入存在很多限制
- 一般来说，向量的相互距离比较有用，而单个向量没有意义
- 检测社区的直接方法是在向量空间使用聚类算法
- 一个顶点可能属于多个社区，聚类算法无法处理

Community GAN
- 用于解决重叠的社区检测和图表示学习
- 输入：关系网络
- 输出：顶点对社区的从属关系以及关系强度
![输入输出](https://github.com/EyreYoung/Notes/blob/master/Paper/img/Figure1.png)

