# springcloud初试





# 服务注册





## 1、Eureka



### 工程

```ini
# Eureka集群

cloud-eureka-server7001
cloud-eureka-server7002
cloud-eureka-server7003

# 支付模块集群
cloud-provider-payment8001
cloud-provider-payment8002
cloud-provider-payment8003

# 消费者
cloud-consumer-order4000

# 通用模块
cloud-api-commons
```







## 2、Zookeeper



### 工程

```ini
# zookeeper集群-3.5.7
172.20.10.11：2181
172.20.10.12：2181
172.20.10.13：2181

# 支付模块集群
cloud-provider-payment8011
cloud-provider-payment8012
cloud-provider-payment8013

# 消费者
cloud-consumer-order4010

# 通用模块
cloud-api-commons
```



### zookeeper配置



**在dataDir目录下建立myid文件，填写id数字**



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





## 3、Consul







# 服务调用







