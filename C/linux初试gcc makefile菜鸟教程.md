## linux初试gcc makefile菜鸟教程
----
**1.实验环境**
>1.ubuntu16([安装教程](https://blog.csdn.net/qq_43938052/article/details/107326122))
>
>2.gcc
>(gcc安装：apt install gcc)
>
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
![image](https://user-images.githubusercontent.com/48900845/112751751-24ffa480-9002-11eb-80a8-ae4262aeceaf.png)

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

![image](https://user-images.githubusercontent.com/48900845/112751762-2f21a300-9002-11eb-8160-4aa943226a6e.png)

OK，今天的文章就肝到这里。

>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)



