## 初试Cisco Packet Tracer–5——路由器连接两个子网

**1.实验环境**

>1.win10
>
>2.Cisco Packet Tracer-7.3.1.0362([下载链接](https://www.netacad.com/zh-hans/courses/packet-tracer/introduction-packet-tracer))

**2.环境搭建**

网络拓扑图

**IP配置**

>PC0-->192.168.100.1
>
>PC1-->192.168.100.2

![image](https://user-images.githubusercontent.com/48900845/112760955-707a7880-902b-11eb-86de-df9374176cb4.png)

![image](https://user-images.githubusercontent.com/48900845/112760962-74a69600-902b-11eb-9adb-7e2811284ee0.png)

![image](https://user-images.githubusercontent.com/48900845/112760967-7a03e080-902b-11eb-95cc-6112d025f145.png)


打开PC0 Command Prompt 测试连通性，如下图所示，网络连通。
```
ping 192.168.100.2
```

![image](https://user-images.githubusercontent.com/48900845/112760983-88ea9300-902b-11eb-9550-fe526a301222.png)

接下来，我们将个人PC1的ip设置为192.168.101.1，子网掩码(Subnet Mask)255.255.255.0，这时PC0 与PC1不在同一网络。

**如何得知主机所在的网络号：ip地址与子网掩码按位与，得到的结果为网络号，网络号不同的主机位于不同的网络中。**

![image](https://user-images.githubusercontent.com/48900845/112760994-9738af00-902b-11eb-918c-2861b87ee48d.png)

这时我们用PC0去ping PC1 ,无法ping通。因为不在同一子网，需要路由器。
```
ping 192.168.101.1
```

![image](https://user-images.githubusercontent.com/48900845/112761022-bdf6e580-902b-11eb-9a61-f6fc9a110f98.png)

添加路由器后的网络拓扑图

![image](https://user-images.githubusercontent.com/48900845/112761027-c51df380-902b-11eb-94f6-5f8b46a4de6a.png)


**大家可以点击Options>>Preferences 把Always Show Port.....勾选上，效果如下图**

![image](https://user-images.githubusercontent.com/48900845/112761042-d0711f00-902b-11eb-9f30-e2c4eff303b7.png)



现在线路有红色的标志，是因为没有开启路由器相应接口。点击路由器>>Config配置

**配置Gig0/0/0接口**
```
勾选Port Status 后面的on
配置ip 192.168.100.254
配置子网掩码 255.255.255.0
```

![image](https://user-images.githubusercontent.com/48900845/112761059-e54db280-902b-11eb-89a2-8a908de108ae.png)

**配置Gig0/0/1接口**
```
勾选Port Status 后面的on
配置ip 192.168.101.254
配置子网掩码 255.255.255.0
```

![image](https://user-images.githubusercontent.com/48900845/112761064-eed71a80-902b-11eb-98b3-d453a929b3a0.png)

开始用PC0 去ping PC1，发现依旧ping不通。因为PC0与PC1不在同一网络，PC0要连通PC1需要设置网关。
```
ping 192.168.101.1
```

![image](https://user-images.githubusercontent.com/48900845/112761072-f7c7ec00-902b-11eb-80c2-81bc969f5406.png)


现在我们开始为PC0，PC1配置网关(Gateway)

![image](https://user-images.githubusercontent.com/48900845/112761087-01e9ea80-902c-11eb-96cd-4c9e39e34167.png)

![image](https://user-images.githubusercontent.com/48900845/112761089-06160800-902c-11eb-9d84-9fb88b4ceb61.png)

PC0 ping PC1，现在可以ping通了，但是你会发现第一次ping丢了一个数据包，这是因为设备都是新的，在PC0发送ICMP(ping 是ICMP echo的应用)之前发起了ARP广播，导致超时。

![image](https://user-images.githubusercontent.com/48900845/112761094-0f06d980-902c-11eb-9cd0-ca04159d0770.png)

PC1 ping PC0

![image](https://user-images.githubusercontent.com/48900845/112761104-1e862280-902c-11eb-91de-1282cfa46db5.png)



>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
