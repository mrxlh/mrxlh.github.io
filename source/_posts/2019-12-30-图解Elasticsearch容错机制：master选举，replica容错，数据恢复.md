---
title: 图解Elasticsearch容错机制：master选举，replica容错，数据恢复
date: 2019-12-30 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch
---

## 图解Elasticsearch容错机制：master选举，replica容错，数据恢复

（1）9 shard，3 node
（2）master node宕机，自动master选举，集群状态为：red
（3）replica容错：新master将replica提升为primary shard，集群状态为：yellow
（4）重启宕机node，master copy replica到该node，使用原有的shard并同步宕机后的修改，green

![Es 容错分析](https://img-blog.csdnimg.cn/20200129173240383.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1OTkwMTI4NjM4,size_16,color_FFFFFF,t_70)