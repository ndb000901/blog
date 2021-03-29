## stm32 i2c初试 OLED

**1.实验环境**

>1.野火STM32指南者(STM32F103VET6)
>
>2.AHT20传感器
>
>3.OLED屏幕0.96寸（[地址](http://www.lcdwiki.com/zh/0.96inch_SPI_OLED_Module)）

**并非广告只是说明使用哪家产品**

**2.环境搭建**

下载相应资料（[下载地址](http://www.lcdwiki.com/zh/0.96inch_SPI_OLED_Module)）

![image](https://user-images.githubusercontent.com/48900845/112811450-aad92980-90ae-11eb-8bc9-b00581504f20.png)

打开相应工程

![image](https://user-images.githubusercontent.com/48900845/112811484-b4629180-90ae-11eb-8478-7e69c1cad47c.png)

除了 main.c 、 oled.c 、 oled.h 、 bmp.h 、 oledfont.h ，其他都是和平台相关的代码。

oledfont.h 、 bmp.h 都存放图片和汉字取模后的点阵数组。

oled.h 存放的是和 OLED 屏相关的一些参数，包括引脚定义。

oled.c 存放的是和 OLED 屏操作相关的一些函数，包括 IIC 的读写， OLED 屏数据写入等

main.c 则是主程序操作了。

一些函数介绍

```
//显示汉字，x,y,为坐标，no为字体大小。
void OLED_ShowCHinese(u8 x,u8 y,u8 no);

//显示一个字符，x,y,为坐标，Char_Size为字体大小，chr为要显示的字符。
void OLED_ShowChar(u8 x,u8 y,u8 chr,u8 Char_Size);

//对OLED_ShowChar的二次封装，显示一个字符串，x,y,为坐标，Char_Size为字体大小，chr为要显示的字符串。
void OLED_ShowString(u8 x,u8 y,u8 *chr,u8 Char_Size);

//显示一个数字，x,y,为坐标，size2为字体大小，len为长度，num为数字
void OLED_ShowNum(u8 x,u8 y,u32 num,u8 len,u8 size2)
```

**3.显示字符**

获取想要显示的字模，设置如下;

![image](https://user-images.githubusercontent.com/48900845/112811543-c47a7100-90ae-11eb-966c-46515489bec3.png)

将生成的数据文件添加至oledfont.h相应的数组中

![image](https://user-images.githubusercontent.com/48900845/112811578-cba17f00-90ae-11eb-8625-ef0afef5c735.png)

烧录程序。

**接线**

![image](https://user-images.githubusercontent.com/48900845/112811639-da883180-90ae-11eb-9b73-11e15d7f5d04.png)

效果图

![image](https://user-images.githubusercontent.com/48900845/112811668-e07e1280-90ae-11eb-91b5-74c42f0f10df.png)


**4.显示传感器温度**

**5.滚屏**

在main.c中添加
```
	  OLED_WR_Byte(0x2e,OLED_CMD);;//关滚动
	  OLED_WR_Byte(0x2A,OLED_CMD);//29向右，2a向左
	  OLED_WR_Byte(0x00,OLED_CMD);//A:空字节
	  OLED_WR_Byte(0x00,OLED_CMD);//B:水平起始页
	  OLED_WR_Byte(0x00,OLED_CMD);//C:水平滚动速度
	  OLED_WR_Byte(0x07,OLED_CMD);//D:水平结束页
	  OLED_WR_Byte(0x01,OLED_CMD);//E:每次垂直滚动位移
	  OLED_WR_Byte(0x2f,OLED_CMD);//开滚动  
```
在oled.c中添加
```
void roll(void)
{
        OLED_WR_Byte(0x2e,OLED_CMD);       
        OLED_WR_Byte(0x29,OLED_CMD);       
        OLED_WR_Byte(0x00,OLED_CMD);       
        OLED_WR_Byte(0x00,OLED_CMD);        
        OLED_WR_Byte(0x07,OLED_CMD);        
        OLED_WR_Byte(0x07,OLED_CMD);        
        OLED_WR_Byte(0x01,OLED_CMD);       
        OLED_WR_Byte(0x2F,OLED_CMD); 
}      
```

>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
