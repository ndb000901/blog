##  linux gdb 调试c代码小例一则
**1.实验环境**
>1.ubuntu20
>
>2.gdb-9.2
>
>3.gcc-9.3.0

**2.代码**
main.c

```
/*************************************************************************
    > File Name: main.c
    > Author: wuhen
    > Created Time: Thu 29 Oct 2020 04:52:54 PM CST
 ************************************************************************/

#include<stdio.h>
int main()
{
	int a = 1;
	int b = 2;
	int c;
	int d;
	c = a + b;
	d = a + b + c;
	printf("a:%d\nb:%d\n",c,d);
	return 0;
}

```


**3.调试**

执行命令，编译
```
gcc -o main.out -g main.c
```

执行命令，开始调试
```
gdb main.out
```
![image](https://user-images.githubusercontent.com/48900845/112751626-8ffcab80-9001-11eb-9851-898404a6c41c.png)


```
start #开始调试
n #运行下一行

```
**关于命令详解大家看[这个](https://man.linuxde.net/gdb)就好**

**相关文章**

[python 初试 opencv](https://blog.csdn.net/qq_43938052/article/details/109489950)
[python 操作摄像头](https://blog.csdn.net/qq_43938052/article/details/109490302)

>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)

