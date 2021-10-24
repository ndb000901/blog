# rabbitmq安装

## 环境

```
ubuntu18.04
```

## erlang 安装

下载地址及安装地址(https://www.erlang-solutions.com/downloads/)

## rabbitmq 安装


下载地址(https://github.com/rabbitmq/rabbitmq-server/releases)


安装教程(https://www.rabbitmq.com/install-debian.html)


erlang与rabbitmq 对应版本(https://www.rabbitmq.com/which-erlang.html)


## 配置


**添加用户并设置权限**

```
rabbitmqctl add_user codesheep 123456
rabbitmqctl set_user_tags codesheep administrator
```

**开启web监控面板**

**地址： http://172.20.10.11:15672/** 

```
rabbitmq-plugins enable rabbitmq_management
```

