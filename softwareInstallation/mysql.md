# mysql安装

## 环境

>manjaro-gnome-21
>
>mysql-8.0.24[地址](https://downloads.mysql.com/archives/community/)

## 安装

**解压**

**新建mysql用户**

```
useradd -M -s /sbin/nologin mysql
```

**初始化**

```
./mysqld --initialize --user=mysql --basedir=/home/hello/local/mysql/mysql-8.0.24 --datadir=/home/hello/local/mysql/mysql-8.0.24/data
```

## Error

**./mysql: error while loading shared libraries: libncurses.so.5: cannot open shared object file: No such file or directory**

```
安装 ncurses5-compat-libs

安装 libnuma
```
