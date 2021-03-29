## 让繁琐的工作自动化——python 处理Excle文件

今天收到一个省市县区的Excle表格，想着整理一下数据，将信息整理为层级关系（省-->市-->(县/区)）存到字典里，以备不时之需。
打开一看，MD，3千行数据，这TM要搞到神马时候。

![image](https://user-images.githubusercontent.com/48900845/112762066-80e12200-9030-11eb-80a8-b888769e0f84.png)

![image](https://user-images.githubusercontent.com/48900845/112762072-850d3f80-9030-11eb-924b-7d7a213bfe2e.png)


*****
叮铃铃~~~~ 叮铃铃 ~~~~，人生苦短，我用python。开搞！！！






****
## **openpyxl的基础使用**

**环境**

>1.pycharm2020.1
>
>2.python3.8
>
>3.openpyxl 2.1.4

openpyxl已经更新到3点多了，我这里演示的是**openpyxl 2.1.4**。

导入openpyxl模块
```
import openpyxl
```

**读取操作**

打开要处理的文件，该函数需要传入一个文件路径。wb是一个Workbook对象。
```
wb = openpyxl.load_workbook("省市县区.xlsx")
```
Excel文档有多个sheet组成。

获得Excel文档所有sheet。
```
sheetList = wb.get_sheet_names()
```
根据sheet名字获取对应表。表由一个Worksheet对象表示，sheet就是一个Worksheet对象。
```
sheet = wb.get_sheet_by_name("sheet名字")
```
取得sheet表格中的值

数值定位：row是行号，column是列号。

字符定位：Excle用字母表示列，数字表示行。
```
x = sheet.cell(row=1, column=1).value #第一种表示
y = sheet['A1'].value #第二种表示
```
列字母和数字之间的转换。

```
openpyxl.cell.column_index_from_string()   #字母---->数字
openpyxl.cell.column_letter()                        #数字---->字母
```


获取sheet有多大。
```
sheet.get_highest_row()        #返回行数
sheet.get_highest_column()  #返回列数
```

遍历sheet
```
for i in range(1, sheet.get_highest_row()  + 1):
    for j in range(1, sheet.get_highest_column()  + 1):
        print(str(sheet1.cell(row=i, column=j).value) + " ", end="")
    print()
```

**写入操作**

创建新的Workbook对象。
```
wb = openpyxl.Workbook()
```
保存文件。(传入文件名)
```
wb.save("haha.xlsx")
```
创建sheet，index表示sheet的次序，title表示sheet的名字。
```
wb.create_sheet(index=0,title='haha')
```
删除sheet，需要传入Worksheet对象，如果知道sheet的名字，就可使用以下代码删除
```
wb.remove_sheet(wb.get_sheet_by_name("sheet名字"))
```
写入数据
```
sheet.cell(row=1, column=1) = x #第一种表示
sheet['A1'] = y #第二种表示
```


*****

## **处理表格的源码**

原表格公众号回复【省市】获得

```
import pprint
import openpyxl
wb = openpyxl.load_workbook("省市县区.xlsx")
sheet = wb.get_sheet_by_name("省市县区")
data = {}

for i in range(2, sheet.get_highest_row() + 1):
    province = sheet.cell(row=i, column=1).value
    city = sheet.cell(row=i, column=2).value
    county = sheet.cell(row=i, column=3).value
    data.setdefault(province, {})
    data[province].setdefault(city, [])
    if data[province][city].count(county) == 0:
        data[province][city].append(county)

print("数据整理完毕，开始写入文件")
with open("cityInfo.py", "w", encoding='utf-8') as file:
    file.write("cityInfo = " + pprint.pformat(data))
print("文件写入完毕")
```




>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
