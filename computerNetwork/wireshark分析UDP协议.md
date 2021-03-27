## wireshark分析UDP协议
**1.实验环境**
>1.manjaro-gnome-20.1.2
>2.wireshark-3.4.0
>3.VMware-16.0.0
>4.ubuntu16.04 (虚拟机192.168.146.100 NAT模式 服务端)
>5.ubuntu16.04 (虚拟机192.168.146.101 NAT模式 客户端)
>6.python3.8

**2.源码**

功能：
客户端脚本执行4次，每次向服务端发送‘cao’字符串，服务端收到后向客户端发送一个字符串。
客户端源码


client.py
```
import socket
client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
client.sendto('cao'.encode('utf-8'), ('192.168.146.100', 7777))
data, addr = client.recvfrom(1024)
print("from:{}   data:{}".format(addr, data))
```

服务端源码
server.py
```
import socket
server = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
server.bind(('0.0.0.0', 7777))
data = ['1234', 'abcd', 'jjjj', 'hello']
i = 0
for i in data:
    data, addr = server.recvfrom(1024)
    print("from:{}   data:{}".format(addr, data))
    server.sendto(i.encode('utf-8'), addr)
```

**3.效果**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201214013231860.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

**4.分析**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201214013610602.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**字段**
>Source Port   源端口
>Destination Port  目的端口
>Length 长度

**UDP的分组结构**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201214013858324.png)
**IPv4伪头部**
当UDP运行在IPv4之上时，为了能够计算校验和，需要在UDP数据包前添加一个“伪头部”。
![
](https://img-blog.csdnimg.cn/2020121401394359.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

**IPv6伪头部**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201214014049323.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
部分图片来源网络，侵删。

>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)