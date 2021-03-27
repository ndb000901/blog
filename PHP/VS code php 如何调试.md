## VS code php 如何调试
今天来写一篇如何调试 ”拍黄片“ 的blog。
废话不说了，直接干。

**开发环境：**

>1.VS code
>2.phpstudy

**1.配置一哈VS code(为了开发体验好一点，需要装几个插件哦)**
>1.PHP Intelephense
>2.PHP Debug
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200427002901750.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

**2.安装XDebug（phpstudy 貌似集成了这玩意）**
>1.在php.ini加入下面三行代码(路径填自己的)
>2.保存，
>3.重启apache服务。
```
xdebug.remote_enable = 1
xdebug.remote_autostart = 1
zend_extension="F:\PHPstudy\phpstudy_pro\Extensions\php\php7.3.4nts\ext\php_xdebug.dll"
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200427003343966.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**3.配置launch.json信息**
端口用默认9000就好
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200427003811803.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
**4.用个小例子试试。**
```
<?php
    $a = 1;
    $b = 2;
    $c = $a + $b;
    echo $c;
?>
```
>1...
>2.添加断点
>3.开启调试
>4.刷新一下浏览器
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200427004251542.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
看到下图，恭喜恭喜，成功喽@@@@
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200427004606679.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070601341824.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)