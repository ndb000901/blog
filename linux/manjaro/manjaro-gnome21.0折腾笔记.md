#  manjaro21.0-gnome折腾笔记

## 机器环境

>1.Lenovo 拯救者 Y9000K
>
>2.**CPU：** intel i7-10875H
>
>3.**显卡：** RTX 2060
>
>4.**硬盘：** 西数SN550 1T + 三星pm981a 1T

## 制作启动盘

工具 [Rufus](https://rufus.ie/downloads/)

## 系统安装

如果有新版bios，请先升级下bios。

开机后看到Lenovo logo后按F2可进入bios，按F12可进入启动项选择。

在bios中将硬盘模式设置为ACHI，否则安装时找不到NVME硬盘。

如果从U盘启动时无法进入安装界面或黑屏，在bios中将Graphic Device 设置为Dynamic Graphics，或者在u盘启动时第一个启动项出按e，然后将driver=free改成driver=intel,按F10保存继续。

# 系统配置

## 配置软件源

```
sudo pacman-mirrors -i -c China -m rank
```

## 更新软件源

```
sudo pacman -Syy
```

## 更新系统

```
sudo pacman -Syyu
```


## 中文输入法

安装
```
sudo pacman -S fcitx-im
sudo pacman -S fcitx-contigtool
sudo pacman -S fcitx-googlepinyin
```

添加配置 ～/.xprofile
```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

**重启或注销**
