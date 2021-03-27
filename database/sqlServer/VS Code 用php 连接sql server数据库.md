## php 连接sql server数据库
折腾了一天，终于把该死的数据库连起了，现在我就将我遇到的问题与配置的一些过程记录一下，希望有所帮助。
**1.环境**
>1.phpstudy
>2.VS Code
>3.php7.3.4nts
>**注意：**
>nts>>线程不安全
>ts>>线程安全

**2.下载与配置**
连接  sql server 需要下载点东西
>1下载[SQLSRV58.EXE](https://docs.microsoft.com/en-us/sql/connect/php/download-drivers-php-sql-server?view=sql-server-ver15)
>这玩意不需要安装，解压后就是这么一堆东西：
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509174542978.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
>上述玩意要根据自己的环境选择，请接着看。
>
在自己的本地站下放一个php脚本看一哈信息。(用phpstudy搭个站)
```
<?php
echo phpinfo();
?>
```
>这是我的环境。
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509175407376.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
>所以我的sqlsrv，就得选7.3，nts，x64
>**注意：选择自己相应版本，如果sqlsrv58里没有，就去下载别的版本sqlsrv。**
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509175634355.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
>把这两个玩意拷贝到对应php版本文件夹下。
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509175820547.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
>然后在php.ini添加以下
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509180110889.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

```
extension=php_sqlsrv_73_nts_x64
extension=php_pdo_sqlsrv_73_nts_x64

```
**3.连接测试**
>1.重启apache

```
<?php  
$serverName = "."; //数据库服务器地址
$uid = "sa";     //数据库用户名
$pwd = "123456"; //数据库密码
$connectionInfo = array("UID"=>$uid, "PWD"=>$pwd, "Database"=>"phpTest");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if( $conn == false)
{
    echo "连接失败！";
    var_dump(sqlsrv_errors());
    exit;
}
else
{
    echo "链接成功";
}
?>
```
>OK，成功了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509180747467.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）