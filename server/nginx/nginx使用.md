# nginx使用



## 1、环境



```ini
Ubuntu 18.04.5 LTS
nginx-1.21.6
```





## 2、安装



### 依赖



```shell
sudo apt install curl gnupg2 ca-certificates lsb-release ubuntu-keyring

# gcc
sudo apt-get install gcc

# openssl
sudo apt-get install openssl libssl-dev  

# zlib
sudo apt-get install zlib1g-dev

# pcre
sudo apt-get install libpcre3 libpcre3-dev  
```



### 下载源码



```ini
# 下载地址
https://nginx.org/en/download.html

wget https://nginx.org/download/nginx-1.21.6.tar.gz
```



### 解压



```ini
tar -zxvf nginx-1.21.6.tar.gz
```



### 编译&安装



```
./configure --prefix=<自定义安装路径>
make
make install
```







## 3、常用命令



**切换到nginx安装路径的sbin目录下**



```ini
# 启动
./nginx

# 重新加载
./nginx -s reload

# 关闭
./nginx -s stop
```







## 4、反向代理



### 案例1



**nginx.conf**



```conf
server {
        listen       1000;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            #root   html;
            #index  index.html index.htm;
	    proxy_pass http://127.0.0.1:10000;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }

```



**location [...]**



```conf
location / {
            #root   html;
            #index  index.html index.htm;
	    proxy_pass http://127.0.0.1:10000;
        }
```



| 符号 | 说明                                                         |
| ---- | ------------------------------------------------------------ |
| =    | 用于不含正则表达式的 uri 前，要求请求字符串与 uri 严格匹配，如果匹配成功，就停止继续向下搜索并立即处理该请求。 |
| ～   | 用于表示 uri 包含正则表达式，并且区分大小写。                |
| ~*   | 用于表示 uri 包含正则表达式，并且不区分大小写。              |
| ^~   | 用于不含正则表达式的 uri 前，要求 Nginx 服务器找到标识 uri 和请求字符串匹配度最高的 location 后，立即使用此 location 处理请求，而不再使用 location块中的正则 uri 和请求字符串做匹配 |



### 案例2



```conf
server {
        listen       1000;
        server_name  www.jiji123456.com;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location /1w/ {
            #root   html;
            #index  index.html index.htm;
	    proxy_pass http://127.0.0.1:10000/;
        }

	location /2w/ {
	    proxy_pass http://127.0.0.1:20000/;
	}

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }

```



### proxy_pass ‘/’ 问题



```ini
# 绝对路径
location /proxy {
    proxy_pass http://127.0.0.1:8080/;
}

http://127.0.0.1/proxy/test/test.txt --> http://10.0.0.1:8080/test/test.txt


# 相对路径

location /proxy {
    proxy_pass http://127.0.0.1:8080;
}

http://127.0.0.1/proxy/test/test.txt --> http://127.0.0.1:8080/proxy/test/test.txt
```





## 5、负载均衡



### nginx.conf



```
    upstream hello {
        server 127.0.0.1:10000;
        server 127.0.0.1:20000;
    }

    server {
        listen       1000;
        server_name  www.jiji123456.com;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location /1w/ {
            #root   html;
            #index  index.html index.htm;
	    proxy_pass http://127.0.0.1:10000/;
        }

	location /2w/ {
	    proxy_pass http://127.0.0.1:20000/;
	}
        location / {
            proxy_pass http://hello;
        }
        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }

```





### 策略



| 策略         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| 轮询（默认） | 每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器 down 掉，能自动剔除 |
| weight       | weight 代表权,重默认为 1,权重越高被分配的客户端越多          |
| ip_hash      | 每个请求按访问 ip 的 hash 结果分配，这样每个访客固定访问一个后端服务器，可以解决 session 的问题 |
| fair         | 按后端服务器的响应时间来分配请求，响应时间短的优先分配。     |





## 6、动静分离



**nginx.conf**



```ini
location /static/ {
            root html;
}
location /dong/ {
            proxy_pass http://127.0.0.1:10000/;
}

```





## 7、集群高可用



**/etc/keepalived/keepalived.conf**



```ini
global_defs {
	notification_email {
		acassen@firewall.loc
		failover@firewall.loc
		sysadmin@firewall.loc
	}
	notification_email_from Alexandre.Cassen@firewall.loc
	smtp_server 192.168.17.129
	smtp_connect_timeout 30
	router_id LVS_DEVEL
}


vrrp_script check {
    script "/home/hello/nginx/check.sh"
    interval 5
    #（检测脚本执行的间隔）
    weight -2
}

vrrp_instance VI_1 {
	state MASTER
	# 备份服务器上将 MASTER 改为 BACKUP
	interface ens33 //网卡
	virtual_router_id 51
	# 主、备机的 virtual_router_id 必须相同
	priority 200
	# 主、备机取不同的优先级，主机值较大，备份机值较小
	advert_int 1
	authentication {
		auth_type PASS
		auth_pass 1111
	}
	virtual_ipaddress {
		172.20.10.14/24 dev ens33 label ens33:1 // VRRP H 虚拟地址
	}

    track_script {
      #引用VRRP脚本，即在 vrrp_script 部分指定的名字。定期运行它们来改变优先级，并最终引发主备切换。
      check
    }
}

```



**check.sh**



```sh
#!/bin/bash
A=`ps -C nginx --no-header |wc -l`
if [ $A -eq 0 ];then
    echo 123456 | sudo -S /home/hello/local/nginx/nginx/sbin/nginx
    sleep 1
    if [ `ps -C nginx --no-header |wc -l` -eq 0 ];then    #nginx重启失败，则停掉keepalived服务
        echo 123456 | sudo -S killall keepalived
    fi
fi

```

