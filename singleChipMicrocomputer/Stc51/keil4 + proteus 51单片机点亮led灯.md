## keil + protues 51单片机点亮led灯

实验环境：keil4 + proteus 8

proteus操作：

1.新建工程，名字随意。

![image](https://user-images.githubusercontent.com/48900845/112809907-1f12cd80-90ad-11eb-9034-b125942f03d4.png)

![image](https://user-images.githubusercontent.com/48900845/112809940-24701800-90ad-11eb-96cc-351a5112459e.png)

![image](https://user-images.githubusercontent.com/48900845/112809962-29cd6280-90ad-11eb-82e1-654e46b36c53.png)

![image](https://user-images.githubusercontent.com/48900845/112809978-2e921680-90ad-11eb-82de-49198a2c2062.png)

![image](https://user-images.githubusercontent.com/48900845/112809997-3356ca80-90ad-11eb-9b0c-39a0e67eecc2.png)


工程已经搞好。

![image](https://user-images.githubusercontent.com/48900845/112810046-3ea9f600-90ad-11eb-811f-8508005f4865.png)


2.搞个芯片进来，爽一波。

![image](https://user-images.githubusercontent.com/48900845/112810080-479ac780-90ad-11eb-8a35-f14217d56051.png)


添加51芯片

![image](https://user-images.githubusercontent.com/48900845/112810127-51242f80-90ad-11eb-938b-4938f5bcab7d.png)


搞个yellow快乐一哈

![image](https://user-images.githubusercontent.com/48900845/112810167-597c6a80-90ad-11eb-9963-b21b0aba235a.png)

3.元件已到位，搞起。

![image](https://user-images.githubusercontent.com/48900845/112810246-68fbb380-90ad-11eb-965d-580fb933527a.png)


把元件搞到右边的板子。然后加个电源。

![image](https://user-images.githubusercontent.com/48900845/112810309-7749cf80-90ad-11eb-93f7-3f627277c3a2.png)

![image](https://user-images.githubusercontent.com/48900845/112810338-7fa20a80-90ad-11eb-9828-9b2d499a5633.png)

连线

![image](https://user-images.githubusercontent.com/48900845/112810375-87fa4580-90ad-11eb-96a6-95e234e596b6.png)


## OK，可以搞代码喽。

在这我也做个keil新建工程的教程吧。

![image](https://user-images.githubusercontent.com/48900845/112810418-947e9e00-90ad-11eb-8ffc-252de003a381.png)

选好路径后，选择CPU，这里我们选择Atmel

![image](https://user-images.githubusercontent.com/48900845/112810442-9b0d1580-90ad-11eb-9acd-7b5f6cf264ac.png)

选择AT89C51

![image](https://user-images.githubusercontent.com/48900845/112810471-a3fde700-90ad-11eb-93c2-8738fb0368b9.png)

选择否

![image](https://user-images.githubusercontent.com/48900845/112810501-abbd8b80-90ad-11eb-807d-acaeb655228a.png)

新建文件，命名随意（我命名main.c）

![image](https://user-images.githubusercontent.com/48900845/112810549-b6782080-90ad-11eb-9c4b-669a0b9a7719.png)

![image](https://user-images.githubusercontent.com/48900845/112810566-bb3cd480-90ad-11eb-84ea-41cb3ce17102.png)


添加文件

![image](https://user-images.githubusercontent.com/48900845/112810606-c6900000-90ad-11eb-9fd4-ca69235c70d1.png)

![image](https://user-images.githubusercontent.com/48900845/112810636-cee83b00-90ad-11eb-8664-25a6085d9d5e.png)

![image](https://user-images.githubusercontent.com/48900845/112810659-d4de1c00-90ad-11eb-9d76-17f99ed71d59.png)


勾选，否则没有hex文件。

![image](https://user-images.githubusercontent.com/48900845/112810711-e45d6500-90ad-11eb-9d6f-6df83faebdc0.png)

写好代码，Build工程

![image](https://user-images.githubusercontent.com/48900845/112810730-ec1d0980-90ad-11eb-89d9-7a58fdfa653c.png)


keil操作：

代码
```
#include<reg52.h>
sbit led = P0 ^ 0;
void main()
{
	led = 0;
	while(1)
	{		 
	}

}
```
Build 工程后，在proteus右键芯片，编辑属性

![image](https://user-images.githubusercontent.com/48900845/112810791-fc34e900-90ad-11eb-87bb-f9af8cdff5b3.png)

将keil生成的hex文件导入

![image](https://user-images.githubusercontent.com/48900845/112810863-0d7df580-90ae-11eb-9d87-da29dc4eb1cc.png)

![image](https://user-images.githubusercontent.com/48900845/112810884-140c6d00-90ae-11eb-9c55-656d8f874299.png)

点击，开始仿真。

![image](https://user-images.githubusercontent.com/48900845/112810923-1cfd3e80-90ae-11eb-9750-43c58c7f138e.png)

![image](https://user-images.githubusercontent.com/48900845/112810945-21c1f280-90ae-11eb-86c2-97e041464718.png)

>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
