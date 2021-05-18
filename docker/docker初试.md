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
docker commit -m "创建镜像" -a "作者" id/名称 test
```

**基于本地模板创建**

```
cat ubuntu_18.04.tar | docker import ubuntu:18.04
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

**2.**
## 4.仓库
