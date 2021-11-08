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







## 解决中文乱码

**SpringMVC中处理编码的过滤器一定要配置到其他过滤器之前，否则无效。**

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

```java
    @RequestMapping(value = "/hello")
    @ResponseBody
    public String hello(HttpServletRequest request) {
        String name = request.getParameter("name");
        String id = request.getParameter("id");
        return "id-->" + id + "  name-->" + name;
    }
```





##  通过控制器方法的形参获取请求参数

```java
    @RequestMapping(value = "/hello")
    @ResponseBody
    public String hello(String id,String name) {
        System.out.println("id-->" + id + "  name-->" + name);
        return "id-->" + id + "  name-->" + name;
    }
```



## @RequestParam



| 属性         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| value        | 请求参数名                                                   |
| required     | 设置是否必须传输请求参数，若为true,必须携带value所指定参数，否则报错400 |
| defaultValue | 不论required何值，当value指定参数没有传输，使用defaultValue  |



```java
    @RequestMapping(value = "/hello")
    @ResponseBody
    public String hello(@RequestParam(value = "id") String id,@RequestParam(value = "name") String name) {
        System.out.println("id-->" + id + "  name-->" + name);
        return "id-->" + id + "  name-->" + name;
    }
```



## @RequestHeader

属性与@RequestParam一致

```java
    @RequestMapping(value = "/hello")
    @ResponseBody
    public String hello(@RequestHeader("Host") String host) {
        System.out.println("id-->" + host);
        return "id-->" + host;
    }
```



## @CookieValue

属性与@RequestParam一致

```java
    @RequestMapping(value = "/hello")
    @ResponseBody
    public String hello(@CookieValue("admin") String admin) {
        System.out.println("admin-->" + admin);
        return "admin-->" + admin;
    }
```



## 通过POJO获取请求参数

**User.java**

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private String name;
    private String id;
}
```



```java
    @RequestMapping(value = "/hello")
    @ResponseBody
    public String hello(User user) {
        System.out.println("id-->" + user.getId() + "  name-->" + user.getName());
        return "id-->" + user.getId() + "  name-->" + user.getName();
    }
```





# 4、域对象共享数据



## 使用servletAPI向request域对象共享数据

```java
    @RequestMapping(value = "/hello")
    public String hello(HttpServletRequest request) {
        request.setAttribute("name","world");
        System.out.println("ssss");
        return "hello";
    }
```



## 使用ModelAndView向request域对象共享数据

```java
    @RequestMapping(value = "/hello")
    public ModelAndView hello(HttpServletRequest request) {
        ModelAndView mav = new ModelAndView();
         /**
         * ModelAndView有Model和View的功能
         * Model主要用于向请求域共享数据
         * View主要用于设置视图，实现页面跳转
         */
        mav.addObject("name","jiji");
        mav.setViewName("hello");
        System.out.println("ssss");
        return mav;
    }
```



## 使用Model向request域对象共享数据

```java
        @RequestMapping(value = "/hello")
        public String hello(Model model) {
            model.addAttribute("name","haha");
            System.out.println("ssss");
            return "hello";
        }
```



## 使用map向request域对象共享数据

```java
        @RequestMapping(value = "/hello")
        public String hello(Map map) {
            map.put("name","haha");
            System.out.println("ssss");
            return "hello";
        }
```



## 使用ModelMap向request域对象共享数据

```java
        @RequestMapping(value = "/hello")
        public String hello(ModelMap modelMap) {
            modelMap.addAttribute("name","jiji");
            System.out.println("ssss");
            return "hello";
        }
```



## 向session域共享数据

```java
    @RequestMapping(value = "/hello")
    public String hello(HttpSession session) {
        session.setAttribute("name","jiji");
        System.out.println("ssss");
        return "hello";
    }
```



## 向application域共享数据

```java
    @RequestMapping(value = "/hello")
    public String hello(HttpSession session) {
        ServletContext application = session.getServletContext();
        application.setAttribute("name","haha");
        System.out.println("ssss");
        return "hello";
    }
```



# 5、SpringMVC视图



## ThymeleafView



## 转发视图



InternalResourceView

```java
    @RequestMapping(value = "/hello")
    public String hello() {
        return "forward:/haha";
    }
```



## 重定向视图--RedirectView

RedirectView

```java
    @RequestMapping(value = "/hello")
    public String hello() {
        return "redirect:/haha";
    }
```



## 视图控制器--view-controller

```xml
    <mvc:view-controller path="/test" view-name="hello"></mvc:view-controller>
```





# 6、HttpMessageConverter-->报文转换器



## @RequestBody

获取请求体

```java
    @RequestMapping(value = "/hello")
    public String hello(@RequestBody String body) {
        System.out.println(body);
        return "hello";
    }
```



## RequestEntity

```java
@RequestMapping(value = "/hello")
public String hello(RequestEntity<String> requestEntity) {
    System.out.println(requestEntity.getHeaders());
    System.out.println(requestEntity.getBody());
    return "hello";
}
```

## @ResponseBody

将方法返回值响应到响应报文。

## SpringMVC 处理json

 

**pom.xml**

```xml
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.13.0</version>

        </dependency>
```

```xml
<mvc:annotation-driven/>
```

## @RestController



等价于@Controller + @ResponseBody

## ResponseEntity



# 7、文件上传和下载

## 依赖

**pom.xml**

```xml
 <dependency>
            <groupId>commons-fileupload</groupId>
            <artifactId>commons-fileupload</artifactId>
            <version>1.4</version>
        </dependency>
```

## 配置



**springmvc.xml**

```xml
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver"></bean>

```

**file.html**

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<form th:action="@{/upload}" method="post" enctype="multipart/form-data">
    <input type="file" name="photo">
    <input type="submit">
</form>

</body>
</html>
```



## 文件下载



```java
    @RequestMapping("/download")
    public ResponseEntity<byte[]> download(HttpSession session) throws IOException {
        ServletContext servletContext = session.getServletContext();
        String realPath = servletContext.getRealPath("/img/1.png");
        InputStream is = new FileInputStream(realPath);
        byte[] bytes = new byte[is.available()];
        is.read(bytes);
        MultiValueMap<String,String> headers = new HttpHeaders();
        headers.add("Content-Disposition","attachment;filename=1.png");
        HttpStatus statusCode = HttpStatus.OK;
        ResponseEntity<byte[]> responseEntity = new ResponseEntity<byte[]>(bytes,headers,statusCode);
        is.close();
        return responseEntity;
    }

```



## 文件上传

```java
    @RequestMapping("/upload")
    public void upload(MultipartFile photo,HttpSession session) throws IOException {
        String name = photo.getOriginalFilename();
        String type = name.substring(name.lastIndexOf("."));
        name = UUID.randomUUID().toString() + type;

        ServletContext servletContext = session.getServletContext();
        String photoPath = servletContext.getRealPath("upload");
        File file = new File(photoPath);
        if (!file.exists()) {
            file.mkdir();
        }
        String finalPath = photoPath + File.separator + name;
        photo.transferTo(new File(finalPath));

    }

```



# 8、拦截器



## 拦截器配置

**springmvc.xml**

```xml
<bean id="myInterceptor" class="xyz.wuhen.springmvc.demo1.interceptor.MyInterceptor"></bean>
    <bean id="myInterceptor2" class="xyz.wuhen.springmvc.demo1.interceptor.MyInterceptor2"></bean>
    <bean id="myInterceptor3" class="xyz.wuhen.springmvc.demo1.interceptor.MyInterceptor3"></bean>
    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/hello"/>
<!--            <mvc:exclude-mapping path="/hello"/>-->
            <ref bean="myInterceptor"></ref>
        </mvc:interceptor>
        <mvc:interceptor>
            <mvc:mapping path="/hello"/>
            <ref bean="myInterceptor2"></ref>
        </mvc:interceptor>
        <mvc:interceptor>
            <mvc:mapping path="/hello"/>
            <ref bean="myInterceptor3"></ref>
        </mvc:interceptor>
    </mvc:interceptors>
```

**MyInterceptor.java**

```java
public class MyInterceptor implements HandlerInterceptor {
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("preHandle-->1");
        return true;
    }

    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("postHandle-->1");
    }

    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("afterCompletion-->1");
    }
}
```



## 拦截器的三个抽象方法

SpringMVC中的拦截器有三个抽象方法：

**preHandle：**控制器方法执行之前执行preHandle()，其boolean类型的返回值表示是否拦截或放行，返回true为放行，即调用控制器方法；返回false表示拦截，即不调用控制器方法。

**postHandle：**控制器方法执行之后执行postHandle()。

**afterComplation：**处理完视图和模型数据，渲染视图完毕之后执行afterComplation()。

## 多个拦截器的执行顺序

a>若每个拦截器的preHandle()都返回true

此时多个拦截器的执行顺序和拦截器在SpringMVC的配置文件的配置顺序有关：

preHandle()会按照配置的顺序执行，而postHandle()和afterComplation()会按照配置的反序执行

b>若某个拦截器的preHandle()返回了false

preHandle()返回false和它之前的拦截器的preHandle()都会执行，postHandle()都不执行，返回false的拦截器之前的拦截器的afterComplation()会执行



# 9、异常处理器

## 基于xml配置异常处理

SpringMVC提供了一个处理控制器方法执行过程中所出现的异常的接口：HandlerExceptionResolver

HandlerExceptionResolver接口的实现类有：DefaultHandlerExceptionResolver和SimpleMappingExceptionResolver

SpringMVC提供了自定义的异常处理器SimpleMappingExceptionResolver，使用方式:

```xml
<bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
    <property name="exceptionMappings">
        <props>
        	<!--
        		properties的键表示处理器方法执行过程中出现的异常
        		properties的值表示若出现指定异常时，设置一个新的视图名称，跳转到指定页面
        	-->
            <prop key="java.lang.ArithmeticException">error</prop>
        </props>
    </property>
    <!--
    	exceptionAttribute属性设置一个属性名，将出现的异常信息在请求域中进行共享
    -->
    <property name="exceptionAttribute" value="ex"></property>
</bean>
```



## 基于注解配置异常处理

**ExceptionController.java**

```java
@ControllerAdvice
public class ExceptionController {
    @ExceptionHandler(ArithmeticException.class)
    public void handleArithmeticException() {
        System.out.println("handleArithmeticException.....");
    }
}
```



# 10、全注解开发



**WebInit.java**

```java
public class WebInit extends AbstractAnnotationConfigDispatcherServletInitializer {

    /**
     * 指定spring的配置类
     * @return
     */
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }

    /**
     * 指定SpringMVC的配置类
     * @return
     */
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{MyWebConfig.class};
    }

    /**
     * 指定DispatcherServlet的映射规则，即url-pattern
     * @return
     */
    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }

    /**
     * 添加过滤器
     * @return
     */
    @Override
    protected Filter[] getServletFilters() {
        CharacterEncodingFilter encodingFilter = new CharacterEncodingFilter();
        encodingFilter.setEncoding("UTF-8");
        encodingFilter.setForceRequestEncoding(true);
        HiddenHttpMethodFilter hiddenHttpMethodFilter = new HiddenHttpMethodFilter();
        return new Filter[]{encodingFilter, hiddenHttpMethodFilter};
    }
}
```

**SpringConfig.java**

```java
@Configuration
public class SpringConfig {
}

```

**MyWebConfig.java**



```java

@Configuration

@ComponentScan(basePackages = "xyz.wuhen.springmvc.demo2.**")
@EnableWebMvc
public class MyWebConfig implements WebMvcConfigurer {


    //使用默认的servlet处理静态资源

    public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
        configurer.enable();
    }

    //配置文件上传解析器
    @Bean
    public CommonsMultipartResolver multipartResolver(){
        return new CommonsMultipartResolver();
    }

    //配置拦截器
    public void addInterceptors(InterceptorRegistry registry) {
        MyInterceptor myInterceptor = new MyInterceptor();
        registry.addInterceptor(myInterceptor).addPathPatterns("/hello");
    }
    //配置视图控制

    public void addViewControllers(ViewControllerRegistry registry) {
        registry.addViewController("/").setViewName("index");
    }

//    //配置异常映射
//    public void configureHandlerExceptionResolvers(List<HandlerExceptionResolver> resolvers) {
//        SimpleMappingExceptionResolver exceptionResolver = new SimpleMappingExceptionResolver();
//        Properties prop = new Properties();
//        prop.setProperty("java.lang.ArithmeticException", "error");
//        //设置异常映射
//        exceptionResolver.setExceptionMappings(prop);
//        //设置共享异常信息的键
//        exceptionResolver.setExceptionAttribute("ex");
//        resolvers.add(exceptionResolver);
//    }

    //配置生成模板解析器
    @Bean
    public ITemplateResolver templateResolver() {
        WebApplicationContext webApplicationContext = ContextLoader.getCurrentWebApplicationContext();
        // ServletContextTemplateResolver需要一个ServletContext作为构造参数，可通过WebApplicationContext 的方法获得
        ServletContextTemplateResolver templateResolver = new ServletContextTemplateResolver(
                webApplicationContext.getServletContext());
        templateResolver.setPrefix("/WEB-INF/templates/");
        templateResolver.setSuffix(".html");
        templateResolver.setCharacterEncoding("UTF-8");
        templateResolver.setTemplateMode(TemplateMode.HTML);
        return templateResolver;
    }

    //生成模板引擎并为模板引擎注入模板解析器
    @Bean
    public SpringTemplateEngine templateEngine(ITemplateResolver templateResolver) {
        SpringTemplateEngine templateEngine = new SpringTemplateEngine();
        templateEngine.setTemplateResolver(templateResolver);
        return templateEngine;
    }

    //生成视图解析器并未解析器注入模板引擎
    @Bean
    public ViewResolver viewResolver(SpringTemplateEngine templateEngine) {
        ThymeleafViewResolver viewResolver = new ThymeleafViewResolver();
        viewResolver.setCharacterEncoding("UTF-8");
        viewResolver.setTemplateEngine(templateEngine);
        return viewResolver;
    }



}

```

