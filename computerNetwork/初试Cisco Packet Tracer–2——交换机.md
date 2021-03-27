## 初试Cisco Packet Tracer–2——交换机
**1.实验环境**
>1.win10
>2.Cisco Packet Tracer-7.3.1.0362([下载链接](https://www.netacad.com/zh-hans/courses/packet-tracer/introduction-packet-tracer))

**2.搭建网络**

因为交换机有带宽很高的内部交换矩阵和背部总线，并且这个背部总线上挂接了所有的端口，通过内部交换矩阵，就能够把数据包直接而迅速地传送到目的节点而非所有节点， 这样就不会浪费网络资源，从而产生非常高的效率。同时在此过程中，数据传输的安全程度非常高，更是受到使用者的欢迎和普遍好评。
和集线器每个端口共享同样带宽不同的是，交换机的数据带宽具有独享性。在这样的前提下，在同一个时间段内，交换机就可以将数据传输到多个节点之间，并且每个节点都可 以当做独立网段而独自享有固定的部分带宽，这样就没有和其他设备进行竞争实用的必要。

**网络结构**
>PC0-->192.168.100.1
>PC1-->192.168.100.2
>PC2-->192.168.100.3

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225182645815.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
PC0 向PC1发送ICMP数据包。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225184050748.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
由于设备是新的，PC0 ARP高速缓存空，发送ICMP数据报时先广播，得到PC1的mac地址后，才发送ICMP数据报。当你再次发送时，这时交换机与集线器的区别就可以体现出来了。交换机会自学习，会记住每个接口对应的mac地址，这样它不会像集线器那样每一个数据包都广播出去，大大提高了效率。详细的过程，请在仿真时观看。

**3.上次的问题解决方案**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225190351699.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
两个用集线器相连接的网络，之间用交换机相连，交换机经过自学习后，可以有效解决碰撞问题，具体细节请仿真观察。
同时使PC0发送ICMP数据包给PC1；PC3发送ICMP数据包给PC5。第一次发送可能会发生碰撞（交换机是新的），第二次发送时不会碰撞（交换机自学习）。


>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)