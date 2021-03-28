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

![image](https://user-images.githubusercontent.com/48900845/112761437-eda6ed00-902d-11eb-8e66-0235f5664a42.png)

更新环境变量
```
source ~/.bash_profile
```
检验
```
node -v
```

![image](https://user-images.githubusercontent.com/48900845/112761441-f4cdfb00-902d-11eb-9320-36c17e9a7108.png)

```
npx -v
```

![image](https://user-images.githubusercontent.com/48900845/112761445-fb5c7280-902d-11eb-83b1-bc91561602c1.png)

```
npm version
```

![image](https://user-images.githubusercontent.com/48900845/112761451-031c1700-902e-11eb-8a58-6f684723d87b.png)

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

![image](https://user-images.githubusercontent.com/48900845/112761470-10d19c80-902e-11eb-8fa8-2b7870780b97.png)


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
