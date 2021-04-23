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


**试验2**

**目的**

>配置vlan
>

>4台PC
>
>2台S3700
>

**网络拓扑**

![image](https://user-images.githubusercontent.com/48900845/115921710-73437e80-a4ae-11eb-871e-a26731f687ee.png)

**PC1配置**

![image](https://user-images.githubusercontent.com/48900845/115921798-98d08800-a4ae-11eb-97ae-02806ddc7e8e.png)

**PC2配置**

![image](https://user-images.githubusercontent.com/48900845/115921840-a554e080-a4ae-11eb-8295-4062cefe8cad.png)

**PC3配置**

![image](https://user-images.githubusercontent.com/48900845/115921881-b30a6600-a4ae-11eb-93cf-24f2284579df.png)

**PC4配置**

![image](https://user-images.githubusercontent.com/48900845/115921906-be5d9180-a4ae-11eb-90e5-4da6a132d711.png)

**LSW1配置**

```
# 创建vlan 1 2
vlan batch 1 2

# 配置e0/0/1
int e0/0/1
port link-type trunk
port trunk allow-pass vlan 1 2

# 配置e0/0/2
int e0/0/2
port link-type access
port default vlan 1

# 配置e0/0/3
int e0/0/3
port link-type access
port default vlan 2

```

**LSW2配置**

```
# 创建vlan 1 2
vlan batch 1 2

# 配置e0/0/1
int e0/0/1
port link-type trunk
port trunk allow-pass vlan 1 2

# 配置e0/0/2
int e0/0/2
port link-type access
port default vlan 1

# 配置e0/0/3
int e0/0/3
port link-type access
port default vlan 2
```
