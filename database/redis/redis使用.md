# 1、redis数据类型

## 字符串(String)



**数据结构：**

底层为简单动态字符串(Simple Dynamic String, SDS)，可修改字符串，类似ArrayList，采用预分配冗余空间的方式来较少内存的频繁分配。

最大长度：512MB

扩容：字符串小于1MB，扩容加倍，超过1MB，扩容加1MB。

**操作命令**

| 命令                         | 说明                                        |
| ---------------------------- | ------------------------------------------- |
| set <key>  <value>           | 添加键值对                                  |
| get <key>                    | 查询键值对                                  |
| append <key> <value>         | 追加value到指定key对应的value末尾           |
| strlen <key>                 | 获得值的长度                                |
| setnx <key> <value>          | 当key不存在时，添加键值对                   |
| incr <key>                   | 将key对应的值加1(对数字值)，若为空，设置为1 |
| decr <key>                   | 将key对应值-1(针对数值),若空，设置为-1      |
| incrby/decrby  <key> <value> | 将key对应的值增加/减小value                 |
| mset <k1> <v1>  <k2> <v2>    | 同时设置多个值                              |
| mget <k1> <k2>               | 同时获取多个值                              |
| msetnx <k1> <v1> <k2> <v2>   | 当所有key 不存在时，可执行成功              |
| getrange <k> <v1> <v2>       | 截取[v1,v2]                                 |
| setrange <k> <start> <v>     | 从start位置开始使用v覆盖                    |
| setex <k> <time> <v>         | 设置键值对过期时间                          |
| getset <k> <v>               | 设置新值，获取旧值                          |
|                              |                                             |
| *NX                          | key不存在可添加                             |
| *XX                          | key存在时可添加，与NX互斥                   |
| *EX                          | key超时秒数                                 |
| *PX                          | key超时毫秒数与EX互斥                       |



## 列表(List)



**数据结构：**

List数据结构为快速链表quickList,在元素较少时使用一块连续的内存存储，这个结构是ziplist(压缩链表)，当数据量过大时使用双向指针，将多个ziplist链接起来使用。

**常用命令**

| 命令                         | 说明                                        |
| ---------------------------- | ------------------------------------------- |
| lpush/rpush <k> <v1> <v2>    | 从左边/右边插入多个值                       |
| lpop/rpop <key>              | 从左边/右边吐出一个值，若键中无值，则键销毁 |
| rpoplpush <k1> <k2>          | 从k1右边吐出一个值插入到k2左边              |
| lrange <k> <start> <stop>    | 获取[start,stop]索引范围数据                |
| lindex <k> <index>           | 获取index位置数据                           |
| llen <k>                     | 获得列表长度                                |
| linsert <k> before <v1> <v2> | 在v1 前插入v2                               |
| lrem <k> <n> <v>             | 从左开始删除n个v                            |
| lset <k> <index> <v>         | 替换index位置的值为v                        |



## 集合(Set)



**数据结构**

Set数据结构为dict字典，用hash表实现。Set 是String 类型的无序集合，不可有重复数据。添加，删除，查找时间复杂度为O(1)

**常用命令**

| 命令                             | 说明                        |
| -------------------------------- | --------------------------- |
| sadd <k> <v1> <v2>               | 添加数据，当v存在时忽略     |
| smembers <k>                     | 取出集合所有值              |
| sismember <k> <v>                | 是否存在v，存在1,不存在0    |
| scard <k>                        | 集合数据个数                |
| srem <k> <v1> <v2>               | 删除数据                    |
| spop <k>                         | 随机吐出一个值              |
| srandmember <k> <n>              | 随机取n个值，不删除         |
| smove <source> <destination> <v> | 把集合中v移到另一个集合     |
| sinter <k1> <k2>                 | 交集                        |
| sunion <k1> <k2>                 | 并集                        |
| sdiff <k1> <k2>                  | 差集(存在于k1,k2中不存在的) |



## 哈希(Hash)



**数据结构：**

类似Java 中Map<String,Object>，当field-value 长度较短且个数较少时，使用ziplist，否则使用hashtable

**常用命令**



| 命令                         | 说明                       |
| ---------------------------- | -------------------------- |
| hset <k> <f> <v>             | 添加                       |
| hget <k> <f>                 | 从k集合取出键f 对应的value |
| hmset <k> <f1> <v1> <k2><v2> | 批量添加                   |
| hexists  <k> <f>             | 查看f是否存在              |
| hkeys <k>                    | 列出所有field              |
| hvals <k>                    | 列出所有value              |
| hincrby <k> <f> <v>          | f增加v                     |
| hsetnx <k> <f> <v>           | 当f不存在时添加            |
|                              |                            |



## 有序集合(Zset)



**数据结构：**

与Java中Map<String,Double>类似，每个value对应一个权重score，数据不可重复。

2个数据结构：

1、hash 用来关联value和权重score，保障value的唯一性，可通过value找到对应的score值。

2、跳跃表，跳跃表的目的在于给元素value排序，根据score的范围获取元素列表。

**常用命令**

| 命令                                   | 说明                                        |
| -------------------------------------- | ------------------------------------------- |
| zadd <k> <s1> <v1> <s2> <v2>           | 添加元素                                    |
| zrange <k> <start> <stop> [withscores] | 返回索引[start,stop]元素，可与score一起返回 |
| zrangebyscore <k> <min> <max>          | 返回score在[min,max]范围的数据，升序        |
| zrevrangebyscore <k> <max> <min>       | 返回score在[min,max]范围的数据，降序        |
| zincrby <k> <incrment> <v>             | 为元素score加上incrment                     |
| zrem <k> <v>                           | 删除值为v的元素                             |
| zcount <k> <min> <max>                 | 统计score在[min,max]个数                    |
| zrank <k> <v>                          | 返回排名，从0开始                           |





## Bitmaps





## HyperLogLog





## Geospatial





# 2、配置文件





# 3、Redis 事务







# 4、Redis持久化



## RDB (Redis Database)



## AOF (Append Only File)







# 5、Redis 主从复制







# 6、Redis 集群





# 7、Redis应用问题



## 缓存穿透



## 缓存击穿



## 缓存雪崩



## 分布式锁











