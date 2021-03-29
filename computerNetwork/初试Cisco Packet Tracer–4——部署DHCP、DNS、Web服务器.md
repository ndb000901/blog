## 初试Cisco Packet Tracer–4——部署DHCP、DNS、Web服务器

**1.实验环境**

>1.win10
>
>2.Cisco Packet Tracer-7.3.1.0362([下载链接](https://www.netacad.com/zh-hans/courses/packet-tracer/introduction-packet-tracer))

**2.环境搭建**

网络拓扑图
3台server设备、3台PC设备、1台交换机2960

![image](https://user-images.githubusercontent.com/48900845/112760734-ac610e00-902a-11eb-9eb8-3e121b0dfcef.png)

DHCP服务器配置，开启DHCP。

![image](https://user-images.githubusercontent.com/48900845/112760745-b256ef00-902a-11eb-9da5-4034c68a3cc3.png)


ip配置为静态

![image](https://user-images.githubusercontent.com/48900845/112760764-b8e56680-902a-11eb-8bc4-fb28f60370b7.png)


Web服务器配置，开启HTTP

![image](https://user-images.githubusercontent.com/48900845/112760779-c1d63800-902a-11eb-9f8e-01d21aadf750.png)


IP配置为静态ip

![image](https://user-images.githubusercontent.com/48900845/112760789-c8fd4600-902a-11eb-89b2-cb83e29c7d92.png)



DNS服务器配置，开启DNS

![image](https://user-images.githubusercontent.com/48900845/112760799-d0245400-902a-11eb-863b-39a1b9a584af.png)


ip配置，其实网关这玩意不填也可以，反正在同一个子网。

![image](https://user-images.githubusercontent.com/48900845/112760807-d7e3f880-902a-11eb-92cd-93c25d0c6043.png)


**3.DHCP服务仿真**

**步骤：** 
点击下图simulation，点击>>PC0>>Desktop>>IP Configuration

![image](https://user-images.githubusercontent.com/48900845/112760850-0661d380-902b-11eb-93bc-9852454442a3.png)

![image](https://user-images.githubusercontent.com/48900845/112760867-15488600-902b-11eb-9d37-c327cdac5769.png)

点击DHCP，此时PC0开始向DHCP服务器获取ip。具体过程请点击下一步观测。

![image](https://user-images.githubusercontent.com/48900845/112760880-21344800-902b-11eb-947e-d51819bb2bff.png)

**4.Web访问仿真**
依旧使用PC0>>打开Web Browser

![image](https://user-images.githubusercontent.com/48900845/112760886-298c8300-902b-11eb-9fdd-475c491dd3ea.png)

访问Web服务器192.168.100.2，详细过程请观察仿真。

![image](https://user-images.githubusercontent.com/48900845/112760897-314c2780-902b-11eb-904d-ffb810cfc00a.png)

**5.DNS服务**

依旧使用PC0>>打开Web Browser

![image](https://user-images.githubusercontent.com/48900845/112760906-3d37e980-902b-11eb-85b3-ffb6e679f37a.png)

这次访问www.baidu.com，观测请求DNS服务器的过程。

![image](https://user-images.githubusercontent.com/48900845/112760914-43c66100-902b-11eb-867a-104f4d6e2094.png)

由于我们的DNS服务器没有数据，无法解析域名对应的ip，最后提示Host Name Unresolved



>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
