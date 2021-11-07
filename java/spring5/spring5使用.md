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



**pom.xml**

```xml
<dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.10</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aspects</artifactId>
            <version>5.3.10</version>
        </dependency>

        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.8.RC1</version>
        </dependency>

        <dependency>
            <groupId>aopalliance</groupId>
            <artifactId>aopalliance</artifactId>
            <version>1.0</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/net.sourceforge.cglib/com.springsource.net.sf.cglib -->
        <dependency>
            <groupId>net.sourceforge.cglib</groupId>
            <artifactId>com.springsource.net.sf.cglib</artifactId>
            <version>2.2.0</version>
        </dependency>

    </dependencies>
```





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



**相同切入点抽取**

```java
// 相同切入点抽取
@Pointcut(value = "execution(* xyz.wuhen.spring2.demo4.User.add(..))")
public void haha() {
    
}
// 前置通知
// @Before 注解表示作为前置通知
@Before(value = "haha()")
public void before() {
    System.out.println("before....");
}
```





## xml方式

**pom.xml**

```xml
<dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.10</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aspects</artifactId>
            <version>5.3.10</version>
        </dependency>

        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.8.RC1</version>
        </dependency>

        <dependency>
            <groupId>aopalliance</groupId>
            <artifactId>aopalliance</artifactId>
            <version>1.0</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/net.sourceforge.cglib/com.springsource.net.sf.cglib -->
        <dependency>
            <groupId>net.sourceforge.cglib</groupId>
            <artifactId>com.springsource.net.sf.cglib</artifactId>
            <version>2.2.0</version>
        </dependency>

    </dependencies>
```





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

## 依赖

```xml
		<!--数据库。。。。。-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.8</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.27</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.3.12</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-orm</artifactId>
            <version>5.3.12</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-tx</artifactId>
            <version>5.3.12</version>
        </dependency>
        <dependency>
          <groupId>org.projectlombok</groupId>
          <artifactId>lombok</artifactId>
          <version>1.18.22</version>
        </dependency>
```

## 表结构

```sql
create table test.user
(
    id    bigint auto_increment comment '主键ID'
        primary key,
    name  varchar(30) null comment '姓名',
    age   int         null comment '年龄',
    email varchar(50) null comment '邮箱'
);
```



## 注解模式

### 配置

**MyConfig.java**

```java
@Configuration
@ComponentScan(basePackages = "xyz.wuhen.spring2.demo5.**")
public class MyConfig {
    @Bean
    public DataSource dataSource() {
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setUrl("jdbc:mysql://127.0.0.1:3306/test");
        dataSource.setUsername("root");
        dataSource.setPassword("root");
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        return dataSource;
    }
    @Bean
    public JdbcTemplate jdbcTemplate(DataSource dataSource) {
        JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
        return jdbcTemplate;
    }

}

```

**User.java**

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@ToString

public class User {
    private int id;
    private String name;
    private int age;
    private String email;
}

```

###  查询多个

**Application.java**

```java
public class Application {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);
        JdbcTemplate jdbcTemplate = (JdbcTemplate) context.getBean("jdbcTemplate",JdbcTemplate.class);
        String sql = "select * from user";
        List<User> list = jdbcTemplate.query(sql,new BeanPropertyRowMapper<User>(User.class));
        System.out.println();
    }
}
```

### 修改

```java
        String sql = "update user set name = 'jone1' where id = ?";
        Object[] objs = {Integer.valueOf(1)};
        int result = jdbcTemplate.update(sql,objs);
        System.out.println(result);
```



### 删除

```java
        String sql = "delete from user where id = ?";
        Object[] objs = {Integer.valueOf(1)};
        int result = jdbcTemplate.update(sql,objs);
        System.out.println(result);
```



### 插入

```java
        String sql = "insert into user(name,age,email) values(?,?,?)";
        Object[] objs = {"jiji",Integer.valueOf(15),"jiji@qq.com"};
        int result = jdbcTemplate.update(sql,objs);
        System.out.println(result);
```



### 查询行数



```java
        String sql = "select count(*) from user";
        int result = jdbcTemplate.queryForObject(sql,Integer.class);
        System.out.println(result);
```

### 插入多行

```java
        String sql = "insert into user(name,age,email) values (?,?,?)";
        List<Object[]> batchArgs = new LinkedList<Object[]>();
        Object[] objs1 = {"haha1",Integer.valueOf(12),"haha1@qq.com"};
        Object[] objs2 = {"haha2",Integer.valueOf(13),"haha2@qq.com"};
        Object[] objs3 = {"haha3",Integer.valueOf(14),"haha3@qq.com"};
        batchArgs.add(objs1);
        batchArgs.add(objs2);
        batchArgs.add(objs3);
        int[] result = jdbcTemplate.batchUpdate(sql,batchArgs);
        System.out.println(Arrays.toString(result));
```





##  xml配置



### 配置

```java
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

    <context:component-scan base-package="xyz.wuhen.spring2.demo5"></context:component-scan>

    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"></property>
        <property name="username" value="root"></property>
        <property name="password" value="root"></property>
        <property name="url" value="jdbc:mysql://127.0.0.1:3306/test"></property>
    </bean>
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="dataSource"></property>
    </bean>


</beans>
```



# 事务操作



## 依赖

**pom.xml**

```xml
		<!--数据库。。。。。-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.8</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.27</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.3.12</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-orm</artifactId>
            <version>5.3.12</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-tx</artifactId>
            <version>5.3.12</version>
        </dependency>
        <dependency>
          <groupId>org.projectlombok</groupId>
          <artifactId>lombok</artifactId>
          <version>1.18.22</version>
        </dependency>
```

## propagation-->事务传播行为



| 传播属性      | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| REQUIRED      | 如果有事务在运行，当前方法就在这个事务内运行，否则，就启动一个新的事务，并在自己的事务内运行。 |
| REQUIRES_NEW  | 当前的方法必须启动新事务，并在自己的事务内运行，如果有事务正在运行，应该将它挂起。 |
| SUPPORTS      | 如果有事务正在运行，当前的方法就在这个事务内运行，否则他可以不运行在事务中。 |
| MANDATORY     | 当前的方法必须运行在事务中，如果没有正在运行的事务，就抛出异常。 |
| NOT_SUPPORTED | 当前的方法不应该运行在事务内部，如果有运行的事务，将它挂起。 |
| NEVER         | 当前的方法不应该运行在事务中，如果有运行的事务，就抛出异常。 |
| NESTED        | 如果有事务在运行，当前方法就应该在这个事务的嵌套事务内运行，否则，就启动一个新的事务，并在它自己的事务内运行。 |

## 并发事务问题



### 脏读

读取了其他并发事务未提交的事务。

### 不可重复读

读取了其他并发事务已提交的数据。针对update、delete。

### 幻读

读取了其他并发事务提交的数据，针对insert。



## 隔离级别



### READ UNCOMMITTED(读未提交)



### READ COMMITTED(读已提交)



### REPEATABLE READ(可重复读)



### SERIALIZABLE(串行化)



| 。。。                     | 脏读 | 不可重复读 | 幻读 |
| -------------------------- | ---- | ---------- | ---- |
| READ UNCOMMITTED(读未提交) | Y    | Y          | Y    |
| READ COMMITTED(读已提交)   |      | Y          | Y    |
| REPEATABLE READ(可重复读)  |      |            | Y    |
| SERIALIZABLE(串行化)       |      |            |      |





## 注解模式



###  @Transactional属性



| 属性          | 说明                                   |
| ------------- | -------------------------------------- |
| timeout       | 超过指定时间不提交，进行回滚，单位秒。 |
| readOnly      | true-->只可查询，false-->可查可写      |
| rollbackFor   | 出现哪些异常进行回滚                   |
| noRollbackFor | 出现哪些异常不进行回滚                 |
| isolation     | 隔离级别                               |



**User.java**

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@ToString

public class User {
    private int id;
    private String name;
    private int age;
    private String email;
}

```

**UserDao.java**

```java
public interface UserDao {
    User selectUserById(Integer id);
    int updateUserById(User user);
}

```

**UserDaoImpl.java**

```java
@Repository

public class UserDaoImpl implements UserDao {
    @Autowired
    private JdbcTemplate jdbcTemplate;

    public User selectUserById(Integer id) {
        String sql = "select * from user where id = ?";
        User user = jdbcTemplate.queryForObject(sql,new BeanPropertyRowMapper<User>(User.class),id);
        return user;
    }


    public int updateUserById(User user) {
        String sql = "update user set age = ? where id = ?";
        Object[] args = {user.getAge(),user.getId()};
        int result = jdbcTemplate.update(sql,args);
        return result;
    }
}

```

**MyConfig.java**

```java
@Configuration
@ComponentScan(basePackages = "xyz.wuhen.spring2.demo6.**")
@EnableTransactionManagement
public class MyConfig {
    @Bean
    public DataSource dataSource() {
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setUrl("jdbc:mysql://127.0.0.1:3306/test");
        dataSource.setUsername("root");
        dataSource.setPassword("root");
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        return dataSource;
    }
    @Bean
    public JdbcTemplate jdbcTemplate(DataSource dataSource) {
        JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
        return jdbcTemplate;
    }
    @Bean
    public DataSourceTransactionManager dataSourceTransactionManager(DataSource dataSource) {
        DataSourceTransactionManager dataSourceTransactionManager = new DataSourceTransactionManager();
        dataSourceTransactionManager.setDataSource(dataSource);
        return dataSourceTransactionManager;
    }
}

```





**Application.java**

```java
public class Application {


    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);
        UserService userService = context.getBean("userService",UserService.class);
        User user = new User();
        user.setAge(510);
        user.setId(4);
        userService.updateUserById(user);
        System.out.println(userService.selectUserById(4));
    }
}

```



## xml模式



**bean.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                            http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                            http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
                            http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">

    <context:property-placeholder location="classpath:user.properties"/>

    <context:component-scan base-package="xyz.wuhen.spring2.demo6"></context:component-scan>

    <!--开启事务注解-->
    <tx:annotation-driven transaction-manager="transactionManager"></tx:annotation-driven>
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"></property>
        <property name="username" value="root"></property>
        <property name="password" value="root"></property>
        <property name="url" value="jdbc:mysql://127.0.0.1:3306/test"></property>
    </bean>
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="dataSource"></property>
    </bean>

    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <bean id="userDao" class="xyz.wuhen.spring2.demo6.dao.impl.UserDaoImpl">
        <property name="jdbcTemplate" ref="jdbcTemplate"></property>
    </bean>
    <bean id="userService" class="xyz.wuhen.spring2.demo6.service.UserService">
        <property name="userDao" ref="userDao"></property>
    </bean>

    <tx:advice id="txadvice">
        <tx:attributes>
            <tx:method name="updateUserById" propagation="REQUIRED"/>
        </tx:attributes>
    </tx:advice>

    <aop:config>
        <aop:pointcut id="pt" expression="execution(* xyz.wuhen.spring2.demo6.dao.impl.UserDaoImpl.updateUserById(..))"/>
        <aop:advisor advice-ref="txadvice" pointcut-ref="pt"></aop:advisor>
    </aop:config>

    <aop:aspectj-autoproxy></aop:aspectj-autoproxy>


</beans>
```





