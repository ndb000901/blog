## 个人博客搭建保姆级教程1——WordPress

今天用WordPress搭建一个个人博客站。废话不说了，开搞。

 ***一、Windows教程***
 
 **1.环境准备**
 >1.[phpstudy](https://www.xp.cn/)(一个集成了PHP MySQL Redis Apache Nginx等一系列工具的软件，让服务器配置简单化。)
 >
 >2.[WordPress](https://github.com/WordPress/WordPress)(由于是开源项目，我们直接clone就好。)
 
 phpstudy安装，一路下一步就好。
 Word Press下载，如果装了git，直接输入以下命令就好。
 
 ```
 git clone  https://github.com/WordPress/WordPress.git
 ```
 
 没有git，那就打开网站（https://github.com/WordPress/WordPress）
 
![image](https://user-images.githubusercontent.com/48900845/112758340-728b0a00-9020-11eb-8b47-a29bd20749dd.png)

 
点击冒绿光的Code，然后点击Download ZIP，然后解压得到源码。

**2.搭建环境**

打开phpstudy

![image](https://user-images.githubusercontent.com/48900845/112758346-7d459f00-9020-11eb-9d99-ca20dec648c7.png)

开启apache

![image](https://user-images.githubusercontent.com/48900845/112758356-89c9f780-9020-11eb-8e03-c98cd6f0c024.png)

**注意：如果出现端口被占用，解决方案：

1.netstat -ano （cmd执行，找到占用端口进程的PID，打开任务管理器，点击结束，之后启动apache)**

![image](https://user-images.githubusercontent.com/48900845/112758374-a403d580-9020-11eb-8cf4-21bf011e40c0.png)

创建网站：

**域名：** （wordpress.myblog.com）（这玩意自己编一个，外网无法访问哦(当然通过某些骚操作也可以)，如果要用外网访问，需要公网ip，改天出个购买服务器与域名的文章）

**端口：** 默认80，如果改了其他端口，在浏览器访问时需要加端口号。ex：http://wordpress.myblog.com：10000

**根目录：** 随意，我用默认的。

![image](https://user-images.githubusercontent.com/48900845/112758379-b2ea8800-9020-11eb-8cf9-06f707938831.png)

访问一下，成功了。（如果没有出来，刷新一下呦）

![image](https://user-images.githubusercontent.com/48900845/112758384-bd0c8680-9020-11eb-89cf-9f9b8491d8df.png)

安装部署wordpress，将下载的源码解压，移动到网站的根目录。

![image](https://user-images.githubusercontent.com/48900845/112758392-c5fd5800-9020-11eb-98b3-161cfb61b17d.png)

在浏览器打开 **http://wordpress.myblog.com/wp-admin/setup-config.php**(把域名换成自己的)

点击let's go

![image](https://user-images.githubusercontent.com/48900845/112758405-d6153780-9020-11eb-9bf7-93415fa906bd.png)

数据库名：WPmyblog（随意，稍后得去创建，要与后面创建数据库一致）

数据库用户名：wuhen（随意，要与后面创建数据库一致）

密码：123456（自己填，要与后面创建数据库一致）

![image](https://user-images.githubusercontent.com/48900845/112758415-e0373600-9020-11eb-9e69-d6eeb28625fc.png)

先去安装，启动mysql，创建对应数据库。phpstudy集成了mysql，直接安装就好。我这装了mysql8.0.12。

![image](https://user-images.githubusercontent.com/48900845/112758424-e9c09e00-9020-11eb-9416-c72b8865304d.png)


创建数据库，要与前面表格填写的一致。

![image](https://user-images.githubusercontent.com/48900845/112758429-f3e29c80-9020-11eb-948f-6a5bc42b6d27.png)

点击submit,看到此页面。

![image](https://user-images.githubusercontent.com/48900845/112758439-fcd36e00-9020-11eb-81dc-ebe166c24e5d.png)

点击 Run........，等待。填写好信息，点击Install

![image](https://user-images.githubusercontent.com/48900845/112758445-05c43f80-9021-11eb-92cd-cf6ec171ce55.png)

成功了!!!!!!!恭喜

![image](https://user-images.githubusercontent.com/48900845/112758453-0d83e400-9021-11eb-8a4e-c88fd828978c.png)

点击Log in

![image](https://user-images.githubusercontent.com/48900845/112758458-15438880-9021-11eb-8b6f-32b324719cea.png)

成功进入。在这你可以将语言更改为中文，也可以更改主题，自己去尽情地探索吧，奥里给。

![image](https://user-images.githubusercontent.com/48900845/112758469-22f90e00-9021-11eb-8997-ab0281ae7f0c.png)


 ***二、Linux教程***
 
 **1.环境准备**
 >1.[ubuntu16.04](https://blog.csdn.net/qq_43938052/article/details/107326122)(看我博客有教程)
 >
 >2.LAMP环境，装系统时默认装了。

**2.环境搭建**

执行命令，切换为root

```
sudo su
```
![image](https://user-images.githubusercontent.com/48900845/112758491-4ae87180-9021-11eb-94a2-de20edef3832.png)

执行命令，查看下ip，我的ip是192.168.190.132

```
ifconfig
```

![image](https://user-images.githubusercontent.com/48900845/112758500-576cca00-9021-11eb-9cb1-9b2db7bd8930.png)

在浏览器访问192.168.190.132，可以看到默认页面，根目录在/var/www/html/，该页面是index.html提供的。

![image](https://user-images.githubusercontent.com/48900845/112758514-65bae600-9021-11eb-83c7-38b23c17ce85.png)

执行命令，切换目录
```
cd /var/www/html
```
然后执行命令，将WordPress clone下来。由于某种原因，clone有些慢。
```
git clone https://github.com/WordPress/WordPress.git
```
访问**http://192.168.190.132/WordPress/wp-admin/install.php**，接下来的操作与windows相似，重点说下创建数据库。

![image](https://user-images.githubusercontent.com/48900845/112758527-7ff4c400-9021-11eb-8ba5-95dbd8fbec94.png)

创建数据库，执行命令，输入MySQL密码，然后连接。
```
mysql -u root -p
```

![image](https://user-images.githubusercontent.com/48900845/112758534-8c791c80-9021-11eb-9e29-e664df852edd.png)


执行命令，创建数据库（数据库名随意，与安装时填一致就好，数据库默认root，密码是安装[Ubuntu16.04](https://blog.csdn.net/qq_43938052/article/details/107326122)时你自己设的）
```
create database WPmyblog;
```

![image](https://user-images.githubusercontent.com/48900845/112758550-9bf86580-9021-11eb-8f74-9cd8f2002db5.png)

输入命令，查看是否成功。成功后输入exit退出。
```
show databases;
```
![image](https://user-images.githubusercontent.com/48900845/112758562-a9adeb00-9021-11eb-9d99-a311786f9549.png)

![image](https://user-images.githubusercontent.com/48900845/112758567-b2062600-9021-11eb-8f65-7de6bae2bfdd.png)

好啦，WordPress的教程到此为止，希望可以帮到大家。


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
