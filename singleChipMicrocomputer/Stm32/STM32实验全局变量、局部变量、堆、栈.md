## STM32实验全局变量、局部变量、堆、栈

**1.实验环境**
>1.野火STM32指南者(STM32F103VET6)
>2.keil5
>3.野火多功能调试助手.exe

**全局变量、静态局部变量保存在全局数据区，初始化的和未初始化的分别保存在一起。普通局部变量保存在堆栈中。
在C\C++中，通常可以把内存理解为4个分区：栈、堆、全局/静态存储区和常量存储区**


>1.内存栈区stack： 存放局部变量名；
2.内存堆区heap： 存放new或者malloc出来的对象；
3.Text & Data & Bss：代码段与静态分配
4.BSS区（未初始化数据段）：并不给该段的数据分配空间，仅仅是记录了数据所需空间的大小。
5.DATA（初始化的数据段）：为数据分配空间，数据保存在目标文件中。


**2.源码**

**使用串口的那个工程文件就好**

main.c
```
#include "stm32f10x.h"
#include "bsp_usart.h"

char global1[16];
char global2[16];
char global3[16];
	
int main(void)
{	
  char part1[16];
  char part2[16];
  char part3[16];

  USART_Config();

  printf("part1: 0x%p\n", part1);
  printf("part2: 0x%p\n", part2);
  printf("part3: 0x%p\n", part3);
	 
  printf("global1: 0x%p\n", global1);
  printf("global2: 0x%p\n", global2);
  printf("global3: 0x%p\n", global3);
  while(1)
	{	
		
	}	
}

```

**3.效果**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201206203014907.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
