## linux如何使用U盘等外接储存设备
**1.插入U盘**
**2.查看**
```
lsblk #查看所有块设备

```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200627195826377.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
我的是256MB的U盘，就是如图所示的sdb设备了，mountpoint为空，因为还没有挂载哩。
sdb对应的路径因该是/dev/sdb喽（你可以用fdisk -l查看一下）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200627204713263.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**3.挂载**
```
mkdir /mnt/usb   #新建一个目录，用来挂载U盘
mount /dev/sdb /mnt/usb   #把U盘挂载到/mnt/usb
lsblk  #查看一下
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020062720514790.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
sdb的mountpoint不在为空，而是刚才的挂载点/mnt/usb
**恭喜！！！可以在/mnt/usb下浏览U盘内容了**

**4.umount**
用完后，先执行
```
umount /dev/sdb /mnt/usb #先卸载
lsblk #查看一下
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200627210056544.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**mountpoint又变为空了。but你用fdisk -l 查看（显示U盘还在），这时你需要关闭驱动器。**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200627210558399.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

**5.安全关闭驱动器**
```
udisksctl power-off -b /dev/sdb				#安全关闭驱动器
fdisk -l #查看
```
这下U盘没了（弹出了）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200627211332229.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
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
作者：DebugWuhen
原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013506161.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)