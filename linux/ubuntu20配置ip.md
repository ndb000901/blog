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

![image](https://user-images.githubusercontent.com/48900845/112807945-0b666780-90ab-11eb-9563-6c283ab86900.png)

测试网络连通性
```
ping baidu.com
```

![image](https://user-images.githubusercontent.com/48900845/112807968-13260c00-90ab-11eb-8a48-4163cf661a88.png)


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
