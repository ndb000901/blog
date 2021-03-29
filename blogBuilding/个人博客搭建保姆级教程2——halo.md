## 个人博客搭建保姆级教程2——halo

halo：java开发的一个优秀的开源博客应用。需要jdk环境，与tomcat。废话不说了，直接开搞。

**Linux部署**

**1.环境准备**
>1.[ubuntu16.04](https://blog.csdn.net/qq_43938052/article/details/107326122)
>
>2.[tomcat8.5.57](https://us.mirrors.quenda.co/apache/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57.tar.gz)
>
>3.JDK8
>
>4.[halo1.3.2(jar包)](https://github.com/halo-dev/halo/releases/download/v1.3.2/halo-1.3.2.jar)


**2.安装JDK8**

执行命令，输入密码，切换root权限。
```
sudo su
```

![image](https://user-images.githubusercontent.com/48900845/112758871-09f15c80-9023-11eb-918a-6504938fd2a0.png)

执行命令，安装JDK8，需要等待一会。
```
apt-get install openjdk-8-jdk
```

![image](https://user-images.githubusercontent.com/48900845/112758880-14135b00-9023-11eb-9572-075db14eea03.png)

执行命令，查看JDK是否安装成功。
```
java -version
```

![image](https://user-images.githubusercontent.com/48900845/112758885-1bd2ff80-9023-11eb-9888-5fbea3e040cc.png)

**3.安装tomcat**

执行以下命令，切换目录
```
cd /usr/local/
```

![image](https://user-images.githubusercontent.com/48900845/112758894-27bec180-9023-11eb-90e3-c4adca794603.png)

执行命令，创建tomcat目录
```
mkdir tomcat
```

![image](https://user-images.githubusercontent.com/48900845/112758908-3311ed00-9023-11eb-9148-09a731903e05.png)

执行命令，切换到tomcat路径下。
```
cd tomcat
```

![image](https://user-images.githubusercontent.com/48900845/112758913-3b6a2800-9023-11eb-813b-1409e6395394.png)

执行命令，下载tomcat
```
wget https://us.mirrors.quenda.co/apache/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57.tar.gz
```

![image](https://user-images.githubusercontent.com/48900845/112758924-4c1a9e00-9023-11eb-962b-11cde63befea.png)

执行命令，解压tomcat
```
tar xvzf apache-tomcat-8.5.57.tar.gz
```

![image](https://user-images.githubusercontent.com/48900845/112758927-550b6f80-9023-11eb-963d-73143906acb5.png)


**4.安装halo**

执行命令，切换目录到webapps
```
cd apache-tomcat-8.5.57/webapps/
```

![image](https://user-images.githubusercontent.com/48900845/112758956-72d8d480-9023-11eb-96a1-07eec55d1a1b.png)


执行命令，下载[halo1.3.2](https://github.com/halo-dev/halo/releases/download/v1.3.2/halo-1.3.2.jar)

```
wget https://github.com/halo-dev/halo/releases/download/v1.3.2/halo-1.3.2.jar -O halo-latest.jar
```

![image](https://user-images.githubusercontent.com/48900845/112758967-83894a80-9023-11eb-9bdc-af5327463d89.png)

**5.运行halo**

执行命令，启动tomcat。(只要执行startup.sh就好，方法随意)，成功如下图。
```
bash /usr/local/tomcat/apache-tomcat-8.5.57/bin/startup.sh
```

![image](https://user-images.githubusercontent.com/48900845/112758971-8c7a1c00-9023-11eb-838d-b5d4dc943f89.png)

执行halo-latest.jar(一定要把路径切换到webapps，否则会找不到jar包)
```
java -jar halo-latest.jar
```
开始启动了。

![image](https://user-images.githubusercontent.com/48900845/112758980-956aed80-9023-11eb-915a-fcb669031abc.png)

启动成功，打开浏览器访http://192.168.190.132:8090（ip换成你自己的，服务器都连到了，应该不会不知道IP吧）端口是8090，不要搞忘了。

![image](https://user-images.githubusercontent.com/48900845/112758989-a3207300-9023-11eb-89b5-12d883b7696b.png)

填写信息

![image](https://user-images.githubusercontent.com/48900845/112758994-aa478100-9023-11eb-837c-e46c3bd52e7f.png)

![image](https://user-images.githubusercontent.com/48900845/112759000-b29fbc00-9023-11eb-8d49-409486795d27.png)

安装

![image](https://user-images.githubusercontent.com/48900845/112759009-b9c6ca00-9023-11eb-903d-7569c4785d5d.png)

登录

![image](https://user-images.githubusercontent.com/48900845/112759018-c0edd800-9023-11eb-85cd-f5a41079d87e.png)

成功了，nice，释放你的激情，尽情地探索吧！！！（可以换主题啥的，自己去玩吧）

![image](https://user-images.githubusercontent.com/48900845/112759039-d6630200-9023-11eb-835c-fa03672c53a1.png)

**windows部署**

**1.环境准备**
>1.[tomcat-8.5.57](https://mirrors.sonic.net/apache/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57-windows-x64.zip)
>
>2.JDK8(这个网上一搜就有了，我就不写了)
>
>3.[halo-1.3.2](https://github.com/halo-dev/halo/releases/download/v1.3.2/halo-1.3.2.jar)

**2.tomcat**

下载（https://mirrors.sonic.net/apache/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57-windows-x64.zip），解压，OK。

![image](https://user-images.githubusercontent.com/48900845/112759076-f4306700-9023-11eb-8095-478e7fb1fb1e.png)

**3.halo**

下载（https://github.com/halo-dev/halo/releases/download/v1.3.2/halo-1.3.2.jar），放到tomcat 下的webapps目录。

**4.运行**

启动tomcat，双击bin目录下startup.bat

![image](https://user-images.githubusercontent.com/48900845/112759109-188c4380-9024-11eb-912b-09bf363b005f.png)

启动halo，（cmd 或 power shell执行下面命令），其实双击下载的jar包也可以，只是看不到日志
```
java -jar (jar包路径)

```
访问http://127.0.0.1:8090/    成功了。后面的操作请参考Linux部署教程。

![image](https://user-images.githubusercontent.com/48900845/112759117-25109c00-9024-11eb-951b-2efbc65ec047.png)



>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
