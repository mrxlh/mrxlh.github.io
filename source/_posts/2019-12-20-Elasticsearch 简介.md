---
title: Elasticsearch 入门
date: 2019-12-20 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch

---

## Elasticsearch 入门

# Elasticsearch的由来

有个帅哥名字叫“Shay Banon”，对就是这位。这是他2013年在dotScale大会上分享Elasticsearch的照片。[youtube上的分享视频](https://link.jianshu.com/?t=https://www.youtube.com/watch?v=fEsmydn747c)

![img](http://image.uczzd.cn/8622803757556180222.jpg)

**Elasticsearch的诞生历史**

许多年前，一个叫Shay Banon的待业工程师跟随他的新婚妻子来到伦敦，他的妻子想在伦敦学习做一名厨师。而他在伦敦寻找工作的期间，接触到了Lucene的早期版本，他想为自己的妻子开发一个方便搜索菜谱的应用。

直接使用Lucene构建搜索会有很多的坑以及重复性的工作，所以Shay便在Lucene的基础上不断进行抽象来让Java程序嵌入搜索变得更容易一些，经过一段时间的打磨，就诞生了他的第一个开源作品，他给自己的这个作品起了个名字，叫 “Compass”，中文即“指南针”的意思。

之后，Shay找到了一份新工作，新工作是处在一个高性能分布式的开发环境中。他在工作中渐渐发现，越来越需要一个易用的高性能、实时、分布式搜索服务，于是他决定重写Compass，将它从一个库打造成了一个独立的server，并将其改名为Elasticsearch。

Elasticsearch发布的第一个版本是在2010年的二月份，从那之后，Elasticsearch便成了Github上最受人瞩目的项目之一，并且很快就有超过300名开发者加入进来贡献了自己的代码。后来Shay和另一位合伙人成立了公司专注打造Elasticsearch，他们对Elasticsearch进行了一些商业化的包装和支持。但是，Elasticsearch承诺，永远都将是开源并且免费的。

不过悲剧的是，Shay承诺为妻子开发的菜谱搜索应用，到现在还没做出来……

1. 什么是搜索

   1. 全文搜索 : [http://www.baidu.com]()

   2. 垂直搜索:[https://www.taobao.com]()  [http://www.laogou.com]()

      搜索:输入要搜索的关键字,然后期望返回这个关键字的相关信息

2. 用数据库做搜索会怎样

   | 商品ID | 商品名称     | 商品描述 |
   | ------ | ------------ | -------- |
   | 1      | 耐克袜子     |          |
   | 2      | 阿迪达斯袜子 |          |
   | 3      | 鸿星尔克袜子 |          |
   | 4      | 三六一度袜子 |          |

   eg: select * from  products where  product_name %袜子%;

   如果出现  袜XX子 这样的词语 是查询不到的

   不能够将搜索词进行拆分 eg : 输入 唐人街案 , 就展示不出 唐人街探案3



   3. 全文检索 说道这里 就不得不引入一个概念 倒排索引

      1.正排索引:eg:书的目录 

      | id   | 名称         |
      | ---- | ------------ |
      | 1    | 紧急救援电影 |
      | 2    | 紧急救援花絮 |
      | 3    | 紧急救援海报 |

      2.倒排索引

      | 关键词 | ids   |
      | ------ | ----- |
      | 紧急   | 1,2,3 |
      | 救援   | 1,2,3 |
      | 电影   | 1     |
      | 花絮   | 2     |
      | 海报   | 3     |

      通过输入 [紧急援] 即可搜索到以上信息 1,2,3 ,上述的这个过程就是全文检索

        3. Lucene

           lucene，就是一个jar包，里面包含了封装好的各种建立倒排索引，以及进行搜索的代码，包括各种算法。我们就用java开发的时候，引入lucene jar，然后基于lucene的api进行去进行开发就可以了。用lucene，我们就可以去将已有的数据建立索引，lucene会在本地磁盘上面，给我们组织索引的数据结构。另外的话，我们也可以用lucene提供的一些功能和api来针对磁盘上的数据

 4. 认识 Elasticsearch

           4. 认识 Elasticsearch
        ​    
              Lucene 是单机,如果机器超过其所能承载的数据量的时候,只有通过增加机器来进行存储,如果自己 做需要考虑数据的备份 数据间的通讯等 此时Elasticsearch 诞生,

5.总结：

Elasticsearch，分布式，高性能，高可用，可伸缩的搜索和分析系统