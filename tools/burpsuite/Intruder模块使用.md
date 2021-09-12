# Intruder模块

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
































