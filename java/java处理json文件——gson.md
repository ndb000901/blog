## java处理json文件——gson

**1.实验环境**

>1.manjaro-21
>
>2.JDK1.8.0-281
>
>3.gson-2.8.6 [项目地址](https://github.com/google/gson)
>

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

**3.**
