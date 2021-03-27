## 让繁琐的工作自动化——python处理JSON文件
不得不说，python真TMD香。由于python解析json过于简洁，我只好写个实例了，不然文章太短。

****

**1.环境**
>1.python3.8
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
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020080623251272.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


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
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200806233203395.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

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
![
](https://img-blog.csdnimg.cn/20200807001548503.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200807001603890.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)

>作者info
作者：DebugWuhen
原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706013520101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70)
