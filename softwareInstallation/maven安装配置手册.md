**安装Maven**

执行命令，切换到opt目录
```
cd /opt
```
执行命令，创建maven文件夹
```
mkdir maven
```

![image](https://user-images.githubusercontent.com/48900845/112761392-b0daf600-902d-11eb-8376-bff1016396db.png)

执行命令，切换到maven目录，下载maven-3.6.3，解压压缩包
```
cd maven
wget http://www.trieuvan.com/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
tar zxvf apache-maven-3.6.3-bin.tar.gz

```
换源(在<mirrors></mirrors>标签中添加 mirror 子节点:)，提升下载速度。(这里用阿里源)
```
vim apache-maven-3.6.3/conf/settings.xml
```
```
<mirror>
    <id>aliyunmaven</id>
    <mirrorOf>*</mirrorOf>
    <name>阿里云公共仓库</name>
    <url>https://maven.aliyun.com/repository/public</url>
</mirror>


```

![image](https://user-images.githubusercontent.com/48900845/112761402-bc2e2180-902d-11eb-93ba-b030b8b8cad8.png)

配置环境变量
```
vim /etc/profile
```
粘贴以下内容，保存profile
```
export MAVEN_HOME=/opt/maven/apache-maven-3.6.3
export PATH=$MAVEN_HOME/bin:$PATH
```

![image](https://user-images.githubusercontent.com/48900845/112761407-c6502000-902d-11eb-8025-4e89d8357ded.png)

刷新环境变量。
```
source /etc/profile
```
检查一下，下图所示，成功。
```
mvn -v
```

![image](https://user-images.githubusercontent.com/48900845/112761414-ccde9780-902d-11eb-8ee7-c5a13e56af2d.png)



>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
