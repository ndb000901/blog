#  manjaro21.0-gnome折腾笔记

## 机器环境

>1.Lenovo 拯救者 Y9000K
>
>2.RTX 2060
>

## 制作启动盘

工具 [Rufus](https://rufus.ie/downloads/)

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
