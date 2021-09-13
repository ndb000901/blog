# nmap使用

## 环境

```
nmap-7.92
```

## 选项

**目标**

|参数|说明|
|----|----|
|-iL <inputfilename>|从主机/网络的列表中输入|
|-iR <num hosts>|选择随机目标|
|--exclude <host1,...>|排除主机/网络|
|--excludefile <exclude_file>|从文件中排除名单|
  
**主机发现**
  
|参数|说明|
|----|----|
|-sL|列表扫描 - 简单列出要扫描的目标|
|-sn|Ping扫描 - 禁用端口扫描|
|-Pn|将所有主机视为在线 -- 跳过主机发现|
|-PS/PA/PU/PY[portlist]|对指定的端口进行TCP SYN/ACK、UDP或SCTP发现|
|-PE/PP/PM|ICMP回应、时间戳和网络掩码请求发现探针|
|-PO[protocol list]|IP协议 ping|  
|-n/-R|从不进行DNS解析/总是解析[默认：有时]|
|--dns-servers <serv1,...>|指定自定义DNS服务器|  
|--system-dns|使用操作系统的DNS解析器|
|--traceroute|追踪到每个主机的一跳路径|  
  
**扫描技术**
  
|参数|说明|
|----|----|
|-sS/sT/sA/sW/sM|TCP SYN/Connect()/ACK/Windows/Maimon扫描|
|-sU|UDP扫描|
|-sN/sF/sX|TCP Null, FIN, 和 Xmas 扫描|
|--scanflags <flags>|自定义TCP扫描标志|
|-sI <zombie host[:probeport]>|空闲扫描|
|-sY/sZ|SCTP INIT/COOKIE-ECHO扫描|
|-sO|IP协议扫描|
|-b|FTP跳转扫描|


**端口扫描设置**
  
|参数|说明|
|----|----|
|-p <port ranges>|只扫描指定的端口|
|--exclude-ports <port ranges>|排除指定的端口进行扫描|
|-F|快速模式 - 扫描比默认扫描更少的端口|
|-r|连续扫描端口 - 不要随机化|
|--top-ports <number>|扫描 <number> 最常用的端口|
|--port-ratio <ratio>|扫描比<ratio>更常见的端口|

**服务/版本检测**
  
|参数|说明|
|----|----|
|-sV|探测开放的端口以确定服务/版本信息|
|--version-intensity <level>|设定从0（轻）到9（尝试所有探测）|
|--version-light|限制在最有可能的探针上（强度2）|
|--version-all|尝试每一个探针（强度9）|
|--version-trace|显示详细的版本扫描活动（用于调试）|


**SCRIPT扫描**
  
|参数|说明|
|----|----|
|-sC|等同于 --script=default|
|--script=<Lua scripts>|<Lua scripts>是一个逗号分隔的列表，其中包括目录、脚本文件或脚本类别的逗号分隔列表|
|--script-args=<n1=v1,...>|向脚本提供参数|
|--script-args-file=filename|在一个文件中提供NSE脚本的args|
|--script-trace|显示所有发送和接收的数据|
|--script-updatedb|更新脚本数据库|
|--script-help=<Lua scripts>|显示关于脚本的帮助|

**操作系统检测**

|参数|说明|
|----|----|
|-O|启用操作系统检测|
|--osscan-limit|限制对有希望的目标进行操作系统检测|
|--osscan-guess|更积极地猜测操作系统|

  
**时间和性能**

|参数|说明|
|----|----|  
|-T<0-5>|设置计时模板（越高越快）|
|--min-hostgroup/max-hostgroup <size>|平行主机扫描组的大小|
|--min-parallelism/max-parallelism <numprobes>|探针并行化|
|--min-rtt-timeout/max-rtt-timeout/initial-rtt-timeout|指定探针往返时间|
|--max-retries|端口扫描探针的重传次数上限|
|--host-timeout|在指定时间后放弃目标|
|--scan-delay/--max-scan-delay <time>|调整探针之间的延迟|
|--min-rate <number>|发送数据包的速度不低于每秒<number>|
|--max-rate <number>|发送数据包的速度不超过每秒<number>|
  
**防火墙/ID规避和欺骗**
  
|参数|说明|
|----|----|  
|-f;--mtu<val>|对数据包进行分片处理（可选择使用给定的MTU）|
|-D <decoy1,...>|用诱饵掩盖一个扫描|
|-S <IP>|欺骗源地址|
|-e <iface>|使用指定的接口|
|-g/--source-port <portnum>|使用指定的端口号|
|--proxies <url1,...>|通过HTTP/SOCKS4代理进行中继连接|
|--data <hex string>|在发送的数据包上添加一个自定义的payload|
|--data-string <string>|在发送的数据包中添加一个自定义的ASCII字符串|
|--data-length <num>|将随机数据添加到发送的数据包中|
|--ip-options <options>|用指定的ip选项发送数据包|
|--ttl <val>|设置IP生存时间字段|
|--spoof-mac <mac address/prefix/vendor name>|欺骗你的MAC地址|
|--badsum|发送带有假的TCP/UDP/SCTP校验和的数据包|
  
**输出**

|参数|说明|
|----|----| 
|-oN/-oX/-oS/-oG <file>|以normal、XML、s|<rIpt kIddi3,和Grepable格式，分别输出到给定的文件名。|
|-oA <basename>|一次性以三种主要格式输出|
|-v|增加粗略程度(使用-vv或更多以获得更大效果)|
|-d|增加调试级别（使用-dd或更多，效果会更好|
|--reason|显示一个端口处于特定状态的原因|
|--open|只显示开放（或可能开放）的端口|
|--packet-trace|显示所有发送和接收的数据包|
|--iflist|打印主机接口和路由（用于调试）|
|--append-output|追加到指定的输出文件中，而不是删掉|
|--resume <filename>|恢复已中止的扫描|
|--noninteractive|禁用通过键盘进行的运行时交互|
|--stylesheet <path/URL>|XSL样式表，将XML输出转换成HTML|
|--webxml|参考Nmap.Org的样式表以获得更多可移植的XML|
|--no-stylesheet|防止将XSL样式表与XML输出联系起来|

**MISC:**
  
|-6|启用IPv6扫描|
|-A|启用操作系统检测、版本检测、脚本扫描和traceroute|
|--datadir|指定自定义Nmap数据文件位置|
|--send-eth/--send-ip|使用原始以太网帧或IP数据包发送|
|--privileged|假设用户是全权限的|
|--unprivileged|假设用户缺乏原始套接字的权限|
|-V|打印版本号|
|-h|打印这个帮助摘要页|
