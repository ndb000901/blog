



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



**数据结构：**

可位操作的字符串

**常用命令**

| 命令                                  | 说明                                   |
| ------------------------------------- | -------------------------------------- |
| setbit <k> <offset> <v>               | 设置bitmaps中某个偏移量的值为0/1       |
| getbit <k> <offset>                   | 获取bitmaps中某个偏移量的值            |
| bitcount <k> <start> <end>            | 统计字符串从[start,end]比特值为1的数量 |
| bitop <and/or/not/xor> <k1> <k2> <k3> | 将k2,k3做and,or,not,xor,将结果存入k1中 |






## HyperLogLog



**数据结构：**

用来做基数统计的算法，每个HyperLogLog键只需要花费 12 KB 内存，就可以计算接近 2^64 个不同元素的基数。

什么是基数?

比如数据集 {1, 3, 5, 7, 5, 7, 8}， 那么这个数据集的基数集为 {1, 3, 5 ,7, 8}, 基数(不重复元素)为5。 基数估计就是在误差可接受的范围内，快速计算基数。

 

**常用命令**

| 命令                 | 说明                                                     |
| -------------------- | -------------------------------------------------------- |
| pfadd <k> <element>  | 添加元素至HyperLogLog，若估计基数变化，则返回1,否则返回0 |
| pfcount <k>          | 返回估计基数                                             |
| pfmerge <k1> <s....> | 将多个HLL合并，结果存至k1                                |






## Geospatial



**简介：**

Redis 3.2 中增加了对GEO类型的支持。GEO，Geographic，地理信息的缩写。该类型，就是元素的2维坐标，在地图上就是经纬度。redis基于该类型，提供了经纬度设置，查询，范围查询，距离查询，经纬度Hash等常见操作



**常用命令**

| 命令                                                    | 说明                                       |
| ------------------------------------------------------- | ------------------------------------------ |
| geoadd <k> <longitude><latitude><member>                | 添加地理位置(经度，维度，名称)             |
| geopos <k> <member>                                     | 获得坐标                                   |
| geodist <k> <m1> <m2> [m\|km\|ft\|mi]                   | 两地距离，m(米),km(千米),ft(英尺),mi(英里) |
| georadius <k> <longitude><latitude> <r> [m\|km\|ft\|mi] | 以给定经纬度为中心，找出r为半径的元素      |
|                                                         |                                            |



# 2、配置文件



## Units单位

大小写不敏感

```ini
# 1k => 1000 bytes
# 1kb => 1024 bytes
# 1m => 1000000 bytes
# 1mb => 1024*1024 bytes
# 1g => 1000000000 bytes
# 1gb => 1024*1024*1024 bytes
```

## INCLUDES包含



可包含其他配置文件

```ini
# include /path/to/local.conf
# include /path/to/other.conf
```

## 网络配置



| 配置           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| bind           | 限制访问ip，未设置-->无限制                                  |
| protected-mode | 如果开启了protected-mode，那么在没有设定bind ip且没有设密码的情况下，Redis只允许接受本机的响应 |
| port           | 端口                                                         |
| tcp-backlog    | backlog队列总和=未完成三次握手队列 + 已经完成三次握手队列    |
| timeout        | 一个空闲的客户端维持多少秒会关闭，0表示关闭该功能。即永不关闭。 |
| tcp-keepalive  | 对访问客户端的一种心跳检测，每个n秒检测一次。单位为秒，如果设置为0，则不会进行Keepalive检测，建议设置成60 |
|                |                                                              |

## 通用



| 配置      | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| daemonize | 是否为后台进程，设置为yes,守护进程，后台启动                 |
| pidfile   | 存放pid文件的位置，每个实例会产生一个不同的pid文件           |
| loglevel  | 指定日志记录级别，Redis总共支持四个级别：debug、verbose、notice、warning，默认为**notice**,四个级别根据使用阶段来选择，生产环境选择notice 或者warning |
| logfile   | 日志文件名称                                                 |
| databases | 设定库的数量 默认16，默认数据库为0                           |



## 安全



| 配置        | 说明 |
| ----------- | ---- |
| requirepass | 密码 |



## 限制



| 配置              | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| maxclients        | 设置redis同时可以与多少个客户端进行连接。默认情况下为10000个客户端 |
| maxmemory         | 最大内存                                                     |
| maxmemory-policy  | 内存满后，策略                                               |
| maxmemory-samples | 设置样本数量，LRU算法和最小TTL算法都并非是精确的算法，而是估算值，所以你可以设置样本的大小，redis默认会检查这么多个key并选择其中LRU的那个。一般设置3到7的数字，数值越小样本越不准确，但性能消耗越小 |
|                   |                                                              |

**maxmemory-policy**

| 策略            | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| volatile-lru    | 使用LRU算法移除key，只对设置了过期时间的键；（最近最少使用） |
| allkeys-lru     | 在所有集合key中，使用LRU算法移除key                          |
| volatile-random | 在过期集合中移除随机的key，只对设置了过期时间的键            |
| allkeys-random  | 在所有集合key中，移除随机的key                               |
| volatile-ttl    | 移除那些TTL值最小的key，即那些最近要过期的key                |
| noeviction      | 不进行移除。针对写操作，只是返回错误信息                     |



# 3、Redis 事务



## Multi   Exec  discard



**multi**

开启组队

```
multi
cmd1
cmd2
cmd3
```

**discard**

放弃组队



**exec**

执行组队命令

## 事务的错误处理



multi阶段：任何一个任务错误都会导致组队失败，所有任务都被取消。

exec状态：若执行出错，则错误命令不成功，其它命令照常执行，不会回滚。

## Watch key [key ...]



在执行multi之前，先执行watch key1 [key2],可以监视一个(或多个) key ，如果在事务执行之前这个 key被其他命令所改动，那么事务将被打断。



## unwatch



如果在执行 WATCH 命令之后，EXEC 命令或DISCARD 命令先被执行了的话，那么就不需要再执行UNWATCH 了。



## Redis事务三特性



| 特性               | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| 单独的隔离操作     | 事务中的所有命令都会序列化、按顺序地执行。事务在执行的过程中，不会被其他客户端发送来的命令请求所打断。 |
| 没有隔离级别的概念 | 队列中的命令没有提交之前都不会实际被执行，因为事务提交前任何指令都不会被实际执行 |
| 不保证原子性       | 事务中如果有一条命令执行失败，其后的命令仍然会被执行，没有回滚 |



# 4、Redis持久化



## RDB (Redis Database)



**配置**

```ini
# The filename where to dump the DB
dbfilename dump.rdb


# Note that you must specify a directory here, not a file name.
dir ./

# Unless specified otherwise, by default Redis will save the DB:
#   * After 3600 seconds (an hour) if at least 1 key changed
#   * After 300 seconds (5 minutes) if at least 100 keys changed
#   * After 60 seconds if at least 10000 keys changed
#
# You can set these explicitly by uncommenting the three following lines.
#
save 3600 1
save 300 100
save 60 10000
```

**恢复**



```ini
# 查询rdb目录
config get dir
```

将rdb文件放至redis-server工作目录下，启动服务后会自动加载。

**fork**

Fork的作用是复制一个与当前进程一样的进程。新进程的所有数据（变量、环境变量、程序计数器等） 数值都和原进程一致，但是是一个全新的进程，并作为原进程的子进程。

**优点**

- 适合大规模的数据恢复
- 对数据完整性和一致性要求不高更适合使用
- 节省磁盘空间
- 恢复速度快

**缺点**

- Fork的时候，内存中的数据被克隆了一份，大致2倍的膨胀性需要考虑
- 虽然Redis在fork时使用了**写时拷贝技术**,但是如果数据庞大时还是比较消耗性能。

- 在一定间隔时间做一次备份，所以如果Redis意外down掉的话，就会丢失最后一次快照后的所有修改。



## AOF (Append Only File)



**简介**

以日志的形式来记录每个写操作（增量保存），将Redis执行过的所有写指令记录下来(读操作不记录)， 只许追加文件但不可以改写文件，redis启动之初会读取该文件重新构建数据，换言之，redis 重启的话就根据日志文件的内容将写指令从前到后执行一次以完成数据的恢复工作。



**配置**

```ini
# AOF and RDB persistence can be enabled at the same time without problems.
# If the AOF is enabled on startup Redis will load the AOF, that is the file
# with the better durability guarantees.
#
# Please check https://redis.io/topics/persistence for more information.

appendonly yes

# The name of the append only file (default: "appendonly.aof")

appendfilename "appendonly.aof"


# no: don't fsync, just let the OS flush the data when it wants. Faster.
# always: fsync after every write to the append only log. Slow, Safest.
# everysec: fsync only one time every second. Compromise.

# appendfsync always
appendfsync everysec
# appendfsync no
```

**优先级**

AOF 与 RDB同时开启，系统默认加载AOF数据（数据完整性好）





**同步频率**



- appendfsync always 始终同步，每次Redis的写入都会立刻记入日志；性能较差但数据完整性比较好

- appendfsync everysec  每秒同步，每秒记入日志一次，如果宕机，本秒的数据可能丢失。

- appendfsync no  redis不主动进行同步，把同步时机交给操作系统。

**正常恢复**

- 修改默认的appendonly no，改为yes
- 将有数据的aof文件复制一份保存到对应目录(查看目录：config get dir)
- 恢复：重启redis然后重新加载

**异常恢复**

- 修改默认的appendonly no，改为yes
- 如遇到AOF文件损坏，通过/usr/local/bin/redis-check-aof--fix appendonly.aof进行恢复
- 备份被写坏的AOF文件
- 恢复：重启redis，然后重新加载

**rewrite**

Redis会记录上次重写时的AOF大小，默认配置是当AOF文件大小是上次rewrite后大小的一倍且文件大于64M时触发。重写虽然可以节约大量磁盘空间，减少恢复时间。但是每次重写还是有一定的负担的，因此设定Redis要满足一定条件才会进行重写。

**优点**

- 备份机制更稳健，丢失数据概率更低。
- 可读的日志文本，通过操作AOF稳健，可以处理误操作。

**缺点**

- 比起RDB占用更多的磁盘空间。
- 恢复备份速度要慢。
- 每次读写都同步的话，有一定的性能压力。
- 存在个别Bug，造成恢复不能。





## 如何使用



- 官方推荐两个都启用。

- 如果对数据不敏感，可以选单独用RDB。

- 不建议单独用 AOF，因为可能会出现Bug。

- 如果只是做纯内存缓存，可以都不用。

# 5、发布订阅

**订阅**

subscribe <channel>

**发布**

publish <channel> <msg>

# 6、Redis 主从复制



## 简介

主机数据更新后根据配置和策略， 自动同步到备机的master/slaver机制，Master以写为主，Slave以读为主。

## 优点

- 读写分离，性能扩展
- 容灾快速恢复

## 配置

```ini
# 节点1(主机)
172.20.10.11：6379
# 节点2(从机)
172.20.10.12：6379
# 节点3(从机)
172.20.10.13：6379

# redis.conf

各节点 bind <主机ip> #若仅允许指定ip连接请设置防火墙

# 查看信息
info replication

# 给从机指定主机
slaveof <主机ip> <端口> 

# 将从机设置为主机
slaveof no one
```

## 恢复

- 主机挂 -->重起即可
- 从机挂-->重新设置(slaveof <主机ip> <端口>)



## 常用模式



**一主二仆**

**薪火相传**

**反客为主**

## 哨兵模式



**配置**

```ini
# 节点1(主机)
172.20.10.11：6379
# 节点2(从机)
172.20.10.12：6379
# 节点3(从机)
172.20.10.13：6379
```

**sentinel.conf**

```ini
sentinel monitor mymaster 172.20.10.11 6379 1
```

**执行命令**

```bash
redis-sentinel sentinel.conf
```

**故障恢复**

主机挂后，将重新选举主机，旧主机变为从机



# 7、Redis 集群



## 配置



```ini

# 端口
port 6379
# pid 位置
pidfile "/var/run/redis_6379.pid"
# rdb文件
dbfilename "dump6379.rdb"
# 工作目录
dir "/home/bigdata/redis_cluster"
# 日志
logfile "/home/bigdata/redis_cluster/redis_err_6379.log"
# 开启集群
cluster-enabled yes
# 设定节点配置文件名
cluster-config-file nodes-6379.conf
# 设定节点失联时间，超过该时间（毫秒），集群自动进行主从切换
cluster-node-timeout 15000

```



**启动**

````
# 节点1
172.20.10.11：6379
# 节点2
172.20.10.11：6380
# 节点3
172.20.10.12：6379
# 节点4
172.20.10.12：6380
# 节点5
172.20.10.13：6379
# 节点6
172.20.10.13：6380


启动所有节点

# 将6个节点组成1主1从集群
./redis-cli --cluster create --cluster-replicas 1 172.20.10.11:6379 172.20.10.11:6380 172.20.10.12:6379 172.20.10.12:6380 172.20.10.13:6379 172.20.10.13:6380

# 查看集群信息
cluster nodes

# 采用集群策略连接，添加数据会自动切换相应的写主机
redis-cli -c -h 172.20.10.11 -p 6379

````



## slots



一个 Redis 集群包含 16384 个插槽（hash slot）， 数据库中的每个键都属于这 16384 个插槽的其中一个， 

集群使用公式 CRC16(key) % 16384 来计算键 key 属于哪个槽， 其中 CRC16(key) 语句用于计算键 key 的 CRC16 校验和 。

## 故障恢复



- 主机挂 从机变主机，主机重启后变为从机。
- 主从皆挂 若cluster-require-full-coverage 为yes，集群挂，反之，某一段插槽挂。

## 优点

- 实现扩容

- 分摊压力

- 无中心配置相对简单

## 缺点

- 多键操作是不被支持的 

- 多键的Redis事务是不被支持的。lua脚本不被支持

- 由于集群方案出现较晚，很多公司已经采用了其他的集群方案，而代理或者客户端分片的方案想要迁移至redis cluster，需要整体迁移而不是逐步过渡，复杂度较大。

# 8、Redis应用问题



## 缓存穿透

**描述**

- key对应的数据在数据源并不存在，每次针对此key的请求从缓存获取不到，请求都会压到数据源，从而可能压垮数据源。比如用一个不存在的用户id获取用户信息，不论缓存还是数据库都没有，若黑客利用此漏洞进行攻击可能压垮数据库。

**解决**

- **对空值缓存：**如果一个查询返回的数据为空（不管是数据是否不存在），我们仍然把这个空结果（null）进行缓存，设置空结果的过期时间会很短，最长不超过五分钟

- **设置可访问的名单（白名单）：**使用bitmaps类型定义一个可以访问的名单，名单id作为bitmaps的偏移量，每次访问和bitmap里面的id进行比较，如果访问id不在bitmaps里面，进行拦截，不允许访问。

- **采用布隆过滤器**：(布隆过滤器（Bloom Filter）是1970年由布隆提出的。它实际上是一个很长的二进制向量(位图)和一系列随机映射函数（哈希函数）。布隆过滤器可以用于检索一个元素是否在一个集合中。它的优点是空间效率和查询时间都远远超过一般的算法，缺点是有一定的误识别率和删除困难。)将所有可能存在的数据哈希到一个足够大的bitmaps中，一个一定不存在的数据会被 这个bitmaps拦截掉，从而避免了对底层存储系统的查询压力。

- **进行实时监控**：当发现Redis的命中率开始急速降低，需要排查访问对象和访问的数据，和运维人员配合，可以设置黑名单限制服务

## 缓存击穿

**描述**

- key对应的数据存在，但在redis中过期，此时若有大量并发请求过来，这些请求发现缓存过期一般都会从后端DB加载数据并回设到缓存，这个时候大并发的请求可能会瞬间把后端DB压垮。

**解决**

- **预先设置热门数据：**在redis高峰访问之前，把一些热门数据提前存入到redis里面，加大这些热门数据key的时长

- **实时调整**：现场监控哪些数据热门，实时调整key的过期时长

- **使用锁**：

  就是在缓存失效的时候（判断拿出来的值为空），不是立即去load db。先使用缓存工具的某些带成功操作返回值的操作（比如Redis的SETNX）去set一个mutex key。当操作返回成功时，再进行load db的操作，并回设缓存,最后删除mutex key；当操作返回失败，证明有线程在load db，当前线程睡眠一段时间再重试整个get缓存的方法

## 缓存雪崩

**描述**

- key对应的数据存在，但在redis中过期，此时若有大量并发请求过来，这些请求发现缓存过期一般都会从后端DB加载数据并回设到缓存，这个时候大并发的请求可能会瞬间把后端DB压垮。缓存雪崩与缓存击穿的区别在于这里针对很多key缓存，前者则是某一个key正常访问。

**解决**

- **构建多级缓存架构：**nginx缓存 + redis缓存 +其他缓存（ehcache等）

- **使用锁或队列**：用加锁或者队列的方式保证来保证不会有大量的线程对数据库一次性进行读写，从而避免失效时大量的并发请求落到底层存储系统上。不适用高并发情况

- **设置过期标志更新缓存：**记录缓存数据是否过期（设置提前量），如果过期会触发通知另外的线程在后台去更新实际key的缓存。

- **将缓存失效时间分散开：**比如我们可以在原有的失效时间基础上增加一个随机值，比如1-5分钟随机，这样每一个缓存的过期时间的重复率就会降低，就很难引发集体失效的事件。

 

## 分布式锁











