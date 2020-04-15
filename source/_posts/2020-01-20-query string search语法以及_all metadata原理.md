---
title: query string search语法以及_all metadata原理
date: 2020-01-20 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch
---

#### query string search语法以及_all metadata原理

##### 1.  query string基础语法

其实就是http请求,报附加的参数 通过url传过来

GET /test_index/test_type/_search?q=test_field:test _

表示 test_index ,test_type  下,test_field所包含的关键字 test 
GET /test_index/test_type/_search?q=+test_field:test  _

 "+" 代表必须包含 test字段,其实 带+ 号 和不带 + 号是一样的

GET /test_index/test_type/_search?q=-test_field:test

"-" 代表 该 test_field 必须不包含 test 关键字 

一个是掌握q=field:search content的语法，还有一个是掌握+和-的含义

##### 2. _all metadata的原理和作用

GET /test_index/test_type/_search?q=test

直接可以搜索所有的field，任意一个field包含指定的关键字就可以搜索出来。我们在进行中搜索的时候，难道是对document中的每一个field都进行一次搜索吗？不是的

es中的_all元数据，在建立索引的时候，我们插入一条document，它里面包含了多个field，此时，es会自动将多个field的值，全部用字符串的方式串联起来，变成一个长的字符串，作为_all field的值，同时建立索引

后面如果在搜索的时候，没有对某个field指定搜索，就默认搜索_all field，其中是包含了所有field的值的

举个例子

{
  "name": "jack",
  "age": 26,
  "email": "jack@sina.com",
  "address": "guamgzhou"
}

其实就是把以上所有的filed进行拼接起来,"jack 26 jack@sina.com guangzhou"，作为这一条document的_all field的值，同时进行分词后建立对应的倒排索引

生产环境不使用

