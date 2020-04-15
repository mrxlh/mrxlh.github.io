---
title: Elasticsearch  mget 的批量查询
date: 2020-01-10 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch
---

###   Elasticsearch  mget 的批量查询

####  1. 批量查询好处

一条一条的查询，比如说要查询100条数据，那么就要发送100次网络请求，这个开销还是很大的
如果进行批量查询的话，查询100条数据，就只要发送1次网络请求，网络请求的性能开销缩减100倍

可以说mget是很重要的，一般来说，在进行查询的时候，如果一次性要查询多条数据的话，那么一定要用batch批量操作的api
尽可能减少网络开销次数，可能可以将性能提升数倍，甚至数十倍，非常非常之重要

####  2. mget的语法

#####  1.单条数据查询语法

GET /test_index/test_type/1
GET /test_index/test_type/2

##### 2. mget批量查询

###### 1.可以是不同index 和type 也可以是同一个 index 和type

~~~
GET /_mget
{
   "docs" : [
      {
         "_index" : "test_index",
         "_type" :  "test_type",
         "_id" :    1
      },
      {
         "_index" : "test_index",
         "_type" :  "test_type",
         "_id" :    2
      }
   ]
}


~~~

返回结果：

~~~
{
  "docs": [
    {
      "_index": "test_index",
      "_type": "test_type",
      "_id": "1",
      "_version": 2,
      "found": true,
      "_source": {
        "test_field1": "test field1",
        "test_field2": "test field2"
      }
    },
    {
      "_index": "test_index",
      "_type": "test_type",
      "_id": "2",
      "_version": 1,
      "found": true,
      "_source": {
        "test_content": "my test"
      }
    }
  ]
}
~~~

###### 2. 查询的document是一个index下的不同type

~~~
GET /test_index/_mget
{
   "docs" : [
      {
         "_type" :  "test_type",
         "_id" :    1
      },
      {
         "_type" :  "test_type",
         "_id" :    2
      }
   ]
}
~~~

###### 3. 查询的数据都在同一个index下的同一个type

~~~
GET /test_index/test_type/_mget
{
   "ids": [1, 2]
}

~~~







