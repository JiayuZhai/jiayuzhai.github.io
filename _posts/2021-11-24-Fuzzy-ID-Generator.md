---
layout: post
title: Fuzzy ID Generator
---
对欺诈场景，常常需要生成基于模糊匹配的ID，又可成为Entity Resolution实体解析，或同人模型。
算法定义是通过一系列能够间接定位一个人的字段集合，通过搜索和匹配的方式，定位一个用户与其他用户是否是同一个人。

## 基本框架
1. 搜索
     - 通过对一批字段的搜索，找出历史上与当前用户存在相似字段的其他用户。
        - 精确搜索 - 建议用NoSQL database提升效率
        - 模糊搜索 - 非常耗时+非常耗资源，常用ES(NGRAM搜索)。Advance: 训练word2vector，找K neighbor。
     - 汇总候选用户的字段。
2. 匹配
     - 当前用户和候选用户做1:n匹配计算
     - 根据字段物理属性，确定匹配方式，为匹配上的字段分配weight权重
        - 精确匹配 - Equal
        - 模糊匹配 - Stop Words, Edit Distance, 
     - 权重和是否满足匹配阈值
3. 分配ID
     - 如果不存在匹配上的候选用户，根据用户ID分配加盐hash的fuzzy_id。
     - 如果存在匹配上的候选用户，分配历史上已经分配过的fuzzy_id.
        - 同时需要更新所有匹配上的候选用户，以及根据他们旧的fuzzy_id关联出来的用户，的新fuzzy_id。
     