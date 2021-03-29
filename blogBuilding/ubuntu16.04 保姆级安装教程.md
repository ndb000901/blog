## **ubuntu16.04安装步骤**

过几天要写一个搭建博客的教程，所以准备工作还是要先搞一下。windows与linux的教程应该都会出，但为了更好的性能与稳定度，我还是强烈建议用linux环境搭建博客。

**1.实验环境**

>1.[ubuntu16.04镜像](http://releases.ubuntu.com/16.04.6/ubuntu-16.04.6-server-amd64.iso)
>
>2.VMware 15.5.6


**2.安装步骤**

![image](https://user-images.githubusercontent.com/48900845/112752354-4ada7880-9005-11eb-9aa3-f98f8fed18de.png)

创建新的虚拟机

![image](https://user-images.githubusercontent.com/48900845/112752362-50d05980-9005-11eb-8b8b-0b889a1ad108.png)

点击下一步

![image](https://user-images.githubusercontent.com/48900845/112752377-5cbc1b80-9005-11eb-8805-fa2412a78a23.png)

点击下一步

![image](https://user-images.githubusercontent.com/48900845/112752391-65145680-9005-11eb-8718-603fa64600a0.png)

选择稍后安装操作系统，点击下一步。

![image](https://user-images.githubusercontent.com/48900845/112752409-7198af00-9005-11eb-9079-010aadb7aed5.png)

选择linux ubuntu 64位，点击下一步。

![image](https://user-images.githubusercontent.com/48900845/112752420-7e1d0780-9005-11eb-99cb-27efc828f64b.png)

名称与位置各位大爷随意，点击下一步。

![image](https://user-images.githubusercontent.com/48900845/112752436-8e34e700-9005-11eb-944f-be31380d5ebb.png)

内核数自己填就好（注意总数不要超过宿主机CPU核心数）

![image](https://user-images.githubusercontent.com/48900845/112752443-98ef7c00-9005-11eb-9053-f8bcf841bb57.png)

内存按照自己需求配置（这个内存只是设定了该虚拟机最大可使用内存，而不是立马就占用了系统资源）。

![image](https://user-images.githubusercontent.com/48900845/112752491-ecfa6080-9005-11eb-8b51-1ba07046bff3.png)


点击下一步

![image](https://user-images.githubusercontent.com/48900845/112752493-f388d800-9005-11eb-8299-0e59b57d77e0.png)

点击下一步

![image](https://user-images.githubusercontent.com/48900845/112752505-fdaad680-9005-11eb-908a-514618baec72.png)

点击下一步

![image](https://user-images.githubusercontent.com/48900845/112752517-07343e80-9006-11eb-8598-343d2cfc46f1.png)

点击下一步

![image](https://user-images.githubusercontent.com/48900845/112752529-0f8c7980-9006-11eb-9dcc-32f2d1f5fd37.png)

点击浏览，选择路径（路径随意）

![image](https://user-images.githubusercontent.com/48900845/112752535-1ca96880-9006-11eb-966b-c1e0abe89d02.png)

点击自定义硬件

![image](https://user-images.githubusercontent.com/48900845/112752543-24690d00-9006-11eb-8a57-2f39cd232bb3.png)

选择之前下载的镜像，点击关闭，然后点击完成。

![image](https://user-images.githubusercontent.com/48900845/112752550-2e8b0b80-9006-11eb-908a-e15e2eb5f4e6.png)

点击开启虚拟机。

![image](https://user-images.githubusercontent.com/48900845/112752556-35b21980-9006-11eb-919c-4065d5472e2b.png)

语言选择English，回车。

![image](https://user-images.githubusercontent.com/48900845/112752561-3cd92780-9006-11eb-85f1-f525c9ba98d0.png)

回车

![image](https://user-images.githubusercontent.com/48900845/112752572-45c9f900-9006-11eb-9b97-b34e228955fd.png)

选择English，回车。

![image](https://user-images.githubusercontent.com/48900845/112752580-51b5bb00-9006-11eb-8cc3-cea8cad8284b.png)

这是要选择国家，先选other，回车。

![image](https://user-images.githubusercontent.com/48900845/112752593-5bd7b980-9006-11eb-9755-f089389b7011.png)

选择Asia(亚洲)

![image](https://user-images.githubusercontent.com/48900845/112752597-62663100-9006-11eb-9435-e7741c7b7f4f.png)

选择China(中国)

![image](https://user-images.githubusercontent.com/48900845/112752608-6b570280-9006-11eb-867d-60e01042f683.png)

回车

![image](https://user-images.githubusercontent.com/48900845/112752615-75790100-9006-11eb-929d-c71e08fc5a1c.png)

不检测键盘（用英文键盘就好），回车。

![image](https://user-images.githubusercontent.com/48900845/112752620-7dd13c00-9006-11eb-89d1-aedfb1e4db93.png)

回车

![image](https://user-images.githubusercontent.com/48900845/112752628-86c20d80-9006-11eb-95c9-0990729f4ed2.png)

等待

![image](https://user-images.githubusercontent.com/48900845/112752634-8e81b200-9006-11eb-9fb5-8fd8889f8c3d.png)

设置主机名（各位大爷随意）

![image](https://user-images.githubusercontent.com/48900845/112752650-980b1a00-9006-11eb-8cb3-c4fdabc8b666.png)

用户名（各位大爷随意）

![image](https://user-images.githubusercontent.com/48900845/112752662-a6f1cc80-9006-11eb-9ec8-455ba097eefc.png)

设置账号（各位大爷随意，登录时用）

![image](https://user-images.githubusercontent.com/48900845/112752666-aeb17100-9006-11eb-88a1-f5f97176dc72.png)

设置密码（随意，但是一定要记住哦）要输两次

![image](https://user-images.githubusercontent.com/48900845/112752676-ba9d3300-9006-11eb-84da-1988fe85cf0c.png)

是否选择弱密码，选择yes,回车。

![image](https://user-images.githubusercontent.com/48900845/112752683-c4bf3180-9006-11eb-8512-d07da8646670.png)

等待

![image](https://user-images.githubusercontent.com/48900845/112752688-cbe63f80-9006-11eb-8b68-25ad04792a9c.png)

你的时区是否是重庆，选择yes。

![image](https://user-images.githubusercontent.com/48900845/112752691-d3a5e400-9006-11eb-8aff-d6c8a5cd3c7a.png)

回车就好

![image](https://user-images.githubusercontent.com/48900845/112752694-db658880-9006-11eb-8328-cab1d7a89c51.png)

回车

![image](https://user-images.githubusercontent.com/48900845/112752706-e1f40000-9006-11eb-9d21-59468a83211f.png)

选择yes

![image](https://user-images.githubusercontent.com/48900845/112752715-eb7d6800-9006-11eb-9e1d-684a7b9f7fad.png)

回车

![image](https://user-images.githubusercontent.com/48900845/112752720-f33d0c80-9006-11eb-91b7-081ce15d1d03.png)

选择yes

![image](https://user-images.githubusercontent.com/48900845/112752728-fa641a80-9006-11eb-9093-6cf229e8ca6a.png)

等待

![image](https://user-images.githubusercontent.com/48900845/112752739-018b2880-9007-11eb-8759-55af4fb11e43.png)

设置http 代理，没有就直接回车喽

![image](https://user-images.githubusercontent.com/48900845/112752746-0c45bd80-9007-11eb-8469-79437aa6b203.png)

![image](https://user-images.githubusercontent.com/48900845/112752751-15cf2580-9007-11eb-8deb-395fd62662a9.png)

这一步等待时间有点长，（可以点回车试试，能否跳过）

![image](https://user-images.githubusercontent.com/48900845/112752760-1cf63380-9007-11eb-9dd9-4f76e01ba28d.png)

选择不自动更新系统

![image](https://user-images.githubusercontent.com/48900845/112752763-241d4180-9007-11eb-883c-5fcbb5141e93.png)

注意：openSSH server一定要选择（点空格可选中），
LAMP(linux + apache + mysql + php)，
Virtual Machine host不要选，本来就是虚拟机（在虚拟机上搞虚拟肯定有问题噻）。

![image](https://user-images.githubusercontent.com/48900845/112752773-34cdb780-9007-11eb-8974-23096e4cae8e.png)

等待

![image](https://user-images.githubusercontent.com/48900845/112752787-4adb7800-9007-11eb-8502-2c0fa03ca05d.png)

设置mysql root密码（一定要记住哦）要输两次

![image](https://user-images.githubusercontent.com/48900845/112752792-5169ef80-9007-11eb-8f99-75f63ead5766.png)

回车

![image](https://user-images.githubusercontent.com/48900845/112752800-59299400-9007-11eb-849c-ea5e13deb230.png)

回车

![image](https://user-images.githubusercontent.com/48900845/112752810-60e93880-9007-11eb-894a-b8447e42e85e.png)

装好了。输入用户名，密码登录。

![image](https://user-images.githubusercontent.com/48900845/112752813-69417380-9007-11eb-9848-6bd0f54d46e1.png)

注意：在Linux上输入密码时，是不回显的（屏幕没啥反应），如果输错了直接回车，重新输就好。

**3.连接服务器**

由于虚拟机显示的命令行看起来有些恼火，so我给各位大爷找了个工具MobaXterm【公众号回复shell即可获得】（来源于互联网）

![image](https://user-images.githubusercontent.com/48900845/112752835-7eb69d80-9007-11eb-8350-f11724fe9822.png)

点击左上角session。

![image](https://user-images.githubusercontent.com/48900845/112752837-85ddab80-9007-11eb-9685-4c1b689ef3d7.png)

点击SSH

![image](https://user-images.githubusercontent.com/48900845/112752843-8c6c2300-9007-11eb-8006-65d9c2018b1c.png)

在虚拟机输入命令ifconfig，查看ip。我的ip为192.168.190.132

![image](https://user-images.githubusercontent.com/48900845/112752847-942bc780-9007-11eb-83b6-2bd1b12551b7.png)


填写ip与用户名，点击OK。

![image](https://user-images.githubusercontent.com/48900845/112752852-9aba3f00-9007-11eb-9939-b6b3adb27fc0.png)

输入密码。

![image](https://user-images.githubusercontent.com/48900845/112752859-a3127a00-9007-11eb-8b55-6e723d654dbd.png)

sudo su切换为root($是普通用户，#是root用户)

输入命令vim /etc/apt/sources.list(换个国内源，提升安装软件的速度)，把原来的删喽或者用#注释了。

**vim的简单使用请自行上网查询，谢谢**

```
deb http://mirrors.aliyun.com/ubuntu/ xenial main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main

deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main

deb http://mirrors.aliyun.com/ubuntu/ xenial universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates universe

deb http://mirrors.aliyun.com/ubuntu/ xenial-security main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main
deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security universe

```

![image](https://user-images.githubusercontent.com/48900845/112752876-b32a5980-9007-11eb-9c1c-69b0fa8902b5.png)

![image](https://user-images.githubusercontent.com/48900845/112752887-c0dfdf00-9007-11eb-87de-90775281b905.png)

执行 apt-get update(更新一下)。

OK，今天的文章就肝到这里。



>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
