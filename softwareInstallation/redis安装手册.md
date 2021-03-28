## Windows安装

**1.实验环境**

>1.win10
>
>2.redis-5.0.9([资源地址](https://github.com/tporadowski/redis/releases/download/v5.0.9/Redis-x64-5.0.9.zip))

**2.安装验证**

下载之后解压。

![image](https://user-images.githubusercontent.com/48900845/112761507-378fd300-902e-11eb-9736-31c06c5cbb42.png)

打开PowerShell，切换到该目录。

![image](https://user-images.githubusercontent.com/48900845/112761514-3f4f7780-902e-11eb-8cd9-457f4810bb89.png)

执行命令，开启服务端
```
.\redis-server.exe
```

![image](https://user-images.githubusercontent.com/48900845/112761526-46768580-902e-11eb-9948-ad241f2b404a.png)

服务端启动成功。
再打开一个PowerShell窗口，切换到该目录，执行命令启动客户端
```
 .\redis-cli.exe
```

验证一下

![image](https://user-images.githubusercontent.com/48900845/112761536-4ecec080-902e-11eb-87c4-08e38694cf07.png)


---

##  ubuntu安装

**1.实验环境**

>1.ubuntu16.04([安装教程](https://blog.csdn.net/qq_43938052/article/details/107326122))
>
>2.gcc 5.4.0
>
>**安装：apt install gcc**
>
>3.make 4.1
>
>**安装 apt install make**
>
>4.redis-6.0.8([下载地址](http://download.redis.io/releases/redis-6.0.8.tar.gz))

**2.安装步骤**

先切换到root权限。

切换路径
```
cd /usr/local
```
新建redis目录
```
mkdir redis
```
下载
```
cd mkdir 
wget http://download.redis.io/releases/redis-6.0.8.tar.gz
```
解压
```
tar xzvf redis-6.0.8.tar.gz
```

![image](https://user-images.githubusercontent.com/48900845/112761560-6dcd5280-902e-11eb-9ef5-534895213fea.png)

编译

**注意：执行make命令前要装好gcc、make**
```
cd redis-6.0.8
make
```
编译成功后，src目录下将生成redis-server、redis-cli

![image](https://user-images.githubusercontent.com/48900845/112761570-7756ba80-902e-11eb-8edd-c9bc29c1dd55.png)

**3.验证**

执行命令，启动服务端
```
./redis-server
```

![image](https://user-images.githubusercontent.com/48900845/112761577-82a9e600-902e-11eb-8e55-a70250ee4d82.png)


成功

再打开一个终端窗口，执行命令，启动客户端。

```
.\redis-cli
```

![image](https://user-images.githubusercontent.com/48900845/112761587-8c334e00-902e-11eb-9d84-59ad30f14722.png)


**4.设置远程连接**

用windows的redis-cli连接虚拟机ubuntu的redis。

在Ubuntu中Ctrl+c先关掉已经运行的redis-server。

写个redis的配置文件
```
vim /etc/redis/redis.conf
#若无该/etc/redis目录，可以创建一个，当然你也可以自定义。
```
写入以下内容，保存。
```
bind 0.0.0.0
```
启动redis服务端
```
cd /usr/local/redis/redis-6.0.8/src/
./redis-server /etc/redis/redis.conf
```

![image](https://user-images.githubusercontent.com/48900845/112761604-9b1a0080-902e-11eb-8251-82a3e0e47ea9.png)

在windows打开PowerShell，切换到redis-cli目录，执行命令。
```
.\redis-cli.exe -h 192.168.146.104 -p 6379
```
-p为端口，在服务端可以自定义。

验证

![image](https://user-images.githubusercontent.com/48900845/112761613-a2410e80-902e-11eb-8bc2-205d8af0c38c.png)

今天的文章到此结束。


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)





