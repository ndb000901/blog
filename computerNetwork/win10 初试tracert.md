## win10 初试tracert

**1.实验环境**

>1.win10
>
>2.tracert

**2.tracert (Traceroute )原理**

ICMP报文类型

![image](https://user-images.githubusercontent.com/48900845/112760192-ba159400-9028-11eb-87ae-f01184f2a1f8.png)

![image](https://user-images.githubusercontent.com/48900845/112760209-be41b180-9028-11eb-876b-1f0c99c1f32c.png)

![image](https://user-images.githubusercontent.com/48900845/112760223-c39efc00-9028-11eb-9810-b2d39d41df2a.png)


Traceroute 是 ICMP 的一个应用，用来跟踪一个分组从源主机到目标主机的路径。
Traceroute 发送的 IP 数据报封装的是无法交付的 UDP 用户数据报，并由目的主机发送终点不可达差错报告报文。

>
>**1.** 源主机向目的主机发送一连串的 IP 数据报。
>
>**2.** 第一个数据报 P1 的生存时间 TTL 设置为 1，当 P1 到达路径上的第一个路由器 R1 时，R1 收下它并把 TTL 减 1，此时 TTL 等于 0，R1 就把 P1 丢弃，并向源主机发送一个 ICMP 时间超过差错报告报文；
>
>**3.** 源主机接着发送第二个数据报 P2，并把 TTL 设置为 2。P2 先到达 R1，R1 收下后把 TTL 减 1 再转发给 R2，R2 收下后也把 TTL 减 1，由于此时 TTL 等于 0，R2 就丢弃 P2，并向源主机发送一个 ICMP 时间超过差错报文。
>
>**4.** 重复以上操作... ...
>
>**5.** 直到最后一个数据报刚刚到达目的主机，主机不转发数据报，也不把 TTL 值减 1。由于数据报封装的是无法交付的 UDP，因此目的主机要向源主机发送 ICMP 终点不可达差错报告报文。
>
>**6.** 综上所述，可以得到源主机到达目的主机所经过的路由器 IP 地址以及到达每个路由器的往返时间。


**3.执行效果**

打开终端>>执行命令

**注意：想追踪哪个，请随意**
```
tracert baidu.com
```

![image](https://user-images.githubusercontent.com/48900845/112760269-d7e2f900-9028-11eb-9388-a166616f7c6b.png)

**tracert用法**

![image](https://user-images.githubusercontent.com/48900845/112760281-dfa29d80-9028-11eb-88b6-6d5ed2fe5cc7.png)



>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
