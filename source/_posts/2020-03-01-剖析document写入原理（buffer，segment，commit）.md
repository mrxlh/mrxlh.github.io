---
title: 剖析document写入原理（buffer，segment，commit）
date: 2020-03-01 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch
---

#### 剖析document写入原理（buffer，segment，commit）

（1）数据写入buffer
（2）commit point
（3）buffer中的数据写入新的index segment
（4）等待在os cache中的index segment被fsync强制刷到磁盘上
（5）新的index sgement被打开，供search使用
（6）buffer被清空

每次commit point时，会有一个.del文件，标记了哪些segment中的哪些document被标记为deleted了
搜索的时候，会依次查询所有的segment，从旧的到新的，比如被修改过的document，在旧的segment中，会标记为deleted，在新的segment中会有其新的数据

![](https://guanyuoss.oss-cn-qingdao.aliyuncs.com/prod/work_order/FMr1GIRdH14.png)

