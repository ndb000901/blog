## Arduino 下初试 stm32开发板
**1.实验环境**
>1.野火STM32指南者(STM32F103VET6)
>2.Arduino IDE 1.8.13([下载链接](https://www.arduino.cc/en/software))
>3.STM32 Flash loader 2.8.0([下载链接](https://www.st.com/zh/development-tools/flasher-stm32.html))


![在这里插入图片描述](https://img-blog.csdnimg.cn/20201212215742843.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201212215758731.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)



**2.配置环境**


 点击开发板管理器
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201213005755358.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
搜索SAM，安装。![](https://img-blog.csdnimg.cn/20201213010506485.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

**下载并烧录bootloader**

clone 大佬的这两个项目
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201213011257609.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

Arduino_STM32   [项目地址](https://github.com/rogerclarkmelbourne/Arduino_STM32)
STM32duino-bootloader   [项目地址](https://github.com/rogerclarkmelbourne/STM32duino-bootloader)

将下载的 Arduino_STM32 项目放到Arduino安装目录的hardware路径。

重启Arduino IDE，可以看到很多stm32的板子
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201213012631138.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
打开 STM32 Flash loader，将stm32 boot0 引脚接为高电平，插上串口线，
开始烧录STM32duino-bootloader项目里binaries下的bin文件。

俺这边烧的是pb0，因为野火指南者pb0接了个绿色的LED。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201213013516949.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201213014018929.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
选择自己对应的串口，我这是COM14
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201213014233719.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
一路下一步，选择自己要烧录的文件。![在这里插入图片描述](https://img-blog.csdnimg.cn/20201213015843409.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020121302034360.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
成功，然后在Arduino IDE编译测试源码，上传到板子。

**注意以下为本人实践经验（不一定大家都适用）：**  
>**1.上传程序时boot0 接高电平，boot1低电平。这时的程序好像是被搞到内存里了，断电或reset就没了。**
>**2.boot0 与boot1都接低电平，貌似无法上传程序。**
>**3.想让程序断电后都在板子上，可以这样操作。boot0接高电平，boot1接低电平，点击上传，程序上传成功，这是将boot0接到低电平，然后断电，这是供电后，程序就会一直在了，不晓得啥子原因。**

**3.测试源码**

**源码功能：** 绿灯闪，不断向串口发“cao,hello!!!!”，直到PC向stm32发送“stop”指令。

```
void setup() {
  // put your setup code here, to run once:
  pinMode(PB0, OUTPUT);
  Serial.begin(115200); //设置波特率
}
void stop()//终止函数
{
  while (1)
  {

  }
}
char incomingByte = 0;
void loop() {
  // 点灯
  digitalWrite(PB0, HIGH);//PB0引脚，高电平
  delay(1000);//延时
  digitalWrite(PB0, LOW);//PB0引脚，低电平
  delay(1000);
  Serial.println("cao,hello!!!!");//这串字符打到串口
  delay(1000);
  String str = "";

  //接受PC机发送给stm32的数据
  while (1)
  {

    if (Serial.available() > 0) {
      // read the incoming byte:
      incomingByte = Serial.read();
      // say what you got:
      Serial.print("I received: ");
      Serial.println(incomingByte, DEC);
      str += incomingByte;
    }
    else
    {
      break;
    }
  }

  //判断是否是结束标志,使用Arduino IDE 工具自带的串口调试工具，每当给stm32发送字符串时，都会在末尾加上ascII码（值为10）
  if (str != "")
  {
    if (str.length() == 5)
    {
      if (str[0] == 's' && str[1] == 't' && str[2] == 'o' && str[3] == 'p')
      {
        Serial.println("Stop!!!!");
        stop();
      }
    }
  }






}
```

**4.效果图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201213021421821.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
工具，串口监视器
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201213021451248.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201213021541566.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)