# springcloud初试





# 一、服务注册与发现



**数据库cloud.payment**

```sql
create table payment
(
    id     bigint auto_increment comment 'ID'
        primary key,
    serial varchar(200) default '' null
)
    charset = utf8;
```





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



### 工程

```ini
# consul
172.20.10.11

# 支付模块集群
cloud-provider-consul-payment8021
cloud-provider-consul-payment8022
cloud-provider-consul-payment8023

# 消费者
cloud-consumer-order4020

# 通用模块
cloud-api-commons
```









# 二、服务调用



## 1、Ribbon





### 工程

```ini
# Eureka集群

cloud-eureka-server7001
cloud-eureka-server7002
cloud-eureka-server7003

# 支付模块集群
cloud-provider-payment8031
cloud-provider-payment8032
cloud-provider-payment8033

# 消费者
cloud-consumer-order4030

# 消费者-自己编写负载均衡算法
cloud-consumer-order4030

# 通用模块
cloud-api-commons
```



### 负载均衡算法



| 类                                                 | 说明                                                         |
| -------------------------------------------------- | ------------------------------------------------------------ |
| com.netflix.loadbalancer.IRule                     | 规则需实现该接口                                             |
| com.netflix.loadbalancer.RoundRobinRule            | 轮询                                                         |
| com.netflix.loadbalancer.RandomRule                | 随机                                                         |
| com.netflix.loadbalancer.RetryRule                 | 先使用RoundRobinRule策略获取服务，若获取服务失败则在指定时间内会进行重试，获取可用的服务 |
| com.netflix.loadbalancer.ResponseTimeWeightedRule  | RoundRobinRule的拓展，响应速度越快的实例权重越大，越容易被选择 |
| com.netflix.loadbalancer.BestAvailableRule         | 先过滤掉由于多次访问故障而处于断路器跳闸状态的服务，然后选择一个并发量最小的服务 |
| com.netflix.loadbalancer.AvailabilityFilteringRule | 先过滤掉故障实例，再选择并发量较小的实例                     |
| com.netflix.loadbalancer.ZoneAvoidanceRule         | 默认规则，复合判断server所在区域的性能和server的可用性选择服务器 |





### 更改负载均衡规则



```
官方文档明确给出了警告：
这个自定义配置类不能放在@ComponentScan所扫描的当前包下以及子包下，
否则我们自定义的这个配置类就会被所有的Ribbon客户端所共享，达不到特殊化定制的目的了。
```



**MyRule.java**

```java
@Configuration
public class MyRule {

    @Bean
    public IRule randomRule() {
        return new RandomRule();
    }
}
```



**MainApp4030.java**

```java
@SpringBootApplication
@EnableEurekaClient
@RibbonClient(name = "CLOUD-PAYMENT-SERVICE",configuration= MyRule.class)
public class MainApp4030 {
    public static void main(String[] args) {
        SpringApplication.run(MainApp4030.class,args);

    }
}
```





## 2、OpenFeign



### 工程

```ini
# Eureka集群

cloud-eureka-server7001
cloud-eureka-server7002
cloud-eureka-server7003

# 支付模块集群
cloud-provider-payment8031
cloud-provider-payment8032
cloud-provider-payment8033

# 消费者
cloud-consumer-openfeign-order4050


```



### 超时控制

```yml
#设置feign客户端超时时间(OpenFeign默认支持ribbon)
ribbon:
#指的是建立连接所用的时间，适用于网络状况正常的情况下,两端连接所用的时间
  ReadTimeout: 5000
#指的是建立连接后从服务器读取到可用资源所用的时间
  ConnectTimeout: 5000
```





### 日志打印功能



**OpenFeignConfig.java**

```java
@Configuration
public class OpenFeignConfig {

    @Bean
    public Logger.Level feignLoggerLevel() {
        return Logger.Level.FULL;
    }
}
```



**application.yml**



```yml
  logging:
    level:
      # feign日志以什么级别监控哪个接口
      com.atguigu.springcloud.service.PaymentFeignService: debug
```







# 三、断路器



## 1、Hystrix



### 工程

```ini
# Eureka集群

cloud-eureka-server7001
cloud-eureka-server7002
cloud-eureka-server7003

# 支付模块
cloud-provider-hystrix-payment8041

# 消费者
cloud-consumer-feign-hystrix-order4060

# 监控面板
cloud-consumer-hystrix-dashboard9001
```



### 概念

```ini
# 服务降级

服务降级一般是指在服务器压力剧增的时候，根据实际业务使用情况以及流量，对一些服务和页面有策略的不处理或者用一种简单的方式进行处理，从而释放服务器资源的资源以保证核心业务的正常高效运行。

# 服务熔断

应对雪崩效应的链路自我保护机制。可看作降级的特殊情况。

# 服务限流
对超出服务处理能力之外的请求进行拦截，对访问服务的流量进行限制。
```



# 四、网关



## 1、Gateway



### 项目

```ini
# Eureka集群

cloud-eureka-server7001
cloud-eureka-server7002
cloud-eureka-server7003

# 支付模块
cloud-provider-gateway-payment8051
cloud-provider-gateway-payment8052
cloud-provider-gateway-payment8053

# 网关
cloud-gateway9527
```





# 五、分布式配置中心



## 1、SpringConfig



### 项目

```ini
# Eureka集群

cloud-eureka-server7001
cloud-eureka-server7002
cloud-eureka-server7003

# 配置中心
cloud-config-center3344

# 客户端
cloud-config-client3355
```





# 六、消息总线



## 1、SpringCloud Bus



### 项目



```ini
# Eureka集群

cloud-eureka-server7001
cloud-eureka-server7002
cloud-eureka-server7003

# 配置中心
cloud-config-center3344

# 客户端
cloud-config-client3355
cloud-config-client3366
```



# 七、消息驱动



## 1、SpringCloud Stream



### 项目



```ini
# Eureka集群

cloud-eureka-server7001
cloud-eureka-server7002
cloud-eureka-server7003

# 生产者
cloud-stream-rabbitmq-provider8801

# 消费者
cloud-stream-rabbitmq-consumer8802
cloud-stream-rabbitmq-consumer8803
```





# 八、链路跟踪



## 1、SpringCloud Sleuth



### 项目



```ini
# Eureka集群

cloud-eureka-server7001
cloud-eureka-server7002
cloud-eureka-server7003

# 支付服务
cloud-provider-payment8061

# 消费者
cloud-consumer-order8062

```



# 九、Nacos



## 1、注册中心



### 项目



```ini
# nacos下载
https://github.com/alibaba/nacos

# nacos管理界面
http://172.20.10.11:8848/nacos

# 支付模块
cloud-alibaba-provider-payment8071
cloud-alibaba-provider-payment8072

# 消费者
cloud-alibaba-nacos-consumer-order8073
```



## 2、配置中心



### 项目



```ini
# 配置中心
172.20.10.11:8848

# 服务
cloud-alibaba-config-nacos-client8074
```



## 3、持久化



### 配置



```ini
vim application.properties

#添加以下内容##
spring.datasource.platform=mysql
 
db.num=1
db.url.0=jdbc:mysql://172.20.10.11:3306/nacos_config?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
db.user=root
db.password=root
###

# 执行/conf/nacos-mysql.sql
```





## 4、集群



### nginx配置



**nginx.conf**

```ini
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;
    
    upstream cluster{
        server 172.20.10.11:8848;
        server 172.20.10.12:8848;
        server 172.20.10.13:8848;
    }

    server {
        listen       10000;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            #root   html;
            #index  index.html index.htm;
	    proxy_pass http://cluster;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}

```



### nacos集群配置



**/conf/cluster.conf**

```ini

#it is ip
172.20.10.11:8848
172.20.10.12:8848
172.20.10.13:8848

```



# 十、Sentinel



## 1、基础使用



### 项目



```ini
cloud-alibaba-sentinel-service8401
```



## 2、sentinel + ribbon



### 项目



```ini
# nacos 集群
172.20.10.11:8848
172.20.10.12:8848
172.20.10.13:8848

# sentinel
172.20.10.8080

# 支付模块
cloud-alibaba-provider-payment9003
cloud-alibaba-provider-payment9004

# 客户端
cloud-alibaba-nacos-consumer-order9001
```



## 3、sentinel + feign



### 项目



```ini
# nacos 集群
172.20.10.11:8848
172.20.10.12:8848
172.20.10.13:8848

# sentinel
172.20.10.8080

# 支付模块
cloud-alibaba-provider-payment9003
cloud-alibaba-provider-payment9004

# 客户端
cloud-alibaba-nacos-consumer-order9002
```





## 4、持久化



### 项目



```ini
# nacos 集群
172.20.10.11:8848
172.20.10.12:8848
172.20.10.13:8848

# sentinel
172.20.10.8080


cloud-alibaba-sentinel-service8402
```





# 十一、Seata



### 项目

```ini
# nacos 集群
172.20.10.11:8848
172.20.10.12:8848
172.20.10.13:8848

# seata
172.20.10.11:8091

# 订单
cloud-alibaba-seata-order2001

# 库存
cloud-alibaba-seata-storage2002

# 帐号
cloud-alibaba-seata-account2003

```

