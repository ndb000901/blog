## stm32 AHT20温度采集
**1.实验环境**

>1.野火STM32指南者(STM32F103VET6)
>2.AHT20传感器


**2.源码**
**main.c**
```
#include "delay.h"
#include "usart.h"
#include "bsp_i2c.h"


int main(void)
{	
	delay_init();     //ÑÓÊ±º¯Êý³õÊ¼»¯	  
	uart_init(115200);	 //´®¿Ú³õÊ¼»¯Îª115200
	IIC_Init();
		while(1)
	{
		printf("¿ªÊ¼²âÁ¿£¬ÇëÉÔµÈ£º");
		read_AHT20_once();
		delay_ms(1500);
  }
}

```

**usart.c**
```
#include "sys.h"
#include "usart.h"


//STM32F103ºËÐÄ°åÀý³Ì
//¿âº¯Êý°æ±¾Àý³Ì
/********** mcudev.taobao.com ³öÆ·  ********/


// 	 
//Èç¹ûÊ¹ÓÃucos,Ôò°üÀ¨ÏÂÃæµÄÍ·ÎÄ¼þ¼´¿É.
#if SYSTEM_SUPPORT_UCOS
#include "includes.h"					//ucos Ê¹ÓÃ	  
#endif
//	 
//STM32¿ª·¢°å
//´®¿Ú1³õÊ¼»¯		   

// 	  
 

//
//¼ÓÈëÒÔÏÂ´úÂë,Ö§³Öprintfº¯Êý,¶ø²»ÐèÒªÑ¡Ôñuse MicroLIB	  
#if 1
#pragma import(__use_no_semihosting)             
//±ê×¼¿âÐèÒªµÄÖ§³Öº¯Êý                 
struct __FILE 
{ 
	int handle; 

}; 

FILE __stdout;       
//¶¨Òå_sys_exit()ÒÔ±ÜÃâÊ¹ÓÃ°ëÖ÷»úÄ£Ê½    
void _sys_exit(int x) 
{ 
	x = x; 
} 
//ÖØ¶¨Òåfputcº¯Êý 
int fputc(int ch, FILE *f)
{      
	while((USART1->SR&0X40)==0);//Ñ­»··¢ËÍ,Ö±µ½·¢ËÍÍê±Ï   
    USART1->DR = (u8) ch;      
	return ch;
}
#endif 

/*Ê¹ÓÃmicroLibµÄ·½·¨*/
 /* 
int fputc(int ch, FILE *f)
{
	USART_SendData(USART1, (uint8_t) ch);

	while (USART_GetFlagStatus(USART1, USART_FLAG_TC) == RESET) {}	
   
    return ch;
}
int GetKey (void)  { 

    while (!(USART1->SR & USART_FLAG_RXNE));

    return ((int)(USART1->DR & 0x1FF));
}
*/
 
#if EN_USART1_RX   //Èç¹ûÊ¹ÄÜÁË½ÓÊÕ
//´®¿Ú1ÖÐ¶Ï·þÎñ³ÌÐò
//×¢Òâ,¶ÁÈ¡USARTx->SRÄÜ±ÜÃâÄªÃûÆäÃîµÄ´íÎó   	
u8 USART_RX_BUF[USART_REC_LEN];     //½ÓÊÕ»º³å,×î´óUSART_REC_LEN¸ö×Ö½Ú.
//½ÓÊÕ×´Ì¬
//bit15£¬	½ÓÊÕÍê³É±êÖ¾
//bit14£¬	½ÓÊÕµ½0x0d
//bit13~0£¬	½ÓÊÕµ½µÄÓÐÐ§×Ö½ÚÊýÄ¿
u16 USART_RX_STA=0;       //½ÓÊÕ×´Ì¬±ê¼Ç	  
  
void uart_init(u32 bound){
    //GPIO¶Ë¿ÚÉèÖÃ
  GPIO_InitTypeDef GPIO_InitStructure;
	USART_InitTypeDef USART_InitStructure;
	NVIC_InitTypeDef NVIC_InitStructure;
	 
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_USART1|RCC_APB2Periph_GPIOA, ENABLE);	//Ê¹ÄÜUSART1£¬GPIOAÊ±ÖÓ
     //USART1_TX   PA.9
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_9; //PA.9
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_AF_PP;	//¸´ÓÃÍÆÍìÊä³ö
    GPIO_Init(GPIOA, &GPIO_InitStructure);
   
    //USART1_RX	  PA.10
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_10;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IN_FLOATING;//¸¡¿ÕÊäÈë
    GPIO_Init(GPIOA, &GPIO_InitStructure);  

   //Usart1 NVIC ÅäÖÃ

    NVIC_InitStructure.NVIC_IRQChannel = USART1_IRQn;
	NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority=3 ;//ÇÀÕ¼ÓÅÏÈ¼¶3
	NVIC_InitStructure.NVIC_IRQChannelSubPriority = 3;		//×ÓÓÅÏÈ¼¶3
	NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;			//IRQÍ¨µÀÊ¹ÄÜ
	NVIC_Init(&NVIC_InitStructure);	//¸ù¾ÝÖ¸¶¨µÄ²ÎÊý³õÊ¼»¯VIC¼Ä´æÆ÷
  
   //USART ³õÊ¼»¯ÉèÖÃ

	USART_InitStructure.USART_BaudRate = bound;//Ò»°ãÉèÖÃÎª9600;
	USART_InitStructure.USART_WordLength = USART_WordLength_8b;//×Ö³¤Îª8Î»Êý¾Ý¸ñÊ½
	USART_InitStructure.USART_StopBits = USART_StopBits_1;//Ò»¸öÍ£Ö¹Î»
	USART_InitStructure.USART_Parity = USART_Parity_No;//ÎÞÆæÅ¼Ð£ÑéÎ»
	USART_InitStructure.USART_HardwareFlowControl = USART_HardwareFlowControl_None;//ÎÞÓ²¼þÊý¾ÝÁ÷¿ØÖÆ
	USART_InitStructure.USART_Mode = USART_Mode_Rx | USART_Mode_Tx;	//ÊÕ·¢Ä£Ê½

    USART_Init(USART1, &USART_InitStructure); //³õÊ¼»¯´®¿Ú
    USART_ITConfig(USART1, USART_IT_RXNE, ENABLE);//¿ªÆôÖÐ¶Ï
    USART_Cmd(USART1, ENABLE);                    //Ê¹ÄÜ´®¿Ú 

}



void USART1_IRQHandler(void)                	//´®¿Ú1ÖÐ¶Ï·þÎñ³ÌÐò
	{
	u8 Res;
#ifdef OS_TICKS_PER_SEC	 	//Èç¹ûÊ±ÖÓ½ÚÅÄÊý¶¨ÒåÁË,ËµÃ÷ÒªÊ¹ÓÃucosIIÁË.
	OSIntEnter();    
#endif
	if(USART_GetITStatus(USART1, USART_IT_RXNE) != RESET)  //½ÓÊÕÖÐ¶Ï(½ÓÊÕµ½µÄÊý¾Ý±ØÐëÊÇ0x0d 0x0a½áÎ²)
		{
		Res =USART_ReceiveData(USART1);//(USART1->DR);	//¶ÁÈ¡½ÓÊÕµ½µÄÊý¾Ý
		
		if((USART_RX_STA&0x8000)==0)//½ÓÊÕÎ´Íê³É
			{
			if(USART_RX_STA&0x4000)//½ÓÊÕµ½ÁË0x0d
				{
				if(Res!=0x0a)USART_RX_STA=0;//½ÓÊÕ´íÎó,ÖØÐÂ¿ªÊ¼
				else USART_RX_STA|=0x8000;	//½ÓÊÕÍê³ÉÁË 
				}
			else //»¹Ã»ÊÕµ½0X0D
				{	
				if(Res==0x0d)USART_RX_STA|=0x4000;
				else
					{
					USART_RX_BUF[USART_RX_STA&0X3FFF]=Res ;
					USART_RX_STA++;
					if(USART_RX_STA>(USART_REC_LEN-1))USART_RX_STA=0;//½ÓÊÕÊý¾Ý´íÎó,ÖØÐÂ¿ªÊ¼½ÓÊÕ	  
					}		 
				}
			}   		 
     } 
#ifdef OS_TICKS_PER_SEC	 	//Èç¹ûÊ±ÖÓ½ÚÅÄÊý¶¨ÒåÁË,ËµÃ÷ÒªÊ¹ÓÃucosIIÁË.
	OSIntExit();  											 
#endif
} 
#endif	


```
**usart.h**
```
#ifndef __USART_H
#define __USART_H
#include "stdio.h"	
#include "sys.h" 

//STM32F103ºËÐÄ°åÀý³Ì
//¿âº¯Êý°æ±¾Àý³Ì
/********** mcudev.taobao.com ³öÆ·  ********/

//	 
//STM32¿ª·¢°å
//´®¿Ú1³õÊ¼»¯		   

#define USART_REC_LEN  			200  	//¶¨Òå×î´ó½ÓÊÕ×Ö½ÚÊý 200
#define EN_USART1_RX 			1		    //Ê¹ÄÜ£¨1£©/½ûÖ¹£¨0£©´®¿Ú1½ÓÊÕ
	  	
extern u8  USART_RX_BUF[USART_REC_LEN]; //½ÓÊÕ»º³å,×î´óUSART_REC_LEN¸ö×Ö½Ú.Ä©×Ö½ÚÎª»»ÐÐ·û 
extern u16 USART_RX_STA;         		//½ÓÊÕ×´Ì¬±ê¼Ç	
//Èç¹ûÏë´®¿ÚÖÐ¶Ï½ÓÊÕ£¬Çë²»Òª×¢ÊÍÒÔÏÂºê¶¨Òå
void uart_init(u32 bound);
#endif


```

**bsp_i2c.c**
```
#include "bsp_i2c.h"
#include "delay.h"

uint8_t   ack_status=0;
uint8_t   readByte[6];
uint8_t   AHT20_status=0;

uint32_t  H1=0;  //Humility
uint32_t  T1=0;  //Temperature

uint8_t  AHT20_OutData[4];
uint8_t  AHT20sendOutData[10] = {0xFA, 0x06, 0x0A, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0xFF};

void IIC_Init(void)
{					     
	GPIO_InitTypeDef GPIO_InitStructure;
	RCC_APB2PeriphClockCmd(	RCC_APB2Periph_GPIOB, ENABLE );	
	   
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_6|GPIO_Pin_7;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP ;   //ÍÆÍìÊä³ö
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOB, &GPIO_InitStructure);
 
	IIC_SCL=1;
	IIC_SDA=1;
 
}
//²úÉúIICÆðÊ¼ÐÅºÅ
void IIC_Start(void)
{
	SDA_OUT();     //sdaÏßÊä³ö
	IIC_SDA=1;	  	  
	IIC_SCL=1;
	delay_us(4);
 	IIC_SDA=0;//START:when CLK is high,DATA change form high to low 
	delay_us(4);
	IIC_SCL=0;//Ç¯×¡I2C×ÜÏß£¬×¼±¸·¢ËÍ»ò½ÓÊÕÊý¾Ý 
}	  
//²úÉúIICÍ£Ö¹ÐÅºÅ
void IIC_Stop(void)
{
	SDA_OUT();//sdaÏßÊä³ö
	IIC_SCL=0;
	IIC_SDA=0;//STOP:when CLK is high DATA change form low to high
 	delay_us(4);
	IIC_SCL=1; 
	IIC_SDA=1;//·¢ËÍI2C×ÜÏß½áÊøÐÅºÅ
	delay_us(4);							   	
}
//µÈ´ýÓ¦´ðÐÅºÅµ½À´
//·µ»ØÖµ£º1£¬½ÓÊÕÓ¦´ðÊ§°Ü
//        0£¬½ÓÊÕÓ¦´ð³É¹¦
u8 IIC_Wait_Ack(void)
{
	u8 ucErrTime=0;
	SDA_IN();      //SDAÉèÖÃÎªÊäÈë  
	IIC_SDA=1;delay_us(1);	   
	IIC_SCL=1;delay_us(1);	 
	while(READ_SDA)
	{
		ucErrTime++;
		if(ucErrTime>250)
		{
			IIC_Stop();
			return 1;
		}
	}
	IIC_SCL=0;//Ê±ÖÓÊä³ö0 	   
	return 0;  
} 
//²úÉúACKÓ¦´ð
void IIC_Ack(void)
{
	IIC_SCL=0;
	SDA_OUT();
	IIC_SDA=0;
	delay_us(2);
	IIC_SCL=1;
	delay_us(2);
	IIC_SCL=0;
}
//²»²úÉúACKÓ¦´ð		    
void IIC_NAck(void)
{
	IIC_SCL=0;
	SDA_OUT();
	IIC_SDA=1;
	delay_us(2);
	IIC_SCL=1;
	delay_us(2);
	IIC_SCL=0;
}					 				     
//IIC·¢ËÍÒ»¸ö×Ö½Ú
//·µ»Ø´Ó»úÓÐÎÞÓ¦´ð
//1£¬ÓÐÓ¦´ð
//0£¬ÎÞÓ¦´ð			  
void IIC_Send_Byte(u8 txd)
{                        
    u8 t;   
		SDA_OUT(); 	    
    IIC_SCL=0;//À­µÍÊ±ÖÓ¿ªÊ¼Êý¾Ý´«Êä
    for(t=0;t<8;t++)
    {              
        IIC_SDA=(txd&0x80)>>7;
        txd<<=1; 	  
		delay_us(2);   //¶ÔTEA5767ÕâÈý¸öÑÓÊ±¶¼ÊÇ±ØÐëµÄ
		IIC_SCL=1;
		delay_us(2); 
		IIC_SCL=0;	
		delay_us(2);
    }	 
} 	    
//¶Á1¸ö×Ö½Ú£¬ack=1Ê±£¬·¢ËÍACK£¬ack=0£¬·¢ËÍnACK   
u8 IIC_Read_Byte(unsigned char ack)
{
	unsigned char i,receive=0;
	SDA_IN();//SDAÉèÖÃÎªÊäÈë
  for(i=0;i<8;i++ )
	{
    IIC_SCL=0; 
    delay_us(2);
		IIC_SCL=1;
    receive<<=1;
    if(READ_SDA)receive++;   
		delay_us(1); 
  }					 
	if (!ack)
			IIC_NAck();//·¢ËÍnACK
	else
			IIC_Ack(); //·¢ËÍACK   
	return receive;
}
 
void IIC_WriteByte(uint16_t addr,uint8_t data,uint8_t device_addr)
{
	IIC_Start();  
	
	if(device_addr==0xA0) //eepromµØÖ·´óÓÚ1×Ö½Ú
		IIC_Send_Byte(0xA0 + ((addr/256)<<1));//·¢ËÍ¸ßµØÖ·
	else
		IIC_Send_Byte(device_addr);	    //·¢Æ÷¼þµØÖ·
	IIC_Wait_Ack(); 
	IIC_Send_Byte(addr&0xFF);   //·¢ËÍµÍµØÖ·
	IIC_Wait_Ack(); 
	IIC_Send_Byte(data);     //·¢ËÍ×Ö½Ú							   
	IIC_Wait_Ack();  		    	   
  IIC_Stop();//²úÉúÒ»¸öÍ£Ö¹Ìõ¼þ 
	if(device_addr==0xA0) //
		delay_ms(10);
	else
		delay_us(2);
}
 
uint16_t IIC_ReadByte(uint16_t addr,uint8_t device_addr,uint8_t ByteNumToRead)  //¶Á¼Ä´æÆ÷»ò¶ÁÊý¾Ý
{	
		uint16_t data;
		IIC_Start();  
		if(device_addr==0xA0)
			IIC_Send_Byte(0xA0 + ((addr/256)<<1));
		else
			IIC_Send_Byte(device_addr);	
		IIC_Wait_Ack();
		IIC_Send_Byte(addr&0xFF);   //·¢ËÍµÍµØÖ·
		IIC_Wait_Ack(); 
 
		IIC_Start();  	
		IIC_Send_Byte(device_addr+1);	    //·¢Æ÷¼þµØÖ·
		IIC_Wait_Ack();
		if(ByteNumToRead == 1)//LM75ÎÂ¶ÈÊý¾ÝÎª11bit
		{
			data=IIC_Read_Byte(0);
		}
		else
			{
				data=IIC_Read_Byte(1);
				data=(data<<8)+IIC_Read_Byte(0);
			}
		IIC_Stop();//²úÉúÒ»¸öÍ£Ö¹Ìõ¼þ	    
		return data;
}


/**********
*ÉÏÃæ²¿·ÖÎªIO¿ÚÄ£¿éI2CÅäÖÃ
*
*´ÓÕâÒÔÏÂ¿ªÊ¼ÎªAHT20µÄÅäÖÃI2C
*º¯ÊýÃûÓÐIICºÍI2CµÄÇø±ð£¬Çë×¢Òâ£¡£¡£¡£¡£¡
*
*2020/2/23×îºóÐÞ¸ÄÈÕÆÚ
*
***********/
void  read_AHT20_once(void)
{
	delay_ms(10);

	reset_AHT20();
	delay_ms(10);

	init_AHT20();
	delay_ms(10);

	startMeasure_AHT20();
	delay_ms(80);

	read_AHT20();
	delay_ms(5);
}


void  reset_AHT20(void)
{

	I2C_Start();

	I2C_WriteByte(0x70);
	ack_status = Receive_ACK();
	if(ack_status) printf("1");
	else printf("1-n-");
	I2C_WriteByte(0xBA);
	ack_status = Receive_ACK();
		if(ack_status) printf("2");
	else printf("2-n-");
	I2C_Stop();

	/*
	AHT20_OutData[0] = 0;
	AHT20_OutData[1] = 0;
	AHT20_OutData[2] = 0;
	AHT20_OutData[3] = 0;
	*/
}



void  init_AHT20(void)
{
	I2C_Start();

	I2C_WriteByte(0x70);
	ack_status = Receive_ACK();
	if(ack_status) printf("3");
	else printf("3-n-");	
	I2C_WriteByte(0xE1);
	ack_status = Receive_ACK();
	if(ack_status) printf("4");
	else printf("4-n-");
	I2C_WriteByte(0x08);
	ack_status = Receive_ACK();
	if(ack_status) printf("5");
	else printf("5-n-");
	I2C_WriteByte(0x00);
	ack_status = Receive_ACK();
	if(ack_status) printf("6");
	else printf("6-n-");
	I2C_Stop();
}



void  startMeasure_AHT20(void)
{
	//------------
	I2C_Start();

	I2C_WriteByte(0x70);
	ack_status = Receive_ACK();
	if(ack_status) printf("7");
	else printf("7-n-");
	I2C_WriteByte(0xAC);
	ack_status = Receive_ACK();
	if(ack_status) printf("8");
	else printf("8-n-");
	I2C_WriteByte(0x33);
	ack_status = Receive_ACK();
	if(ack_status) printf("9");
	else printf("9-n-");
	I2C_WriteByte(0x00);
	ack_status = Receive_ACK();
	if(ack_status) printf("10");
	else printf("10-n-");
	I2C_Stop();
}



void read_AHT20(void)
{
	uint8_t   i;

	for(i=0; i<6; i++)
	{
		readByte[i]=0;
	}

	//-------------
	I2C_Start();

	I2C_WriteByte(0x71);
	ack_status = Receive_ACK();
	readByte[0]= I2C_ReadByte();
	Send_ACK();

	readByte[1]= I2C_ReadByte();
	Send_ACK();

	readByte[2]= I2C_ReadByte();
	Send_ACK();

	readByte[3]= I2C_ReadByte();
	Send_ACK();

	readByte[4]= I2C_ReadByte();
	Send_ACK();

	readByte[5]= I2C_ReadByte();
	SendNot_Ack();
	//Send_ACK();

	I2C_Stop();

	//--------------
	if( (readByte[0] & 0x68) == 0x08 )
	{
		H1 = readByte[1];
		H1 = (H1<<8) | readByte[2];
		H1 = (H1<<8) | readByte[3];
		H1 = H1>>4;

		H1 = (H1*1000)/1024/1024;

		T1 = readByte[3];
		T1 = T1 & 0x0000000F;
		T1 = (T1<<8) | readByte[4];
		T1 = (T1<<8) | readByte[5];

		T1 = (T1*2000)/1024/1024 - 500;

		AHT20_OutData[0] = (H1>>8) & 0x000000FF;
		AHT20_OutData[1] = H1 & 0x000000FF;

		AHT20_OutData[2] = (T1>>8) & 0x000000FF;
		AHT20_OutData[3] = T1 & 0x000000FF;
	}
	else
	{
		AHT20_OutData[0] = 0xFF;
		AHT20_OutData[1] = 0xFF;

		AHT20_OutData[2] = 0xFF;
		AHT20_OutData[3] = 0xFF;
		printf("Ê§°ÜÁË");

	}
	printf("\r\n");
	printf("ÎÂ¶È:%d%d.%d",T1/100,(T1/10)%10,T1%10);
	printf("Êª¶È:%d%d.%d",H1/100,(H1/10)%10,H1%10);
	printf("\r\n");
}




uint8_t  Receive_ACK(void)
{
	uint8_t result=0;
	uint8_t cnt=0;

	IIC_SCL = 0;
	SDA_IN(); 
	delay_us(4);

	IIC_SCL = 1;
	delay_us(4);

	while(READ_SDA && (cnt<100))
	{
		cnt++;
	}

	IIC_SCL = 0;
	delay_us(4);

	if(cnt<100)
	{
		result=1;
	}
	return result;
}



void  Send_ACK(void)
{
	SDA_OUT();
	IIC_SCL = 0;
	delay_us(4);

	IIC_SDA = 0;
	delay_us(4);

	IIC_SCL = 1;
	delay_us(4);
	IIC_SCL = 0;
	delay_us(4);

	SDA_IN();
}



void  SendNot_Ack(void)
{
	SDA_OUT();
	IIC_SCL = 0;
	delay_us(4);

	IIC_SDA = 1;
	delay_us(4);

	IIC_SCL = 1;
	delay_us(4);

	IIC_SCL = 0;
	delay_us(4);

	IIC_SDA = 0;
	delay_us(4);
}


void I2C_WriteByte(uint8_t  input)
{
	uint8_t  i;
	SDA_OUT();
	for(i=0; i<8; i++)
	{
		IIC_SCL = 0;
		delay_ms(5);

		if(input & 0x80)
		{
			IIC_SDA = 1;
			//delaymm(10);
		}
		else
		{
			IIC_SDA = 0;
			//delaymm(10);
		}

		IIC_SCL = 1;
		delay_ms(5);

		input = (input<<1);
	}

	IIC_SCL = 0;
	delay_us(4);

	SDA_IN();
	delay_us(4);
}	


uint8_t I2C_ReadByte(void)
{
	uint8_t  resultByte=0;
	uint8_t  i=0, a=0;

	IIC_SCL = 0;
	SDA_IN();
	delay_ms(4);

	for(i=0; i<8; i++)
	{
		IIC_SCL = 1;
		delay_ms(3);

		a=0;
		if(READ_SDA)
		{
			a=1;
		}
		else
		{
			a=0;
		}

		//resultByte = resultByte | a;
		resultByte = (resultByte << 1) | a;

		IIC_SCL = 0;
		delay_ms(3);
	}

	SDA_IN();
	delay_ms(10);

	return   resultByte;
}


void  set_AHT20sendOutData(void)
{
	/* --------------------------
	 * 0xFA 0x06 0x0A temperature(2 Bytes) humility(2Bytes) short Address(2 Bytes)
	 * And Check (1 byte)
	 * -------------------------*/
	AHT20sendOutData[3] = AHT20_OutData[0];
	AHT20sendOutData[4] = AHT20_OutData[1];
	AHT20sendOutData[5] = AHT20_OutData[2];
	AHT20sendOutData[6] = AHT20_OutData[3];

//	AHT20sendOutData[7] = (drf1609.shortAddress >> 8) & 0x00FF;
//	AHT20sendOutData[8] = drf1609.shortAddress  & 0x00FF;

//	AHT20sendOutData[9] = getXY(AHT20sendOutData,10);
}


void  I2C_Start(void)
{
	SDA_OUT();
	IIC_SCL = 1;
	delay_ms(4);

	IIC_SDA = 1;
	delay_ms(4);
	IIC_SDA = 0;
	delay_ms(4);

	IIC_SCL = 0;
	delay_ms(4);
}



void  I2C_Stop(void)
{
	SDA_OUT();
	IIC_SDA = 0;
	delay_ms(4);

	IIC_SCL = 1;
	delay_ms(4);

	IIC_SDA = 1;
	delay_ms(4);
}


```

**bsp_i2c.h**
```
#ifndef __BSP_I2C_H
#define __BSP_I2C_H

#include "sys.h"
#include "delay.h"
#include "usart.h"
//Ê¹ÓÃIIC1 ¹ÒÔØM24C02,OLED,LM75AD,HT1382    PB6,PB7
 
#define SDA_IN()  {GPIOB->CRL&=0X0FFFFFFF;GPIOB->CRL|=(u32)8<<28;}
#define SDA_OUT() {GPIOB->CRL&=0X0FFFFFFF;GPIOB->CRL|=(u32)3<<28;}
 
//IO²Ù×÷º¯Êý	 
#define IIC_SCL    PBout(6) //SCL
#define IIC_SDA    PBout(7) //SDA	 
#define READ_SDA   PBin(7)  //ÊäÈëSDA 


//IICËùÓÐ²Ù×÷º¯Êý
void IIC_Init(void);                //³õÊ¼»¯IICµÄIO¿Ú				 
void IIC_Start(void);				//·¢ËÍIIC¿ªÊ¼ÐÅºÅ
void IIC_Stop(void);	  			//·¢ËÍIICÍ£Ö¹ÐÅºÅ
void IIC_Send_Byte(u8 txd);			//IIC·¢ËÍÒ»¸ö×Ö½Ú
u8 IIC_Read_Byte(unsigned char ack);//IIC¶ÁÈ¡Ò»¸ö×Ö½Ú
u8 IIC_Wait_Ack(void); 				//IICµÈ´ýACKÐÅºÅ
void IIC_Ack(void);					//IIC·¢ËÍACKÐÅºÅ
void IIC_NAck(void);				//IIC²»·¢ËÍACKÐÅºÅ
 
void IIC_WriteByte(uint16_t addr,uint8_t data,uint8_t device_addr);
uint16_t IIC_ReadByte(uint16_t addr,uint8_t device_addr,uint8_t ByteNumToRead);//¼Ä´æÆ÷µØÖ·£¬Æ÷¼þµØÖ·£¬Òª¶ÁµÄ×Ö½ÚÊý  


void  read_AHT20_once(void);
void  reset_AHT20(void);
void  init_AHT20(void);	
void  startMeasure_AHT20(void);
void  read_AHT20(void);
uint8_t  Receive_ACK(void);
void  Send_ACK(void);
void  SendNot_Ack(void);
void I2C_WriteByte(uint8_t  input);
uint8_t I2C_ReadByte(void);	
void  set_AHT20sendOutData(void);
void  I2C_Start(void);
void  I2C_Stop(void);
#endif


```

**delay.c**
```
#include "delay.h"
#include "sys.h"

//STM32F103ºËÐÄ°åÀý³Ì
//¿âº¯Êý°æ±¾Àý³Ì
/********** mcudev.taobao.com ³öÆ·  ********/


// 	 
//Èç¹ûÊ¹ÓÃucos,Ôò°üÀ¨ÏÂÃæµÄÍ·ÎÄ¼þ¼´¿É.
#if SYSTEM_SUPPORT_UCOS
#include "includes.h"					//ucos Ê¹ÓÃ	  
#endif
//	 

//STM32¿ª·¢°å
//Ê¹ÓÃSysTickµÄÆÕÍ¨¼ÆÊýÄ£Ê½¶ÔÑÓ³Ù½øÐÐ¹ÜÀí
//°üÀ¨delay_us,delay_ms

// 	 
static u8  fac_us=0;//usÑÓÊ±±¶³ËÊý
static u16 fac_ms=0;//msÑÓÊ±±¶³ËÊý
#ifdef OS_CRITICAL_METHOD 	//Èç¹ûOS_CRITICAL_METHOD¶¨ÒåÁË,ËµÃ÷Ê¹ÓÃucosIIÁË.
//systickÖÐ¶Ï·þÎñº¯Êý,Ê¹ÓÃucosÊ±ÓÃµ½
void SysTick_Handler(void)
{				   
	OSIntEnter();		//½øÈëÖÐ¶Ï
    OSTimeTick();       //µ÷ÓÃucosµÄÊ±ÖÓ·þÎñ³ÌÐò               
    OSIntExit();        //´¥·¢ÈÎÎñÇÐ»»ÈíÖÐ¶Ï
}
#endif

//³õÊ¼»¯ÑÓ³Ùº¯Êý
//µ±Ê¹ÓÃucosµÄÊ±ºò,´Ëº¯Êý»á³õÊ¼»¯ucosµÄÊ±ÖÓ½ÚÅÄ
//SYSTICKµÄÊ±ÖÓ¹Ì¶¨ÎªHCLKÊ±ÖÓµÄ1/8
//SYSCLK:ÏµÍ³Ê±ÖÓ
void delay_init()	 
{

#ifdef OS_CRITICAL_METHOD 	//Èç¹ûOS_CRITICAL_METHOD¶¨ÒåÁË,ËµÃ÷Ê¹ÓÃucosIIÁË.
	u32 reload;
#endif
	SysTick_CLKSourceConfig(SysTick_CLKSource_HCLK_Div8);	//Ñ¡ÔñÍâ²¿Ê±ÖÓ  HCLK/8
	fac_us=SystemCoreClock/8000000;	//ÎªÏµÍ³Ê±ÖÓµÄ1/8  
	 
#ifdef OS_CRITICAL_METHOD 	//Èç¹ûOS_CRITICAL_METHOD¶¨ÒåÁË,ËµÃ÷Ê¹ÓÃucosIIÁË.
	reload=SystemCoreClock/8000000;		//Ã¿ÃëÖÓµÄ¼ÆÊý´ÎÊý µ¥Î»ÎªK	   
	reload*=1000000/OS_TICKS_PER_SEC;//¸ù¾ÝOS_TICKS_PER_SECÉè¶¨Òç³öÊ±¼ä
							//reloadÎª24Î»¼Ä´æÆ÷,×î´óÖµ:16777216,ÔÚ72MÏÂ,Ô¼ºÏ1.86s×óÓÒ	
	fac_ms=1000/OS_TICKS_PER_SEC;//´ú±íucos¿ÉÒÔÑÓÊ±µÄ×îÉÙµ¥Î»	   
	SysTick->CTRL|=SysTick_CTRL_TICKINT_Msk;   	//¿ªÆôSYSTICKÖÐ¶Ï
	SysTick->LOAD=reload; 	//Ã¿1/OS_TICKS_PER_SECÃëÖÐ¶ÏÒ»´Î	
	SysTick->CTRL|=SysTick_CTRL_ENABLE_Msk;   	//¿ªÆôSYSTICK    
#else
	fac_ms=(u16)fac_us*1000;//·ÇucosÏÂ,´ú±íÃ¿¸ömsÐèÒªµÄsystickÊ±ÖÓÊý   
#endif
}								    

#ifdef OS_CRITICAL_METHOD	//Ê¹ÓÃÁËucos
//ÑÓÊ±nus
//nusÎªÒªÑÓÊ±µÄusÊý.		    								   
void delay_us(u32 nus)
{		
	u32 ticks;
	u32 told,tnow,tcnt=0;
	u32 reload=SysTick->LOAD;	//LOADµÄÖµ	    	 
	ticks=nus*fac_us; 			//ÐèÒªµÄ½ÚÅÄÊý	  		 
	tcnt=0;
	told=SysTick->VAL;        	//¸Õ½øÈëÊ±µÄ¼ÆÊýÆ÷Öµ
	while(1)
	{
		tnow=SysTick->VAL;	
		if(tnow!=told)
		{	    
			if(tnow<told)tcnt+=told-tnow;//ÕâÀï×¢ÒâÒ»ÏÂSYSTICKÊÇÒ»¸öµÝ¼õµÄ¼ÆÊýÆ÷¾Í¿ÉÒÔÁË.
			else tcnt+=reload-tnow+told;	    
			told=tnow;
			if(tcnt>=ticks)break;//Ê±¼ä³¬¹ý/µÈÓÚÒªÑÓ³ÙµÄÊ±¼ä,ÔòÍË³ö.
		}  
	}; 									    
}
//ÑÓÊ±nms
//nms:ÒªÑÓÊ±µÄmsÊý
void delay_ms(u16 nms)
{	
	if(OSRunning==TRUE)//Èç¹ûosÒÑ¾­ÔÚÅÜÁË	    
	{		  
		if(nms>=fac_ms)//ÑÓÊ±µÄÊ±¼ä´óÓÚucosµÄ×îÉÙÊ±¼äÖÜÆÚ 
		{
   			OSTimeDly(nms/fac_ms);//ucosÑÓÊ±
		}
		nms%=fac_ms;				//ucosÒÑ¾­ÎÞ·¨Ìá¹©ÕâÃ´Ð¡µÄÑÓÊ±ÁË,²ÉÓÃÆÕÍ¨·½Ê½ÑÓÊ±    
	}
	delay_us((u32)(nms*1000));	//ÆÕÍ¨·½Ê½ÑÓÊ±,´ËÊ±ucosÎÞ·¨Æô¶¯µ÷¶È.
}
#else//²»ÓÃucosÊ±
//ÑÓÊ±nus
//nusÎªÒªÑÓÊ±µÄusÊý.		    								   
void delay_us(u32 nus)
{		
	u32 temp;	    	 
	SysTick->LOAD=nus*fac_us; //Ê±¼ä¼ÓÔØ	  		 
	SysTick->VAL=0x00;        //Çå¿Õ¼ÆÊýÆ÷
	SysTick->CTRL|=SysTick_CTRL_ENABLE_Msk ;          //¿ªÊ¼µ¹Êý	 
	do
	{
		temp=SysTick->CTRL;
	}
	while(temp&0x01&&!(temp&(1<<16)));//µÈ´ýÊ±¼äµ½´ï   
	SysTick->CTRL&=~SysTick_CTRL_ENABLE_Msk;       //¹Ø±Õ¼ÆÊýÆ÷
	SysTick->VAL =0X00;       //Çå¿Õ¼ÆÊýÆ÷	 
}
//ÑÓÊ±nms
//×¢ÒânmsµÄ·¶Î§
//SysTick->LOADÎª24Î»¼Ä´æÆ÷,ËùÒÔ,×î´óÑÓÊ±Îª:
//nms<=0xffffff*8*1000/SYSCLK
//SYSCLKµ¥Î»ÎªHz,nmsµ¥Î»Îªms
//¶Ô72MÌõ¼þÏÂ,nms<=1864 
void delay_ms(u16 nms)
{	 		  	  
	u32 temp;		   
	SysTick->LOAD=(u32)nms*fac_ms;//Ê±¼ä¼ÓÔØ(SysTick->LOADÎª24bit)
	SysTick->VAL =0x00;           //Çå¿Õ¼ÆÊýÆ÷
	SysTick->CTRL|=SysTick_CTRL_ENABLE_Msk ;          //¿ªÊ¼µ¹Êý  
	do
	{
		temp=SysTick->CTRL;
	}
	while(temp&0x01&&!(temp&(1<<16)));//µÈ´ýÊ±¼äµ½´ï   
	SysTick->CTRL&=~SysTick_CTRL_ENABLE_Msk;       //¹Ø±Õ¼ÆÊýÆ÷
	SysTick->VAL =0X00;       //Çå¿Õ¼ÆÊýÆ÷	  	    
} 
#endif

```
delay.h

```
#ifndef __DELAY_H
#define __DELAY_H 			   
#include "sys.h"
//	 

//STM32F103ºËÐÄ°åÀý³Ì
//¿âº¯Êý°æ±¾Àý³Ì
/********** mcudev.taobao.com ³öÆ·  ********/


//Ê¹ÓÃSysTickµÄÆÕÍ¨¼ÆÊýÄ£Ê½¶ÔÑÓ³Ù½øÐÐ¹ÜÀí
//°üÀ¨delay_us,delay_ms

// 	 
void delay_init(void);
void delay_ms(u16 nms);
void delay_us(u32 nus);

#endif

```
**sys.c**
```
#include "sys.h"


//STM32F103ºËÐÄ°åÀý³Ì
//¿âº¯Êý°æ±¾Àý³Ì
/********** mcudev.taobao.com ³öÆ·  ********/

//	 

//STM32¿ª·¢°å
//ÏµÍ³ÖÐ¶Ï·Ö×éÉèÖÃ»¯		   

//********************************************************************************  
void NVIC_Configuration(void)
{

    NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);	//ÉèÖÃNVICÖÐ¶Ï·Ö×é2:2Î»ÇÀÕ¼ÓÅÏÈ¼¶£¬2Î»ÏìÓ¦ÓÅÏÈ¼¶

}


```

**sys.h**
```
#ifndef __SYS_H
#define __SYS_H	
#include "stm32f10x.h"
//	 


//STM32F103ºËÐÄ°åÀý³Ì
//¿âº¯Êý°æ±¾Àý³Ì
/********** mcudev.taobao.com ³öÆ·  ********/



// 	 

//0,²»Ö§³Öucos
//1,Ö§³Öucos
#define SYSTEM_SUPPORT_UCOS		0		//¶¨ÒåÏµÍ³ÎÄ¼þ¼ÐÊÇ·ñÖ§³ÖUCOS
																	    
	 
//Î»´ø²Ù×÷,ÊµÏÖ51ÀàËÆµÄGPIO¿ØÖÆ¹¦ÄÜ
//¾ßÌåÊµÏÖË¼Ïë,²Î¿¼<<CM3È¨ÍþÖ¸ÄÏ>>µÚÎåÕÂ(87Ò³~92Ò³).
//IO¿Ú²Ù×÷ºê¶¨Òå
#define BITBAND(addr, bitnum) ((addr & 0xF0000000)+0x2000000+((addr &0xFFFFF)<<5)+(bitnum<<2)) 
#define MEM_ADDR(addr)  *((volatile unsigned long  *)(addr)) 
#define BIT_ADDR(addr, bitnum)   MEM_ADDR(BITBAND(addr, bitnum)) 
//IO¿ÚµØÖ·Ó³Éä
#define GPIOA_ODR_Addr    (GPIOA_BASE+12) //0x4001080C 
#define GPIOB_ODR_Addr    (GPIOB_BASE+12) //0x40010C0C 
#define GPIOC_ODR_Addr    (GPIOC_BASE+12) //0x4001100C 
#define GPIOD_ODR_Addr    (GPIOD_BASE+12) //0x4001140C 
#define GPIOE_ODR_Addr    (GPIOE_BASE+12) //0x4001180C 
#define GPIOF_ODR_Addr    (GPIOF_BASE+12) //0x40011A0C    
#define GPIOG_ODR_Addr    (GPIOG_BASE+12) //0x40011E0C    

#define GPIOA_IDR_Addr    (GPIOA_BASE+8) //0x40010808 
#define GPIOB_IDR_Addr    (GPIOB_BASE+8) //0x40010C08 
#define GPIOC_IDR_Addr    (GPIOC_BASE+8) //0x40011008 
#define GPIOD_IDR_Addr    (GPIOD_BASE+8) //0x40011408 
#define GPIOE_IDR_Addr    (GPIOE_BASE+8) //0x40011808 
#define GPIOF_IDR_Addr    (GPIOF_BASE+8) //0x40011A08 
#define GPIOG_IDR_Addr    (GPIOG_BASE+8) //0x40011E08 
 
//IO¿Ú²Ù×÷,Ö»¶Ôµ¥Ò»µÄIO¿Ú!
//È·±£nµÄÖµÐ¡ÓÚ16!
#define PAout(n)   BIT_ADDR(GPIOA_ODR_Addr,n)  //Êä³ö 
#define PAin(n)    BIT_ADDR(GPIOA_IDR_Addr,n)  //ÊäÈë 

#define PBout(n)   BIT_ADDR(GPIOB_ODR_Addr,n)  //Êä³ö 
#define PBin(n)    BIT_ADDR(GPIOB_IDR_Addr,n)  //ÊäÈë 

#define PCout(n)   BIT_ADDR(GPIOC_ODR_Addr,n)  //Êä³ö 
#define PCin(n)    BIT_ADDR(GPIOC_IDR_Addr,n)  //ÊäÈë 

#define PDout(n)   BIT_ADDR(GPIOD_ODR_Addr,n)  //Êä³ö 
#define PDin(n)    BIT_ADDR(GPIOD_IDR_Addr,n)  //ÊäÈë 

#define PEout(n)   BIT_ADDR(GPIOE_ODR_Addr,n)  //Êä³ö 
#define PEin(n)    BIT_ADDR(GPIOE_IDR_Addr,n)  //ÊäÈë

#define PFout(n)   BIT_ADDR(GPIOF_ODR_Addr,n)  //Êä³ö 
#define PFin(n)    BIT_ADDR(GPIOF_IDR_Addr,n)  //ÊäÈë

#define PGout(n)   BIT_ADDR(GPIOG_ODR_Addr,n)  //Êä³ö 
#define PGin(n)    BIT_ADDR(GPIOG_IDR_Addr,n)  //ÊäÈë



void NVIC_Configuration(void);



#endif


```