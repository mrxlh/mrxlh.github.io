---
title: _multi-index&multi-type搜索模式使用以及搜索原理初步图解
date: 2020-01-18 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch
---

####  _multi-index&multi-type搜索模式使用以及搜索原理初步图解

##### 1. multi-index和multi-type搜索模式

告诉你如何一次性搜索多个index和多个type下的数据

| 指令                               | 描述                                          |
| ---------------------------------- | --------------------------------------------- |
| /_search                           | 所有索引，所有type下的所有数据都搜索出来      |
| /index1/_search                    | 指定一个index，搜索其下所有type的数据         |
| /index1,index2/_search             | 同时搜索两个index下的数据                     |
| / *1, *2 /_search                  | 按照通配符去匹配多个索引                      |
| /index1/type1/_search              | 搜索一个index下指定的type的数据               |
| /index1/type1,type2/_search        | 可以搜索一个index下多个type的数据             |
| /index1,index2/type1,type2/_search | 搜索多个index下的多个type的数据               |
| / _all/type1,type2/_search         | _all，可以代表搜索所有index下的指定type的数据 |



##### 2. 图解

![](https://guanyuoss.oss-cn-qingdao.aliyuncs.com/prod/work_order/wuNEvdhPDPI.png)