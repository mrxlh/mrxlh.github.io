## _document的_source元数据以及定制返回结果解析

#### 1._source元数据

_source元数据：就是说，我们在创建一个document的时候，使用的那个放在request body中的json串，默认情况下，在get的时候，会原封不动的返回回来。

~~~json
put /test_index/test_type/1
{
  "test_field1": "test field1",
  "test_field2": "test field2"
}

get /test_index/test_type/1

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
}

~~~



#### 2.定制返回结果

定制返回的结果，指定_source中，返回哪些field

eg:?_source=key1,key2

~~~json
1. 
GET /test_index/test_type/1?_source=test_field1
{
  "_index": "test_index",
  "_type": "test_type",
  "_id": "1",
  "_version": 2,
  "found": true,
  "_source": {
    "test_field2": "test field2"
  }
}
2.
GET /test_index/test_type/1?_source=test_field1,test_field2
{
  "_index": "test_index",
  "_type": "test_type",
  "_id": "1",
  "_version": 2,
  "found": true,
  "_source": {
    "test_field2": "test field2"
  }
}
~~~

