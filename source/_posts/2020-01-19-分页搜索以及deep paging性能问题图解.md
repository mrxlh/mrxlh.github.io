---
title: 分页搜索以及deep paging性能问题图解
date: 2020-01-19 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch
---

#### 分页搜索以及deep paging性能问题图解

#####  1. 分页

GET /_search?size=10
GET /_search?size=10&from=0
GET /_search?size=10&from=20

分页的上机实验

GET /test_index/test_type/_search

"hits": {
​    "total": 9,
​    "max_score": 1,

我们假设将这9条数据分成3页，每一页是3条数据，来实验一下这个分页搜索的效果

GET /test_index/test_type/_search?from=0&size=3

{
  "took": 2,
  "timed_out": false,
  "_shards": {
​    "total": 5,
​    "successful": 5,
​    "failed": 0
  },
  "hits": {
​    "total": 9,
​    "max_score": 1,
​    "hits": [
​      {
​        "_index": "test_index",
​        "_type": "test_type",
​        "_id": "8",
​        "_score": 1,
​        "_source": {
​          "test_field": "test client 2"
​        }
​      },
​      {
​        "_index": "test_index",
​        "_type": "test_type",
​        "_id": "6",
​        "_score": 1,
​        "_source": {
​          "test_field": "tes test"
​        }
​      },
​      {
​        "_index": "test_index",
​        "_type": "test_type",
​        "_id": "4",
​        "_score": 1,
​        "_source": {
​          "test_field": "test4"
​        }
​      }
​    ]
  }
}

第一页：id=8,6,4

GET /test_index/test_type/_search?from=3&size=3

第二页：id=2,自动生成,7

GET /test_index/test_type/_search?from=6&size=3

第三页：id=1,11,3

##### 2.deep paging

![](https://guanyuoss.oss-cn-qingdao.aliyuncs.com/prod/work_order/addadNSGzJ8.png)





