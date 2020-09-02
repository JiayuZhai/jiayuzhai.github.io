---
layout: post
title: Cassandra Key 
---
Key 介绍

1. Partition Key (将数据分散到集群的 node 上)
2. Clustering Key (决定同一个分区内相同 Partition Key 数据的排序，默认为升序，我们可以在建表语句里面手动设置排序的方式（DESC 或 ASC）)
3. Primary Key (Partition Key)
4. Composite Primary Key (Partition Key + Clustering Key)