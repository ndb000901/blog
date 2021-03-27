## 初试Cisco Packet Tracer–4——部署DHCP、DNS、Web服务器

**1.实验环境**
>1.win10
>2.Cisco Packet Tracer-7.3.1.0362([下载链接](https://www.netacad.com/zh-hans/courses/packet-tracer/introduction-packet-tracer))

**2.环境搭建**

网络拓扑图
3台server设备、3台PC设备、1台交换机2960
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020122601184256.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
DHCP服务器配置，开启DHCP。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226023254957.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

ip配置为静态
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226012558620.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

Web服务器配置，开启HTTP
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226012701725.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

IP配置为静态ip
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226023609271.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


DNS服务器配置，开启DNS


![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226023749894.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

ip配置，其实网关这玩意不填也可以，反正在同一个子网。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226023711325.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

**3.DHCP服务仿真**

**步骤：** 点击下图simulation，点击>>PC0>>Desktop>>IP Configuration

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226013400881.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226013654113.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
点击DHCP，此时PC0开始向DHCP服务器获取ip。具体过程请点击下一步观测。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226013741957.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**4.Web访问仿真**
依旧使用PC0>>打开Web Browser
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020122601510021.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
访问Web服务器192.168.100.2，详细过程请观察仿真。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226023955460.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**5.DNS服务**
依旧使用PC0>>打开Web Browser
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020122601510021.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
这次访问www.baidu.com，观测请求DNS服务器的过程。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226024329456.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
由于我们的DNS服务器没有数据，无法解析域名对应的ip，最后提示Host Name Unresolved

>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)