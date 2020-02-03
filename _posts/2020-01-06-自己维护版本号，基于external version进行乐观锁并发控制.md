###  自己维护版本号，基于external version进行乐观锁并发控制

#### 1.external version

es提供了一个feature，就是说，你可以不用它提供的内部_version版本号来进行并发控制，可以基于你自己维护的一个版本号来进行并发控制。 一句话，当你 可不想用es内部的_version来进行控制，而是用你自己维护的那个version来进行控制。此时就是可以采用 external version 

?version=1
?version=1&version_type=external

version_type=external，唯一的区别在于，_version，只有当你提供的version与es中的_version一模一样的时候，才可以进行修改，只要不一样，就报错；

当version_type=external的时候，只有当你提供的version比es中的_version大的时候，才能完成修改

es，_version=1，?version=1，才能更新成功
es，_version=1，?version>1&version_type=external，才能成功，比如说?version=2&version_type=external

####  2. 构建一条数据

PUT /test_index/test_type/8
{
  "test_field": "test"
}

{
  "_index": "test_index",
  "_type": "test_type",
  "_id": "8",
  "_version": 1,
  "result": "created",
  "_shards": {
​    "total": 2,
​    "successful": 1,
​    "failed": 0
  },
  "created": true
}

####  3.模拟两个客户端同时查询到这条数据

GET /test_index/test_type/8

{
  "_index": "test_index",
  "_type": "test_type",
  "_id": "8",
  "_version": 1,
  "found": true,
  "_source": {
​    "test_field": "test"
  }
}

#### 4.第一个客户端先进行修改，此时客户端程序是在自己的数据库中获取到了这条数据的最新版本号，比如说是2

PUT /test_index/test_type/8?version=2&version_type=external
{
  "test_field": "test client 1"
}

{
  "_index": "test_index",
  "_type": "test_type",
  "_id": "8",
  "_version": 2,
  "result": "updated",
  "_shards": {
​    "total": 2,
​    "successful": 1,
​    "failed": 0
  },
  "created": false
}

### 5.模拟第二个客户端，同时拿到了自己数据库中维护的那个版本号，也是2，同时基于version=2发起了修改

PUT /test_index/test_type/8?version=2&version_type=external
{
  "test_field": "test client 2"
}

{
  "error": {
​    "root_cause": [
​      {
​        "type": "version_conflict_engine_exception",
​        "reason": "[test_type][8]: version conflict, current version [2] is higher or equal to the one provided [2]",
​        "index_uuid": "6m0G7yx7R1KECWWGnfH1sw",
​        "shard": "1",
​        "index": "test_index"
​      }
​    ],
​    "type": "version_conflict_engine_exception",
​    "reason": "[test_type][8]: version conflict, current version [2] is higher or equal to the one provided [2]",
​    "index_uuid": "6m0G7yx7R1KECWWGnfH1sw",
​    "shard": "1",
​    "index": "test_index"
  },
  "status": 409
}

报错了



####  6. 在并发控制成功后，重新基于最新的版本号发起更新

GET /test_index/test_type/8

{
  "_index": "test_index",
  "_type": "test_type",
  "_id": "8",
  "_version": 2,
  "found": true,
  "_source": {
​    "test_field": "test client 1"
  }
}

PUT /test_index/test_type/8?version=3&version_type=external
{
  "test_field": "test client 2"
}

{
  "_index": "test_index",
  "_type": "test_type",
  "_id": "8",
  "_version": 3,
  "result": "updated",
  "_shards": {
​    "total": 2,
​    "successful": 1,
​    "failed": 0
  },
  "created": false
}