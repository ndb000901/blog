# docker初试

## 1.实验环境

>1.ubuntu18.04
>

**docker version**

```
Client: Docker Engine - Community
 Version:           20.10.6
 API version:       1.41
 Go version:        go1.13.15
 Git commit:        370c289
 Built:             Fri Apr  9 22:46:01 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.6
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.13.15
  Git commit:       8728dd2
  Built:            Fri Apr  9 22:44:13 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.4
  GitCommit:        05f951a3781f4f2c1911b05e61c160e9c30eaa8e
 runc:
  Version:          1.0.0-rc93
  GitCommit:        12644e614e25b05da6fd08a38ffa0cfe1903fdec
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0

```

[**安装教程**](https://github.com/ndb000901/blog/blob/main/softwareInstallation/docker%E5%AE%89%E8%A3%85.md)

## 2.镜像

**1.获取镜像**

```
docker pull ubuntu
```

**2.查看镜像信息**

```
# 列出本地镜像
docker images

# 镜像详细信息
docker inspect 标签/id
```

**3.搜索镜像**

[官方仓库](https://hub.docker.com/)

**docker search 表头**
 
|表头|说明|
|----|----|
|NAME|名字|
|DESCRIPTION|描述|
|STARS|星级|
|OFFICIAL|是否官方创建|
|AUTOMATED|是否自动创建|

```
docker search mysql
```
**4.创建镜像**

**基于已有镜像的容器创建**

**docker commit一些选项**

|选项|说明|
|----|----|
|-a,--author=""|作者信息|
|-m,--message=""|提交消息|
|-p,--pause=true|提交时暂停容器运行|

```
docker commit -m "创建镜像" -a "作者" id/名称 镜像名
```

**基于本地模板创建**

```
cat ubuntu_18.04.tar | docker import - ubuntu:18.04
```

**基于Dockerfile创建**

```
```

**5.删除镜像**

删除镜像需删除依赖于该镜像的所有容器。

-f 强制删除镜像，不推荐。

```
docker rmi 标签/id
```

**6.存出镜像**

将ubuntu:18.04存出

```
docker save -o ubuntu_18.04.tar ubuntu:18.04
```

**7.载入镜像**

载入ubuntu_18.04.tar

```
docker load --input ubuntu_18.04.tar
或
docker load < ubuntu_18.04.tar
```

**8.上传镜像**

上传本地ubuntu:18.04

```
docker tag ubuntu:18.04 user/ubuntu:18.04 test
docker push user/ubuntu:18.04
```

## 3.容器

**1.容器的状态**

|状态|说明|
|----|----|
|created|已创建|
|restarting|重启中|
|running|Up（运行中）|
|removing|迁移中|
|paused|暂停|
|exited|停止|
|dead|死亡|

**2.创建容器**

docker create 创建的容器处于停止状态，需要start启动。

docker run 等价上述步骤。

```
# 方法1
docker create -it ubuntu:18.04
docker start id/名称

# 方法2
docker run ubuntu:18.04 /bin/echo "hello world"
```

**守护态运行**

-d 后台以守护态运行

```
docker run -d ubuntu:18.04 /bin/bash "while true;do echo hello,world;sleep 1;done"
```

**3.查看容器**

-a 所有容器

```
docker ps -a
```

**4.终止容器**

```
docker stop id/名称
```

**5.删除容器**

**docker rm一些参数**

|参数|说明|
|----|----|
|-f,--force=false|强行终止并删除一个运行中的容器|
|-l,--link=false|删除容器连接，但保留容器|
|-v,--volumes=false|删除容器挂载的数据卷|

```
docker rm id/名称
```

**6.进入容器**

推荐使用方法2

```
docker run -tid ubuntu:18.04

# 方法1
docker attach id/名称

# 方法2
docker exec -ti id/名称

#方法3
nsenter --target PID --mount --uts --ipc --net --pid

```

**7.导出容器**

```
docker export id/名称 > filename
```

**8.导入容器**

```
cat filename | docker import - 镜像名
```

## 4.仓库

本地仓库

```
docker run -d -p 5000:5000 registry
```

## 5.数据管理

**1.数据卷**

容器与主机共享数据

**在容器内创建一个数据卷**

--name 容器命名

-v 创建一个数据卷

```
# 创建容器
docker run --name hello -dti -v /hello ubuntu:18.04

# 连接hello
docker exec -ti hello /bin/bash

#  查看
ls /
```

**挂载主机目录作为数据卷**

```
# 创建容器
docker run --name hello -dti -v /home/ubuntu:/hello ubuntu:18.04

# 连接hello
docker exec -ti hello /bin/bash

#  查看
ls /hello
```

**挂载本地主机文件作为数据卷**

```
# 创建容器
docker run --name hello -dti -v ~/.bash_history:~/.bash_history ubuntu:18.04

# 连接hello
docker exec -ti hello /bin/bash

#  查看
cat ~/.bash_history
```

**2.数据卷容器**

容器与容器之间共享数据

--volumes-from 挂载的数据卷并不需要保持运行状态

```
docker run -it -v /dbdata --name dbdata ubuntu:18.04
docker run -it --volumes-from dbdata --name db1 ubuntu:18.04
docker run -it --volumes-from dbdata --name db2 ubuntu:18.04
```


**只删除挂载的容器数据卷并不会被删除，需加-v**

**删除：docker rm -v id/名称**


## 6.网络基础配置

## 7.Dockerfile


