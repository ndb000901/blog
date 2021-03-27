##  Ubuntu Centos静态ip设置
**1.实验环境**
>1.VMware16.0.0
>2.Ubuntu16.04([安装教程](https://blog.csdn.net/qq_43938052/article/details/107326122))
>3.Centos8
>4.VMware网络模式：NAT

**2.配置VMnet8**

打开PowerShell，执行命令，查看虚拟网卡是否安装。
```
ipconfig
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006181925536.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
VMnet8用于NAT模式。
若无上图两块虚拟网卡，请打开VMware，虚拟网络编辑器，还原默认设置。（需要管理员权限）若有上图虚拟网卡，自行跳过这一步。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006182245732.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006182504749.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)

打开控制面板，右击VMnet8属性。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006195711697.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
点击属性
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006195817134.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
配置
IP地址你也可以自定义。
比如IP地址你定义为192.168.146.1，那么你的网关的前3段要一样192.168.146
**你可以翻阅一下有关子网掩码、网络地址和主机地址等知识**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006195905189.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
接下来开始配置VMware。因为需要配置静态ip，所以要将本地DHCP服务给取消了。配置子网IP，子网掩码。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006201023791.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
填写网关，要与前面的配置一致
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006201105144.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
一路保存。开启ubuntu，centOS开始配置。

**3.ubuntu配置**
执行命令，查看网络信息。
```
ifconfig
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006201631148.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
我们需要给ens33配置一个静态ip，执行命令，开始配置。
```
vim /etc/network/interfaces
```
配置内容如下
**iface ens33 inet static 静态ip（static，原来是dhcp）
address ip地址
netmask 子网掩码
gateway 网关**
```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback
auto ens33
iface ens33 inet static
address 192.168.146.104
netmask 255.255.255.0
gateway 192.168.146.2

```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006201859768.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)

保存。
执行命令，配置DNS服务器
```
vim /etc/resolvconf/resolv.conf.d/base
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006202340235.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)

保存。
重启一下机子就好
```
reboot
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006202615378.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)

成功。

**4.CentOS配置**
执行命令，查看网络
```
ifconfig
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006203129922.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
需要配置ens33。
执行命令，开始配置。
```
vim /etc/sysconfig/network-scripts/ifcfg-ens33
```
填写以下内容
BOOTPROTO填static
IPADDR填你要设定的IP
GATEWAY填写网关
NETMASK填写子网掩码
DNS1填写DNS服务器地址，填网关就好
ONBOOT填yes
```
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
IPADDR=192.168.146.129
GATEWAY=192.168.146.2
NETMASK=255.255.255.0
DNS1=192.168.146.2
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
UUID=152a6305-70b6-4b63-b7b9-6b9c52c0c752
DEVICE=ens33
ONBOOT=yes

```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006203347983.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
执行命令，配置resolv.conf，填写你的网关就好。
```
vim /etc/resolv.conf
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201006212256769.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
重启机子
```
reboot
```

今天的文章就肝到这里了。

>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
