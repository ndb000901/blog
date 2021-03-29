## 让繁琐的工作自动化——python处理JSON文件

不得不说，python真TMD香。由于python解析json过于简洁，我只好写个实例了，不然文章太短。

****

**1.环境**

>1.python3.8
>
>2.pycharm 2020.1


**2.读取JSON数据**

当然首先要导入json模块
```
import json
```
读取json数据
```
data = '{"a":123,"b":"lala"}'
result = json.loads(data)
print(result)
print(result['a'])

```

交互式界面

![image](https://user-images.githubusercontent.com/48900845/112762217-18df0b80-9031-11eb-9e35-4f17627d66e8.png)



**3.写出JSON数据**

导入模块
```
import json
```

输出json数据，将python字典转为json数据
```
data = {'a':1234,'b':'lalala'}
result = json.dumps(data)
print(result)
```

![image](https://user-images.githubusercontent.com/48900845/112762229-20061980-9031-11eb-94fc-64eabfd6889a.png)


## 实例，抓取中国地震台网数据，解析JSON数据包。

**完整源码**

```
import json
import requests

res = requests.get('http://news.ceic.ac.cn/ajax/google')
text = res.text.encode('utf-8')
result = json.loads(text)

print('%-20s' % 'id' '%-20s' % '地点' '%-20s' % '震级' '%-20s' % '经度' '%-20s' % '纬度' '%-20s' % '深度' '%-20s' % '时间')
for e in result:

    print('%-20s' % str(e['id']), '%-20s' % str(e['LOCATION_C']), '%-20s' % str(e['M']), '%-20s' % str(e['EPI_LON']), '%-20s' % str(e['EPI_LAT']), '%-20s' % str(e['EPI_DEPTH']), '%-20s' % str(e['O_TIME']))

```


排版有点烂，各位大爷多多包涵。

![image](https://user-images.githubusercontent.com/48900845/112762239-2c8a7200-9031-11eb-80bb-661790cab334.png)

![image](https://user-images.githubusercontent.com/48900845/112762241-30b68f80-9031-11eb-9a31-06ebbd75da8c.png)




>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
