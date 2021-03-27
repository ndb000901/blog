## ubuntu忘记用户名与密码解决方案
很多朋友经常忘记自己的用户名以及密码。为啥哩，因为他们装好了系统后就没用过，放在电脑里吃灰，等到要用的时候，发现记不得用户名及密码了。哎呀，不小心说漏了，sorry，sorry。
**1.环境**
>1.VMware15.5.6
>2.ubuntu16.04

**2.解决方案**
开启ubuntu虚拟机时长按esc键（**注意：你的鼠标要聚焦到虚拟机哦，否则你的esc键是作用到物理机的。**），选择如图选项，回车。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731132107339.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
选择第二个选项，按e键编辑。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731132707504.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
找到linux 下一行，从最后面的nomodeset开始回删，删到root那。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731133135924.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
然后添加rw single init=/bin/bash，按F10或者ctrl + x
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731133621528.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
瞧，我们进入系统了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731133756888.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

执行命令，查看下用户名。我的用户名是wuhen3。
```
cat /etc/shadow
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731133949654.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
执行命令，修改密码。
```
passwd 用户名
```
**注意：如果你的密码修改没成功，可能是你用了”1234“这种弱密码，试着在密码中添加个字母试试。**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731134310408.png)

重启你的系统。登录试试。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731134749870.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
成功。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731134851644.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


