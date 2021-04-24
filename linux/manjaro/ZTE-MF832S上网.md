## ZTE-MF832S上网

**实验环境**

>1.ZTE-MF832S
>
>2.manjaro21-gnome
>

**配置端口**

波特率9600

```
sudo minicom -s配置端口
```

![image](https://user-images.githubusercontent.com/48900845/115966078-ac3b2c00-a55e-11eb-8355-fbd26bcfd957.png)


**AT命令**

ctrl + a + e
```
AT+CGDCONT=1,"IP"
AT+CFUN=1
AT+CEREG=1
AT+CGREG?
AT+CEREG?
AT+ZGACT=1,1
AT+CGPADDR=1
```
