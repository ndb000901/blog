## 个人博客搭建保姆级教程3——hexo

About :A fast, simple & powerful blog framework, powered by Node.js.(官网介绍)
今天的目标是：白嫖！白嫖！
白嫖服务器！！白嫖域名！！

**Linux部署**

**1.环境部署**
>1.[ubuntu16.04](https://blog.csdn.net/qq_43938052/article/details/107326122)
>
>2.[node.js-12.18.2](https://nodejs.org/dist/v12.18.2/node-v12.18.2-linux-x64.tar.xz)
>
>3.hexo

**2.安装node.js**

执行命令，切换目录，创建文件夹
```
cd /usr/local
mkdir node
cd node
```

下载（https://nodejs.org/dist/v12.18.2/node-v12.18.2-linux-x64.tar.xz）
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

![image](https://user-images.githubusercontent.com/48900845/112759195-8a648d00-9024-11eb-8ff0-3d3abf3dc3ce.png)

更新环境变量
```
source ~/.bash_profile
```
检验
```
node -v
```

![image](https://user-images.githubusercontent.com/48900845/112759201-93555e80-9024-11eb-9293-cc7cae714686.png)

```
npx -v
```

![image](https://user-images.githubusercontent.com/48900845/112759210-99e3d600-9024-11eb-95f8-eee4eb64d010.png)

```
npm version
```

![image](https://user-images.githubusercontent.com/48900845/112759221-a1a37a80-9024-11eb-92ee-fa59a28ca34f.png)

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

![image](https://user-images.githubusercontent.com/48900845/112759232-b122c380-9024-11eb-9e9f-09a2f5c68075.png)

安装hexo-cli
```
cnpm install hexo-cli -g
```

![image](https://user-images.githubusercontent.com/48900845/112759244-bbdd5880-9024-11eb-8c16-be60b634e7a4.png)

执行命令，检查一下
```
hexo -v
```

![image](https://user-images.githubusercontent.com/48900845/112759280-dc0d1780-9024-11eb-8866-d0b6f2ecd308.png)

安装hexo-server(随着Hexo 3的发布，服务器已与主模块分离。要开始使用服务器，您首先必须安装hexo-server。)
```
cnpm install hexo-server --save
```

初始化一个博客，在建好的blog文件夹下。ls 查看会出现以下文件。执行hexo init后一定要执行cnpm install。
```
hexo init
cnpm install
```

![image](https://user-images.githubusercontent.com/48900845/112759294-e7604300-9024-11eb-9b8e-f4e63c67bcee.png)


启动hexo服务
```
hexo server
```

![image](https://user-images.githubusercontent.com/48900845/112759302-f0511480-9024-11eb-82fc-7cbd5e83abc3.png)

打开浏览器，访问http://(服务器ip):4000

![image](https://user-images.githubusercontent.com/48900845/112759309-f7782280-9024-11eb-9ca1-b97054c6e23f.png)

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


![image](https://user-images.githubusercontent.com/48900845/112759318-065ed500-9025-11eb-9d07-c144513ed3f7.png)

成功！！！！

**4.更换主题**

如果不喜欢默认主题，可以自己换一个，网上有很多主题，下面我来演示以下。
[主题官网](https://hexo.io/themes/)自己上去找自己喜欢的。
![image](https://user-images.githubusercontent.com/48900845/112759335-1676b480-9025-11eb-94f1-7cf0de434a26.png)

我以Tranquilpeak举例（不同主题可能安装有所不同，自行参照教程）
hexo 主题都是在themes目录下，配置文件在_config.yml里，有个theme。

```
cd themes
```

landscape为默认主题

![image](https://user-images.githubusercontent.com/48900845/112759347-29898480-9025-11eb-81ad-a4368583cf0c.png)

[下载tranquilpeak主题](https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak.git) 请将目录cd 到themes
```
git clone https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak.git tranquilpeak

```
修改配置文件（blog下_config.yml）theme修改为tranquilpeak
```
vim ../_config.yml

```

![image](https://user-images.githubusercontent.com/48900845/112759359-36a67380-9025-11eb-8f7a-339abbc90ed0.png)

执行命令(一定要在tranquilpeak文件夹)
```
cd tranquilpeak
cnpm install && cnpm run prod
```
等待

![image](https://user-images.githubusercontent.com/48900845/112759365-41f99f00-9025-11eb-9e34-6c511fef0517.png)

启动服务(如果你在tranquilpeak目录无法启动服务，
请执行cd命令回到上一级目录，再执行。)
```
cd ..
hexo server
```
访问，这个主题蛮好看。

![image](https://user-images.githubusercontent.com/48900845/112759385-550c6f00-9025-11eb-9e0d-123534069018.png)

**5.白嫖github服务器及域名**

你需要有个GitHub的账号，自己去搞一个。

Create a new repository，repository name必须是 **（用户名.github.io）**  选不选public自己随意。 

![image](https://user-images.githubusercontent.com/48900845/112759405-68b7d580-9025-11eb-9d91-784677602573.png)

点击create(下面冒绿光的)

![image](https://user-images.githubusercontent.com/48900845/112759407-6fdee380-9025-11eb-89df-82d4b32bed6c.png)

仓库已建好。
执行命令，安装工具 hexo-deployer-git
```
cnpm insatll --save hexo-deployer-git
```

![image](https://user-images.githubusercontent.com/48900845/112759419-78371e80-9025-11eb-8282-3db6b3625eae.png)

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

![image](https://user-images.githubusercontent.com/48900845/112759429-8422e080-9025-11eb-91d4-090b0eeb117e.png)


执行命令，把博客推送到github仓库。这时可能会出现以下报错，解决方案：[初学git安装与配置windows版](https://blog.csdn.net/qq_43938052/article/details/106485840)，配置一下git， 在你git上面增加SSH key就可（生成的key在 ~/.ssh/id_rsa.pub）

```
hexo d
```

![image](https://user-images.githubusercontent.com/48900845/112759446-94d35680-9025-11eb-9b18-e15ed4f5b968.png)

配置好git后执行命令
```
hexo d
```
刷新仓库，多了些东东

![image](https://user-images.githubusercontent.com/48900845/112759456-a4529f80-9025-11eb-985c-af7df83c48d7.png)


访问https://(用户名).github.io/

![image](https://user-images.githubusercontent.com/48900845/112759475-b8969c80-9025-11eb-8fde-e7b34a9107de.png)


OK，白嫖服务器与域名结束了。放开手脚去打造属于你的hexo吧。

**Windows部署**

**1.安装node.js**

[下载win版安装包](https://nodejs.org/dist/v12.18.3/node-v12.18.3-x64.msi)

![image](https://user-images.githubusercontent.com/48900845/112759489-ca783f80-9025-11eb-9aa3-1adaf904ada0.png)

点击next

![image](https://user-images.githubusercontent.com/48900845/112759506-d401a780-9025-11eb-8593-ecbad1d6bcb2.png)

勾选接受，next

![image](https://user-images.githubusercontent.com/48900845/112759511-dcf27900-9025-11eb-9ef7-f6453d0201fc.png)

直接next，安装程序会帮你Add to PATH(添加环境变量)

![image](https://user-images.githubusercontent.com/48900845/112759517-e54ab400-9025-11eb-9a95-5c23f53e4643.png)

next

![image](https://user-images.githubusercontent.com/48900845/112759521-eda2ef00-9025-11eb-9e54-6484613b180a.png)


打开cmd，或者power shell执行命令，操作与Linux 部署相似。请参考Linux部署。


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)


