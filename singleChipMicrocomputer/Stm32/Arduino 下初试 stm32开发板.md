## Arduino 下初试 stm32开发板

**1.实验环境**

>1.野火STM32指南者(STM32F103VET6)
>
>2.Arduino IDE 1.8.13([下载链接](https://www.arduino.cc/en/software))
>
>3.STM32 Flash loader 2.8.0([下载链接](https://www.st.com/zh/development-tools/flasher-stm32.html))

![image](https://user-images.githubusercontent.com/48900845/112812076-48345d80-90af-11eb-8ee9-995dfa5eee01.png)

![image](https://user-images.githubusercontent.com/48900845/112812108-4ec2d500-90af-11eb-9398-9da7001f9328.png)


**2.配置环境**


 点击开发板管理器
 
![image](https://user-images.githubusercontent.com/48900845/112812147-58e4d380-90af-11eb-80c4-545c3e15d1df.png)

搜索SAM，安装。

![image](https://user-images.githubusercontent.com/48900845/112812177-613d0e80-90af-11eb-93d3-b2d111ad062a.png)

**下载并烧录bootloader**

clone 大佬的这两个项目

![image](https://user-images.githubusercontent.com/48900845/112812210-6ac67680-90af-11eb-9299-eea9533f53fd.png)


Arduino_STM32   [项目地址](https://github.com/rogerclarkmelbourne/Arduino_STM32)

STM32duino-bootloader   [项目地址](https://github.com/rogerclarkmelbourne/STM32duino-bootloader)

将下载的 Arduino_STM32 项目放到Arduino安装目录的hardware路径。

重启Arduino IDE，可以看到很多stm32的板子

![image](https://user-images.githubusercontent.com/48900845/112812242-7619a200-90af-11eb-9b4d-55dc73ce9096.png)

打开 STM32 Flash loader，将stm32 boot0 引脚接为高电平，插上串口线，
开始烧录STM32duino-bootloader项目里binaries下的bin文件。

俺这边烧的是pb0，因为野火指南者pb0接了个绿色的LED。

![image](https://user-images.githubusercontent.com/48900845/112812350-99445180-90af-11eb-9c7c-007bf65e71c5.png)

![image](https://user-images.githubusercontent.com/48900845/112812362-9ea19c00-90af-11eb-9e92-0a0bc04b75b0.png)

选择自己对应的串口，我这是COM14

![image](https://user-images.githubusercontent.com/48900845/112812391-a9f4c780-90af-11eb-89d1-5ec918ed9714.png)

一路下一步，选择自己要烧录的文件。

![image](https://user-images.githubusercontent.com/48900845/112812426-b5e08980-90af-11eb-849f-c2bd41884e63.png)

![image](https://user-images.githubusercontent.com/48900845/112812438-baa53d80-90af-11eb-9cff-81fb2a27b57e.png)

成功，然后在Arduino IDE编译测试源码，上传到板子。

**注意以下为本人实践经验（不一定大家都适用）：**  

>**1.上传程序时boot0 接高电平，boot1低电平。这时的程序好像是被搞到内存里了，断电或reset就没了。**
>
>**2.boot0 与boot1都接低电平，貌似无法上传程序。**
>
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

![image](https://user-images.githubusercontent.com/48900845/112812500-cc86e080-90af-11eb-808f-8279a215a716.png)

工具，串口监视器
![image](https://user-images.githubusercontent.com/48900845/112812532-d6a8df00-90af-11eb-907c-90ef468b3de3.png)

![image](https://user-images.githubusercontent.com/48900845/112812570-df011a00-90af-11eb-971f-b68934935ba5.png)

>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
