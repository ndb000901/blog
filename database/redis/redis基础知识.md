# redis基础知识

## 数据类型

**字符串(String)**

**最大储存512MB**

```
# 添加
set <keyName> "value"
# 获取
get <keyName>
# 删除
del <keyName>
```

**哈希(Hash)**

**redis hash 是一个键值对集合，每个hash可以储存2^32 - 1个键值对**

```
# 添加
hmset <集合名> <键1> <值1> <键2> <值2>

# 获取
hget <集合名> <键>

# 删除
del <集合名>
```

**列表(List)**


**redis list是字符串列表，每个list可以储存2^32 - 1个元素**

```
# 添加
lpush <列表名> <值>

# 查看第x至y
lrange <列表名> x y

# 删除
del <列表名>

```

**集合(Set)**

**redis set 是string类型的无序集合，最大储存2^32 - 1个元素，元素唯一**

```
# 添加
sadd <集合名> <值>

# 查看 
smembers <集合名>

# 删除 
del <集合名>
```

**有序集合(zset)**

**redis zset 和set一样也是string类型元素集合，最大元素2^32 - 1,元素不允许重复。每个元素关联一个double类型的分数，redis通过该值排序**

```
# 添加
zadd <集合名> <分数> <值>

# 删除
del <集合名>

# 查看第x至y个元素
zrangebyscore <集合名> x y
```
