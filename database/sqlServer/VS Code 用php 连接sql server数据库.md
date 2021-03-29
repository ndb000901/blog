## php 连接sql server数据库

折腾了一天，终于把该死的数据库连起了，现在我就将我遇到的问题与配置的一些过程记录一下，希望有所帮助。

**1.环境**
>1.phpstudy
>
>2.VS Code
>
>3.php7.3.4nts
>
>**注意：**
>nts>>线程不安全
>
>ts>>线程安全

**2.下载与配置**

连接  sql server 需要下载点东西

>1下载[SQLSRV58.EXE](https://docs.microsoft.com/en-us/sql/connect/php/download-drivers-php-sql-server?view=sql-server-ver15)
>这玩意不需要安装，解压后就是这么一堆东西：
>
>![image](https://user-images.githubusercontent.com/48900845/112751937-1ebdf800-9003-11eb-8489-864fe97e3022.png)
>
>上述玩意要根据自己的环境选择，请接着看。
>

在自己的本地站下放一个php脚本看一哈信息。(用phpstudy搭个站)

```
<?php
echo phpinfo();
?>
```
>这是我的环境。
>
>![image](https://user-images.githubusercontent.com/48900845/112751957-30070480-9003-11eb-9f8e-ce552e45ade4.png)
>
>所以我的sqlsrv，就得选7.3，nts，x64
>
>**注意：选择自己相应版本，如果sqlsrv58里没有，就去下载别的版本sqlsrv。**
![image](https://user-images.githubusercontent.com/48900845/112751970-41e8a780-9003-11eb-9362-ba74d99c6f25.png)

>把这两个玩意拷贝到对应php版本文件夹下。
![image](https://user-images.githubusercontent.com/48900845/112751978-4745f200-9003-11eb-8113-4836f262154d.png)

>然后在php.ini添加以下
![image](https://user-images.githubusercontent.com/48900845/112751981-4c0aa600-9003-11eb-935c-c4003079cc46.png)


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
![image](https://user-images.githubusercontent.com/48900845/112752004-65135700-9003-11eb-9074-bec43960cf88.png)


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
