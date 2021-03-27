## Windows安装
**1.实验环境**
>1.win10
>2.redis-5.0.9([资源地址](https://github.com/tporadowski/redis/releases/download/v5.0.9/Redis-x64-5.0.9.zip))

**2.安装验证**
下载之后解压。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006162305557.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)

打开PowerShell，切换到该目录。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020100616244235.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
执行命令，开启服务端
```
.\redis-server.exe
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006162551202.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
服务端启动成功。
再打开一个PowerShell窗口，切换到该目录，执行命令启动客户端
```
 .\redis-cli.exe
```

验证一下


![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006162904833.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)

---

##  ubuntu安装
**1.实验环境**
>1.ubuntu16.04([安装教程](https://blog.csdn.net/qq_43938052/article/details/107326122))
>2.gcc 5.4.0
>**安装：apt install gcc**
>3.make 4.1
>**安装 apt install make**
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
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006164642432.png#pic_center)
编译
**注意：执行make命令前要装好gcc、make**
```
cd redis-6.0.8
make
```
编译成功后，src目录下将生成redis-server、redis-cli

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020100616535683.png#pic_center)

**3.验证**
执行命令，启动服务端
```
./redis-server
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006165722166.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
成功
再打开一个终端窗口，执行命令，启动客户端。
```
.\redis-cli
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006165930485.png#pic_center)

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
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006172627660.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)

在windows打开PowerShell，切换到redis-cli目录，执行命令。
```
.\redis-cli.exe -h 192.168.146.104 -p 6379
```
-p为端口，在服务端可以自定义。

验证
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006172930736.png#pic_center)
今天的文章到此结束。
>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)







