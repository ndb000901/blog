## 个人博客搭建保姆级教程2——halo
halo：java开发的一个优秀的开源博客应用。需要jdk环境，与tomcat。废话不说了，直接开搞。

**Linux部署**

**1.环境准备**
>1.[ubuntu16.04](https://blog.csdn.net/qq_43938052/article/details/107326122)
>2.[tomcat8.5.57](https://us.mirrors.quenda.co/apache/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57.tar.gz)
>3.JDK8
>4.[halo1.3.2(jar包)](https://github.com/halo-dev/halo/releases/download/v1.3.2/halo-1.3.2.jar)


**2.安装JDK8**
执行命令，输入密码，切换root权限。
```
sudo su
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718195641684.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
执行命令，安装JDK8，需要等待一会。
```
apt-get install openjdk-8-jdk
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718195824773.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
执行命令，查看JDK是否安装成功。
```
java -version
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718200007276.png)
**3.安装tomcat**
执行以下命令，切换目录
```
cd /usr/local/
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718200153410.png)
执行命令，创建tomcat目录
```
mkdir tomcat
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718200309362.png)
执行命令，切换到tomcat路径下。
```
cd tomcat
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718200416818.png)
执行命令，下载tomcat
```
wget https://us.mirrors.quenda.co/apache/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57.tar.gz
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718200956570.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
执行命令，解压tomcat
```
tar xvzf apache-tomcat-8.5.57.tar.gz
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718201233518.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

**4.安装halo**
执行命令，切换目录到webapps
```
cd apache-tomcat-8.5.57/webapps/
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718201849486.png)
执行命令，下载[halo1.3.2](https://github.com/halo-dev/halo/releases/download/v1.3.2/halo-1.3.2.jar)
```
wget https://github.com/halo-dev/halo/releases/download/v1.3.2/halo-1.3.2.jar -O halo-latest.jar
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718202135654.png)
**5.运行halo**
执行命令，启动tomcat。(只要执行startup.sh就好，方法随意)，成功如下图。
```
bash /usr/local/tomcat/apache-tomcat-8.5.57/bin/startup.sh
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718202552405.png)
执行halo-latest.jar(一定要把路径切换到webapps，否则会找不到jar包)
```
java -jar halo-latest.jar
```
开始启动了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020071820303274.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
启动成功，打开浏览器访**http://192.168.190.132:8090**（ip换成你自己的，服务器都连到了，应该不会不知道IP吧）端口是8090，不要搞忘了。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718212825810.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
填写信息
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718213319847.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718213403253.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
安装
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020071821350581.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
登录
![](https://img-blog.csdnimg.cn/20200718213532127.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
成功了，nice，释放你的激情，尽情地探索吧！！！（可以换主题啥的，自己去玩吧）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718213611762.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**windows部署**

**1.环境准备**
>1.[tomcat-8.5.57](https://mirrors.sonic.net/apache/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57-windows-x64.zip)
>2.JDK8(这个网上一搜就有了，我就不写了)
>3.[halo-1.3.2](https://github.com/halo-dev/halo/releases/download/v1.3.2/halo-1.3.2.jar)

**2.tomcat**
下载（**https://mirrors.sonic.net/apache/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57-windows-x64.zip**），解压，OK。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718215402477.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**3.halo**
下载（https://github.com/halo-dev/halo/releases/download/v1.3.2/halo-1.3.2.jar），放到tomcat 下的webapps目录。
**4.运行**
启动tomcat，双击bin目录下startup.bat

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718220631522.png)
启动halo，（cmd 或 power shell执行下面命令），其实双击下载的jar包也可以，只是看不到日志
```
java -jar (jar包路径)

```
访问http://127.0.0.1:8090/    成功了。后面的操作请参考Linux部署教程。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718221209226.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)