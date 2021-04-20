# html学习总结



## 一些元素

**注意：HTML对大小写不敏感**

**\<html\>元素**

```
```

**\<head\>元素**

```
```

**\<body\>元素**

```
```

**\<title\>元素**

```
```

**\<h\>元素**

作用：标题,范围\<h1\>~\<h6\>,\<h1最大\>,\<h6\>
```
```

**\<p\>元素**

作用：定义一个段落

```
<p>这是一个段落</p>
```

**\<br\>**

作用：换行，无关闭标签。

```
<br>
```

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
