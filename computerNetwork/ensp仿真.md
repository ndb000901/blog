## ensp仿真

**1.实验环境**

>1.ensp-1.2.00.510
>
>2.vmware16
>
>3.win7虚拟机
>
>VirtualBox-5.2.44
>

**2.实验1**

**目的**

>通过路由器打通两台处于不同子网主机的链路。
>

>2台PC
>
>路由器：2台AR2220

**网络拓扑**

![image](https://user-images.githubusercontent.com/48900845/115917028-32486b80-a4a8-11eb-9786-fa4601e90c1e.png)

**R1配置**

```
# 配置g0/0/1 ip
sys
int g0/0/1
ip add 192.168.0.254 24

# 配置g0/0/0 ip
int g0/0/0
ip add 192.168.1.1

# 添加静态路由
q
ip route-static 192.168.2.0 24 g0/0/0 192.168.1.2

# 查看静态路由表

dis ip routing-table
```

![image](https://user-images.githubusercontent.com/48900845/115917862-59536d00-a4a9-11eb-9b35-17ec3b25e91f.png)

**R2配置**

```
# 配置g0/0/1 ip
sys
int g0/0/1
ip add 192.168.2.254 24

# 配置g0/0/0 ip
int g0/0/0
ip add 192.168.1.2

# 添加静态路由
q
ip route-static 192.168.0.0 24 g0/0/0 192.168.1.1

# 查看静态路由表

dis ip routing-table
```

![image](https://user-images.githubusercontent.com/48900845/115918477-252c7c00-a4aa-11eb-9ca2-0a87bdde3261.png)

**PC1**

![image](https://user-images.githubusercontent.com/48900845/115918605-4db47600-a4aa-11eb-93f2-71df8b34f501.png)

**PC2**

![image](https://user-images.githubusercontent.com/48900845/115918657-5dcc5580-a4aa-11eb-828a-3098a28d9d7d.png)


