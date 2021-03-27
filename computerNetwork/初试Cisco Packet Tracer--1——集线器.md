## 初试Cisco Packet Tracer--1——集线器

**1.实验环境**
>1.win10
>2.Cisco Packet Tracer-7.3.1.0362([下载链接](https://www.netacad.com/zh-hans/courses/packet-tracer/introduction-packet-tracer))

**2.搭建网络**

**实验前必读：**
集线器相比于交换机更为简单，它可以被视作有多个端口的中继器，从一个端口接受比特位（或符号），再从其他端口提交。它对物理层数据包有所感知，可以检测到其开始、挂起及冲突。在检测到冲突时会发送拥塞信号以传播这一事件。集线器不能对经过它的网络流量做更进一步地检查与管理：任何进入的数据包都会被广播到其他端口。集线器/中继器无法储存数据——数据包必须在接收时被发送，一旦发生冲突，就会丢包（发送端应当能够侦测到，并重新发送）。基于此，集线器只能以半双工模式工作。因此，由于冲突域更广，相比于使用更复杂的网络设备，使用集线器的数据网络更容易出现数据包冲突。

集线器（hub）属于纯硬件网络底层设备，基本上不具有类似于交换机的"智能记忆"能力和"学习"能力。它也不具备交换机所具有的MAC地址表，所以它发送数据时都是没有针对性的，而是采用广播方式发送。也就是说当它要向某节点发送数据时，不是直接把数据发送到目的节点，而是把数据包发送到与集线器相连的所有节点，如图所示，简单明了。


搭建网络的元件都在如下工具栏里。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225160040923.png)
将所需元件添加至工作空间后，点击闪电符号，开始连接线路。
**闪电符号可以帮你自动选择线的种类，当然你也可自己选择**
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020122516055943.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
左键点击PC0>>Desktop>>IP Configuration，配置ip。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225160515921.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
PC0 IP
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225160936174.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
PC1 IP
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225161034322.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
PC2 IP
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225170108284.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
根据下图构建ICMP数据报，使其从PC0发到PC1，但是由于是新建的机子，PC0 ARP高速缓存为空，所以先构建ARP广播帧。点击5逐步观察数据报流向。你可以查看右侧Event List里的详情，查看数据如何封装。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225170008720.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
点击右侧 Event List 面板中的Reset Simulation后，重新开始ICMP数据包，现在PC0 ARP高速缓存已有PC1的mac地址，所以不需构建ARP广播。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225171525749.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**3.感受碰撞**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225175115121.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
构建这样一种情形。
>PC0给PC1发送
PC3给PC5发送

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225175214487.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
 如上图，线路会出现碰撞，导致发送失败。
**如何解决这个问题呢？下期分析**


>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)