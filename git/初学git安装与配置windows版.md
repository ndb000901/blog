## windows版

今晚搞了git，遇到了一些问题，赶紧来记录一哈。

**1.[Git下载](https://git-scm.com/downloads)与安装**

>注意：安装是图形化安装，跟个指示就可。
>
>有这个Git bash就可。
>
>![image](https://user-images.githubusercontent.com/48900845/112805019-a6f5d900-90a7-11eb-910d-baed0ef87c48.png)


**2.开始配置**

>**a.打开Git bash**
>
>![image](https://user-images.githubusercontent.com/48900845/112761137-54c3a200-902c-11eb-9083-4e0d25ee527d.png)
>
>**>b.配置信息**
>1.git config --global user.name "Your Name"
>
> 2.git config --global user.email "email@example.com"
> 
>**注意：** 
>
>Your Name是你要设置的名字，email@example.com是你要设置的邮箱。
>
>git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。
>
>3.ssh-keygen -t rsa -C "email@example.com"
>
>**注意：** email@example.com是你要设置的邮箱。
>
>**接着显示：**
>
>Generating public/private rsa key pair.
>
>Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa)
>
>4.执行3后会显示一个路径，找到下图id_rsa.pub文件，记事本打开，全部复制，打开你的github。
>
>**如果没有那个文件（请打开显示隐藏文件，不会请百度）**
>
>![image](https://user-images.githubusercontent.com/48900845/112761161-77ee5180-902c-11eb-9427-28be2d14f681.png)
>
>点击右上角头像
>
>![image](https://user-images.githubusercontent.com/48900845/112761171-889ec780-902c-11eb-8a40-8309fd6bb176.png)
>
>点击**SSHa and GPG keys**
>
>![image](https://user-images.githubusercontent.com/48900845/112761180-97857a00-902c-11eb-87d2-654d25c46c0a.png)

>点击 new DSSH key，将复制内容粘贴进去保存。
>
>![image](https://user-images.githubusercontent.com/48900845/112761192-b08e2b00-902c-11eb-804b-14bcdf2a6aa4.png)

>5.ssh -T git@github.com（Git bash 试试）
>
>跳出下面信息，OK了。
>
>![image](https://user-images.githubusercontent.com/48900845/112761200-bd128380-902c-11eb-8a7a-b7ee27049913.png)
>
>

**3.建本地库**

>**若看不懂以下命令，请看下linux基础命令**
>
>a.mkdir hello（新建目录）
>
>b.cd hello
>
>c.git init（把这个目录变成Git可以管理的仓库）
>
>d.在hello目录下创建一个文件readme.txt(文件名随意，创建方法随意，测试用)。
>
>e.git add readme.txt（把文件添加到仓库）
>
>f.git commit -m "wrote a readme file"（把文件提交到仓库，引号里面是提交说明）
>

**4.建远程仓库**

>**a.直接new一个**
>
>![image](https://user-images.githubusercontent.com/48900845/112761230-f2b76c80-902c-11eb-8d61-6d5ab294d41b.png)
>
>点击create.
>
>b.git remote add origin git@github.com:用户名/仓库名.git
>
>**注意：远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。**
>
>c.git push -u origin master
>
>**由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。**
>
>d.刷新github hello 仓库发现和你本地库一致，OK。
>
>e.从现在起，只要本地作了提交，就可以通过命令：git push origin master



>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
