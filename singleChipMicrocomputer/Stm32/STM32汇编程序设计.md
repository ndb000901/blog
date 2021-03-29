## STM32汇编程序设计

**1.实验环境**

>1.野火STM32指南者(STM32F103VET6)
>
>2.keil5

**2.环境搭建**

新建工程

![image](https://user-images.githubusercontent.com/48900845/112813252-94cc6880-90b0-11eb-8844-db5904c4f5e2.png)

![image](https://user-images.githubusercontent.com/48900845/112813268-99911c80-90b0-11eb-83af-34ce8750cd56.png)

添加源文件（.s）

![image](https://user-images.githubusercontent.com/48900845/112813295-a0b82a80-90b0-11eb-8632-9d2f0776ce7b.png)


```
 AREA MYDATA, DATA
	
 AREA MYCODE, CODE
	ENTRY
	EXPORT __main

__main
	MOV R0, #10
	MOV R1, #11
	MOV R2, #12
	MOV R3, #13
	;LDR R0, =func01

	BL	func01
	;LDR R1, =func02
	BL	func02
	
	BL 	func03
	LDR LR, =func01
	LDR PC, =func03
	B .
		
func01
	MOV R5, #05
	BX LR
	
func02
	MOV R6, #06
	BX LR
	
func03
	MOV R7, #07
	MOV R8, #08	
	BX LR

```

连接开发板，开始debug

![image](https://user-images.githubusercontent.com/48900845/112813336-ad3c8300-90b0-11eb-8907-66c76b3ae327.png)

生成的hex文件

![image](https://user-images.githubusercontent.com/48900845/112813364-b4fc2780-90b0-11eb-9707-7b7aca0ff400.png)


## 点灯

源码
```
LED0 EQU 0x40010c00
RCC_APB2ENR EQU 0x40021018
GPIOA_CRH EQU 0x40010804



Stack_Size      EQU     0x00000400

                AREA    STACK, NOINIT, READWRITE, ALIGN=3
Stack_Mem       SPACE   Stack_Size
__initial_sp




                AREA    RESET, DATA, READONLY

__Vectors       DCD     __initial_sp               ; Top of Stack
                DCD     Reset_Handler              ; Reset Handler
                    
                    
                AREA    |.text|, CODE, READONLY
                    
                THUMB
                REQUIRE8
                PRESERVE8
                    
                ENTRY
Reset_Handler 
                BL LED_Init
MainLoop        BL LED_ON
                BL Delay
                BL LED_OFF
                BL Delay
                
                B MainLoop
             
LED_Init
                PUSH {R0,R1, LR}
                
                LDR R0,=RCC_APB2ENR
                ORR R0,R0,#0x04
                LDR R1,=RCC_APB2ENR
                STR R0,[R1]
                
                LDR R0,=GPIOA_CRH
                BIC R0,R0,#0x0F
                LDR R1,=GPIOA_CRH
                STR R0,[R1]
                
                LDR R0,=GPIOA_CRH
                ORR R0,R0,#0x03
                LDR R1,=GPIOA_CRH
                STR R0,[R1]
                
                MOV R0,#1 
                LDR R1,=LED0
                STR R0,[R1]
             
                POP {R0,R1,PC}

             
LED_ON
                PUSH {R0,R1, LR}    
                
                MOV R0,#0 
                LDR R1,=LED0
                STR R0,[R1]
             
                POP {R0,R1,PC}
             
LED_OFF
                PUSH {R0,R1, LR}    
                
                MOV R0,#1 
                LDR R1,=LED0
                STR R0,[R1]
             
                POP {R0,R1,PC}             
             
Delay
                PUSH {R0,R1, LR}
                
                MOVS R0,#0
                MOVS R1,#0
                MOVS R2,#0
                
DelayLoop0        
                ADDS R0,R0,#1

                CMP R0,#330
                BCC DelayLoop0
                
                MOVS R0,#0
                ADDS R1,R1,#1
                CMP R1,#330
                BCC DelayLoop0

                MOVS R0,#0
                MOVS R1,#0
                ADDS R2,R2,#1
                CMP R2,#15
                BCC DelayLoop0
                
                
                POP {R0,R1,PC}    
             
    ;         NOP
             END

```


