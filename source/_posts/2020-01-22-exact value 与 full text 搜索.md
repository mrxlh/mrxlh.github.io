---
title: exact value 与 full text 搜索
date: 2020-01-22 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch
---

####  exact value 与 full text 搜索

##### 1. exact value 

eg: 

录入: 2017-01-01，采用exact value，搜索的时候，必须输入2017-01-01，才能搜索出来
如果你输入一个01，是搜索不出来的; 也就是说  搜索的文字 必须与录入的一模一样才能搜索出来

##### 2. full text (可以泛泛理解为全文检索)

（1）缩写 vs. 全程：cn vs. china
（2）格式转化：like liked likes
（3）大小写：Tom vs tom
（4）同义词：like vs love

eg:

录入: 2017-01-01，es 可以将其拆分为 2017, 01, 01，搜索2017，或者01，都可以搜索出来
china，搜索cn，也可以将china搜索出来
likes，搜索like，也可以将likes搜索出来
Tom，搜索tom，也可以将Tom搜索出来
like，搜索love，同义词，也可以将like搜索出来

就不是说单纯的只是匹配完整的一个值，而是可以对值进行拆分词语后（分词）进行匹配，也可以通过缩写、时态、大小写、同义词等进行匹配



