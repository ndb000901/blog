## linux初试gcc makefile菜鸟教程
----
**1.实验环境**
>1.ubuntu16([安装教程](https://blog.csdn.net/qq_43938052/article/details/107326122))
>2.gcc
>(gcc安装：apt install gcc)
>3.make
>(make安装 apt install make)

用C举个小例子

**2.源码**

main.c
~~~
/*************************************************************************
    > File Name: main.c
    > Author: wuhen
    > Mail: wuhen1090@qq.com
    > Created Time: Fri 25 Sep 2020 09:52:19 PM CST
 ************************************************************************/

#include<stdio.h>
int sub(int a,int b);
int main()
{
        int a;
        int b;
        float c;
        printf("请敲个数 a=");
        scanf("%d",&a);
        printf("请敲个数 b=");
        scanf("%d",&b);
        c = sub(a,b);
        printf("c=%.1f\n",c);
        return 0;
}

~~~
sub.c
~~~

/*************************************************************************
    > File Name: sub.c
    > Author: wuhen
    > Mail: wuhen1090@qq.com
    > Created Time: Fri 25 Sep 2020 09:48:26 PM CST
 ************************************************************************/
float sub(int a,int b)
{
        return a + b;
}
~~~
**编译一下**
```
gcc -o out main.c sub.c
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200925224619757.png#pic_center)
**Nice，成功了**

**3.makefile**
当做一个大些的工程时，使用刚才的方式就有些恼火，so，我们可以用神器——make来解决它。

makefile
```
all:main.o sub.o
        gcc -o all main.o sub.o
main.o:main.c
        gcc -c main.c
sub.o:sub.c
        gcc -c sub.c
clean:
        rm main.o sub.o

```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200925225213815.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
OK，今天的文章就肝到这里。
>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


