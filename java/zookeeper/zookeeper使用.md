# Zookeeper使用



## 服务端启动



```
Usage: ./zkServer.sh [--config <conf-dir>] {start|start-foreground|stop|restart|status|print-cmd}
```



## 客户端启动



**连接服务端**

```
./zkCli.sh -server 172.20.10.11:2181
```

## 客户端交互命令



### 可用命令

```ini
ZooKeeper -server host:port cmd args
	addauth scheme auth
	close 
	config [-c] [-w] [-s]
	connect host:port
	create [-s] [-e] [-c] [-t ttl] path [data] [acl]
	delete [-v version] path
	deleteall path
	delquota [-n|-b] path
	get [-s] [-w] path
	getAcl [-s] path
	history 
	listquota path
	ls [-s] [-w] [-R] path
	ls2 path [watch]
	printwatches on|off
	quit 
	reconfig [-s] [-v version] [[-file path] | [-members serverID=host:port1:port2;port3[,...]*]] | [-add serverId=host:port1:port2;port3[,...]]* [-remove serverId[,...]*]
	redo cmdno
	removewatches path [-c|-d|-a] [-l]
	rmr path
	set [-s] [-v version] path data
	setAcl [-s] [-v version] [-R] path acl
	setquota -n|-b val path
	stat [-w] path
	sync path

```



### ls -s \<path\>

```ini
[zk: 172.20.10.13:2181(CONNECTED) 3] ls -s /haha
# 创建节点的事务 zxid
# 每次修改 ZooKeeper 状态都会产生一个 ZooKeeper 事务 ID。事务 ID 是 ZooKeeper 中所
# 有修改总的次序。每次修改都有唯一的 zxid，如果 zxid1 小于 zxid2，那么 zxid1 在 zxid2 之
# 前发生。
[ki]cZxid = 0x100000068
# znode 被创建的毫秒数（从 1970 年开始）
ctime = Fri Nov 12 19:01:53 UTC 2021
# znode 最后更新的事务 zxid
mZxid = 0x100000068
# znode 最后修改的毫秒数（从 1970 年开始）
mtime = Fri Nov 12 19:01:53 UTC 2021
# znode 最后更新的子节点 zxid
pZxid = 0x100000074
# znode 子节点变化号，znode 子节点修改次数
cversion = 1
# znode 数据变化号
dataVersion = 0
# znode 访问控制列表的变化号
aclVersion = 0
# 如果是临时节点，这个是 znode 拥有者的 session id。如果不是
# 临时节点则是 0。
ephemeralOwner = 0x0
# znode 的数据长度
dataLength = 10
# znode 子节点数量
numChildren = 1

```

### 节点类型

**持久**

```
create /haha
```

**持久 + 有序号**

```
create -s /haha
```

**临时**

```
create -e /haha
```

**临时 + 有序号**

```
create -e -s /haha
```

### 节点值

**建立节点时设置值**

```
create /haha value
```

**获取值**

```
get /haha
```

**修改值**

```
set /haha newValue
```

### 删除节点



**delete**

```ini
# 不包含子节点
delete <path>
```

**deleteall**

```ini
# 包含子节点
deleteall <path>
```



## 客户端API



**pom.xml**

```xml
<dependency>
<groupId>org.apache.zookeeper</groupId>
<artifactId>zookeeper</artifactId>
<version>3.5.7</version>
</dependency>
```

**Application.java**

```java
public class Application {
    private static String connectString = "172.20.10.11:2181";
    private static int sessionTimeout = 2000;
    private static ZooKeeper cli;
    public static void main(String[] args) throws IOException, InterruptedException, KeeperException {
        cli = new ZooKeeper(connectString, sessionTimeout, new Watcher() {
            public void process(WatchedEvent event) {
                System.out.println("getType---->" + event.getType() + "    getPath--->" + event.getPath());
                List<String> list = new LinkedList<>();
                try {
                    list.addAll(cli.getChildren("/",true));
                    list.forEach(v->{
                        System.out.println(v);
                    });
                } catch (KeeperException e) {
                    e.printStackTrace();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }

            }
        });

//        String nodeCreated = cli.create("/haha","haha-value".getBytes(), ZooDefs.Ids.OPEN_ACL_UNSAFE,CreateMode.PERSISTENT);

//        List<String> children = cli.getChildren("/haha", true);
//        for (String v : children) {
//            System.out.println(v);
//        }
//        System.out.println("end-----");
//        Thread.sleep(20 * 1000);

        Stat exists = cli.exists("/haha123", true);
        System.out.println(exists);
    }
}

```



# 服务动态上下线



**client.java**

```java
package xyz.wuhen.zookeeper.demo2;

import org.apache.zookeeper.WatchedEvent;
import org.apache.zookeeper.Watcher;
import org.apache.zookeeper.ZooKeeper;

import java.io.IOException;
import java.nio.channels.SeekableByteChannel;
import java.nio.charset.StandardCharsets;
import java.util.ArrayList;
import java.util.List;

public class Client {
    private static String connectString = "172.20.10.11:2181";
    private static int sessionTimeOut = 2000;
    private ZooKeeper client = null;
    private String parentNode = "/servers";

    public void getConnect() throws IOException {
        client = new ZooKeeper(connectString, sessionTimeOut, new Watcher() {
            @Override
            public void process(WatchedEvent event) {
                try {
                    getServerList();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        });
    }

    public void getServerList() throws Exception {
        List<String> children = client.getChildren(parentNode,true);
        ArrayList<String> servers = new ArrayList<>();

        for (String child : children) {
            servers.add(new String(child));
        }
        System.out.println(servers);
    }

    public void business() throws Exception {
        System.out.println("client is working ....");
        Thread.sleep(Integer.MAX_VALUE);
    }

    public static void main(String[] args) throws Exception {
        Client work = new Client();
        work.getConnect();
        work.getServerList();
        work.business();
    }
}

```



**server.java**

```java
package xyz.wuhen.zookeeper.demo2;

import org.apache.zookeeper.*;

import java.io.IOException;
import java.nio.charset.StandardCharsets;

public class Server {

    private static String connectString = "172.20.10.11:2181";
    private static int sessionTimeOut = 2000;
    private ZooKeeper server = null;
    private String parentNode = "/servers";

    public void getConnect() throws IOException {
        server = new ZooKeeper(connectString, sessionTimeOut, new Watcher() {
            @Override
            public void process(WatchedEvent event) {

            }
        });
    }

    public void registerServer(String hostname) throws Exception {
        String create = server.create(parentNode + "/servers",hostname.getBytes(), ZooDefs.Ids.OPEN_ACL_UNSAFE, CreateMode.EPHEMERAL_SEQUENTIAL);
        System.out.println(hostname + " is online " + create);
    }

    public void business(String hostname) throws Exception {
        System.out.println(hostname + " is working....");
        Thread.sleep(Integer.MAX_VALUE);
    }

    public static void main(String[] args) throws Exception {
        Server server = new Server();
        server.getConnect();
        server.registerServer("server");
        server.business("server");
    }
}

```



# 分布式锁



## Curator



### 依赖

**pom.xml**

```xml
<dependency>
<groupId>org.apache.curator</groupId>
<artifactId>curator-framework</artifactId>
<version>4.3.0</version>
</dependency>
<dependency>
<groupId>org.apache.curator</groupId>
<artifactId>curator-recipes</artifactId>
<version>4.3.0</version>
</dependency>
<dependency>
<groupId>org.apache.curator</groupId>
<artifactId>curator-client</artifactId>
<version>4.3.0</version>
</dependency>
```

**Application.java**

```java
public class Application {
    private String rootNode = "/locks";

    private String connectString = "172.20.10.11:2181";
    private int connectionTimeout = 2000;
    private int sessionTimeOut = 2000;

    public static void main(String[] args) {
        new Application().work();
    }
    private void work() {
        final InterProcessLock lock1 = new InterProcessMutex(getCuratorFramework(),rootNode);
        final InterProcessLock lock2 = new InterProcessMutex(getCuratorFramework(),rootNode);
        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    lock1.acquire();
                    System.out.println("Thread1 --->lock1");
                    lock1.acquire();
                    System.out.println("Thread1 --->lock2");
                    Thread.sleep(5000);
                    lock1.release();
                    System.out.println("Thread1 ---->unlock1");
                    lock1.release();
                    System.out.println("Thread1 ---->unlock2");

                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }).start();

        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    lock2.acquire();
                    System.out.println("Thread2 --->lock1");
                    lock2.acquire();
                    System.out.println("Thread2 --->lock2");
                    Thread.sleep(5000);
                    lock2.release();
                    System.out.println("Thread2 ---->unlock1");
                    lock2.release();
                    System.out.println("Thread2 ---->unlock2");

                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }).start();
    }

    public CuratorFramework getCuratorFramework() {
        RetryPolicy policy = new ExponentialBackoffRetry(3000,3);
        CuratorFramework client = CuratorFrameworkFactory.builder()
                .connectString(connectString)
                .connectionTimeoutMs(connectionTimeout)
                .sessionTimeoutMs(sessionTimeOut)
                .retryPolicy(policy).build();

        client.start();
        System.out.println("zookeeper 初始化完成...");
        return client;
    }
}

```





# 选举机制



## 选举机制



**半数机制，超过半数的投票通过，即通过。**

### 第一次启动选举规则

投票过半数时，服务器 id 大的胜出

### 第二次启动选举规则

1、EPOCH 大的直接胜出
2、EPOCH 相同，事务 id 大的胜出
3、事务 id 相同，服务器 id 大的胜出

# 生产集群安装多少 zk 合适





## 安装奇数台



## 生产经验

- 10 台服务器：3 台 zk；
- 20 台服务器：5 台 zk；
- 100 台服务器：11 台 zk；
- 200 台服务器：11 台 zk
- 服务器台数多：
  - 好处，提高可靠性；
  - 坏处：提高通信延时;

# 