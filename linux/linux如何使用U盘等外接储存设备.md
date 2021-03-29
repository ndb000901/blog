## linux如何使用U盘等外接储存设备

**1.插入U盘**

**2.查看**

```
lsblk #查看所有块设备

```

![image](https://user-images.githubusercontent.com/48900845/112807530-998e1e00-90aa-11eb-8b0e-0e651fc77158.png)

我的是256MB的U盘，就是如图所示的sdb设备了，mountpoint为空，因为还没有挂载哩。

sdb对应的路径因该是/dev/sdb喽（你可以用fdisk -l查看一下）

![image](https://user-images.githubusercontent.com/48900845/112807573-a6ab0d00-90aa-11eb-9fdc-02cbb7416da4.png)

**3.挂载**

```
mkdir /mnt/usb   #新建一个目录，用来挂载U盘
mount /dev/sdb /mnt/usb   #把U盘挂载到/mnt/usb
lsblk  #查看一下
```

![image](https://user-images.githubusercontent.com/48900845/112807622-b1fe3880-90aa-11eb-8226-0a118879eaac.png)

sdb的mountpoint不在为空，而是刚才的挂载点/mnt/usb

**恭喜！！！可以在/mnt/usb下浏览U盘内容了**

**4.umount**

用完后，先执行
```
umount /dev/sdb /mnt/usb #先卸载
lsblk #查看一下
```

![image](https://user-images.githubusercontent.com/48900845/112807668-be829100-90aa-11eb-9871-ad9701482d38.png)

**mountpoint又变为空了。but你用fdisk -l 查看（显示U盘还在），这时你需要关闭驱动器。**

![image](https://user-images.githubusercontent.com/48900845/112807710-c9d5bc80-90aa-11eb-9751-0796823896f9.png)


**5.安全关闭驱动器**

```
udisksctl power-off -b /dev/sdb				#安全关闭驱动器
fdisk -l #查看
```

这下U盘没了（弹出了）

![image](https://user-images.githubusercontent.com/48900845/112807759-d823d880-90aa-11eb-9f70-fe4bd9aaeafd.png)

**注意：如果提示**
```
The program 'udisksctl' is currently not installed. You can install it by typing:
apt install udisks2

```
**安装udisks2再试**
```
apt install udisks2 #安装udisks2
```
**6.拔掉U盘**


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
