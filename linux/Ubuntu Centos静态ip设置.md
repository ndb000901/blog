##  Ubuntu Centos静态ip设置

**1.实验环境**

>1.VMware16.0.0
>
>2.Ubuntu16.04([安装教程](https://blog.csdn.net/qq_43938052/article/details/107326122))
>
>3.Centos8
>
>4.VMware网络模式：NAT

**2.配置VMnet8**

打开PowerShell，执行命令，查看虚拟网卡是否安装。
```
ipconfig
```

![image](https://user-images.githubusercontent.com/48900845/112806401-50899a00-90a9-11eb-8d6d-fe3fe95e6a56.png)


VMnet8用于NAT模式。

若无上图两块虚拟网卡，请打开VMware，虚拟网络编辑器，还原默认设置。（需要管理员权限）若有上图虚拟网卡，自行跳过这一步。

![image](https://user-images.githubusercontent.com/48900845/112806452-5c755c00-90a9-11eb-8162-eead8e9da02d.png)

![image](https://user-images.githubusercontent.com/48900845/112806472-61d2a680-90a9-11eb-9e6b-c5e56dc17b80.png)


打开控制面板，右击VMnet8属性。

![image](https://user-images.githubusercontent.com/48900845/112806533-72831c80-90a9-11eb-9c04-9bc00b6f1df4.png)

点击属性

![image](https://user-images.githubusercontent.com/48900845/112806555-7a42c100-90a9-11eb-9871-434094e59edc.png)

配置

IP地址你也可以自定义。

比如IP地址你定义为192.168.146.1，那么你的网关的前3段要一样192.168.146

**你可以翻阅一下有关子网掩码、网络地址和主机地址等知识**

![image](https://user-images.githubusercontent.com/48900845/112806602-8af33700-90a9-11eb-9a1a-d53cb9c36600.png)

接下来开始配置VMware。因为需要配置静态ip，所以要将本地DHCP服务给取消了。配置子网IP，子网掩码。

![image](https://user-images.githubusercontent.com/48900845/112806621-93e40880-90a9-11eb-92bb-e1befd18276e.png)

填写网关，要与前面的配置一致

![image](https://user-images.githubusercontent.com/48900845/112806666-9e9e9d80-90a9-11eb-8e4d-aa03a1153681.png)

一路保存。开启ubuntu，centOS开始配置。

**3.ubuntu配置**

执行命令，查看网络信息。
```
ifconfig
```

![image](https://user-images.githubusercontent.com/48900845/112806701-a9593280-90a9-11eb-8963-96a61554876d.png)

我们需要给ens33配置一个静态ip，执行命令，开始配置。
```
vim /etc/network/interfaces
```

配置内容如下

**iface ens33 inet static 静态ip（static，原来是dhcp）**

**address ip地址**

**netmask 子网掩码**

**gateway 网关**

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

![image](https://user-images.githubusercontent.com/48900845/112806845-cee63c00-90a9-11eb-834a-b7c7d09d546b.png)

保存。
执行命令，配置DNS服务器
```
vim /etc/resolvconf/resolv.conf.d/base
```

![image](https://user-images.githubusercontent.com/48900845/112806903-ddccee80-90a9-11eb-9d87-be913a49d4d0.png)

保存。
重启一下机子就好
```
reboot
```

![image](https://user-images.githubusercontent.com/48900845/112806945-e9b8b080-90a9-11eb-9fd5-399cb283cee2.png)


成功。

**4.CentOS配置**

执行命令，查看网络
```
ifconfig
```

![image](https://user-images.githubusercontent.com/48900845/112806992-f5a47280-90a9-11eb-94d8-62c9e99b9b34.png)

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

![image](https://user-images.githubusercontent.com/48900845/112807052-094fd900-90aa-11eb-9118-e6f536826313.png)

执行命令，配置resolv.conf，填写你的网关就好。
```
vim /etc/resolv.conf
```

![image](https://user-images.githubusercontent.com/48900845/112807085-140a6e00-90aa-11eb-96a7-a41e56d042d2.png)

重启机子
```
reboot
```

今天的文章就肝到这里了。


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
