---
title: distributed document store （分布式文档存储）
date: 2020-01-12 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch

---

###  distributed document store （分布式文档存储）

Elasticsearch其实最核心的功能，就是一个分布式的文档数据存储系统。ES是分布式的。文档数据存储系统。文档数据，存储系统。

文档数据：es可以存储和操作json文档类型的数据，而且这也是es的核心数据结构。

存储系统：es可以对json文档类型的数据进行存储，查询，创建，更新，删除，等等操作。？其实ES满足了这些功能，就可以说已经是一个NoSQL的存储系统了。



根据ES的特性可以构建以下应用程序 ：

1. 数据量较大，es的分布式本质，可以帮助你快速进行扩容，承载大量数据
2. 数据结构灵活多变，随时可能会变化，而且数据结构之间的关系，非常复杂，如果我们用传统数据库，就要面临大量的表操作
3. 对数据的相关操作，较为简单，比如就是一些简单的增删改查，用我们之前讲解的那些document操作就可以搞定
4. NoSQL数据库，适用的也是类似于上面的这种场景