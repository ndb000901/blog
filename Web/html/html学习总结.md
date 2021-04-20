# html学习总结



## 一些元素

**注意：HTML对大小写不敏感**

**\<html\>元素**

\<html\>定义了整个文档

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

</body>
</html>
```

## \<head\>元素

可以插入到\<head\>的元素：\<title\>, \<style\>, \<meta\>, \<link\>, \<script\>, \<noscript\> 和 \<base\>

```
```

**\<title\>元素**

定义了该网页的标题

```
<title>MyTitle</title>
```

**\<style\>元素**

引用CSS

```
<style type="text/css">
body {background-color:yellow}
p {color:blue}
</style>
```

**\<meta\>元素**

用来定义一些元数据

**description：** 为网页定义描述语言
**keywords：** 为搜索引擎定义搜素关键字
**author：** 定义作者
**charset：** 字符集

```
<head>
<meta name="description" content="fuck">
<meta name="keywords" content="hello,world">
<meta name="author" content="hello">
<meta charset="UTF-8">
</head>
```

**\<link\>元素**

通常用于链接外部CSS

```
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

**\<script\>元素**

用于加载脚本

```
<script>
alert("hello,world");
</script>
```

**\<base\>元素**

描述了基本的链接地址/链接目标，该标签作为HTML文档中所有的链接标签的默认链接。

```
<head>
<base href="https://www.github.com" target="_blank">
</head>
<body>
<img src="images/stickman.gif" >
<a href="tags/tag_base.asp">HTML base Tag</a>
</body>
```

****

**\<body\>元素**

\<body\>元素定义了 HTML 文档的主体

```
<body>
</body>
```

**\<h\>元素**

作用：标题,范围\<h1\>~\<h6\>,\<h1最大\>,\<h6\>最小。

```
<body>
    <h1>一级标题</h1>
    <h2>二级标题</h2>
    <h3>三级标题</h3>
    <h4>四级标题</h4>
    <h5>五级标题</h5>
    <h6>六级标题</h6>
</body>
```

![image](https://user-images.githubusercontent.com/48900845/115442031-2197bb80-a244-11eb-9d61-b1879842c528.png)


**\<p\>元素**

作用：定义一个段落

```
<p>这是一个段落</p>
```

**\<br\>元素**

作用：换行，无关闭标签。

```
<br>
```

**\<a\>元素**

```
<a href="url">link text</a>
```

**\<img\>元素**

src为图片地址,alt为替换文本,当图片无法正常显示,将显示文本。

```
<img src="haha.jpg" alt="haha">
```

****

## \<td\>表格

**\<table\>元素**

表示表格

**\<tr\>元素**

表示行

**\<th\>元素**

表示表头

**\<td\>元素**

表示数据

```
<table border="1">
    <tr>
        <th>Header 1</th>
        <th>Header 2</th>
    </tr>
    <tr>
        <td>row 1, cell 1</td>
        <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>row 2, cell 1</td>
        <td>row 2, cell 2</td>
    </tr>
</table>
```
![image](https://user-images.githubusercontent.com/48900845/115448953-dd5ce900-a24c-11eb-8570-0128793b0db9.png)


****

****

****

## 属性

**class**

可以有多个

```
<p class="haha jiji"></p>
```

**id**

只能有一个

```
<p id="myId"><</p>
```

**style**

定义样式

```
<p style="color: red;">haha</p>
```

![image](https://user-images.githubusercontent.com/48900845/115447952-a9cd8f00-a24b-11eb-8b54-a4f0493af584.png)

**title**

提供一些额外信息

```
<p title="jiji">haha</p>
```

****
****

## CSS引用

**外部引用**

```
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

**内部引用**

```
<!DOCTYPE html>
<html>
<head>
<style>
body {background-color: powderblue;}
h1   {color: blue;}
p    {color: red;}
</style>
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

**内联**

```
<h1 style="color:blue;">A Blue Heading</h1>
<p style="color:red;">A red paragraph.</p>
```

****

## javaScript引用

javaScript脚本需位于<script></script>之间。
脚本可放至<head><body>
  
```
<script>
  alert("hello");
</script>
```

**外部引用**

**src为脚本位置**

```
<!DOCTYPE html>
<html>
<body>
<script src="myScript.js"></script>
</body>
</html>
```
