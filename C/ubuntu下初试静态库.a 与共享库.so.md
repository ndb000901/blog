##  ubuntu下初试静态库.a 与共享库.so

**实验目的：** 欲将a1.c，a2.c生成静态库.a与共享库.so以供test.c使用。
**阅读技术基础：** 需有gcc、makefile的一些基础，以及熟悉linux基础操作。
****
**1.实验环境**
>1.ubuntu16.04([安装教程](https://blog.csdn.net/qq_43938052/article/details/107326122))
>2.gcc-5.4.0（**安装：apt install gcc** ）
>3.make-4.1（**安装：apt install make** ）

**2.测试源码**
****

a1.c
```
/*************************************************************************
    > File Name: a1.c
    > Author: wuhen
    > Created Time: Tue 13 Oct 2020 12:41:27 AM CST
 ************************************************************************/

#include<stdio.h>
void print1(int arg)
{
        printf("A1 print arg:%d\n",arg);
}

```
a2.c
```
/*************************************************************************
    > File Name: a2.c
    > Author: wuhen
    > Created Time: Tue 13 Oct 2020 12:43:22 AM CST
 ************************************************************************/

#include<stdio.h>
void print2(char *arg)
{
        printf("A2 print arg:%s\n",arg);
}

```
a.h

```
/*************************************************************************
    > File Name: a.h
    > Author: wuhen
    > Created Time: Tue 13 Oct 2020 12:55:06 AM CST
 ************************************************************************/

#ifndef A_H
#define A_H
void print1(int);
void print2(char*);
#endif

```

test.c
```
/*************************************************************************
    > File Name: test.c
    > Author: wuhen
    > Created Time: Tue 13 Oct 2020 02:11:53 AM CST
 ************************************************************************/

#include<stdio.h>
#include"a.h"
int main()
{
        print1(4);
        print2("hello,world!!!");
        return 0;

}

```
makefile
```
all:a1.o a2.o test.o
        gcc -o all a1.o a2.o test.o
a1.o:a1.c
        gcc -c a1.c
a2.o:a2.c
        gcc -c a2.c
test.o:test.c a.h
        gcc -c a.h test.c
static:
        ar crv lib.a a1.o a2.o
        gcc -o test1 test.c lib.a

createso:
        gcc -c -fpic *.c a.h
        gcc -shared a1.o a2.o -o lib.so
        gcc -o test2 test.c lib.so
        sudo cp lib.so /usr/lib/
clean:
        rm a1.o a2.o test.o

```

**3.验证**
执行命令，测试源码是否可以正常编译。
```
make
./all
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013103458911.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
执行命令，生成静态库lib.a，使用test.c测试静态库是否可以正常使用。
```
make static
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013103706896.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
执行命令，生成共享库lib.so，并使用test.c进行测试。
```
make createso
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020101310402569.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
**4.附录**
gcc帮助信息
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013105012463.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013105042594.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)

****
ar帮助信息
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013105250219.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013105309568.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)

>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
