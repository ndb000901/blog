## java处理json文件——gson

**1.实验环境**

>1.manjaro-21
>
>2.JDK1.8.0-281
>
>3.gson-2.8.6 [项目地址](https://github.com/google/gson)
>

**在Gradle/Android中使用**

```
dependencies {
    implementation 'com.google.code.gson:gson:2.8.6'
}
```

**在Maven中使用**

```
<dependencies>
    <!--  Gson: Java to Json conversion -->
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.8.6</version>
      <scope>compile</scope>
    </dependency>
</dependencies>
```

**2.将一个对象转为json字符串**

**MyJson.java**
```
public class MyJson {

    private String name;
    private int age;
    private String email;

    public MyJson() {

    }

    public MyJson(String name,int age,String email) {
        this.name = name;
        this.age = age;
        this.email = email;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public String getEmail() {
        return email;
    }
}

```

**Application.java**

```
import com.google.gson.Gson;

public class Application {
    public static void main(String[] args) {
        MyJson myJson = new MyJson("Tom",15,"haha@jiji.com");
        Gson gson = new Gson();
        String json = gson.toJson(myJson);
        System.out.println(json);
    }
}
```

输出结果

```
{"name":"Tom","age":15,"email":"haha@jiji.com"}
```

**3.将json字符串解析为java对象**

**Application.java**
```
import com.google.gson.Gson;

public class Application {
    public static void main(String[] args) {
        MyJson myJson = new MyJson();
        Gson gson = new Gson();
        String text = "{\"name\":\"Tom\",\"age\":19,\"email\":\"hello@jiba.com\"}";
        myJson = gson.fromJson(text,myJson.getClass());
        System.out.println(myJson.getName());
        System.out.println(myJson.getAge());
        System.out.println(myJson.getEmail());
    }
}
```

**输出结果**

```
Tom
19
hello@jiba.com
```

**4.将ArrayList转为json数组**

**Application.java**
```
import com.google.gson.Gson;

public class Application {
    public static void main(String[] args) {
        Gson gson = new Gson();
        ArrayList<MyJson> list = new ArrayList<>();
        list.add(new MyJson("name1",10,"ki@jiba.com"));
        list.add(new MyJson("name2",19,"hi@jiba.com"));
        String json = gson.toJson(list);
        System.out.println(json);
    }
}
```

**输出结果**

```
[{"name":"name1","age":10,"email":"ki@jiba.com"},{"name":"name2","age":19,"email":"hi@jiba.com"}]
```

**5.将json数组转为ArrayList**

**Application.java**
```
import com.google.gson.Gson;

public class Application {
    public static void main(String[] args) {
        Gson gson = new Gson();    
        ArrayList<MyJson> list = new ArrayList<>();
        Type listType = new TypeToken<List<MyJson>>(){}.getType();
        String text = "[{\"name\":\"name1\",\"age\":10,\"email\":\"ki@jiba.com\"},{\"name\":\"name2\",\"age\":19,\"email\":\"hi@jiba.com\"}]";
        list = gson.fromJson(text,listType);

        for (MyJson obj : list) {
            System.out.println(obj.getName());
            System.out.println(obj.getAge());
            System.out.println(obj.getEmail());
        }
    }
}

```

**输出结果**

```
name1
10
ki@jiba.com
name2
19
hi@jiba.com
```

**6.从文件流读取json数据转换为java对象**

**myJson.json**
```
[
  {
    "name": "name1",
    "age": 10,
    "email": "ki@jiba.com"
  },
  {
    "name": "name2",
    "age": 19,
    "email": "hi@jiba.com"
  }
]


```

**Application.java**
```
public class Application {
    public static void main(String[] args) throws IOException {
        ArrayList<MyJson> list = new ArrayList<>();
        Type listType = new TypeToken<List<MyJson>>(){}.getType();
        Gson gson = new Gson();
        File file = new File("/home/hello/myCode/java/json/gson/src/main/java/xyz/wuhen/gson/myJson.json");
        FileReader reader = new FileReader(file);
        list = gson.fromJson(reader,listType);
        for (MyJson obj : list) {
            System.out.println(obj.getName());
            System.out.println(obj.getAge());
            System.out.println(obj.getEmail());
        }
   }
}
```

**输出结果**

```
name1
10
ki@jiba.com
name2
19
hi@jiba.com
```

**7.从URL读取json数据字节流转为java对象**

**Application.java**
```
public class Application {
    public static void main(String[] args) throws IOException {
        ArrayList<MyJson> list = new ArrayList<>();
        Type listType = new TypeToken<List<MyJson>>(){}.getType();
        Gson gson = new Gson();
        URL url = new URL("http://127.0.0.1/myJson.json");
        JsonReader reader = new JsonReader(new InputStreamReader(url.openStream()));
        list = gson.fromJson(reader,listType);
        for (MyJson obj : list) {
            System.out.println(obj.getName());
            System.out.println(obj.getAge());
            System.out.println(obj.getEmail());
        }
    }
}
```

**输出结果**

```
name1
10
ki@jiba.com
name2
19
hi@jiba.com
```
