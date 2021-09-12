# Intruder模块

## 环境

```
burpsuite-v2021.8.2 Community Edition
```
## Target

**功能：配置攻击目标服务器**

## Positions

**Attack type**

|类别|说明|
|----|----|
|Sniper|对变量依次进行破解，多个标记依次进行，n个标记，需1个字典|
|Battering ram|对变量进行同时破解，多个标记同时进行，n个标记，需n个字典|
|Pitchfork|每个变量对应一个字典，取每个字典的对应项，n个标记，需n个字典|
|Cluster bomb|每个变量对应一个字典，并进行交集，各种组合，n个标记，需n个字典|

## Payloads

**功能：设置payload,配置字典**

|模块|说明|
|----|----|
|Payload Sets Payload|数量类型设置|
|Payload Options|加载字典|
|Payload Processing|对生成的payload进行编码、加密、截取|
|Payload Encoding|配置需url编码的字符|

## Resource Pool

## Options

|模块|说明|
|----|----|
|Request Headers|http请求头设置|
|Error Handling|设置攻击时如何处理错误|
|Attack Results|设置攻击结果的显示|
|Grep-Match|在响应中找出指定的内容|
|Grep-Extract|通过正则提取返回信息中的内容|
|Grep-Payloads|在结果中添加一个复选框指示当前负载的值在每个响应发现新的结果列|
|Redirections|设置在进行攻击时如何处理重定向|
































