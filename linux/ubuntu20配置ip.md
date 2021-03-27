## ubuntu20配置ip
**1.实验环境**
>1.ubuntu20

**2.配置ip**

打开终端，修改以下文件，文件名可能不一致，请灵活处理。
ens33取决自己的实际情况。
```
vim /etc/netplan/01-network-manager-all.yaml
```

```
# Let NetworkManager manage all devices on this system
network:
  version: 2
  #renderer: NetworkManager
  ethernets:
    ens33:
      addresses: [192.168.146.200/24]
      dhcp4: no
      dhcp6: no
      gateway4: 192.168.146.2
      nameservers:
        addresses: [192.168.146.2,8.8.8.8]

```
**注意：冒号后需空格，每一级缩进严格**

执行命令，配置ip
```
netplan apply
```

查看ip
```
ip addr
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201229030302356.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
测试网络连通性
```
ping baidu.com
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201229030355306.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)