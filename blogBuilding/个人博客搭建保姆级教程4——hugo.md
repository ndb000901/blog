
## 个人博客搭建保姆级教程4——hugo
**官方介绍：** The world’s fastest framework for building websites.
****

**Linux部署**

**1.环境**
>1.[ubuntu16.04](https://blog.csdn.net/qq_43938052/article/details/107326122)
>2.[hugo-v0.74.3](https://github.com/gohugoio/hugo/releases/tag/v0.74.3)

**2.安装hugo**
我们可以下载[hugo-v0.74.3](https://github.com/gohugoio/hugo/releases/tag/v0.74.3)的软件包进行安装。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801190749592.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
执行以下命令（需先切换至root），先创建一个目录，然后下载安装包。(**由于某种原因，下载速度有点慢**)
```
cd ~/
mkdir hugo 
cd hugo
wget https://github.com/gohugoio/hugo/releases/download/v0.74.3/hugo_0.74.3_Linux-64bit.deb
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801192305369.png)
现在开始安装
```
dpkg -i hugo_0.74.3_Linux-64bit.deb
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801192718449.png)
执行命令，检查是否安装成功。
```
hugo version
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801192814885.png)
安装成功了。

**3.生成一个站点**
在hugo目录下，执行命令。
**注意：blog（执行命令后，会在当前路径新建blog文件夹，你也可以写个路径名）**
```
hugo new site blog

```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801193901484.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801193841497.png)

切换目录到blog文件夹
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801194000501.png)
**4.搞个主题**
**注意：各种骚气主题安装可能略有不同，仔细看安装文档。**
**[主题官网](https://themes.gohugo.io/)** 
很多好看的主题，自己选一个哦。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801195024359.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

我用[cupper主题](https://themes.gohugo.io/cupper-hugo-theme/) 举个例子。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801212728825.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


执行命令，将目录切换至blog目录下的themes，下载主题。
```
cd themes
git clone https://github.com/zwbetz-gh/cupper-hugo-theme.git cupper
```

回到blog目录，执行命令，启动服务。8080是端口，你可以自己写个别的。ip写你自己的。
**端口范围：0~65535，建议大于1024。如果端口被占用，换个别的。**
```
cd ~/hugo/blog
hugo server -D --bind 192.168.190.129 -p 8080 --baseURL=http://192.168.190.129:8080 --buildDrafts --theme=cupper

```
访问http://192.168.190.129:8080/（用你自己的IP，主题找你自己喜欢的，我只是随便做个演示。）



想换站点标题，请修改blog下的config.toml文件。修改title后面的字符串。
```
vim config.toml
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801202844830.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801213517225.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


**5.如何发文章**
hugo 支持markdown语法。

执行命令，新建一篇文章。（我用以前的文章做个演示）
```
hugo new post/Linux如何使用U盘等外接储存设备.md
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801203607688.png)
新建成功，文件在content目录下，现在我们来编辑一下。
```
vim content/post/Linux如何使用U盘等外接储存设备.md
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801203407976.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
保存文件，然后开启服务。
```
hugo server -D --bind 192.168.190.129 -p 8080 --baseURL=http://192.168.190.129:8080 --buildDrafts --theme=cupper
```

访问**http://192.168.190.129:8080/post/**
**注意：一定要加post目录哦**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801213848260.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
访问第一篇文章。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801214004631.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

**6.部署到github**
**需要配置好git [看这个教程](https://blog.csdn.net/qq_43938052/article/details/106485840)**
你需要有个GitHub的账号，自己去搞一个。

Create a new repository，repository name必须是 **（用户名.github.io）**  选不选public自己随意。 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723150421863.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
点击create(下面冒绿光的)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723150739193.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
仓库已建好。
执行命令，生成静态文件。在public文件夹下。
```
hugo --theme=cupper --baseUrl="https://ndb000901.github.io/" --buildDrafts
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801220423104.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
切换目录到public下，初始化git仓库，将站点部署到仓库。
```
git init
git add .
git commit -m "第一次提交"
git remote add origin git@github.com:ndb000901/ndb000901.github.io.git #将用户名换成你自己的
git push -u origin master
```
访问**https://ndb000901.github.io/post**

![](https://img-blog.csdnimg.cn/20200801221013284.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801221039361.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
成功部署。
****

**Windows部署**

**1.下载hugo**
[hugo下载](https://github.com/gohugoio/hugo/releases/tag/v0.74.3)，解压。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801232810735.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
打开文件管理
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801233248819.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
右击此电脑，点击属性
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801233455292.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
点击高级系统设置
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801233554968.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
点击环境变量
![在这里插入图片描述](https://img-blog.csdnimg.cn/202008012336322.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


选择PATH，点击编辑。没有PATH，自己新建一个。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020080123390225.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

新建一个，加入解压出hugo.exe的路径。然后保存。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020080123402274.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


打开cmd，或者powershell。验证环境变量是否添加成功。
```
hugo version
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801234222860.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801234249169.png)

接下来的工作与linux部署类似。请参考Linux部署。

****

>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)






