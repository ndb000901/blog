# ElasticSearch使用





# HTTP操作



## 索引操作



### 创建索引



**请求**

```http
PUT /shopping HTTP/1.1
Host: 172.20.10.11:9200
```

**响应**

```json

{
"acknowledged"【响应结果】: true, # true 操作成功
"shards_acknowledged"【分片结果】: true, # 分片操作成功
"index"【索引名称】: "shopping"
}
# 注意：创建索引库的分片数默认 1 片，在 7.0.0 之前的 Elasticsearch 版本中，默认 5 片
```

不可重复添加



### 查看所有索引



**请求**

```http
GET /_cat/indices?v=null HTTP/1.1
Host: 172.20.10.11:9200
```

**响应**

```json
health status index    uuid                   pri rep docs.count docs.deleted store.size pri.store.size
yellow open   shopping yun3l758QYiDkjmAfuCkxQ   1   1          0            0       208b           208b

```

| 表头           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| health         | 健康状态：green(集群完整)、yellow(单点正常，集群不完整)、red(单点不正常) |
| status         | 索引状态                                                     |
| index          | 索引名                                                       |
| uuid           | 索引统一编号                                                 |
| pri            | 主分片数量                                                   |
| rep            | 副本数量                                                     |
| docs.count     | 可用文档数量                                                 |
| docs.deleted   | 文档删除数量                                                 |
| store.size     | 主分片和副分片整体占空间大小                                 |
| pri.store.size | 主分片占空间大小                                             |



### 查看单个索引



**请求**

```http
GET /shopping HTTP/1.1
Host: 172.20.10.11:9200
```

**响应**

```json
{
    "shopping": {
        "aliases": {},
        "mappings": {},
        "settings": {
            "index": {
                "creation_date": "1636886288686",
                "number_of_shards": "1",
                "number_of_replicas": "1",
                "uuid": "yun3l758QYiDkjmAfuCkxQ",
                "version": {
                    "created": "7080099"
                },
                "provided_name": "shopping"
            }
        }
    }
}
```

**字段说明**



```json
{
    "shopping"【索引名】: {
        "aliases"【别名】: {},
        "mappings"【映射】: {},
        "settings"【设置】: {
            "index"【设置 - 索引】: {
                "creation_date"【设置 - 索引 - 创建时间】: "1614265373911",
                "number_of_shards"【设置 - 索引 - 主分片数量】: "1",
                "number_of_replicas"【设置 - 索引 - 副分片数量】: "1",
                "uuid"【设置 - 索引 - 唯一标识】: "eI5wemRERTumxGCc1bAk2A",
                "version"【设置 - 索引 - 版本】: {
                    "created": "7080099"
                },
                "provided_name"【设置 - 索引 - 名称】: "shopping"
            }
        }
    }
}
```

 

### 删除索引



**请求**

```http
DELETE /shopping HTTP/1.1
Host: 172.20.10.11:9200
```



**响应**

```json
{
    "acknowledged": true
}
```



## 文档操作



### 创建文档



**请求**

```http
POST /shopping/phone HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 118

{
    "title": "小米手机",
    "category": "小米",
    "images": "http://www.gulixueyuan.com/xm.jpg",
    "price": 3999.00
}
```

**响应**

```json
{
    "_index": "shopping",
    "_type": "phone",
    "_id": "rGtuHn0ByN8TTRagGDOD",
    "_version": 1,
    "result": "created",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "_seq_no": 0,
    "_primary_term": 1
}
```

**字段说明**

```json
{
"_index"【索引】: "shopping",
"_type"【类型-文档】: "_doc",
"_id"【唯一标识】: "Xhsa2ncBlvF_7lxyCE9G", #可以类比为 MySQL 中的主键，随机生成
"_version"【版本】: 1,
"result"【结果】: "created", #这里的 create 表示创建成功
"_shards"【分片】: {
"total"【分片 - 总数】: 2,
"successful"【分片 - 成功】: 1,
"failed"【分片 - 失败】: 0
},
"_seq_no": 0,
"_primary_term": 1
}
```



只能使用POST方式



**指明主键后可使用PUT**

**请求**

```http
PUT /shopping/phone/1 HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 118

{
    "title": "小米手机",
    "category": "小米",
    "images": "http://www.gulixueyuan.com/xm.jpg",
    "price": 4999.00
}
```

**响应**

```json
{
    "_index": "shopping",
    "_type": "phone",
    "_id": "1",
    "_version": 1,
    "result": "created",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "_seq_no": 1,
    "_primary_term": 1
}
```



### 查看文档



**需指明唯一标识**

**请求**

```http
GET /shopping/phone/1 HTTP/1.1
Host: 172.20.10.11:9200
```

**响应**

```json
{
    "_index": "shopping",
    "_type": "phone",
    "_id": "1",
    "_version": 2,
    "_seq_no": 2,
    "_primary_term": 1,
    "found": true,
    "_source": {
        "title": "小米手机",
        "category": "小米",
        "images": "http://www.gulixueyuan.com/xm.jpg",
        "price": 4999.00
    }
}
```

**字段解析**

```json
{
"_index"【索引】: "shopping",
"_type"【文档类型】: "_doc",
"_id": "1",
"_version": 2,
"_seq_no": 2,
"_primary_term": 2,
"found"【查询结果】: true, # true 表示查找到，false 表示未查找到
"_source"【文档源信息】: {
"title": "华为手机",
"category": "华为",
"images": "http://www.gulixueyuan.com/hw.jpg",
"price": 4999.00
}
}
```



### 修改文档



**请求**

```http
POST /shopping/phone/1 HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 118

{
    "title": "小米手机",
    "category": "小米",
    "images": "http://www.gulixueyuan.com/xm.jpg",
    "price": 9999.00
}
```



**响应**

```json
{
    "_index": "shopping",
    "_type": "phone",
    "_id": "1",
    "_version": 3,
    "result": "updated",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "_seq_no": 3,
    "_primary_term": 1
}
```

**字段说明**

```json
{
"_index": "shopping",
"_type": "_doc",
"_id": "1",
"_version"【版本】: 2,
"result"【结果】: "updated", # updated 表示数据被更新
"_shards": {
"total": 2,
"successful": 1,
"failed": 0
},
"_seq_no": 2,
"_primary_term": 2
}
```

### 修改字段



**修改局部数据**

**请求**

```http
POST /shopping/phone/1/_update HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 47

{
    "doc": {
        "price": 3000.00
    }
}

```

**响应**

```json
{
    "_index": "shopping",
    "_type": "phone",
    "_id": "1",
    "_version": 6,
    "result": "updated",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "_seq_no": 6,
    "_primary_term": 1
}
```



### 删除文档



**请求**

```http
DELETE /shopping/phone/1/ HTTP/1.1
Host: 172.20.10.11:9200
```

**响应**

```json
{
    "_index": "shopping",
    "_type": "phone",
    "_id": "1",
    "_version": 7,
    "result": "deleted",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "_seq_no": 7,
    "_primary_term": 1
}
```



### 条件删除



**先增加数据**

```json
{
    "title": "小米手机",
    "category": "小米",
    "images": "http://www.gulixueyuan.com/xm.jpg",
    "price": 4000.00
}

{
    "title": "华为手机",
    "category": "华为",
    "images": "http://www.gulixueyuan.com/hw.jpg",
    "price": 4000.00
}
```

**请求**

```http
POST /shopping/_delete_by_query HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 82

{
    "query": {
        "match": {
            "price": 4000.00
        }
    }
}
```



**响应**

```json
{
    "took": 349,
    "timed_out": false,
    "total": 2,
    "deleted": 2,
    "batches": 1,
    "version_conflicts": 0,
    "noops": 0,
    "retries": {
        "bulk": 0,
        "search": 0
    },
    "throttled_millis": 0,
    "requests_per_second": -1.0,
    "throttled_until_millis": 0,
    "failures": []
}
```



**字段解析**

```json
{
"took"【耗时】: 175,
"timed_out"【是否超时】: false,
"total"【总数】: 2,
"deleted"【删除数量】: 2,
"batches": 1,
"version_conflicts": 0,
"noops": 0,
"retries": {
"bulk": 0,
"search": 0
},
"throttled_millis": 0,
"requests_per_second": -1.0,
"throttled_until_millis": 0,
"failures": []
}
```



## 映射操作



### 创建映射



**请求**

```http
POST /student/_mapping HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 277

{
    "properties": {
        "name": {
            "type": "text",
            "index": true
        },
        "sex": {
            "type": "text",
            "index": false
        },
        "age": {
            "type": "long",
            "index": false
        }
    }
}
```

**响应**

```json
{
    "acknowledged": true
}
```

**映射数据**

字段名：随便写。

type：类型

- String类型
  - text：可分词
  - keyword：不可分词

- 数值类型
  - 基本：long、integer、short、byte、double、float、half_float
  -  浮点数的高精度类型：scaled_float

- Date：日期
- Array：数组
- Object：对象

index：是否索引，默认true。设置为true，字段可进行搜索

store：是否将数据单独储存，默认false。

- 原始的文本会存储在_source 里面，默认情况下其他提取出来的字段都不是独立存储
  的，是从_source 里面提取出来的。当然你也可以独立的存储某个字段，只要设置
  "store": true 即可，获取独立存储的字段要比从_source 中解析快得多，但是也会占用
  更多的空间，所以要根据实际业务需求来设置。

analyzer：分词器。

### 查看映射



**请求**

```http
GET /student/_mapping HTTP/1.1
Host: 172.20.10.11:9200
```

**响应**

```json
{
    "student": {
        "mappings": {
            "properties": {
                "age": {
                    "type": "long",
                    "index": false
                },
                "name": {
                    "type": "text"
                },
                "sex": {
                    "type": "text",
                    "index": false
                }
            }
        }
    }
}
```





### 索引映射关联



**不需要先创建student1**

**请求**

```http
PUT /student1 HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 377

{
    "settings": {},
    "mappings": {
        "properties": {
            "name": {
                "type": "text",
                "index": true
            },
            "sex": {
                "type": "text",
                "index": false
            },
            "age": {
                "type": "long",
                "index": false
            }
        }
    }
}
```

**响应**

```json
{
    "acknowledged": true,
    "shards_acknowledged": true,
    "index": "student1"
}
```





## 高级查询



### 查询所有文档



**添加数据**

```http
# POST /student/_doc/1001
{
    "name": "zhangsan",
    "nickname": "zhangsan",
    "sex": "男",
    "age": 30
}
# POST /student/_doc/1002
{
    "name": "lisi",
    "nickname": "lisi",
    "sex": "男",
    "age": 20
}
# POST /student/_doc/1003
{
    "name": "wangwu",
    "nickname": "wangwu",
    "sex": "女",
    "age": 40
}
# POST /student/_doc/1004
{
    "name": "zhangsan1",
    "nickname": "zhangsan1",
    "sex": "女",
    "age": 50
}
# POST /student/_doc/1005
{
    "name": "zhangsan2",
    "nickname": "zhangsan2",
    "sex": "女",
    "age": 30
}
```





**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 48

{
    "query": {
        "match_all": {}
    }
}


# "query"：这里的 query 代表一个查询对象，里面可以有不同的查询属性
# "match_all"：查询类型，例如：match_all(代表查询所有)， match，term ， range 等等
# {查询条件}：查询条件会根据类型的不同，写法也有差异
```

**响应**

```json
{
    "took": 8,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 5,
            "relation": "eq"
        },
        "max_score": 1.0,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.0,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan",
                    "sex": "男",
                    "age": 30
                }
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1002",
                "_score": 1.0,
                "_source": {
                    "name": "lisi",
                    "nickname": "lisi",
                    "sex": "男",
                    "age": 20
                }
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1003",
                "_score": 1.0,
                "_source": {
                    "name": "wangwu",
                    "nickname": "wangwu",
                    "sex": "女",
                    "age": 40
                }
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1004",
                "_score": 1.0,
                "_source": {
                    "name": "zhangsan1",
                    "nickname": "zhangsan1",
                    "sex": "女",
                    "age": 50
                }
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1005",
                "_score": 1.0,
                "_source": {
                    "name": "zhangsan2",
                    "nickname": "zhangsan2",
                    "sex": "女",
                    "age": 30
                }
            }
        ]
    }
}
```



**字段说明**

```json
{
    "took【查询花费时间，单位毫秒】": 1116,
    "timed_out【是否超时】": false,
    "_shards【分片信息】": {
        "total【总数】": 1,
        "successful【成功】": 1,
        "skipped【忽略】": 0,
        "failed【失败】": 0
    },
    "hits【搜索命中结果】": {
        "total"【搜索条件匹配的文档总数】: {
            "value"【总命中计数的值】: 3,
            "relation"【计数规则】: "eq" # eq 表示计数准确， gte 表示计数不准确
        },
        "max_score【匹配度分值】": 1.0,
        "hits【命中结果集合】": [
			。。。
        }
    ]
}
}
```



### 匹配查询



match 匹配类型查询，会把查询条件进行分词，然后进行查询，多个词条之间是 or 的关系



**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 83

{
    "query": {
        "match": {
            "name":"zhangsan"
        }
    }
}
```

**响应**

```json
{
    "took": 1,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": 1.3862942,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.3862942,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan",
                    "sex": "男",
                    "age": 30
                }
            }
        ]
    }
}
```





### 字段匹配查询



multi_match 与 match 类似，不同的是它可以在多个字段中查询。

**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 181

{
    "query": {
        "multi_match": {
            "query": "zhangsan",
            "fields": [
                "name",
                "nickname"
            ]
        }
    }
}
```

**响应**

```json
{
    "took": 7,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": 1.3862942,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.3862942,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan",
                    "sex": "男",
                    "age": 30
                }
            }
        ]
    }
}
```





### 关键字精确查询

term 查询，精确的关键词匹配查询，不对查询条件进行分词。

**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 124

{
    "query": {
        "term": {
            "name": {
                "value": "zhangsan"
            }
        }
    }
}
```

**响应**

```json
{
    "took": 1,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": 1.3862942,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.3862942,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan",
                    "sex": "男",
                    "age": 30
                }
            }
        ]
    }
}
```





### 多关键字精确查询

terms 查询和 term 查询一样，但它允许你指定多值进行匹配。
如果这个字段包含了指定值中的任何一个值，那么这个文档满足条件，类似于 mysql 的 in

**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 140

{
    "query": {
        "terms": {
            "name": [
                "zhangsan",
                "lisi"
            ]
        }
    }
}
```

**响应**

```json
{
    "took": 2,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 2,
            "relation": "eq"
        },
        "max_score": 1.0,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.0,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan",
                    "sex": "男",
                    "age": 30
                }
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1002",
                "_score": 1.0,
                "_source": {
                    "name": "lisi",
                    "nickname": "lisi",
                    "sex": "男",
                    "age": 20
                }
            }
        ]
    }
}
```





### 指定字段查询



默认情况下，Elasticsearch 在搜索的结果中，会把文档中保存在_source 的所有字段都返回。
如果我们只想获取其中的部分字段，我们可以添加_source 的过滤

**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 179

{
    "_source": [
        "name",
        "nickname"
    ],
    "query": {
        "terms": {
            "nickname": [
                "zhangsan"
            ]
        }
    }
}
```

**响应**

```json
{
    "took": 3,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": 1.0,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.0,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan"
                }
            }
        ]
    }
}
```





### 过滤字段



includes：来指定想要显示的字段
excludes：来指定不想要显示的字段

**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 219

{
    "_source": {
        "includes": [
            "name",
            "nickname"
        ]
    },
    "query": {
        "terms": {
            "nickname": [
                "zhangsan"
            ]
        }
    }
}
```

**响应**

```json
{
    "took": 4,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": 1.0,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.0,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan"
                }
            }
        ]
    }
}
```





### 组合查询



`bool`把各种其它查询通过`must`（必须 ）、`must_not`（必须不）、`should`（应该）的方
式进行组合



**实例**

```json
{
    "query": {
        "bool": {
            "must": [
                {
                    "match": {
                        "name": "zhangsan"
                    }
                }
            ],
            "must_not": [
                {
                    "match": {
                        "age": "40"
                    }
                }
            ],
            "should": [
                {
                    "match": {
                        "sex": "男"
                    }
                }
            ]
        }
    }
}
```



**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 220

{
    "query": {
        "bool": {
            "must": [
                {
                    "match": {
                        "name": "zhangsan"
                    }
                }
            ]
        }
    }
}
```

**响应**

```json
{
    "took": 2,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": 1.3862942,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.3862942,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan",
                    "sex": "男",
                    "age": 30
                }
            }
        ]
    }
}
```





### 范围查询

range 查询找出那些落在指定区间内的数字或者时间。range 查询允许以下字符



| 操作符 | 说明     |
| ------ | -------- |
| gt     | 大于     |
| gte    | 大于等于 |
| lt     | 小于     |
| lte    | 小于等于 |



**所查字段index需为true**

**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 141

{
    "query": {
        "range": {
            "age": {
                "gte": 30,
                "lte": 35
            }
        }
    }
}
```

**响应**

```json

```







### 模糊查询



返回包含与搜索字词相似的字词的文档。
编辑距离是将一个术语转换为另一个术语所需的一个字符更改的次数。这些更改可以包括：

- 更改字符（box → fox）
- 删除字符（black → lack） 
- 插入字符（sic → sick）
- 转置两个相邻字符（act → cat）

为了找到相似的术语，fuzzy 查询会在指定的编辑距离内创建一组搜索词的所有可能的变体
或扩展。然后查询返回每个扩展的完全匹配。
通过 fuzziness 修改编辑距离。一般使用默认值 AUTO，根据术语的长度生成编辑距离。

**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 125

{
    "query": {
        "fuzzy": {
            "name": {
                "value": "zhangsan"
            }
        }
    }
}
```

**响应**

```json
{
    "took": 25,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 3,
            "relation": "eq"
        },
        "max_score": 1.3862942,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.3862942,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan",
                    "sex": "男",
                    "age": 30
                }
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1004",
                "_score": 1.2130076,
                "_source": {
                    "name": "zhangsan1",
                    "nickname": "zhangsan1",
                    "sex": "女",
                    "age": 50
                }
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1005",
                "_score": 1.2130076,
                "_source": {
                    "name": "zhangsan2",
                    "nickname": "zhangsan2",
                    "sex": "女",
                    "age": 30
                }
            }
        ]
    }
}
```





### 单字段排序



sort 可以让我们按照不同的字段进行排序，并且通过 order 指定排序的方式。desc 降序，asc升序。



**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 192

{
    "query": {
        "match": {
            "name": "zhangsan"
        }
    },
    "sort": [
        {
            "age": {
                "order": "desc"
            }
        }
    ]
}
```

**响应**

```json
{
    "took": 2,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": null,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": null,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan",
                    "sex": "男",
                    "age": 30
                },
                "sort": [
                    30
                ]
            }
        ]
    }
}
```





### 多字段排序





**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 247

{
    "query": {
        "match_all": {}
    },
    "sort": [
        {
            "age": {
                "order": "desc"
            }
        },
        {
            "_score": {
                "order": "desc"
            }
        }
    ]
}
```

**响应**

```json
{
    "took": 2,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 5,
            "relation": "eq"
        },
        "max_score": null,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1004",
                "_score": 1.0,
                "_source": {
                    "name": "zhangsan1",
                    "nickname": "zhangsan1",
                    "sex": "女",
                    "age": 50
                },
                "sort": [
                    50,
                    1.0
                ]
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1003",
                "_score": 1.0,
                "_source": {
                    "name": "wangwu",
                    "nickname": "wangwu",
                    "sex": "女",
                    "age": 40
                },
                "sort": [
                    40,
                    1.0
                ]
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.0,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan",
                    "sex": "男",
                    "age": 30
                },
                "sort": [
                    30,
                    1.0
                ]
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1005",
                "_score": 1.0,
                "_source": {
                    "name": "zhangsan2",
                    "nickname": "zhangsan2",
                    "sex": "女",
                    "age": 30
                },
                "sort": [
                    30,
                    1.0
                ]
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1002",
                "_score": 1.0,
                "_source": {
                    "name": "lisi",
                    "nickname": "lisi",
                    "sex": "男",
                    "age": 20
                },
                "sort": [
                    20,
                    1.0
                ]
            }
        ]
    }
}
```







### 高亮查询



在进行关键字搜索时，搜索出的内容中的关键字会显示不同的颜色，称之为高亮。

Elasticsearch 可以对查询内容中的关键字部分，进行标签和样式(高亮)的设置。
在使用 match 查询的同时，加上一个 highlight 属性：

- pre_tags：前置标签
- post_tags：后置标签
- fields：需要高亮的字段
- title：这里声明 title 字段需要高亮，后面可以为这个字段设置特有配置，也可以空

**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 237

{
    "query": {
        "match": {
            "name": "zhangsan"
        }
    },
    "highlight": {
        "pre_tags": "<font color='red'>",
        "post_tags": "</font>",
        "fields": {
            "name": {}
        }
    }
}
```

**响应**

```json
{
    "took": 31,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": 1.3862942,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.3862942,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan",
                    "sex": "男",
                    "age": 30
                },
                "highlight": {
                    "name": [
                        "<font color='red'>zhangsan</font>"
                    ]
                }
            }
        ]
    }
}
```







### 分页查询



from：当前页的起始索引，默认从 0 开始。 from = (pageNum - 1) * size
size：每页显示多少条

**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 186

{
    "query": {
        "match_all": {}
    },
    "sort": [
        {
            "age": {
                "order": "desc"
            }
        }
    ],
    "from": 0,
    "size": 2
}
```

**响应**

```json
{
    "took": 2,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 5,
            "relation": "eq"
        },
        "max_score": null,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1004",
                "_score": null,
                "_source": {
                    "name": "zhangsan1",
                    "nickname": "zhangsan1",
                    "sex": "女",
                    "age": 50
                },
                "sort": [
                    50
                ]
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1003",
                "_score": null,
                "_source": {
                    "name": "wangwu",
                    "nickname": "wangwu",
                    "sex": "女",
                    "age": 40
                },
                "sort": [
                    40
                ]
            }
        ]
    }
}
```







### 聚合查询

聚合允许使用者对 es 文档进行统计分析，类似与关系型数据库中的 group by，当然还有很多其他的聚合，例如取最大值、平均值等等。

**对某个字段取最大值 max**

**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 135

{
    "aggs": {
        "max_age": {
            "max": {
                "field": "age"
            }
        }
    },
    "size": 0
}
```

**响应**

```json
{
    "took": 15,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 5,
            "relation": "eq"
        },
        "max_score": null,
        "hits": []
    },
    "aggregations": {
        "max_age": {
            "value": 50.0
        }
    }
}
```

**对某个字段取最小值 min**



**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 135

{
    "aggs": {
        "min_age": {
            "min": {
                "field": "age"
            }
        }
    },
    "size": 0
}
```



**响应**

```json
{
    "took": 2,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 5,
            "relation": "eq"
        },
        "max_score": null,
        "hits": []
    },
    "aggregations": {
        "min_age": {
            "value": 20.0
        }
    }
}
```

**对某个字段取总和**



**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 135

{
    "aggs": {
        "sum_age": {
            "sum": {
                "field": "age"
            }
        }
    },
    "size": 0
}
```



**响应**

```json
{
    "took": 2,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 5,
            "relation": "eq"
        },
        "max_score": null,
        "hits": []
    },
    "aggregations": {
        "sum_age": {
            "value": 170.0
        }
    }
}
```

**对某个字段的平均值**



**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 135

{
    "aggs": {
        "avg_age": {
            "avg": {
                "field": "age"
            }
        }
    },
    "size": 0
}
```



**响应**

```json
{
    "took": 2,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 5,
            "relation": "eq"
        },
        "max_score": null,
        "hits": []
    },
    "aggregations": {
        "avg_age": {
            "value": 34.0
        }
    }
}
```



**对某个字段的值进行去重之后再取总数**



**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 148

{
    "aggs": {
        "distinct_age": {
            "cardinality": {
                "field": "age"
            }
        }
    },
    "size": 0
}
```

**响应**

```json
{
    "took": 1,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 5,
            "relation": "eq"
        },
        "max_score": null,
        "hits": []
    },
    "aggregations": {
        "distinct_age": {
            "value": 4
        }
    }
}
```







**State 聚合**



**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 139

{
    "aggs": {
        "stats_age": {
            "stats": {
                "field": "age"
            }
        }
    },
    "size": 0
}
```



**响应**

```json
{
    "took": 10,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 5,
            "relation": "eq"
        },
        "max_score": null,
        "hits": []
    },
    "aggregations": {
        "distinct_age": {
            "value": 4
        }
    }
}
```



### 桶聚合查询



**桶聚和相当于 sql 中的 group by 语句**

**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 141

{
    "aggs": {
        "age_groupby": {
            "terms": {
                "field": "age"
            }
        }
    },
    "size": 0
}
```

**响应**

```json
{
    "took": 6,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 5,
            "relation": "eq"
        },
        "max_score": null,
        "hits": []
    },
    "aggregations": {
        "age_groupby": {
            "doc_count_error_upper_bound": 0,
            "sum_other_doc_count": 0,
            "buckets": [
                {
                    "key": 30,
                    "doc_count": 2
                },
                {
                    "key": 20,
                    "doc_count": 1
                },
                {
                    "key": 40,
                    "doc_count": 1
                },
                {
                    "key": 50,
                    "doc_count": 1
                }
            ]
        }
    }
}
```



**在 terms 分组下再进行聚合**

**请求**

```http
GET /student/_search HTTP/1.1
Host: 172.20.10.11:9200
Content-Type: application/json
Content-Length: 265

{
    "aggs": {
        "age_groupby": {
            "terms": {
                "field": "age"
            },
            "aggs":{
                "sum_age":{
                    "sum":{"field":"age"}
                }
            }
        }
    },
    "size": 0
}
```

**响应**

```json
{
    "took": 3,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 5,
            "relation": "eq"
        },
        "max_score": null,
        "hits": []
    },
    "aggregations": {
        "age_groupby": {
            "doc_count_error_upper_bound": 0,
            "sum_other_doc_count": 0,
            "buckets": [
                {
                    "key": 30,
                    "doc_count": 2,
                    "sum_age": {
                        "value": 60.0
                    }
                },
                {
                    "key": 20,
                    "doc_count": 1,
                    "sum_age": {
                        "value": 20.0
                    }
                },
                {
                    "key": 40,
                    "doc_count": 1,
                    "sum_age": {
                        "value": 40.0
                    }
                },
                {
                    "key": 50,
                    "doc_count": 1,
                    "sum_age": {
                        "value": 50.0
                    }
                }
            ]
        }
    }
}
```







# Java API操作



## 依赖

**pom.xml**

```xml
<dependencies>
        <dependency>
            <groupId>org.elasticsearch</groupId>
            <artifactId>elasticsearch</artifactId>
            <version>7.8.0</version>
        </dependency>
        <!-- elasticsearch 的客户端 -->
        <dependency>
            <groupId>org.elasticsearch.client</groupId>
            <artifactId>elasticsearch-rest-high-level-client</artifactId>
            <version>7.8.0</version>
        </dependency>
        <!-- elasticsearch 依赖 2.x 的 log4j -->
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-api</artifactId>
            <version>2.8.2</version>
        </dependency>
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-core</artifactId>
            <version>2.8.2</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.9.9</version>
        </dependency>
        <!-- junit 单元测试 -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
    </dependencies>
```





## 索引操作



### 创建索引



**IndexCreate.java**

```java
public class IndexCreate {

    public static void main(String[] args) throws IOException {
        // 创建客户端对象
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        // 创建索引-请求对象
        CreateIndexRequest request = new CreateIndexRequest("user");


        // 发送请求
        CreateIndexResponse response = client.indices().create(request, RequestOptions.DEFAULT);
        boolean result = response.isAcknowledged();

        System.out.println(result);
        // 关闭客户端连接
        client.close();
    }
}

```



### 查看索引



**IndexGet.java**

```java
public class IndexGet {



    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        GetIndexRequest request = new GetIndexRequest("user");
        GetIndexResponse response = client.indices().get(request, RequestOptions.DEFAULT);
        System.out.println("aliases:" + response.getAliases());
        System.out.println("mappings:" + response.getMappings());
        System.out.println("settings" + response.getSettings());
        
        client.close();
    }
}

```



### 删除索引



**IndexDelete.java**

```java
public class IndexDelete {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        DeleteIndexRequest request = new DeleteIndexRequest("user");

        AcknowledgedResponse response = client.indices().delete(request, RequestOptions.DEFAULT);
        System.out.println(response.isAcknowledged());

        client.close();
    }
}

```



## 文档操作



**User.java**

```java
package xyz.wuhen.es.demo2;

public class User {
    private String name;
    private Integer age;
    private String sex;

    public User() {

    }

    public User(String name,Integer age,String sex) {
        this.name = name;
        this.age = age;
        this.sex = sex;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }
}

```



### 新增文档



**CreateUser.java**

```java
public class CreateUser {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );
        // 新建文档-请求对象
        IndexRequest request = new IndexRequest();
        // 设置索引及id
        request.index("user").id("1001");

        //数据转json
        User user = new User("zhangsan",30,"男");
        ObjectMapper objectMapper = new ObjectMapper();
        String data = objectMapper.writeValueAsString(user);

        // 添加数据
        request.source(data, XContentType.JSON);
        IndexResponse response = client.index(request, RequestOptions.DEFAULT);

        System.out.println("_index:" + response.getIndex());
        System.out.println("_id:" + response.getId());
        System.out.println("_result:" + response.getResult());

        client.close();
    }
}

```



### 修改文档



**UpdateUser.java**

```java
public class UpdateUser {

    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        UpdateRequest request = new UpdateRequest();

        request.index("user").id("1001");
        request.doc(XContentType.JSON,"sex","女");

        UpdateResponse response = client.update(request, RequestOptions.DEFAULT);
        System.out.println("_index:" + response.getIndex());
        System.out.println("_id:" + response.getId());
        System.out.println("_result:" + response.getResult());

        client.close();
    }
}

```



### 查询文档



**GetUser.java**

```java
public class GetUser {

    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        GetRequest request = new GetRequest().index("user").id("1001");
        GetResponse response = client.get(request, RequestOptions.DEFAULT);

        System.out.println("_index:" + response.getIndex());
        System.out.println("_type:" + response.getType());
        System.out.println("_id:" + response.getId());
        System.out.println("source:" + response.getSource());
        client.close();
    }
}

```



### 删除文档



**DeleteUser.java**

```java
public class DeleteUser {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        DeleteRequest request = new DeleteRequest().index("user").id("1001");
        DeleteResponse response = client.delete(request, RequestOptions.DEFAULT);
        System.out.println(response.toString());
        client.close();
    }
}

```





### 批量操作



**批量新增**

**BatchCreateUser.java**

```java
public class BatchCreateUser {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        BulkRequest request = new BulkRequest();
        request.add(new IndexRequest().index("user").id("1001").source(XContentType.JSON,"name","haha"))
                .add(new IndexRequest().index("user").id("1002").source(XContentType.JSON,"name","jiji"));

        BulkResponse response = client.bulk(request, RequestOptions.DEFAULT);
        System.out.println("took:" + response.getTook());
        System.out.println("items:" + response.getItems());
        client.close();
    }
}

```





**批量删除**

**BatchDeleteUser.java**

```java
public class BatchDeleteUser {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        BulkRequest request = new BulkRequest();
        request.add(new DeleteRequest().index("user").id("1001"));
        request.add(new DeleteRequest().index("user").id("1002"));
        BulkResponse response = client.bulk(request, RequestOptions.DEFAULT);
        System.out.println("took:" + response.getTook());
        System.out.println("items:" + response.getItems());
        client.close();

    }
}

```







## 高级查询



**所有数据**



```json
{
    "took": 1,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 5,
            "relation": "eq"
        },
        "max_score": 1.0,
        "hits": [
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.0,
                "_source": {
                    "name": "zhangsan",
                    "nickname": "zhangsan",
                    "sex": "男",
                    "age": 30
                }
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1002",
                "_score": 1.0,
                "_source": {
                    "name": "lisi",
                    "nickname": "lisi",
                    "sex": "男",
                    "age": 20
                }
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1003",
                "_score": 1.0,
                "_source": {
                    "name": "wangwu",
                    "nickname": "wangwu",
                    "sex": "女",
                    "age": 40
                }
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1004",
                "_score": 1.0,
                "_source": {
                    "name": "zhangsan1",
                    "nickname": "zhangsan1",
                    "sex": "女",
                    "age": 50
                }
            },
            {
                "_index": "student",
                "_type": "_doc",
                "_id": "1005",
                "_score": 1.0,
                "_source": {
                    "name": "zhangsan2",
                    "nickname": "zhangsan2",
                    "sex": "女",
                    "age": 30
                }
            }
        ]
    }
}
```





### 请求体查询



**查询所有索引数据**



```java
public class Test1 {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        SearchRequest request = new SearchRequest();
        request.indices("student");
        // 构建查询请求体
        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

        // 查询所有数据
        sourceBuilder.query(QueryBuilders.matchAllQuery());
        request.source(sourceBuilder);

        SearchResponse response = client.search(request,RequestOptions.DEFAULT);

        // 查询匹配
        SearchHits hits = response.getHits();
        System.out.println("took:" + response.getTook());
        System.out.println("timeout:" + response.isTimedOut());
        System.out.println("total:" + hits.getTotalHits());
        System.out.println("MaxScore:" + hits.getMaxScore());
        System.out.println("hits=======>>");
        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        client.close();
    }
}

```





**term查询，查询条件为关键字**

**Test2.java**

```java
public class Test2 {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        SearchRequest request = new SearchRequest();
        request.indices("student");
        // 构建查询请求体
        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

        // 查询所有数据
        sourceBuilder.query(QueryBuilders.termQuery("age","30"));
        request.source(sourceBuilder);

        SearchResponse response = client.search(request, RequestOptions.DEFAULT);

        // 查询匹配
        SearchHits hits = response.getHits();
        System.out.println("took:" + response.getTook());
        System.out.println("timeout:" + response.isTimedOut());
        System.out.println("total:" + hits.getTotalHits());
        System.out.println("MaxScore:" + hits.getMaxScore());
        System.out.println("hits=======>>");
        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        client.close();
    }

}

```





**分页查询**

**Test3.java**

```java
public class Test3 {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        SearchRequest request = new SearchRequest();
        request.indices("student");
        // 构建查询请求体
        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

        // 查询所有数据
        sourceBuilder.query(QueryBuilders.matchAllQuery());
        sourceBuilder.from(0);
        sourceBuilder.size(2);
        request.source(sourceBuilder);

        SearchResponse response = client.search(request, RequestOptions.DEFAULT);

        // 查询匹配
        SearchHits hits = response.getHits();
        System.out.println("took:" + response.getTook());
        System.out.println("timeout:" + response.isTimedOut());
        System.out.println("total:" + hits.getTotalHits());
        System.out.println("MaxScore:" + hits.getMaxScore());
        System.out.println("hits=======>>");
        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        client.close();
    }
    
}

```





**数据排序**

**Test4.java**

```java
public class Test4 {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        SearchRequest request = new SearchRequest();
        request.indices("student");
        // 构建查询请求体
        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

        // 查询所有数据
        sourceBuilder.query(QueryBuilders.matchAllQuery());
        sourceBuilder.sort("age", SortOrder.ASC);

        request.source(sourceBuilder);

        SearchResponse response = client.search(request, RequestOptions.DEFAULT);

        // 查询匹配
        SearchHits hits = response.getHits();
        System.out.println("took:" + response.getTook());
        System.out.println("timeout:" + response.isTimedOut());
        System.out.println("total:" + hits.getTotalHits());
        System.out.println("MaxScore:" + hits.getMaxScore());
        System.out.println("hits=======>>");
        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        client.close();

    }
}

```



**过滤字段**

**Test5.java**

```java
public class Test5 {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        SearchRequest request = new SearchRequest();
        request.indices("student");
        // 构建查询请求体
        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

        // 查询所有数据
        sourceBuilder.query(QueryBuilders.matchAllQuery());
        String[] excludes = {};
        String[] includes = {"name","age"};
        sourceBuilder.fetchSource(includes,excludes);

        request.source(sourceBuilder);

        SearchResponse response = client.search(request, RequestOptions.DEFAULT);

        // 查询匹配
        SearchHits hits = response.getHits();
        System.out.println("took:" + response.getTook());
        System.out.println("timeout:" + response.isTimedOut());
        System.out.println("total:" + hits.getTotalHits());
        System.out.println("MaxScore:" + hits.getMaxScore());
        System.out.println("hits=======>>");
        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        client.close();

    }
}


```



**Bool查询**

**Test6.java**

```java
public class Test6 {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        SearchRequest request = new SearchRequest();
        request.indices("student");
        // 构建查询请求体
        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

        BoolQueryBuilder boolQueryBuilder = QueryBuilders.boolQuery();
        boolQueryBuilder.must(QueryBuilders.matchQuery("age","30"));
        boolQueryBuilder.mustNot(QueryBuilders.matchQuery("name","zhangsan"));
        boolQueryBuilder.should(QueryBuilders.matchQuery("sex","男"));

        // 查询所有数据
        sourceBuilder.query(boolQueryBuilder);
        request.source(sourceBuilder);

        SearchResponse response = client.search(request, RequestOptions.DEFAULT);

        // 查询匹配
        SearchHits hits = response.getHits();
        System.out.println("took:" + response.getTook());
        System.out.println("timeout:" + response.isTimedOut());
        System.out.println("total:" + hits.getTotalHits());
        System.out.println("MaxScore:" + hits.getMaxScore());
        System.out.println("hits=======>>");
        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        client.close();

    }
}
```



**范围查询**

**Test7.java**

```java
public class Test7 {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        SearchRequest request = new SearchRequest();
        request.indices("student");
        // 构建查询请求体
        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

        RangeQueryBuilder rangeQueryBuilder = QueryBuilders.rangeQuery("age");

        rangeQueryBuilder.gte("30");
        rangeQueryBuilder.lte("40");
        // 查询所有数据
        sourceBuilder.query(rangeQueryBuilder);
        request.source(sourceBuilder);

        SearchResponse response = client.search(request, RequestOptions.DEFAULT);

        // 查询匹配
        SearchHits hits = response.getHits();
        System.out.println("took:" + response.getTook());
        System.out.println("timeout:" + response.isTimedOut());
        System.out.println("total:" + hits.getTotalHits());
        System.out.println("MaxScore:" + hits.getMaxScore());
        System.out.println("hits=======>>");
        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        client.close();

    }
}

```





**模糊查询**

**Test8.java**

```java
public class Test8 {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        SearchRequest request = new SearchRequest();
        request.indices("student");
        // 构建查询请求体
        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

        // 查询所有数据
        sourceBuilder.query(QueryBuilders.fuzzyQuery("name","zhangsan").fuzziness(Fuzziness.ONE));
        request.source(sourceBuilder);

        SearchResponse response = client.search(request, RequestOptions.DEFAULT);

        // 查询匹配
        SearchHits hits = response.getHits();
        System.out.println("took:" + response.getTook());
        System.out.println("timeout:" + response.isTimedOut());
        System.out.println("total:" + hits.getTotalHits());
        System.out.println("MaxScore:" + hits.getMaxScore());
        System.out.println("hits=======>>");
        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        client.close();
    }
}

```





### 高亮查询



**Test9.java**

```java
public class Test9 {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        SearchRequest request = new SearchRequest();
        request.indices("student");
        // 构建查询请求体
        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

        TermQueryBuilder termQueryBuilder = QueryBuilders.termQuery("name","zhangsan");

        // 查询所有数据
        sourceBuilder.query(termQueryBuilder);
        request.source(sourceBuilder);

        // 构建高亮
        HighlightBuilder highlightBuilder = new HighlightBuilder();
        highlightBuilder.preTags("<font color='red'>");
        highlightBuilder.postTags("</font>");
        highlightBuilder.field("name");

        sourceBuilder.highlighter(highlightBuilder);

        SearchResponse response = client.search(request, RequestOptions.DEFAULT);

        // 查询匹配
        SearchHits hits = response.getHits();
        System.out.println("took:" + response.getTook());
        System.out.println("timeout:" + response.isTimedOut());
        System.out.println("total:" + hits.getTotalHits());
        System.out.println("MaxScore:" + hits.getMaxScore());
        System.out.println("hits=======>>");
        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());

            Map<String, HighlightField> highlightFieldMap = hit.getHighlightFields();
            System.out.println(highlightFieldMap);
        }
        client.close();

    }
}

```



### 聚合查询



**最大年龄**

**Test10.java**

```java
public class Test10 {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        SearchRequest request = new SearchRequest().indices("student");

        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();
        sourceBuilder.aggregation(AggregationBuilders.max("maxAge").field("age"));
        request.source(sourceBuilder);

        SearchResponse response = client.search(request,RequestOptions.DEFAULT);

        SearchHits hits = response.getHits();
        System.out.println(response);
        client.close();
    }
}

```





**分组统计**

**Test11.java**



```java
public class Test11 {
    public static void main(String[] args) throws IOException {
        RestHighLevelClient client = new RestHighLevelClient(
                RestClient.builder(new HttpHost("172.20.10.11",9200,"http"))
        );

        SearchRequest request = new SearchRequest().indices("student");

        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();
        sourceBuilder.aggregation(AggregationBuilders.terms("age_groupby").field("age"));
        request.source(sourceBuilder);

        SearchResponse response = client.search(request, RequestOptions.DEFAULT);

        SearchHits hits = response.getHits();
        System.out.println(response);
        client.close();
    }
}


```







