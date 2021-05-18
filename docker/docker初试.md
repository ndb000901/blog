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

```

```
## 3.容器

## 4.仓库
