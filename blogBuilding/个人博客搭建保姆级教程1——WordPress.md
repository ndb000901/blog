## 个人博客搭建保姆级教程1——WordPress
今天用WordPress搭建一个个人博客站。废话不说了，开搞。

 ***一、Windows教程***
 **1.环境准备**
 >1.[phpstudy](https://www.xp.cn/)(一个集成了PHP MySQL Redis Apache Nginx等一系列工具的软件，让服务器配置简单化。)
 >2.[WordPress](https://github.com/WordPress/WordPress)(由于是开源项目，我们直接clone就好。)
 
 phpstudy安装，一路下一步就好。
 Word Press下载，如果装了git，直接输入以下命令就好。
 ```
 git clone  https://github.com/WordPress/WordPress.git
 ```
 没有git，那就打开网站（https://github.com/WordPress/WordPress）
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716213358709.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
点击冒绿光的Code，然后点击Download ZIP，然后解压得到源码。
**2.搭建环境**
打开phpstudy
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020071621370776.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
开启apache
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716221035882.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**注意：如果出现端口被占用，解决方案：
1.netstat -ano （cmd执行，找到占用端口进程的PID，打开任务管理器，点击结束，之后启动apache)**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716221423122.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
创建网站：
**域名：** （wordpress.myblog.com）（这玩意自己编一个，外网无法访问哦(当然通过某些骚操作也可以)，如果要用外网访问，需要公网ip，改天出个购买服务器与域名的文章）
**端口：** 默认80，如果改了其他端口，在浏览器访问时需要加端口号。ex：http://wordpress.myblog.com：10000
**根目录：** 随意，我用默认的。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716221718790.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
访问一下，成功了。（如果没有出来，刷新一下呦）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716222532309.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
安装部署wordpress，将下载的源码解压，移动到网站的根目录。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716223103286.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
在浏览器打开 **http://wordpress.myblog.com/wp-admin/setup-config.php**(把域名换成自己的)
点击let's go
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716223547431.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
数据库名：WPmyblog（随意，稍后得去创建，要与后面创建数据库一致）
数据库用户名：wuhen（随意，要与后面创建数据库一致）
密码：123456（自己填，要与后面创建数据库一致）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717005110618.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
先去安装，启动mysql，创建对应数据库。phpstudy集成了mysql，直接安装就好。我这装了mysql8.0.12。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716224611535.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
创建数据库，要与前面表格填写的一致。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716224944438.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
点击submit,看到此页面。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716225213318.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
点击 Run........，等待。填写好信息，点击Install
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020071622552922.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
成功了!!!!!!!恭喜
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716225651933.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
点击Log in
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716225737990.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
成功进入。在这你可以将语言更改为中文，也可以更改主题，自己去尽情地探索吧，奥里给。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716225826410.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

 ***二、Linux教程***
 
 **1.环境准备**
 >1.[ubuntu16.04](https://blog.csdn.net/qq_43938052/article/details/107326122)(看我博客有教程)
 >2.LAMP环境，装系统时默认装了。

**2.环境搭建**
执行命令，切换为root
```
sudo su
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716230859274.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
执行命令，查看下ip，我的ip是192.168.190.132
```
ifconfig
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716231055575.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
在浏览器访问192.168.190.132，可以看到默认页面，根目录在/var/www/html/，该页面是index.html提供的。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716231214969.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
执行命令，切换目录
```
cd /var/www/html
```
然后执行命令，将WordPress clone下来。由于某种原因，clone有些慢。
```
git clone https://github.com/WordPress/WordPress.git
```
访问**http://192.168.190.132/WordPress/wp-admin/install.php**，接下来的操作与windows相似，重点说下创建数据库。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717003420435.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
创建数据库，执行命令，输入MySQL密码，然后连接。
```
mysql -u root -p
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717003532715.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
执行命令，创建数据库（数据库名随意，与安装时填一致就好，数据库默认root，密码是安装[Ubuntu16.04](https://blog.csdn.net/qq_43938052/article/details/107326122)时你自己设的）
```
create database WPmyblog;
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717003605262.png)
输入命令，查看是否成功。成功后输入exit退出。
```
show databases;
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717003659729.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717004207308.png)
好啦，WordPress的教程到此为止，希望可以帮到大家。

>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)