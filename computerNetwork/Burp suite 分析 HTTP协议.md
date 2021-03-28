## Burp suite 分析 HTTP协议

**1.实验环境**
>1.manjaro-gnome-20.1.2
>
>2.Burp suite-Community-v2020.11.1([下载地址](https://portswigger.net/burp/communitydownload))

**2.Burp suite安装与配置**


打开Firefox，安装下图插件。

![image](https://user-images.githubusercontent.com/48900845/112759866-82f2b300-9027-11eb-9109-22406fbc436e.png)

配置代理，端口号可自行选择(选择空闲的就可)。

![image](https://user-images.githubusercontent.com/48900845/112759873-8a19c100-9027-11eb-8f61-d61f5a0778b5.png)

配置Burp suite，端口要与前面的配置一致。

![image](https://user-images.githubusercontent.com/48900845/112759882-9140cf00-9027-11eb-8472-c7fef4263608.png)

访问http://burp/下载burpsuite ca证书

**需开启刚刚配置的代理**

![image](https://user-images.githubusercontent.com/48900845/112759892-9e5dbe00-9027-11eb-8a0f-c379cd70e536.png)

点击右上角CA Certificate

![image](https://user-images.githubusercontent.com/48900845/112759900-a9185300-9027-11eb-84f7-d4e9cccddb1f.png)

点击首选项>>隐私与安全>>查看证书

![image](https://user-images.githubusercontent.com/48900845/112759905-b03f6100-9027-11eb-9bac-3b4bb02cafeb.png)

导入刚刚下载的证书

![image](https://user-images.githubusercontent.com/48900845/112759913-b7666f00-9027-11eb-8be9-83c3d153a4e2.png)

![image](https://user-images.githubusercontent.com/48900845/112759926-bf261380-9027-11eb-8e86-9d97e53a5bc2.png)


**3.分析HTTP**

开启拦截，在Firefox输入https://www.baidu.com

![image](https://user-images.githubusercontent.com/48900845/112759937-ce0cc600-9027-11eb-9473-226d66de8df3.png)

![image](https://user-images.githubusercontent.com/48900845/112759941-d238e380-9027-11eb-921d-f72ea0a2dbc1.png)


至此，你就可以拦截请求与响应开始装逼了(请参照附录分析)。

**HTTP状态码**

所有HTTP响应的第一行都是状态行，依次是当前HTTP版本号，3位数字组成的状态代码，以及描述状态的短语，彼此由空格分隔。
状态代码的第一个数字代表当前响应的类型：

>1xx消息——请求已被服务器接收，继续处理
>
>2xx成功——请求已成功被服务器接收、理解、并接受
>
>3xx重定向——需要后续操作才能完成这一请求
>
>4xx请求错误——请求含有词法错误或者无法被执行
>
>5xx服务器错误——服务器在处理某个正确请求时发生错误

**HTTP请求方法**

请读者自行学习GET与POST(重点哦)

>GET
>
>POST
>
>HEAD
>
>PUT
>
>DELETE
>
>TRACE
>
>OPTIONS
>
>CONNECT

****
## 附录
****


**请求字段**

![image](https://user-images.githubusercontent.com/48900845/112759982-fa284700-9027-11eb-8e78-6f9da87f48b3.png)

![image](https://user-images.githubusercontent.com/48900845/112759985-fe546480-9027-11eb-8d9b-3c7f7c17250c.png)

![image](https://user-images.githubusercontent.com/48900845/112760006-0dd3ad80-9028-11eb-946f-9ce5f27cda59.png)

![image](https://user-images.githubusercontent.com/48900845/112759992-044a4580-9028-11eb-80b1-28aad9ba0f86.png)



**响应字段**

![image](https://user-images.githubusercontent.com/48900845/112760052-35c31100-9028-11eb-9cd9-c44dcad3b507.png)

![image](https://user-images.githubusercontent.com/48900845/112760057-3b205b80-9028-11eb-8ba3-0921f90df43c.png)

![image](https://user-images.githubusercontent.com/48900845/112760067-407da600-9028-11eb-9702-6c8f964dd914.png)

![image](https://user-images.githubusercontent.com/48900845/112760071-46738700-9028-11eb-9dad-a223d2f45c3d.png)




>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
