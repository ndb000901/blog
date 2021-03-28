## VS code php 如何调试

今天来写一篇如何调试 ”拍黄片“ 的blog。
废话不说了，直接干。

**开发环境：**

>1.VS code
>
>2.phpstudy

**1.配置一哈VS code(为了开发体验好一点，需要装几个插件哦)**

>1.PHP Intelephense
>
>2.PHP Debug
![image](https://user-images.githubusercontent.com/48900845/112752092-ea970700-9003-11eb-9332-c0633ef9bd72.png)


**2.安装XDebug（phpstudy 貌似集成了这玩意）**
>1.在php.ini加入下面三行代码(路径填自己的)
>
>2.保存，
>
>3.重启apache服务。
```
xdebug.remote_enable = 1
xdebug.remote_autostart = 1
zend_extension="F:\PHPstudy\phpstudy_pro\Extensions\php\php7.3.4nts\ext\php_xdebug.dll"
```
![image](https://user-images.githubusercontent.com/48900845/112752117-0d292000-9004-11eb-9fa4-70f45f318932.png)


**3.配置launch.json信息**
端口用默认9000就好

![image](https://user-images.githubusercontent.com/48900845/112752127-174b1e80-9004-11eb-98cd-6ef621b3d033.png)

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
>
>2.添加断点
>
>3.开启调试
>
>4.刷新一下浏览器
>

![image](https://user-images.githubusercontent.com/48900845/112752142-2af68500-9004-11eb-9916-b6620ad72c7e.png)

看到下图，恭喜恭喜，成功喽@@@@

![image](https://user-images.githubusercontent.com/48900845/112752146-2fbb3900-9004-11eb-8996-ff4d034ea47b.png)


>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）

![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
