---
title: 2个node环境下replica shard是如何分配的
date: 2019-12-28 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch
---

## 2个node环境下replica shard是如何分配的

（1）replica shard分配：3个primary shard，3个replica shard，1 node
（2）primary ---> replica同步
（3）读请求：既可以请求到primary shard  也可以请求到 replica shard



![image](https://img-blog.csdnimg.cn/20200128121901180.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1OTkwMTI4NjM4,size_16,color_FFFFFF,t_70)







