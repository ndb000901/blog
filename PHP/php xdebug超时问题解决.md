**实验环境**
>1.VS code
>2.phpstudy
>
**[如何搭建配置调试环境](https://blog.csdn.net/qq_43938052/article/details/105781238)**

修改vhost.conf文件。
加入以下代码

```
IPCConnectTimeout 3000
IPCCommTimeout 3000
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200602153657367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
>Virtual Host 即 Vhost ，是linux中的虚拟主机系统。
虚拟主机 (Virtual Host) 是在同一台机器搭建属于不同域名或者基于不同 IP 的多个网站服务的技术.。可以为运行在同一物理机器上的各个网站指配不同的 IP 和端口， 也可让多个网站拥有不同的域名。

**重启apache**
>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)