---
title: mapping复杂数据类型以及object类型数据底层结构
date: 2020-02-08 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch
---

#####  mapping复杂数据类型以及object类型数据底层结构

######  1、multivalue field

{ "tags": [ "tag1", "tag2" ]}

建立索引时与string是一样的，数据类型不能混

###### 2. empty field

null，[]，[null]

###### 3、object field

PUT /company/employee/1
{
  "address": {
​    "country": "china",
​    "province": "guangdong",
​    "city": "guangzhou"
  },
  "name": "jack",
  "age": 27,
  "join_date": "2017-01-01"
}



GET /company/_mapping/employee

address：object类型(数据结构)

{
  "company": {
​    "mappings": {
​      "employee": {
​        "properties": {
​          "address": {
​            "properties": {
​              "city": {
​                "type": "text",
​                "fields": {
​                  "keyword": {
​                    "type": "keyword",
​                    "ignore_above": 256
​                  }
​                }
​              },
​              "country": {
​                "type": "text",
​                "fields": {
​                  "keyword": {
​                    "type": "keyword",
​                    "ignore_above": 256
​                  }
​                }
​              },
​              "province": {
​                "type": "text",
​                "fields": {
​                  "keyword": {
​                    "type": "keyword",
​                    "ignore_above": 256
​                  }
​                }
​              }
​            }
​          },
​          "age": {
​            "type": "long"
​          },
​          "join_date": {
​            "type": "date"
​          },
​          "name": {
​            "type": "text",
​            "fields": {
​              "keyword": {
​                "type": "keyword",
​                "ignore_above": 256
​              }
​            }
​          }
​        }
​      }
​    }
  }
}

{
  "address": {
​    "country": "china",
​    "province": "guangdong",
​    "city": "guangzhou"
  },
  "name": "jack",
  "age": 27,
  "join_date": "2017-01-01"
}

{
​    "name":            [jack],
​    "age":          [27],
​    "join_date":      [2017-01-01],
​    "address.country":         [china],
​    "address.province":   [guangdong],
​    "address.city":  [guangzhou]
}

复杂的数据结构 

{
​    "authors": [
​        { "age": 26, "name": "Jack White"},
​        { "age": 55, "name": "Tom Jones"},
​        { "age": 39, "name": "Kitty Smith"}
​    ]
}

ES 底层会行转列存储

{
​    "authors.age":    [26, 55, 39],
​    "authors.name":   [jack, white, tom, jones, kitty, smith]
}

