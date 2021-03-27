## 个人博客搭建保姆级教程3——hexo
About :A fast, simple & powerful blog framework, powered by Node.js.(官网介绍)
今天的目标是：白嫖！白嫖！
白嫖服务器！！白嫖域名！！

**Linux部署**

**1.环境部署**
>1.[ubuntu16.04](https://blog.csdn.net/qq_43938052/article/details/107326122)
>2.[node.js-12.18.2](https://nodejs.org/dist/v12.18.2/node-v12.18.2-linux-x64.tar.xz)
>3.hexo

**2.安装node.js**

执行命令，切换目录，创建文件夹
```
cd /usr/local
mkdir node
cd node
```

下载（**https://nodejs.org/dist/v12.18.2/node-v12.18.2-linux-x64.tar.xz**）
```
wget https://nodejs.org/dist/v12.18.2/node-v12.18.2-linux-x64.tar.xz
```
解压
```
tar xJvf node-v12.18.2-linux-x64.tar.xz
```
配置，修改~/.bash_profile文件，加入以下内容
```
vim ~/.bash_profile
```
```
# Nodejs
export PATH=/usr/local/node/node-v12.16.3-linux-x64/bin:$PATH
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200722235958573.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
更新环境变量
```
source ~/.bash_profile
```
检验
```
node -v
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723000146367.png)
```
npx -v
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723000208310.png)
```
npm version
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723000246650.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
成功了

**3.安装hexo**
**在下述步骤中，若出现已经安装了node和hexo，但是使用时出现找不到命令，请执行source ~/.bash_profile，刷新。**
**注意，所有的安装过程都在blog文件夹里搞，如果出了什么问题，你可以直接干掉blog目录，重新创建一个。**
创建个博客目录，切换到该目录下。
```
mkdir ~/blog
cd  ~/blog
```
NPM下载速度不太友好，执行命令，安装CNPM。淘宝有个NPM的镜像源CNPM，速度可以。
```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
查看一下是否安装成功
```
cnpm -v
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020072300292367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
安装hexo-cli
```
cnpm install hexo-cli -g
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723003033670.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
执行命令，检查一下
```
hexo -v
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723003148734.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
安装hexo-server(随着Hexo 3的发布，服务器已与主模块分离。要开始使用服务器，您首先必须安装hexo-server。)
```
cnpm install hexo-server --save
```

初始化一个博客，在建好的blog文件夹下。ls 查看会出现以下文件。执行hexo init后一定要执行cnpm install。
```
hexo init
cnpm install
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723003758672.png)

启动hexo服务
```
hexo server
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723114609168.png)
打开浏览器，访问http://(服务器ip):4000
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723123517424.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
新建一个博客，hexo会建一个markdown文件（在source/_post/目录下）
```
hexo new "博客标题"
```
将博客内容搞进去(为了演示，这里我将以前写的博客搞了进去)
```
vim source/_post/博客标题.md
```
执行命令，生成静态文件。
```
hexo generate
```
启动服务
```
hexo server
```


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723125852342.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
成功！！！！

**4.更换主题**
如果不喜欢默认主题，可以自己换一个，网上有很多主题，下面我来演示以下。
[主题官网](https://hexo.io/themes/)自己上去找自己喜欢的。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723143858328.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
我以Tranquilpeak举例（不同主题可能安装有所不同，自行参照教程）
hexo 主题都是在themes目录下，配置文件在_config.yml里，有个theme。
```
cd themes
```
landscape为默认主题
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723144159504.png)
[下载tranquilpeak主题](https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak.git) 请将目录cd 到themes
```
git clone https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak.git tranquilpeak

```
修改配置文件（blog下_config.yml）theme修改为tranquilpeak
```
vim ../_config.yml

```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723144643183.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
执行命令(一定要在tranquilpeak文件夹)
```
cd tranquilpeak
cnpm install && cnpm run prod
```
等待
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020072314492014.png)
启动服务(如果你在tranquilpeak目录无法启动服务，
请执行cd命令回到上一级目录，再执行。)
```
cd ..
hexo server
```
访问，这个主题蛮好看。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723145340226.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**5.白嫖github服务器及域名**
你需要有个GitHub的账号，自己去搞一个。

Create a new repository，repository name必须是 **（用户名.github.io）**  选不选public自己随意。 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723150421863.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
点击create(下面冒绿光的)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723150739193.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
仓库已建好。
执行命令，安装工具 hexo-deployer-git
```
cnpm insatll --save hexo-deployer-git
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723151245843.png)
配置blog目录下的_config.yml
```
vim _config.yml
```
在# Deployment 下加入以下内容，repo填自己仓库的地址
```
deploy:
  type: git
  repo: https://github.com/ndb000901/ndb000901.github.io.git
  branch: master

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723152120256.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
执行命令，把博客推送到github仓库。这时可能会出现以下报错，解决方案：[初学git安装与配置windows版](https://blog.csdn.net/qq_43938052/article/details/106485840)，配置一下git， 在你git上面增加SSH key就可（生成的key在 ~/.ssh/id_rsa.pub）
```
hexo d
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723155311579.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
配置好git后执行命令
```
hexo d
```
刷新仓库，多了些东东
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723155852268.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
访问https://(用户名).github.io/
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723160012499.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

OK，白嫖服务器与域名结束了。放开手脚去打造属于你的hexo吧。

**Windows部署**
**1.安装node.js**
[下载win版安装包](https://nodejs.org/dist/v12.18.3/node-v12.18.3-x64.msi)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723161603402.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
点击next
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723161746657.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


勾选接受，next

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723161835213.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
直接next，安装程序会帮你Add to PATH(添加环境变量)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723161958916.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
next
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723162112138.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


打开cmd，或者power shell执行命令，操作与Linux 部署相似。请参考Linux部署。

>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


















