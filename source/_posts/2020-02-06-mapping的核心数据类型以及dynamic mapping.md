---
title: mapping的核心数据类型以及dynamic mapping
date: 2020-02-06 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch
---

#####  mapping的核心数据类型以及dynamic mapping

###### 1、核心的数据类型

string
byte，short，integer，long
float，double
boolean
date

###### 2、dynamic mapping

动态映射

true or false	-->	boolean
123		-->	long
123.45		-->	double
2017-01-01	-->	date
"hello world"	-->	string/text

###### 3、查看 mapping

GET /index/_mapping/type