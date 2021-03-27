**安装Maven**
执行命令，切换到opt目录
```
cd /opt
```
执行命令，创建maven文件夹
```
mkdir maven
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718203538718.png)

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
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718204305557.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
配置环境变量
```
vim /etc/profile
```
粘贴以下内容，保存profile
```
export MAVEN_HOME=/opt/maven/apache-maven-3.6.3
export PATH=$MAVEN_HOME/bin:$PATH
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718204747107.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
刷新环境变量。
```
source /etc/profile
```
检查一下，下图所示，成功。
```
mvn -v
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/202007182050239.png)

>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

