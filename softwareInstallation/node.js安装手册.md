**安装node.js**

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
成功了。

*****
**换源**
NPM下载速度不太友好，执行命令，安装CNPM。淘宝有个NPM的镜像源CNPM，速度可以。
```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
查看一下是否安装成功
```
cnpm -v
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020072300292367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)