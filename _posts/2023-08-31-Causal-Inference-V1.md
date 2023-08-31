---
layout: post
title: Causal Inference V1
---

风控背景读因果推断 - 个人总结V1

## 什么问题

风控是一个典型的二分类问题。相应的输入，输出和算法都比较好理解。
 - 输入就是一组特征，特征是用于描述待预测实体的各种维度的变量。
 - 输出一个是分类结果，也就是有风险或无风险。也可以是一个风险分数，作为预测为有风险的概率。
 - 模型就是对训练集所提供的历史数据和已知标签进行拟合，来预测未来数据的风险情况。

当然风控场景本身还会有各种各样的扩展，泛化和引申。这里先描述风控是因为从一个风控背景的人的认知角度，后面是如何理解因果推断问题的。

分类回归问题为代表的预测问题，其实有一个前提存在，就是特征可以决定结果，而非有其他决定因素或是相互产生影响的关系。而因果推断问题则是除了特征这个固有属性的影响外，“干预”也是其中一个影响。从预测问题的角度，可能“干预”也可以认为是特征的一种，且目前是为了得到结果的正确预测；而因果推断中，需要解决的问题是，对于一个“干预”（或“不干预”），所产生影响的效果的估计，而非结果的预测。

在这个问题定义下，几个核心概念就可以给出了：
 - 单位：干预所施加的对象。
 - 干预：应用在单位上的行为。
 - 干预结果：干预施加在单位上造成的理论结果。
 - 观测结果：干预施加在单位上造成的事实观测结果。
 - 反事实结果：施加其他干预（或不施加）在单位上造成的结果。
 - 干预前特征：与干预无关的变量。通常是单位的固有属性。
 - 干预后特征：与干预有关的变量。通常是中间结果。
 - 实验组：施加了干预的同一组单位。
 - 对照组：未施加干预的同一组单位。

以及三个假设：
 - 单位和干预的稳定性：单位被干预，不受其他单位的影响。一种干预只有施加和不施加，没有量的区别。
 - 可忽略性：相同的干预前特征下，不同单位被施加或不施加一个干预是随机的。
 - 存在性：对于任何的干预前特征值，不会出现一定施加干预或一定不施加干预。

最后是因果推断问题需要计算的干预影响：
 - 平均干预影响 = （实验组的结果 - 对照组的结果）的期望



## 参考文献

[1] [Yao, Liuyi, et al. "A survey on causal inference." ACM Transactions on Knowledge Discovery from Data (TKDD) 15.5 (2021): 1-46.](https://dl.acm.org/doi/pdf/10.1145/3444944)