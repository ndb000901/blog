# shell脚本编写

## 一些语法基础

**1.如何定义一个变量**

变量名由字母、数字、下划线组成，不可以数字开头，不可使用保留关键字。

等号左右不可有空格。

```
haha="jiji"
```
**使用变量：在变量名前加上$**
 
```
echo $haha
```

**可以在变量外加上‘{}’**

其实加与不加都可以，加花括号可以帮助解释器更好地识别变量边界。

```
echo "hello world ${haha}"
```

**readonly 只读变量**

readonly 关键字修饰的变量不可修改。

```
readonly haha="jiji"
```

**数组**

**定义**

数组内可有不同类型数据
```
myArray=(1 2 ‘kkk’ 4)

# 或者(下标可以不连续，无限制)

myArray[0]=10
myArray[0]=11
myArray[0]=12

```

**读取数组内容**

**通过索引**
```
myArray=(1 2 'jiji' 4)
echo ${myArray[0]}
echo ${myArray[1]}
echo ${myArray[2]}
echo ${myArray[3]}
```

**输出结果**

```
1
2
jiji
4
```

**获取所有元素**

使用@、*获取。

```
myArray=(1 2 'jiji' 4)
echo ${myArray[@]}
echo ${myArray[*]}
```

**输出结果**

```
1 2 jiji 4
1 2 jiji 4
```

**获取数组长度**

```
myArray=(1 2 'jiji' 4)
echo ${#myArray[@]}
echo ${#myArray[*]}
```

**输出结果**

```
4
4
```

**2.流程控制**

**if-else**

```
if [ 1 == 1 ]
then
    echo "OK"
fi
```

**多个if-else**

**注意：**

判断条件'[]'与变量要有空格

```
a=1
b=2

if [ $a == $b ]
then
    echo "a等于b"
elif [ $a -gt $b ]
then
    echo "a大于b"
elif [ $a -lt $b ]
then
    echo "a小于b"
fi
```

**for 循环**

```
for i in 1 2 3 4
do
    echo $i
done
```

**输出结果**

```
1
2
3
4
```

**while 循环**

```
int=1
while (( $int<5 ))
do
    echo $int
    let "int++"
done
```

**输出结果**

```
1
2
3
4
```

**case**

若无匹配项，则执行*。

```
echo "请输入一个数："
read num
case $num in
    1)
        echo "1"
    ;;
    2)
        echo "2"
    ;;
    3) 
        echo "3"
    ;;
    4) 
        echo "4"
    ;;
    *)
        echo "other"
    ;;
esac
```

**输出结果**

```
# 输入2
请输入一个数：
2
2

# 输入 11

请输入一个数：
11
other
```

**无限循环**

```
while :
do
    echo "hello,world"
done

while true
do
    echo "hello,world"
done

for((;;));do
echo "jiji"
done
```

**until**

**int等于3时停止**

```
int=1
until (($int==3))
do
    echo "$int"
    let "int++"
done
```

**break**

跳出循环

**continue**

跳出本次循环


**3.传递参数**

通常在执行脚本时，会为脚本传递一些参数

```
echo "$0"
echo "$1"
echo "$2"
echo "$3"
echo "$4"

echo "传递参数的个数：$#"
echo "当前id:$$"
echo "$*"
echo "$@"
echo "最后一个id：$!"
echo "退出状态：$?"
```
**执行命令**

```
./hello.sh a b c d
```
**输出结果**

```
./hello.sh
a
b
c
d
传递参数的个数：4
当前id:15412
a b c d
a b c d
最后一个id：
退出状态：0
```

|参数|说明|
|----|----|
|$0|脚本名|
|$n|第n个参数|
|$#|传递参数的个数|
|$!|后台最后一个进程id|
|$$|当前进程id|
|$?|退出状态码|
|$*|单字符串，所有参数|
|$@|多字符串，所有参数|
