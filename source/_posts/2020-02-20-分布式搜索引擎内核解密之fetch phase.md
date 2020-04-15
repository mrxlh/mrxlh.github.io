---
title: 分布式搜索引擎内核解密之query phase
date: 2020-02-20 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch
---

#### 分布式搜索引擎内核解密之fetch phase

##### 1、fetch phbase工作流程

（1）coordinate node构建完priority queue之后，就发送mget请求去所有shard上获取对应的document
（2）各个shard将document返回给coordinate node
（3）coordinate node将合并后的document结果返回给client客户端

![](https://guanyuoss.oss-cn-qingdao.aliyuncs.com/prod/work_order/_zKICQtJ0iI.png)



##### 2、一般搜索，如果不加from和size，就默认搜索前10条，按照_score(相关度分数)排序

