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

****

## 从u盘系统操作本机manjaro系统

执行以下命令
```
manjaro-chroot -a
```

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
## 安装RTX2060驱动

执行命令

```
mhwd-tui
```

![image](https://user-images.githubusercontent.com/48900845/113739426-5c70fe00-9732-11eb-8c6e-c97389430e0f.png)

选择4安装

安装成功后，可重启进入bios,将Graphic Device 设置为Discrete Graphics，然后执行以下命令验证

```
nvidia-smi
```

![image](https://user-images.githubusercontent.com/48900845/113739657-93dfaa80-9732-11eb-8fbb-c69cf707ae7f.png)


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

## 美化

主题 壁纸 图标 --> [官网](https://www.gnome-look.org/browse/cat/)

各种拓展 --> [官网](https://extensions.gnome.org/)


## privoxy (http https 转 socks5)

安装

```
sudo pacman -S privoxy
```

配置/etc/privoxy/config

```
listen-address  0.0.0.0:1081          # 监听http https端口
forward-socks5  /  127.0.0.1:1080  .  # socks5 端口
```

启动/停止/重启

```
systemctl start privoxy
systemctl stop privoxy
systemctl restart privoxy
```

## proxychains配置

安装

```
sudo pacman -S proxychains
```

配置/etc/proxychains.conf

```
Examples:

socks5	192.168.67.78	1080	lamer	secret
http	192.168.89.3	8080	justu	hidden
socks4	192.168.1.49	1080
http	192.168.39.93	8080
```

## oh-my-zsh

安装

```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

语法高亮 zsh-syntax-highlighting 

命令补全插件 zsh-autosuggestions

```
cd ~/.oh-my-zsh/custom/plugins/
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
git clone https://github.com/zsh-users/zsh-autosuggestions
```

修改配置文件

```
vim ~/.zshrc
plugins=(
	git
	zsh-autosuggestions
	zsh-syntax-highlighting
)
```

## powerlevel10k

安装

```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

Oh My Zsh

```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

修改配置

```
vim ~/.zshrc

ZSH_THEME="powerlevel10k/powerlevel10k“
```

刷新

```
source ~/.zshrc
```
根据提示开始配置
