
# 转载-->https://www.csdn.net/tags/NtjacgwsNzk5MC1ibG9n.html

# Redis-info命令结果解析

```
127.0.0.1:8376> info all
# Server    --- 服务器信息
redis_version:2.8.20  -- redis服务器版本
redis_git_sha1:00000000  -- Git SHA1
redis_git_dirty:0  -- Git Dirty Flag
redis_build_id:b873423ea3d4fc14  -- redis build id
redis_mode:standalone  -- redis的运行模式：standalone还是cluster
os:Linux 3.10.0-327.18.2.el7.x86_64 x86_64  -- Redis所在的操作系统
arch_bits:64  -- Redis内核架构：32位还是64位
multiplexing_api:epoll  -- Redis所使用的事件处理机制
gcc_version:4.8.5  -- Redis编译时所使用的gcc版本
process_id:5786  -- Redis服务器进程的pid
run_id:9ec59b0b8f8f3e819463b8d28fca9ba89abce933  -- Redis服务器的随机标识符（用于sentinel和cluster）
tcp_port:8376  -- Redis服务器的监听端口
uptime_in_seconds:6728387  -- Redis服务器启动的总时长，单位是秒
uptime_in_days:77  -- Redis服务器启动的总时长，单位是天
hz:10  -- Redis内部调度（关闭timeout客户端，删除过期的key等）频率，程序规定serverCron每秒运行10次
lru_clock:13372390  -- 自增的时钟，用于LRU管理，该时钟100ms执行一次。（参考参数hz）
config_file:/home/hadoop/redis_8376/redis.conf  -- Redis配置文件路径


# Clients  --- 已连接的客户端信息
connected_clients:193  -- 已连接的客户端数量（不包括slave连接的客户端）。
client_longest_output_list:0  -- 当前连接的客户端最长输出列表，用client list命令观察omem字段最大值。
client_biggest_input_buf:0  -- 当前连接的客户端最大输入缓存，用client list命令观察qbuf和qbuf-free两字段最大值。
blocked_clients:0  -- 正在等待阻塞命令（BLPOP，BRPOP，BRPOPLPUSH）的客户端数量。


# Memory  -- 内存信息
used_memory:11750252808  --Redis分配的内存总量（字节）
used_memory_human:10.94G  --人类可读的内存总量
used_memory_rss:16637059072  --操作系统角度，redis分配的内存总量。与top命令一致。
used_memory_peak:13654200496  -- Redis内存消耗峰值
used_memory_peak_human:12.72G  -- 人类可读的Redis内存消耗峰值
used_memory_lua:35840  -- LUA引擎使用的内存大小（字节）
mem_fragmentation_ratio:1.42  -- used_memory_rss / used_memory。小于1表示使用了swap，大于1表示碎片较多
mem_allocator:jemalloc-3.6.0  -- 编译时指定的Redis所使用的内存分配器


# Persistence  -- rdb和aof的持久化信息
loading:0  -- 服务器是否正在载入持久化文件
rdb_changes_since_last_save:10493799192  -- 离最近一次成功生成rdb文件，写入命令的个数，既有多少个写入命令没有持久化
rdb_bgsave_in_progress:0  -- 服务器是否正在创建rdb文件。
rdb_last_save_time:1516593579  -- 离最近一次成功创建rdb文件多久了
rdb_last_bgsave_status:ok  -- 最近一次持久化rdb文件是否成功
rdb_last_bgsave_time_sec:0  -- 最近一次成功生成rdb文件耗时的秒数
rdb_current_bgsave_time_sec:-1  -- 如果服务器正在创建rdb文件，这里就是当前创建rdb文件已经耗费的秒数。
aof_enabled:0  -- 是否已经开启了AOF
aof_rewrite_in_progress:0  -- AOF的rewrite操作是否在进行中。
aof_rewrite_scheduled:0  -- rewrite任务计划，当客户端发送bgrewriteaof指令，如果当前rewrite子进程正在执行，那么将客户端请求的bgrewriteaof变为计划任务，待aof子进程结束后执行rewrite 
aof_last_rewrite_time_sec:-1  -- 最近一次AOF rewrite耗费的时长
aof_current_rewrite_time_sec:-1  -- 如果rewrite操作正在执行，此处为所使用时间
aof_last_bgrewrite_status:ok  -- 上次bgrewrite操作的状态
aof_last_write_status:ok  -- 上次AOF写入状态


# Stats  --- 统计信息
total_connections_received:19534660  -- 新创建的连接个数，如果新创建的连接过多，过度的创建和销毁链接对性能有影响，说明端连接严重或链接池使用有问题。
total_commands_processed:14796974293  -- redis处理的命令数
instantaneous_ops_per_sec:16301  -- redis当前的qps
total_net_input_bytes:661322565150  -- redis网络入口流量字节数
total_net_output_bytes:695291247545  -- redis网络出口流量字节数  
instantaneous_input_kbps:921.09  -- redis网络入口kps
instantaneous_output_kbps:984.72  -- redis网络出口kps
rejected_connections:0  -- 拒绝连接的个数
sync_full:1  -- 主从完全同步成功的次数
sync_partial_ok:0  -- 主从部分同步成功的次数
sync_partial_err:0  -- 主从部分同步失败的次数
expired_keys:1049725658  -- 运行以来过期的key的数量
evicted_keys:0  -- 运行以来剔除的key的数量
keyspace_hits:2756196607  -- 命中次数
keyspace_misses:0  -- 没命中次数
pubsub_channels:0  -- 当前使用中的频道数量
pubsub_patterns:0  -- 当前使用的模式数
latest_fork_usec:1284  -- 最近一次fork操作阻塞redis进程的耗时数，单位微秒


# Replication  -- 主从信息
role:master  -- 实例的角色，master还是slave
connected_slaves:1  -- 连接的slave实例的个数
slave0:ip=172.22.0.58,port=8376,state=online,offset=626043133432,lag=1  -- 从库信息
master_repl_offset:626043468677  -- 主从同步偏移量，此值如果和上面的offset相同，说明没延迟
repl_backlog_active:1  -- 复制积压缓冲区是否开启
repl_backlog_size:1048576  -- 复制积压缓冲区大小
repl_backlog_first_byte_offset:626042420102  -- 复制缓冲区偏移量大小
repl_backlog_histlen:1048576  -- 此值等于 master_repl_offset - repl_backlog_first_byte_offset,该值不会超过repl_backlog_size的大小


# CPU  --- CPU信息
used_cpu_sys:165529.61  -- 所有Redis主进程在核心态所占用的CPU时间
used_cpu_user:129734.81  -- 所有Redis主进程在用户态所占用的CPU时间
used_cpu_sys_children:0.00  -- 后台进程在核心态所占用的CPU时间
used_cpu_user_children:0.00  -- 后台进程在用户态所占用的CPU时间


# Commandstats -- 各种命令的统计信息
# calls: 每个命令执行次数
# usec:总共消耗的CPU时长(单位微秒)
# usec_per_call:平均每次消耗的CPU时长(单位微秒)
cmdstat_setnx:calls=1058600944,usec=3625955232,usec_per_call=3.43
cmdstat_del:calls=20,usec=27367,usec_per_call=1368.35
cmdstat_setbit:calls=5041217639,usec=3122287725,usec_per_call=0.62
cmdstat_getrange:calls=1,usec=1690,usec_per_call=1690.00
cmdstat_zincrby:calls=1676839306,usec=50540232309,usec_per_call=30.14
cmdstat_zcount:calls=29906442,usec=104796077,usec_per_call=3.50
cmdstat_select:calls=4215899299,usec=5929025928,usec_per_call=1.41
cmdstat_expire:calls=2726290157,usec=7765181091,usec_per_call=2.85
cmdstat_keys:calls=77,usec=88002,usec_per_call=1142.88
cmdstat_scan:calls=47677,usec=15868864,usec_per_call=332.84
cmdstat_ping:calls=41455097,usec=58940755,usec_per_call=1.42
cmdstat_psync:calls=1,usec=1461,usec_per_call=1461.00
cmdstat_replconf:calls=6717280,usec=10878864,usec_per_call=1.62
cmdstat_flushdb:calls=20,usec=999516,usec_per_call=49975.80
cmdstat_info:calls=326,usec=39375,usec_per_call=120.78
cmdstat_bitcount:calls=7,usec=167648,usec_per_call=23949.71


# Keyspace
db0:keys=400,expires=0,avg_ttl=0
```
