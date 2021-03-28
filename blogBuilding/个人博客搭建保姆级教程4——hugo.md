
## 个人博客搭建保姆级教程4——hugo

**官方介绍：** The world’s fastest framework for building websites.
****

**Linux部署**

**1.环境**
>1.[ubuntu16.04](https://blog.csdn.net/qq_43938052/article/details/107326122)
>
>2.[hugo-v0.74.3](https://github.com/gohugoio/hugo/releases/tag/v0.74.3)

**2.安装hugo**

我们可以下载[hugo-v0.74.3](https://github.com/gohugoio/hugo/releases/tag/v0.74.3)的软件包进行安装。

![image](https://user-images.githubusercontent.com/48900845/112759571-2d69d680-9026-11eb-97ca-aeebd7d72d9d.png)

执行以下命令（需先切换至root），先创建一个目录，然后下载安装包。(**由于某种原因，下载速度有点慢**)

```
cd ~/
mkdir hugo 
cd hugo
wget https://github.com/gohugoio/hugo/releases/download/v0.74.3/hugo_0.74.3_Linux-64bit.deb
```

![image](https://user-images.githubusercontent.com/48900845/112759579-38bd0200-9026-11eb-8366-077ce1c42ab4.png)

现在开始安装
```
dpkg -i hugo_0.74.3_Linux-64bit.deb
```

![image](https://user-images.githubusercontent.com/48900845/112759587-41153d00-9026-11eb-9448-0dca9340ded8.png)

执行命令，检查是否安装成功。
```
hugo version
```

![image](https://user-images.githubusercontent.com/48900845/112759595-483c4b00-9026-11eb-9655-e301c9ac6cf1.png)

安装成功了。

**3.生成一个站点**

在hugo目录下，执行命令。

**注意：blog（执行命令后，会在当前路径新建blog文件夹，你也可以写个路径名）**

```
hugo new site blog

```

![image](https://user-images.githubusercontent.com/48900845/112759607-57bb9400-9026-11eb-8456-202abcdd1fed.png)

![image](https://user-images.githubusercontent.com/48900845/112759612-5c804800-9026-11eb-820f-acc1babb536c.png)


切换目录到blog文件夹

![image](https://user-images.githubusercontent.com/48900845/112759618-630ebf80-9026-11eb-8a69-0ccf0a0c5ad5.png)

**4.搞个主题**

**注意：各种骚气主题安装可能略有不同，仔细看安装文档。**

**[主题官网](https://themes.gohugo.io/)** 

很多好看的主题，自己选一个哦。

![image](https://user-images.githubusercontent.com/48900845/112759628-728e0880-9026-11eb-8db9-affc217e02ad.png)


我用[cupper主题](https://themes.gohugo.io/cupper-hugo-theme/) 举个例子。

![image](https://user-images.githubusercontent.com/48900845/112759633-7b7eda00-9026-11eb-908e-a739fc992be8.png)



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

![image](https://user-images.githubusercontent.com/48900845/112759647-8fc2d700-9026-11eb-9f17-e9dd8927a581.png)

![image](https://user-images.githubusercontent.com/48900845/112759649-92bdc780-9026-11eb-8949-2c77ede8025d.png)

**5.如何发文章**

hugo 支持markdown语法。

执行命令，新建一篇文章。（我用以前的文章做个演示）
```
hugo new post/Linux如何使用U盘等外接储存设备.md
```

![image](https://user-images.githubusercontent.com/48900845/112759661-a0734d00-9026-11eb-930a-daaa005ab1cf.png)

新建成功，文件在content目录下，现在我们来编辑一下。
```
vim content/post/Linux如何使用U盘等外接储存设备.md
```

![image](https://user-images.githubusercontent.com/48900845/112759670-a79a5b00-9026-11eb-91cf-d8bf2bd3ac65.png)

保存文件，然后开启服务。
```
hugo server -D --bind 192.168.190.129 -p 8080 --baseURL=http://192.168.190.129:8080 --buildDrafts --theme=cupper
```

访问**http://192.168.190.129:8080/post/**
**注意：一定要加post目录哦**

![image](https://user-images.githubusercontent.com/48900845/112759691-bed94880-9026-11eb-817c-ee0cf8dc1187.png)

访问第一篇文章。

![image](https://user-images.githubusercontent.com/48900845/112759699-c567c000-9026-11eb-892c-bb5a17ee9544.png)


**6.部署到github**

**需要配置好git [看这个教程](https://blog.csdn.net/qq_43938052/article/details/106485840)**

你需要有个GitHub的账号，自己去搞一个。

Create a new repository，repository name必须是 **（用户名.github.io）**  选不选public自己随意。 

![image](https://user-images.githubusercontent.com/48900845/112759711-d3b5dc00-9026-11eb-9333-ee0ef081fb5c.png)

点击create(下面冒绿光的)

![image](https://user-images.githubusercontent.com/48900845/112759717-dadcea00-9026-11eb-85ab-0ee2de719e8d.png)

仓库已建好。
执行命令，生成静态文件。在public文件夹下。
```
hugo --theme=cupper --baseUrl="https://ndb000901.github.io/" --buildDrafts
```

![image](https://user-images.githubusercontent.com/48900845/112759725-e3cdbb80-9026-11eb-966f-ea17b008dcdf.png)

切换目录到public下，初始化git仓库，将站点部署到仓库。
```
git init
git add .
git commit -m "第一次提交"
git remote add origin git@github.com:ndb000901/ndb000901.github.io.git #将用户名换成你自己的
git push -u origin master
```
访问**https://ndb000901.github.io/post**

![image](https://user-images.githubusercontent.com/48900845/112759738-f1834100-9026-11eb-94b9-da2f76eae921.png)

![image](https://user-images.githubusercontent.com/48900845/112759743-f647f500-9026-11eb-8247-582a76cdec5a.png)

成功部署。
****

**Windows部署**

**1.下载hugo**
[hugo下载](https://github.com/gohugoio/hugo/releases/tag/v0.74.3)，解压。

![image](https://user-images.githubusercontent.com/48900845/112759748-0233b700-9027-11eb-91a6-9040ecaa2cb0.png)

打开文件管理

![image](https://user-images.githubusercontent.com/48900845/112759755-0a8bf200-9027-11eb-96ec-943c4aeb2ae2.png)

右击此电脑，点击属性

![image](https://user-images.githubusercontent.com/48900845/112759761-1081d300-9027-11eb-8578-dd1cc1213a75.png)

点击高级系统设置

![image](https://user-images.githubusercontent.com/48900845/112759765-17a8e100-9027-11eb-8edc-ba4ad9329dde.png)

点击环境变量

![image](https://user-images.githubusercontent.com/48900845/112759773-1e375880-9027-11eb-96ee-944ae0899ad9.png)

选择PATH，点击编辑。没有PATH，自己新建一个。

![image](https://user-images.githubusercontent.com/48900845/112759781-268f9380-9027-11eb-9f43-5398f191fe8a.png)


新建一个，加入解压出hugo.exe的路径。然后保存。

![image](https://user-images.githubusercontent.com/48900845/112759790-2e4f3800-9027-11eb-9183-198d1dba7ae0.png)


打开cmd，或者powershell。验证环境变量是否添加成功。
```
hugo version
```

![image](https://user-images.githubusercontent.com/48900845/112759811-3f984480-9027-11eb-9d4f-fef59d3f12d5.png)

![image](https://user-images.githubusercontent.com/48900845/112759814-445cf880-9027-11eb-8e5d-b0607b8a8a74.png)


接下来的工作与linux部署类似。请参考Linux部署。

****


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)






