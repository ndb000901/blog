# spring5 使用

##  

# 1、Bean 管理



## 接口



**BeanFactory**

- IOC容器的基本实现，是spring内部的使用接口，不提供开发人员进行使用，加载配置文件时不会创建对象，在获取对象时才去创建对象。

**ApplicationContext**

- BeanFactory接口的子接口，提供更多更强大的功能，一般由开发人员进行使用。加载配置文件时进行创建对象。



## Bean作⽤域



| 作⽤域            | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| singleton（默认） | Spring IOC容器将单个bean定义绑定到单个对象实例。             |
| prototype         | 单个bean定义可以被绑定到多个对象实例                         |
| request           | 单个bean定义被绑定到单个的Http请求⽣命周期。就是每⼀次HTTP请求都有属于他⾃⼰的单独实例创建，这个只在web-aware的Spring ApplicationContext中有效。 |
| session           | 单个bean的定义会被绑定到Http Session的⽣命周期中，这个只在web-aware的SpringApplicationContext中有效。 |
| application       | 单个bean的定义会被绑定到ServletContext的⽣命周期中，这个只在web-aware的SpringApplicationContext中有效。 |
| websocket         | 单个bean的定义会被绑定到WebSocket的⽣命周期中，这个只在web-aware的Spring |
|                   |                                                              |







## xml方式



### demo1-->hello,world



**Application.java**

```java
public class Application {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");

        User user = (User)context.getBean("user");
        System.out.println();
    }
}
```

**bean1.xml**

```xml
    <bean id="user" class="xyz.wuhen.spring2.demo1.bean.User">
        <property name="name" value="haha"></property>
        <property name="age" value="11"></property>
    </bean>
```

**User.java**

```java
public class User {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

```

### demo2-->set、map、list、array...bean配置



**application.java**

```java
public class Application {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");

        Stu stu = (Stu)context.getBean("stu");
        System.out.println();
    }
}
```



**bean1.xml**

```xml
<bean id="stu" class="xyz.wuhen.spring2.demo1.bean.Stu">
        <!--数组-->
        <property name="strs">
            <array>
                <value>strs-->1</value>
                <value>strs-->2</value>
                <value>strs-->3</value>
            </array>
        </property>
        <!--Map-->
        <property name="map">
            <map>
                <entry key="map-->key1" value="map-->value1"></entry>
                <entry key="map-->key2" value="map-->value2"></entry>
                <entry key="map-->key3" value="map-->value3"></entry>
            </map>
        </property>
        <!--List-->
        <property name="list">
            <list>
                <value>list-->1</value>
                <value>list-->2</value>
                <value>list-->3</value>
                <value>list-->4</value>
            </list>
        </property>
        <!--Set-->
        <property name="set">
            <set>
                <value>set-->1</value>
                <value>set-->2</value>
                <value>set-->3</value>
            </set>
        </property>
    </bean>
```





**Stu.java**

```java
public class Stu {
    private String[] strs;
    private List<String> list;
    private Map<String,String> map;
    private Set<String> set;

    public String[] getStrs() {
        return strs;
    }

    public void setStrs(String[] strs) {
        this.strs = strs;
    }

    public List<String> getList() {
        return list;
    }

    public void setList(List<String> list) {
        this.list = list;
    }

    public Map<String, String> getMap() {
        return map;
    }

    public void setMap(Map<String, String> map) {
        this.map = map;
    }

    public Set<String> getSet() {
        return set;
    }

    public void setSet(Set<String> set) {
        this.set = set;
    }
}

```

### demo3--->c命名空间

使用构造函数



**bean.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="user" class="xyz.wuhen.spring2.demo1.bean.User" c:name="jaj" c:age="13">

    </bean>

</beans>
```



### demo4--->p命名空间

使用set方法

**bean1.xml**

```xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="user" class="xyz.wuhen.spring2.demo1.bean.User" p:name="jiji" p:age="12"></bean>


</beans>
```

**Application.java**

```java
public class Application {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        User user = context.getBean("user",User.class);
        System.out.println();
    }
}

```



**User.java**

```java
public class User {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

```



### demo5--->引入外部properties配置文件



**bean1.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                            http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <context:property-placeholder location="classpath:user.properties"/>
    <bean id="user" class="xyz.wuhen.spring2.demo1.bean.User">
        <property name="name" value="${user.name}"></property>
        <property name="age" value="${user.age}"></property>
    </bean>

</beans>
```

**User.java**

```java


public class User {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public User() {

    }
}

```

**user.properties**

```properties
user.name=haha123
user.age=110
```



## 注解方式



### 开启注解扫描

```xml
<context:component-scan base-package="xyz.wuhen.spring2.demo1.bean"></context:component-scan>
```



### 创建Bean

**@Component**

创建 bean 实例

**@Service**

创建 bean 实例

**@Repository**

创建 bean 实例

**@Controller**

创建 bean 实例

**@Configuration**

```java
@Configuration //作为配置类，替代 xml 配置文件
@ComponentScan(basePackages = {"xyz.wuhen"})
public class SpringConfig {
}
```

**@Bean**

作用在加了@Configuration配置类定义的方法上，创建Bean实例。

### 属性注入



**@Autowired：** 根据属性类型进行自动装配

**@Qualifier：**根据名称进行注入,这个@Qualifier 注解的使用，和上面@Autowired 一起使用

**@Resource：**可以根据类型注入，可以根据名称注入

**@Value：**注入普通类型属性



## Bean生命周期

- 1、构造函数
- 2、setName执行
- 3、setAge执行
- 4、postProcessBeforeInitialization
- 5、初始化函数
- 6、postProcessAfterInitialization
- 7、使用Bean
- 8、销毁函数



**bean1.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                            http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <context:property-placeholder location="classpath:user.properties"/>

    <context:component-scan base-package="xyz.wuhen.spring2.demo1"></context:component-scan>
    <bean id="user" class="xyz.wuhen.spring2.demo1.bean.User" init-method="init" destroy-method="destory">
        <property name="name" value="${user.name}"></property>
        <property name="age" value="${user.age}"></property>
    </bean>

</beans>
```

**MyBeanPost.java**

```java
@Component
public class MyBeanPost implements BeanPostProcessor {
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("postProcessBeforeInitialization");
        return bean;
    }

    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("postProcessAfterInitialization");
        return bean;
    }
}

```

**User.java**

```java
public class User {
    @Value("haha")
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        System.out.println("setName执行");
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        System.out.println("setAge执行");
        this.age = age;
    }

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public User() {
        System.out.println("构造函数");
    }

    public void init() {
        System.out.println("初始化函数");
    }
    public void destory() {
        System.out.println("销毁函数");
    }
}

```

**Application.java**

```java
public class Application {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");

        User user = context.getBean("user",User.class);
        ((ClassPathXmlApplicationContext) context).close();

        System.out.println();
    }
}

```



# 2、AOP 操作



## JDK 动态代理



**JDKProxy.java**

```java
public class JDKProxy {
    public static void main(String[] args) {
        Class[] interfaces = {UserDao.class};
        UserDaoImpl userDaoImpl = new UserDaoImpl();
        UserDao userDao = (UserDao) Proxy.newProxyInstance(JDKProxy.class.getClassLoader(),interfaces,new UserDaoProxy(userDaoImpl));
        int result = userDao.add(1,2);
        System.out.println("result: " + result);
    }

}

```

**UserDao.java**

```java
public interface UserDao {
    public int add(int a,int b);
    public String update(String id);

}

```

**UserDaoImpl.java**

```java
public class UserDaoImpl implements UserDao {
    public int add(int a, int b) {
        return a + b;
    }

    public String update(String id) {
        return id;
    }
}

```

**UserDaoProxy.java**

```java
// 创建代理对象
public class UserDaoProxy implements InvocationHandler {
    public Object obj;
    public UserDaoProxy(Object obj) {
        this.obj = obj;
    }
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("方法之前执行。。。。" + method.getName() + ": 传递的参数..." + Arrays.toString(args));
        Object res = method.invoke(obj,args);
        System.out.println("方法执行之后。。。" + obj);
        return res;
    }
}

```



## AOP术语



### 连接点-->类里面哪些方法可以被增强，这些方法被称为连接点



### 切入点-->实际被增强的方法



### 通知-->实际增强的逻辑部分



**前置通知**

```java
@Before(value = "execution....")
```



**后置通知**

```java
@AfterReturning(value = "execution...")
```



**环绕通知**

```java
@Around(value = "execution...")
```



**异常通知**

```java
@AfterThrowing(value = "execution...")
```



**最终通知**

```java
@After(value = "execution...")
```





### 切面-->把通知应用到切入点过程



### 切入点表达式



**作用：**指定对哪个类的哪个方法进行增强。

**语法结构：**execution(\[权限修饰符\]\[返回类型\]\[类全路径\]\[方法名称\]([参数列表])

```java
# 对add进行增强
execution(* xuz.wuhen.dao.BookDao.add(..))
# 对类中所有方法进行增强
execution(* xyz.wuhen.dao.BookDao.*(..))
# 对包中所有类的所有方法进行增强
execution(* xyz.wuhen.dao.*.*(..))
```





## 注解方式



**Application.java**

```java
public class Application {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);
        User user = context.getBean("user",User.class);
        user.add();

    }
}
```

**User.java**

```java
@Component()
public class User {
    public void add() {
        System.out.println("add.......");
    }
}
```

**UserProxy.java**

```java
@Component
@Aspect //生成代理对象
public class UserProxy {
    //前置通知
    @Before(value = "execution(* xyz.wuhen.spring2.demo3.User.add(..))")
    public void before() {
        System.out.println("before....");
    }

    // 后置通知
    @AfterReturning(value = "execution(* xyz.wuhen.spring2.demo3.User.add(..))")
    public void afterReturning() {
        System.out.println("afterReturning....");
    }

    // 环绕通知
    @Around(value = "execution(* xyz.wuhen.spring2.demo3.User.add(..))")
    public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("around..前.....");
        proceedingJoinPoint.proceed();
        System.out.println("around..后.....");
    }
    // 异常通知
    @AfterThrowing(value = "execution(* xyz.wuhen.spring2.demo3.User.add(..))")
    public void afterThrowing() {
        System.out.println("afterThrowing....");
    }

    // 最终通知
    @After(value = "execution(* xyz.wuhen.spring2.demo3.User.add(..))")
    public void after() {
        System.out.println("after.....");
    }
}

```

**MyConfig.java**

```java
@Configuration
@ComponentScan(basePackages = "xyz.wuhen.spring2.demo3.**")
@EnableAspectJAutoProxy(proxyTargetClass = true)
public class MyConfig {

}
```





## xml方式

**Application.java**

```java
public class Application {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        User user = context.getBean("user",User.class);
        user.add();
    }
}
```

**User.java**

```java
public class User {
    public void add() {
        System.out.println("add....");
    }
}
```

**UserProxy.java**

```java
public class UserProxy {
    // 前置通知
    public void before() {
        System.out.println("before....");
    }
    // 后置通知
    public void afterReturning() {
        System.out.println("afterReturning....");
    }
    // 异常通知
    public void afterThrowing() {
        System.out.println("afterThrowing....");
    }

    // 最终通知
    public void after() {
        System.out.println("after....");
    }
    // 环绕通知
    public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("around前....");
        proceedingJoinPoint.proceed();
        System.out.println("around后....");
    }
}

```



**bean.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                            http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                            http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">

    <context:property-placeholder location="classpath:user.properties"/>

    <context:component-scan base-package="xyz.wuhen.spring2.demo4"></context:component-scan>

    <aop:aspectj-autoproxy></aop:aspectj-autoproxy>

    <bean id="user" class="xyz.wuhen.spring2.demo4.User"></bean>
    <bean id="userProxy" class="xyz.wuhen.spring2.demo4.UserProxy"></bean>

    <aop:config>
        <aop:pointcut id="p" expression="execution(* xyz.wuhen.spring2.demo4.User.add(..))"/>
        <aop:aspect ref="userProxy">
            <aop:before method="before" pointcut-ref="p"></aop:before>
            <aop:after-returning method="afterReturning" pointcut-ref="p"></aop:after-returning>
            <aop:after method="after" pointcut-ref="p"></aop:after>
            <aop:around method="around" pointcut-ref="p" ></aop:around>
            <aop:after-throwing method="afterThrowing" pointcut-ref="p"></aop:after-throwing>


        </aop:aspect>

    </aop:config>


</beans>
```









# JdbcTemplate









# 事务操作







