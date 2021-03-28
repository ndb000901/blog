## wireshark 分析tcp协议

**1.实验环境**

>1.manjaro-gnome-20.1.2
>
>2.wireshark-3.4.0
>
>3.VMware-16.0.0
>
>4.ubuntu16.04 (虚拟机192.168.146.100 NAT模式 服务端)
>
>5.ubuntu16.04 (虚拟机192.168.146.101 NAT模式 客户端)
>
>6.python3.8


**2.实验源码**

server.py

**运行于192.168.146.100**
```
import socket
server = socket.socket()
server.bind(('0.0.0.0', 7777))
server.listen(5)
print('开始服务')
while True:
    conn, addr = server.accept()
    print('a new connect from ', addr)
    conn.sendall(bytes('hello,world!', encoding='utf-8'))
    conn.close()
```

client.py

**运行于192.168.146.101**
```
import socket
client = socket.socket()
client.connect(('192.168.146.100', 7777))
data = client.recv(1024)
client.close()
print(data.decode('utf-8'))
```

**3.wireshare分析**

三次握手，一次传输数据，四次挥手。

![image](https://user-images.githubusercontent.com/48900845/112760317-0c56b500-9029-11eb-8ca6-1b9087b315ec.png)

TCP Flags字段

>SYN表示建立连接
>
>FIN表示关闭连接
>
>ACK表示响应
>
>PSH表示有 DATA数据传输
>
>RST表示连接重置

TCP Seq 字段

>TCP 协议为每个包编号（sequence number，简称 SEQ），以便接收的一方按照顺序还原。万一发生丢包，也可以知道丢失的是哪一个包。

TCP ACK字段

>ACK 携带两个信息。
>
>期待要收到下一个数据包的编号
>
>接收方的接收窗口的剩余容量

TCP Window

>接受窗口大小，这个是可变的，用来调节数据发送速率。

IP Flags字段

>1.长度3比特。
>
>2.该字段第一位不使用。
>
>3.第二位是DF（Don't Fragment）位，DF位设为1时表明路由器不能对该上层数据包分段。如果一个上层数据包无法在不分段的情况下进行转发，则路由器会丢弃该上层数据包并返回一个错误信息。
>
>4.第三位是MF（More Fragments）位，当路由器对一个上层数据包分段，则路由器会在除了最后一个分段的IP包的包头中将MF位设为1。

IP Protocol字段

>8bit的协议字段表示在IP上层承载的是什么协议。
>
>0x01表示ICMP协议
>
>0x06表示TCP协议
>
>0x11表示UDP协议等。

数据帧的Type

>IP:  0x0800
>
>ARP: 0x0806

源与目的

>Ethernet：源Mac地址与目的Mac地址
>
>IP：源ip地址与目的ip地址
>
>TCP：源端口与目的端口
>
关于三次握手，四次挥手，请阅读[这篇文章](https://hit-alibaba.github.io/interview/basic/network/TCP.html)





>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
