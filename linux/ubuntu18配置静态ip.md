# ubuntu18配置静态ip

## 1.环境

>1.ubuntu18.04

## 2.配置

**/etc/netplan/.yaml**

```
# This is the network config written by 'subiquity'
network:
  ethernets:
    ens33:
      dhcp4: no
      addresses: [192.168.43.60/24]
      gateway4: 192.168.43.1
      nameservers:
        addresses: [192.168.202.1]
  version: 2

```

**执行命令**

```
sudo netplan apply
```
