## java解析html文件——Jsoup

**1.实验环境**

>1.manjaro-gonme21
>
>2.Jsoup-1.13.1 [项目地址](https://github.com/jhy/jsoup)
>
>3.JDK-1.8.0_281
>

**Maven使用Jsoup**

```
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.13.1</version>
</dependency>
```


**Gradle使用Jsoup**

```
implementation 'org.jsoup:jsoup:1.13.1'
```

**2.从String解析html**

将String解析为Document对象

**Application.java**

```
public class Application {

    public static void main(String[] args) throws IOException {
        String html = "<html>\n" +
                "<head>\n" +
                "<title>Try jsoup</title>\n" +
                "</head>\n" +
                "<body>\n" +
                "<p>This is <a href=\"http://jsoup.org/\">jsoup</a>.</p>\n" +
                "</body>\n" +
                "</html>";
        Document document = Jsoup.parse(html);
        System.out.println(document);
    }
}
```

**输出结果**

```
<html> 
 <head> 
  <title>Try jsoup</title> 
 </head> 
 <body> 
  <p>This is <a href="http://jsoup.org/">jsoup</a>.</p>  
 </body>
</html>
```

**3.从文件流解析html**

```
```

**4.从网络数据流解析html**

```
```
