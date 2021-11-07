# springMVC使用



# 1、Hello World



## 依赖

**pom.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>springmvc-demo1</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>

    <dependencies>
        <!--lombok-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.22</version>
        </dependency>

        <!--SpringMVC-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.3.12</version>
        </dependency>

        <!--测试-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
        </dependency>

        <!--ServletAPI-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
        </dependency>

        <!--thymeleaf-->
        <dependency>
            <groupId>org.thymeleaf</groupId>
            <artifactId>thymeleaf-spring5</artifactId>
            <version>3.0.12.RELEASE</version>
        </dependency>
    </dependencies>

</project>
```





## xml配置



**src/main/webapp/WEB-INF/web.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceResponseEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>

    </filter-mapping>

    <!-- 配置SpringMVC的前端控制器，对浏览器发送的请求统一进行处理 -->
    <servlet>
        <servlet-name>springMVC</servlet-name>

        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!-- 通过初始化参数指定SpringMVC配置文件的位置和名称 -->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc.xml</param-value>
        </init-param>
        <!--
 		作为框架的核心组件，在启动过程中有大量的初始化操作要做
		而这些操作放在第一次请求时才执行会严重影响访问速度
		因此需要通过此标签将启动控制DispatcherServlet的初始化时间提前到服务器启动时
	    -->
        <load-on-startup>1</load-on-startup>

    </servlet>
    <servlet-mapping>
        <servlet-name>springMVC</servlet-name>
        <!--
        设置springMVC的核心控制器所能处理的请求的请求路径
        /所匹配的请求可以是/login或.html或.js或.css方式的请求路径
        但是/不能匹配.jsp请求路径的请求
        -->
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

**src/main/resources/springmvc.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!-- 自动扫描包 -->
    <context:component-scan base-package="xyz.wuhen.springmvc.demo1"></context:component-scan>

    <!-- 配置Thymeleaf视图解析器 -->
    <bean id="viewResolver" class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
        <property name="order" value="1"></property>
        <property name="characterEncoding" value="UTF-8"></property>
        <property name="templateEngine">
            <bean class="org.thymeleaf.spring5.SpringTemplateEngine">
                <property name="templateResolver">
                    <bean class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">
                        <!-- 视图前缀 -->
                        <property name="prefix" value="/WEB-INF/templates/"></property>
                        <!-- 视图后缀 -->
                        <property name="suffix" value=".html"></property>
                        <property name="templateMode" value="HTML5"></property>
                        <property name="characterEncoding" value="UTF-8"></property>
                    </bean>
                </property>
            </bean>
        </property>

    </bean>

    <!--
       处理静态资源，例如html、js、css、jpg
      若只设置该标签，则只能访问静态资源，其他请求则无法访问
      此时必须设置<mvc:annotation-driven/>解决问题
     -->
    <mvc:default-servlet-handler/>

    <!-- 开启mvc注解驱动 -->
    <mvc:annotation-driven>
        <mvc:message-converters>
            <!-- 处理响应中文内容乱码 -->
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                <property name="defaultCharset" value="UTF-8" />
                <property name="supportedMediaTypes">
                    <list>
                        <value>text/html</value>
                        <value>application/json</value>
                    </list>
                </property>
            </bean>
        </mvc:message-converters>
    </mvc:annotation-driven>
</beans>
```

## 注解配置





## 解决中文乱码



**src/main/resources/springmvc.xml**

```xml
<!-- 开启mvc注解驱动 -->
    <mvc:annotation-driven>
        <mvc:message-converters>
            <!-- 处理响应中文内容乱码 -->
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                <property name="defaultCharset" value="UTF-8" />
                <property name="supportedMediaTypes">
                    <list>
                        <value>text/html</value>
                        <value>application/json</value>
                    </list>
                </property>
            </bean>
        </mvc:message-converters>
    </mvc:annotation-driven>
</beans>
```

**src/main/webapp/WEB-INF/web.xml**

```xml
    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceResponseEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>

    </filter-mapping>
```

**tomcat配置文件server.xml**

```xml
    <Connector port="8080" URIEncoding="UTF-8" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```



# 2、@RequestMapping注解



## 使用位置



### 类

设置映射请求的请求路径的初始信息。

### 方法

设置映射请求请求路径的具体信息

## 属性



### value

设置一个或多个请求地址



### method

设置请求方法

满足value不满足method，报405错误

### params



| 表达式       | 说明                  |
| ------------ | --------------------- |
| param        | 必须存在param请求参数 |
| !param       | 不能存在param请求参数 |
| param=value  | param必须等于value    |
| param!=value | param必须不等于value  |

若满足method、value但不满足params，页面报400错误

### headers



通过请求头信息匹配请求映射

| 表达式        | 说明                     |
| ------------- | ------------------------ |
| header        | 必须存在header请求头信息 |
| !header       | 不能存在header请求头信息 |
| header=value  | header必须等于value      |
| header!=value | header必须不等于value    |

若满足value、method属性，但不满足headers属性，报404错误。



##  各种请求方式注解



### @GetMapping

### @PostMapping

### @PutMapping

### @DeleteMapping

### @PatchMapping



## Ant风格路径



| 标志 | 说明           |
| ---- | -------------- |
| ？   | 任意单个字符   |
| *    | 0个或多个字符  |
| **   | 任意一层或多层 |



**注意：在使用\*\*时，只能使用/\*\*/xxx方式**



## 路径占位符

```java
@RequestMapping("/test/{id}/{name}")
public String test(@PathVariable("id") String id,@PathVariable String name) {

}
```



# 3、SpringMVC获取请求参数



## 通过ServletAPI获取



##  通过控制器方法的形参获取请求参数



## @RequestParam



## @RequestHeader



## @CookieValue



## 通过POJO获取请求参数





# 4、域对象共享数据



## 使用servletAPI向request域对象共享数据



## 使用ModelAndView向request域对象共享数据



## 使用Model向request域对象共享数据



## 使用map向request域对象共享数据



## 使用ModelMap向request域对象共享数据



## 向session域共享数据



## 向application域共享数据



# 5、SpringMVC视图





# 6、HttpMessageConverter-->报文转换器







# 7、文件上传和下载



## 文件下载



## 文件上传



# 8、拦截器



# 9、异常处理器

## 基于xml配置异常处理



## 基于注解配置异常处理

