
## 让繁琐的工作自动化——python处理CSV文件

CSV：CSV文件是一种简化的电子表格，不同于Excle(二进制文件)，CSV是纯文本文件。

****



**1.环境**

>1.python3.8
>
>2.pycharm2020.1

**2.读取**

****
**本期实例数据**
```
haha,18,10.0
jiji,16,12.1
lala,17,11.9
papa,11,13.3

```

![image](https://user-images.githubusercontent.com/48900845/112762127-bb4abf00-9030-11eb-9720-275c57179ad9.png)

![image](https://user-images.githubusercontent.com/48900845/112762129-bf76dc80-9030-11eb-9ac9-76ee5b99ab5b.png)

****



首先导入csv模块，不需要安装，python自带的。
```
import csv
```
要想用csv模块读取csv文件数据，需要先创建一个Reader对象，Reader可以遍历文件的每一行。

**注意：Reader对象只能循环遍历一次，如果想要再次遍历，需要重新创建。**

```
file = open("haha.csv")
reader = csv.reader(file)
data = list(reader)
print(data)
```
以下为在交互式界面操作。

![image](https://user-images.githubusercontent.com/48900845/112762140-c867ae00-9030-11eb-9532-6a095423bf3c.png)


使用Reader对象遍历数据，Reader.line_num标志当前遍历到第几行。
```
import csv
file = open("haha.csv")
reader = csv.reader(file)
for row in reader:
    print(("第{}行  " + str(row)).format(reader.line_num))
```

**3.写入**

将数据写入到CSV文件，需要用到Writer对象。

与读取一样，先导入csv模块，然后打开文件。

**encoding是编码；newline等于空字符，若不设置，在Windows系统上，行距会变成下图所示。**

![image](https://user-images.githubusercontent.com/48900845/112762172-e503e600-9030-11eb-90f8-266b1ecbf2ba.png)

```
import csv
file = open('haha.csv', 'w', encoding='utf-8', newline='')
```
创建Writer对象，csv.writer()有两个参数需要注意。

delimiter： 单元格分隔符，默认为逗号，可以修改为其他。

lineterminator：行终止符，默认为换行符，可以自行修改。
```
writer = csv.writer(file)
```

写入数据，使用writer.writerow（），该函数接受一个列表，返回写入该行的字符数（包括换行符）
```
writer.writerow(['haha', '18', '10.0'])
writer.writerow(['jiji', '16', '12.1'])
writer.writerow(['lala', '17', '11.9'])
writer.writerow(['papa', '11', '13.3'])
```

写入完整源码
```
import csv
file = open('haha.csv', 'w', encoding='utf-8')
writer = csv.writer(file)
writer.writerow(['haha', '18', '10.0'])
writer.writerow(['jiji', '16', '12.1'])
writer.writerow(['lala', '17', '11.9'])
writer.writerow(['papa', '11', '13.3'])
file.close()
```
## 原创不易，点个赞再走吧。


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
