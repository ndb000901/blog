## 处理Ubuntu python多版本管理问题

前几天在Ubuntu遇到了Python多版本问题，今天心血来潮，想把自己摸索到的方法记录下来。

```
系统安装的Python版本
python2.7
python3.6
python3.7
```

```
系统pip版本
pip
pip2
pip3
```
当我用python3.7开发程序时，需要用pip3安装依赖包，pip3总是把包给我搞到python3.6下，让我很不爽。
下面介绍一种解决方法：

1.找到python,pip所在目录。

```
我的系统在/usr/bin/路径下。
命令 cd /usr/bin
查看一下 ls -l
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020032323410832.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323234459547.png)
冒绿光的是可以执行滴文件
冒蓝光的是链接文件(您可以理解为类似Windows的快捷方式)

要想更改pip3 install的安装位置，可以这么操作。

```
编辑pip3(这玩意就是个Python脚本)
vim pip3
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323234817578.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
将第一行的python版本修改你想要的版本，然后保存，问题就解决喽。



另一个问题就是你在shell命令使用Python时，Python版本问题。

比如你的系统安装了Python2.7，Python3.6，Python3.7

这时你在命令窗口
输入python2 ----->使用Python2.7版本
输入python3 ----->使用Python3.6版本
如何使用Python3.7呢

```
cd /usr/bin
找到python3.7目录（就是找到前面说的冒绿光的python3.7目录）
添加软链接
ln -s /usr/bin/python3.7(找到python3.7的路径) /usr/bin/python3.7 (软链接名字您老随意)
```
为啥软连接的路径在/usr/bin下呢

```
$PATH
```
这些目录应该都可以，你可以试试。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324000643781.png)
 >作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013253951.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)