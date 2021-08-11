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

# 删除
del <列表名>

```

**集合(Set)**

**有序集合(zset)**

