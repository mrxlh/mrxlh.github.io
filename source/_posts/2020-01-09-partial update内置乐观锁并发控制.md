---
title: partial update内置乐观锁并发控制
date: 2020-01-09 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch

---

### partial update内置乐观锁并发控制

#### 1. partial update内置乐观锁并发控制

如果partial update更新时候，所携带的_version 小于ES中所存储的version版本，则这个partial  update 失败

#### 2.retry_on_conflict

  1>. 再次获取document的数据和最新的版本（最新的数据）

  2>.基于最新版本号再次去更新，若成功则不需要再次重试了； 

  3>. 若失败，则重复1和2两个步骤，最多重复的次数是根据retry 哪个参数的指定 eg:6 次

  eg:   post /index/type/id/_update?retry_on_conflict=5

#### 3._version

和当前版本号一直时才能更新，否则就报错

post /index/type/id/_update?retry_on_conflict=5&version=6

