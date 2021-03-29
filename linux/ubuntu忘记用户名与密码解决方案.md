## ubuntu忘记用户名与密码解决方案

很多朋友经常忘记自己的用户名以及密码。为啥哩，因为他们装好了系统后就没用过，放在电脑里吃灰，等到要用的时候，发现记不得用户名及密码了。哎呀，不小心说漏了，sorry，sorry。

**1.环境**

>1.VMware15.5.6
>
>2.ubuntu16.04

**2.解决方案**

开启ubuntu虚拟机时长按esc键（**注意：你的鼠标要聚焦到虚拟机哦，否则你的esc键是作用到物理机的。**），选择如图选项，回车。

![image](https://user-images.githubusercontent.com/48900845/112808137-42d51400-90ab-11eb-939e-d6495f337c06.png)

选择第二个选项，按e键编辑。

![image](https://user-images.githubusercontent.com/48900845/112808162-49fc2200-90ab-11eb-882a-b9d6fa2a7eb8.png)

找到linux 下一行，从最后面的nomodeset开始回删，删到root那。

![image](https://user-images.githubusercontent.com/48900845/112808192-53858a00-90ab-11eb-8445-75c37a9d01b0.png)

然后添加rw single init=/bin/bash，按F10或者ctrl + x

![image](https://user-images.githubusercontent.com/48900845/112808235-5c765b80-90ab-11eb-8c2e-a82ad4b3e80b.png)

瞧，我们进入系统了。

![image](https://user-images.githubusercontent.com/48900845/112808267-64360000-90ab-11eb-96e2-f0cfb8b1d3b4.png)


执行命令，查看下用户名。我的用户名是wuhen3。
```
cat /etc/shadow
```

![image](https://user-images.githubusercontent.com/48900845/112808311-6f892b80-90ab-11eb-97aa-5cd9e0d74467.png)

执行命令，修改密码。
```
passwd 用户名
```

**注意：如果你的密码修改没成功，可能是你用了”1234“这种弱密码，试着在密码中添加个字母试试。**

![image](https://user-images.githubusercontent.com/48900845/112808349-7adc5700-90ab-11eb-8306-6b6ca36d7f33.png)


重启你的系统。登录试试。

![image](https://user-images.githubusercontent.com/48900845/112808372-82036500-90ab-11eb-9329-af7c00bdeb95.png)

成功。

![image](https://user-images.githubusercontent.com/48900845/112808431-8b8ccd00-90ab-11eb-95c1-71593e49e91d.png)




>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)

