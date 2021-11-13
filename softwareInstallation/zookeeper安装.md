# Zookeeper安装



## 环境

```
1.ubuntu18.04
2.zookeeper3.5.7
```

**zookeeper下载地址(https://zookeeper.apache.org/releases.html)[https://zookeeper.apache.org/releases.html]**



## 安装



自己找个目录，解压即可。

## 配置



**conf/zoo.cfg**

```ini
# The number of milliseconds of each tick
# 通信心跳时间，Zookeeper服务器与客户端心跳时间，单位毫秒
tickTime=2000
# The number of ticks that the initial 
# synchronization phase can take
# LF初始通信时限
initLimit=10
# The number of ticks that can pass between 
# sending a request and getting an acknowledgement
# LF同步通信时限
syncLimit=5
# the directory where the snapshot is stored.
# do not use /tmp for storage, /tmp here is just 
# example sakes.
# 保存Zookeeper中的数据
dataDir=/home/hello/local/zookeeper/apache-zookeeper-3.5.7-bin/data
# the port at which the clients will connect
# 客户端连接端口，通常不做修改。
clientPort=2181
# the maximum number of client connections.
# increase this if you need to handle more clients
#maxClientCnxns=60
#
# Be sure to read the maintenance section of the 
# administrator guide before turning on autopurge.
#
# http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
#
# The number of snapshots to retain in dataDir
#autopurge.snapRetainCount=3
# Purge task interval in hours
# Set to "0" to disable auto purge feature
#autopurge.purgeInterval=1

#######################cluster##########################
server.1=172.20.10.11:2888:3888
server.2=172.20.10.12:2888:3888
server.3=172.20.10.13:2888:3888

```

**集群配置**

在dataDir目录下建立myid文件，填写id数字



**备注：server.A=B:C:D**

```
A--->myid
B--->主机地址
C--->Follower 与集群中的 Leader 服务器交换信息的端口
D--->选举端口
```



