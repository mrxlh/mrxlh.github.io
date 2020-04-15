---
title: mapping复杂数据类型以及object类型数据底层结构
date: 2020-02-04 17:07:11
tags: ['Elasticsearch']
categories: Elasticsearch
---

#### mapping复杂数据类型以及object类型数据底层结构

课程大纲

##### 1、multivalue field

{ "tags": [ "tag1", "tag2" ]}

建立索引时与string是一样的，数据类型不能混 即 tags中对应的数组的类型是一样的

##### 2、empty field

null，[]，[null]

对于空串的处理

##### 3、object field

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

address：object类型

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

对于这样的数据类型

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

在es 中会转换成这样的存储方式

{
​    "name":            [jack],
​    "age":          [27],
​    "join_date":      [2017-01-01],
​    "address.country":         [china],
​    "address.province":   [guangdong],
​    "address.city":  [guangzhou]
}

包含多个对象的数据类型

{
​    "authors": [
​        { "age": 26, "name": "Jack White"},
​        { "age": 55, "name": "Tom Jones"},
​        { "age": 39, "name": "Kitty Smith"}
​    ]
}

在ES中会从 行式  存储转为 列式 存储

{
​    "authors.age":    [26, 55, 39],
​    "authors.name":   [jack, white, tom, jones, kitty, smith]
}