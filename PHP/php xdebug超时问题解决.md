**实验环境**

>1.VS code
>
>2.phpstudy
>

**[如何搭建配置调试环境](https://blog.csdn.net/qq_43938052/article/details/105781238)**

修改vhost.conf文件。
加入以下代码

```
IPCConnectTimeout 3000
IPCCommTimeout 3000
```

![image](https://user-images.githubusercontent.com/48900845/112752274-c12aab00-9004-11eb-9486-cc2a36195279.png)

>Virtual Host 即 Vhost ，是linux中的虚拟主机系统。
>
虚拟主机 (Virtual Host) 是在同一台机器搭建属于不同域名或者基于不同 IP 的多个网站服务的技术.。可以为运行在同一物理机器上的各个网站指配不同的 IP 和端口， 也可让多个网站拥有不同的域名。

**重启apache**


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
