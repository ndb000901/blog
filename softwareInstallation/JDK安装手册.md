##  ubuntu安装教程
**1.实验环境**
>1.ubuntu16.04([安装教程](https://blog.csdn.net/qq_43938052/article/details/107326122))
>2.jdk-14.0.1([下载地址](https://www.oracle.com/java/technologies/javase/jdk14-archive-downloads.html))

我下载的是这个
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201004114256152.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
**2.解压**
将jdk下载到/usr/local/java

```
cd /usr/local
mkdir java
cd java
tar -zxvf jdk-14.0.1_linux-x64_bin.tar.gz
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201004114714390.png#pic_center)
解压后会出现一个jdk-14.0.1文件夹。

**3.配置JDK环境变量**

vim /etc/profile
加入以下内容
```
JAVA_HOME=/usr/local/java/jdk-14.0.1
CLASSPATH=$JAVA_HOME/lib/
PATH=$PATH:$JAVA_HOME/bin
export PATH JAVA_HOME CLASSPATH
```
刷新一下
```
source /etc/profile
```
验证一下
```
java -version
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201004115809878.png#pic_center)

nice，安装成功！！！！

----------

## windows
**1.实验环境**
>1.win10
>2.jdk-14.0.1([下载地址](https://www.oracle.com/java/technologies/javase/jdk14-archive-downloads.html))

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201004120557808.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)

由于是图形化安装，就不写详细过程了，**注意记住安装路径**。

**2.配置环境**
右键此电脑，点击属性。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201004121359512.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
点击高级系统设置
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201004121445740.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
点击环境变量
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201004121532285.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
JAVA_HOME（值填写jdk安装路径）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201004122545810.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
CLASSPATH
```
.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar
```
在PATH里添加
```
%JAVA_HOME%\bin
%JAVA_HOME%\jre\bin
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201004122858628.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
一路保存

**3.验证**
```
java -version
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201004123101157.png#pic_center)

nice，成功了！！！！！！

--------

>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)



