##  ubuntu安装教程

**1.实验环境**

>1.ubuntu16.04([安装教程](https://blog.csdn.net/qq_43938052/article/details/107326122))
>
>2.jdk-14.0.1([下载地址](https://www.oracle.com/java/technologies/javase/jdk14-archive-downloads.html))

我下载的是这个

![image](https://user-images.githubusercontent.com/48900845/112761285-2b574600-902d-11eb-8c61-80046f0993f3.png)

**2.解压**

将jdk下载到/usr/local/java

```
cd /usr/local
mkdir java
cd java
tar -zxvf jdk-14.0.1_linux-x64_bin.tar.gz
```

![image](https://user-images.githubusercontent.com/48900845/112761292-33af8100-902d-11eb-8bc7-942f4b552936.png)

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

![image](https://user-images.githubusercontent.com/48900845/112761299-3dd17f80-902d-11eb-9ceb-9a1b73fc5dc9.png)


nice，安装成功！！！！

----------

## windows

**1.实验环境**

>1.win10
>
>2.jdk-14.0.1([下载地址](https://www.oracle.com/java/technologies/javase/jdk14-archive-downloads.html))

![image](https://user-images.githubusercontent.com/48900845/112761312-47f37e00-902d-11eb-8866-d9b45813b336.png)

由于是图形化安装，就不写详细过程了，**注意记住安装路径**。

**2.配置环境**

右键此电脑，点击属性。

![image](https://user-images.githubusercontent.com/48900845/112761323-5b064e00-902d-11eb-80fb-86d99c396aa3.png)

点击高级系统设置

![image](https://user-images.githubusercontent.com/48900845/112761335-69ed0080-902d-11eb-808c-5e4f2bd30525.png)


点击环境变量

![image](https://user-images.githubusercontent.com/48900845/112761339-71140e80-902d-11eb-8795-2873793c1837.png)


JAVA_HOME（值填写jdk安装路径）

![image](https://user-images.githubusercontent.com/48900845/112761344-78d3b300-902d-11eb-8c07-08287a5b2bcf.png)

CLASSPATH
```
.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar
```
在PATH里添加
```
%JAVA_HOME%\bin
%JAVA_HOME%\jre\bin
```

![image](https://user-images.githubusercontent.com/48900845/112761354-85580b80-902d-11eb-8de3-02f663233d35.png)

一路保存

**3.验证**

```
java -version
```

![image](https://user-images.githubusercontent.com/48900845/112761368-8f7a0a00-902d-11eb-96ee-9af33f3ab53e.png)


nice，成功了！！！！！！

--------


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)



