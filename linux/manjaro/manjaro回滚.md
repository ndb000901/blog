# manjaro回滚

**环境**

>联想Y9000K2020H
>RTX2060

**今天的一波更新，我的系统挂比了。屏幕亮度无法调节，显卡驱动问题**


**安装downgrade**

```
sudo pacman -S downgrade
```

**回滚软件**

```
sudo downgrade 包名
```

**需降级的软件**

```
linux510-nvidia-460.80-1
lib32-nvidia-utils-460.80-1
nvidia-utils-460.80-1
mhwd-nvidia-460.80-1
```

**[下载RTX2060驱动](https://cn.download.nvidia.cn/XFree86/aarch64/460.84/NVIDIA-Linux-aarch64-460.84.run)**

```
sudo ./NVIDIA-Linux-x86_64-460.84.run
```



## dash版本

![image](https://user-images.githubusercontent.com/48900845/131479994-c4572551-64b9-4307-96ea-2138be4b1384.png)

![image](https://user-images.githubusercontent.com/48900845/131480255-95cef22e-ebdc-4396-bb63-883b00836dcb.png)
