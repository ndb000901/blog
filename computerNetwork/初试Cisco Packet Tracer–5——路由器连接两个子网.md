## 初试Cisco Packet Tracer–5——路由器连接两个子网

**1.实验环境**
>1.win10
>2.Cisco Packet Tracer-7.3.1.0362([下载链接](https://www.netacad.com/zh-hans/courses/packet-tracer/introduction-packet-tracer))

**2.环境搭建**

网络拓扑图
**IP配置**

>PC0-->192.168.100.1
>PC1-->192.168.100.2


![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226155346996.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226155650386.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226155723939.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)



打开PC0 Command Prompt 测试连通性，如下图所示，网络连通。
```
ping 192.168.100.2
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226155555840.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
接下来，我们将个人PC1的ip设置为192.168.101.1，子网掩码(Subnet Mask)255.255.255.0，这时PC0 与PC1不在同一网络。
**如何得知主机所在的网络号：ip地址与子网掩码按位与，得到的结果为网络号，网络号不同的主机位于不同的网络中。**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226155910953.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
这时我们用PC0去ping PC1 ,无法ping通。因为不在同一子网，需要路由器。
```
ping 192.168.101.1
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226160914563.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
添加路由器后的网络拓扑图

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226164342892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

**大家可以点击Options>>Preferences 把Always Show Port.....勾选上，效果如下图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226164316150.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


现在线路有红色的标志，是因为没有开启路由器相应接口。点击路由器>>Config配置

**配置Gig0/0/0接口**
```
勾选Port Status 后面的on
配置ip 192.168.100.254
配置子网掩码 255.255.255.0
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226163651388.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**配置Gig0/0/1接口**
```
勾选Port Status 后面的on
配置ip 192.168.101.254
配置子网掩码 255.255.255.0
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226164117711.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
开始用PC0 去ping PC1，发现依旧ping不通。因为PC0与PC1不在同一网络，PC0要连通PC1需要设置网关。
```
ping 192.168.101.1
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226164630831.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

现在我们开始为PC0，PC1配置网关(Gateway)

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020122616473581.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226164830902.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
PC0 ping PC1，现在可以ping通了，但是你会发现第一次ping丢了一个数据包，这是因为设备都是新的，在PC0发送ICMP(ping 是ICMP echo的应用)之前发起了ARP广播，导致超时。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226165123966.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
PC1 ping PC0
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226165556313.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)