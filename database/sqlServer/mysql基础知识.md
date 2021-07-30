# mysql基础知识



## 创建数据库

```
create database <数据库名>;
```

## 删除数据库

```
drop database <数据库名>;
```

## 创建表

```
create table <表名> (列名1 列1类别...,
                     列名2 列2类别...);
```

## 删除表

```
drop table <表名>;
```

## 修改表

**修改表名**

```
alter table <表名> rename to <新表名>
```

**增加字段**

```
alter table <表名> add <字段名> <字段类型>
```

**删除字段**

```
alter table <表名> drop <字段名>
```

**修改字段**

```
# modify
alter table <表名> modify <字段名> <新类型>

# change
alter table <表名> change <旧字段名> <新字段名> <新类型>
```

## 增加数据

```
insert into <表名> (字段1，字段2，字段3) values(值1，值2，值3),(值1，值2，值3),(值1，值2，值3);
```

## 删除数据

```
delete from <表名> where ...;
```

**注意：若不加where条件，将删除表中所有数据**

## 修改数据

```
update <表名> set <字段1>=<值1>,<字段2>=<值2>,<字段3>=<值3>;
```

## 查询数据

```
select <需查询的字段名> from <表明>
```
## 数据排序

```
select <字段名...> from <表名> order by <字段名> [ASC 或 DESC];
```

|参数|说明|
|----|----|
|ASC|升序|
|DESC|降序|

## like使用

```
select <字段1,字段2> from <表名> where <字段1> like '%ji%';
```

|参数|说明|
|----|----|
|%|匹配任意长度字符|
|\_|匹配任意单个字符|
|\[\]|表示括号内所列字符中的一个(类似正则表达式)|
|\[^\]|表示不在括号所列之内的单个字符|


## 连接

|类别|说明|
|----|----|
|inner join|内连接|
|left join|左连接|
|right join|右连接|

**内连接：获取两个表中字段匹配关系的记录**

**左连接：获取左表所有记录，即使右表没有对应匹配的记录**

**右连接：获取右表所有记录，即使左表没有对应匹配的记录**

## union

**用于连接两个以上的select 语句的结果组合到一个结果集合中，多个select 语句默认删除重复的数据**

```
select <字段> from <表名> [where...] union [all | distinct] select <字段> from <表名> [where...]
```

|参数|说明|
|----|----|
|distinct|删除结果集中重复的数据，union默认删除了重复的数据|
|all|返回所以结果，包括重复数据|

## 分组(group by)

**根据一个或多个列对结果集进行分组**

```
select <字段> from <表名> group by <字段>
```


## 事务

**在mysql中并不是所有的数据库引擎都支持事务，Innodb数据库引擎支持事务**

**事务的四个特性(ACID)**

|特性|说明|
|----|----|
|原子性(Atomicity)|一个事务中的所有操作，要么全部完成，要不全部不完成，不可卡在中间某个步骤。若执行错误，会被回滚到执行事务之前的状态。|
|一致性(Consistency)|成功执行事务后，数据库的完整性不会遭到破坏。|
|隔离性(Isolation)|数据库允许多个并发事务同时对其数据进行读写和修改的能力。事务隔离级别:读未提交、读提交、可重复读、串行化|
|持久性(Durability)|执行事务后，对数据的修改是永久的|

**改变mysql的自动提交模式**

**mysql 命令行默认设置，事务为自动提交**

```
set autocommit=0  #禁止自动提交
set autocommit=1  #开启自动提交
```

**begin 或 start transaction 显示开启一个事务**

**commit 或 commit work 提交事务**

**rollback 或 rollback work 回滚，并撤销正在进行的所以未提交的修改**

**savepoint identifier savepoint 允许在事务中创建一个保存点，可有多个**

**release savepoint identifier 删除一个事务的保存点，当没有指定保存点，抛出一个异常**

**rollback to identifier 把事务回滚到标记点**

**set transaction 用来设置事务隔离级别**


## 普通索引

**优点：大大提高查询速度**

**缺点：降低更新表的速度，例如insert、update、delete。占用较多储存空间**

**创建索引**

```
create index <索引名> on <表名> (字段名)
```

**添加索引(修改表结构)**

```
alter table <表名> add index <索引名>(字段名)
```

**删除索引**

```
drop index [索引名] on <表名>
```

## 唯一索引

**索引列的值必须唯一，但允许有空值。如果是组合索引，则列值的组合必须唯一**

**创建索引**

```
create unique index <索引名> on <表名> (字段名)
```

**修改表字段，添加索引**

```
alter table <表名> add unique [索引名] (字段名) 
```

**常见alter命令添加和删除索引**

```
# 添加主键，索引值必须唯一，且不为NULL
alter table <表名> add primary key <字段名>

# 索引值唯一，可有多个NULL
alter table <表名> add unique <索引名>(字段名)

# 索引值可出现多次
alter table <表名> add index <索引名>(字段名)

# 全文索引
alter table <表名> add fulltext <索引名>(字段名)

# 删除索引
alter table <表名> drop index <字段>
```

## 临时表

**只在当前连接存在，关闭连接后销毁**

**创建**

```
create temporary table <表明>();
```

## 复制表

```
# 显示创建表的sql语句
show create table <表名>;
```

## 元数据

```
# 显示版本
select version()

# 显示当前数据库名
select database()

# 显示当前用户名
select user()

# 服务器状态
show status

# 服务器配置变量
show variables
```

## 导出数据

**导出sql格式的数据**

```
mysqldump -u root -p --no-create-info --tab=<路径> <数据库> <表名>

mysqldump -u root -p <数据库> <表名> > dump.txt

select * from <表名> into outfile '<文件路径>'
```

## 导入数据

**使用mysql导入**

```
mysql -u <用户名> -p <密码> < <数据sql脚本>
```

**使用source导入**

```
create database <数据库名>;
use <数据库名>
set names utf8;
source <脚本路径>
```

**使用 load data导入**

**若指定local关键词，则文件从本地查找**

```
load data local infile '<文件路径>' into table <表名>

# 设置列顺序
load data local infile '<文件路径>' into table <表名> (列1,列2...);

```

**使用mysqlimport 导入数据**

```
mysqlimport -u <用户名> -p --local <表名> <数据文件>

# 设置列顺序
mysqlimport -u <用户名> -p --local --columns=列1,列2... <表名> <数据文件>

# 设置格式
mysqlimport -u <用户名> -p --local --fields-terminated-by":" --line-terminated-by="\r\n" <表名> <数据文件>
```

## 运算符

**逻辑运算符**

**位运算符**

|符号|说明|
|----|----|
|&|按位与|
|\||按位或|
|^|按位异或|
|!|取反|
|<<|左移|
|>>|右移|
