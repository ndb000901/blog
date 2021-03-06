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


## 从u盘系统操作本机manjaro系统

执行以下命令
```
manjaro-chroot -a
```
****

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


## ssh 工具 electerm

```
$ wget https://github.com/electerm/electerm/releases/download/v1.3.54/electerm-1.3.54-linux-x64.tar.gz
$ sudo tar -zxvf electerm-1.3.54-linux-x64.tar.gz -C /opt
# 保存上面的图标到 /opt/electerm-1.3.54-linux-x64/ 目录为 icon.png
# 编写启动脚本
$ sudo vim /usr/share/applications/electerm.desktop
[Desktop Entry]
Name=electerm
Exec=electerm
Terminal=false
Type=Application
Icon=/opt/electerm-1.3.54-linux-x64/icon.png
Exec=/opt/electerm-1.3.54-linux-x64/electerm
StartupWMClass=plasmashell
Comment=Terminal/ssh/sftp client(linux, mac, win) based on electron/ssh2/node-pty/xterm/antd/subx and other libs
Categories=Development;System;TerminalEmulator;

```

## IDEA插件

```
# 阿里代码规范
Alibaba Java Coding Guidelines
# 右侧预览，方便快速定位，Ctrl+Shift+G 快速打开关闭
CodeGlance
# mybatis 代码到 xml 跳转
Free Mybatis plugin
# 分析依赖冲突插件
Maven Helper
# 括号开始结尾，高亮显示
HighlightBracketPair
# 多彩括号，区域代码高亮
Rainbow Brackets
# 翻译
Translation
# 字符串各种显示格式转换
String Manipulation
CamelCase
# git 显示插件，可以在每行显示修改人和修改时间
GitToolBox
# 热加载修改的代码而无需重启项目，使用参考下方链接
JRebel and XRebel for IntelliJ

```

## WPS

## Etcher 

启动盘制作工具

## Cisco Packet Tracer

```
# 下载地址
https://www.computernetworkingnotes.com/ccna-study-guide/download-packet-tracer-for-windows-and-linux.html
# clone 
git clone https://aur.archlinux.org/packettracer.git
# 进入clone项目的目录，若已经安装java-runtime，可修改PKGBUILD文件depends删除java-runtime

# 执行命令
makepkg -sic 

```
