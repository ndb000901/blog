# springboot 入门



#  自动配置



# Web开发



## 拦截器

**MyInterceptor.java**

```java
public class MyInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("preHandle---->1");
        return true;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("postHandle---->1");
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("afterCompletion-->1");
    }
}

```

**WebConfig.java**

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new MyInterceptor())
                .addPathPatterns("/hello");
    }

}

```



## 自定义 Converter



**User.java**

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@ToString
public class User {
    private String id;
    private String name;
}

```



**MyConverter.java**

```java

public class UserConverter implements Converter<String,User> {
    @Override
    public User convert(String source) {
        if (source != null && !source.equals("")) {
            String[] data = source.split(";");
            if (data.length < 2) {
                return null;
            }
            return new User(data[0],data[1]);
        }
        return null;
    }

}

```

**WebConfig.java**

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addFormatters(FormatterRegistry registry) {
        UserConverter userConverter = new UserConverter();
        registry.addConverter(userConverter);
    }


}

```



## 内容协商



### xml依赖配置

**pom.xml**

```xml
 <dependency>
            <groupId>com.fasterxml.jackson.dataformat</groupId>
            <artifactId>jackson-dataformat-xml</artifactId>
</dependency>
```

### 开启请求参数内容协商模式



**application.yaml**

```yaml
spring:
  mvc:
    contentnegotiation:
      favor-parameter: true #开启请求参数内容协商模式
```

**请求实例**

```
http://127.0.0.1:8888/hello?format=xml
http://127.0.0.1:8888/hello?format=json
```

### 自定义 MessageConverter



**UserMessageConverter.java**

```java
public class UserMessageConverter implements HttpMessageConverter<User> {
    @Override
    public List<MediaType> getSupportedMediaTypes(Class<?> clazz) {
        return HttpMessageConverter.super.getSupportedMediaTypes(clazz);
    }

    @Override
    public boolean canRead(Class<?> clazz, MediaType mediaType) {
        return false;
    }

    @Override
    public boolean canWrite(Class<?> clazz, MediaType mediaType) {
        return clazz.isAssignableFrom(User.class);
    }

    @Override
    public List<MediaType> getSupportedMediaTypes() {
        return MediaType.parseMediaTypes("application/wuhen-code");
    }

    @Override
    public User read(Class<? extends User> clazz, HttpInputMessage inputMessage) throws IOException, HttpMessageNotReadableException {
        return null;
    }

    @Override
    public void write(User user, MediaType contentType, HttpOutputMessage outputMessage) throws IOException, HttpMessageNotWritableException {
        String data = user.getId() + "+" + user.getName();
        OutputStream body = outputMessage.getBody();
        body.write(data.getBytes(StandardCharsets.UTF_8));
    }
}

```

**WebConfig.java**

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {


    @Override
    public void extendMessageConverters(List<HttpMessageConverter<?>> converters) {
        converters.add(new UserMessageConverter());
    }

}

```



## 文件上传、下载



**file.html**

```html
<h1>file</h1>
    <form th:action="@{/upload}" enctype="multipart/form-data" method="post">
        <input type="file" name="photo">
        <input type="submit">
    </form>
```



**FileController.java**

```java
@Controller
public class FileController {


    @RequestMapping("/file")
    public String file() {
        return "file";
    }


    @RequestMapping("/upload")
    public void upload(@RequestPart("photo") MultipartFile photo) throws IOException {
        if (!photo.isEmpty()) {
            String path = "/home/hello/";
            String name = photo.getOriginalFilename();
            photo.transferTo(new File(path + name));
        }
    }
}
```

**Application.yaml**

```ymal
spring:
  servlet:
    multipart:
      enabled: true
      max-file-size: 100MB
      max-request-size: 100MB
```





## 异常处理





# 数据访问



## Mysql



### 配置



**pom.xml**

```xml
        <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.27</version>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.17</version>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-jdbc -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
            <version>2.5.6</version>
        </dependency>
```



## Redis



### 配置



**pom.xml**

```xml


        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-data-redis -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
            <version>2.5.6</version>
        </dependency>

```



## MyBatis



### 依赖

**pom.xml**

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis.spring.boot/mybatis-spring-boot-starter -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.2.0</version>
        </dependency>

        <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.27</version>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.17</version>
        </dependency>
```

### 配置



**src/main/resources/mybatis.xml**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <settings>
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>

</configuration>
```

**src/main/resources/mapper/UserDaoMapper.xml**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="xyz.wuhen.springboot.demo3.dao.UserDao">
    <select id="selectUserById" resultType="xyz.wuhen.springboot.demo3.bean.User">
        select * from user where id = #{id}
    </select>
</mapper>
```

**UserDao.java**

```java
@Mapper
public interface UserDao {
    User selectUserById(int id);
}

```

**UserDaoService.java**

```java
@Service
public class UserDaoService {
    @Autowired
    private UserDao userDao;

    public User selectUserById(int id) {
        return userDao.selectUserById(id);
    }
}

```



### 分页



**PageHelper(https://github.com/pagehelper/Mybatis-PageHelper/blob/master/wikis/zh/HowToUse.md)**

### 一级缓存



### 二级缓存





## MyBatis-Plus





# 原理



## 自定义starter



**参考demo(https://github.com/ndb000901/springboot-starter-hello)**



## 启动原理



### 启动过程

**构建springApplication**

**执行run方法**



### 源码分析



**SpringApplication.java**

```java
// 创建 SpringApplicatio
public SpringApplication(ResourceLoader resourceLoader, Class<?>... primarySources) {
		this.resourceLoader = resourceLoader;
		Assert.notNull(primarySources, "PrimarySources must not be null");
		this.primarySources = new LinkedHashSet<>(Arrays.asList(primarySources));
		// 判定当前应用的类型
    	this.webApplicationType = WebApplicationType.deduceFromClasspath();
		// bootstrappers：初始启动引导器（List<Bootstrapper>）：去spring.factories文件中找 org.springframework.boot.Bootstrapper
    	this.bootstrapRegistryInitializers = getBootstrapRegistryInitializersFromSpringFactories();
    	// 找ApplicationContextInitializer；去spring.factories找ApplicationContextInitializer 
    	//List<ApplicationContextInitializer<?>> initializers
		setInitializers((Collection) getSpringFactoriesInstances(ApplicationContextInitializer.class));

    	// 找 ApplicationListener；应用监听器。去spring.factories找 ApplicationListener
		// List<ApplicationListener<?>> listeners
		setListeners((Collection) getSpringFactoriesInstances(ApplicationListener.class));
		this.mainApplicationClass = deduceMainApplicationClass();
	}
```



**SpringApplication.java**

```java
// 运行 SpringApplication
public ConfigurableApplicationContext run(String... args) {
    	// 记录应用的启动时间
		StopWatch stopWatch = new StopWatch();
		stopWatch.start();
    	// 创建引导上下文（Context环境）
    	//createBootstrapContext()获取到所有之前的 bootstrappers 挨个执行 intitialize() 来完成对引导启动器上下文环境设置
    
		DefaultBootstrapContext bootstrapContext = createBootstrapContext();
		ConfigurableApplicationContext context = null;
    	// 让当前应用进入headless模式。java.awt.headless
		configureHeadlessProperty();
    
    	//获取所有RunListener（运行监听器）【为了方便所有Listener进行事件感知】
    
    	//getSpringFactoriesInstances 去spring.factories找SpringApplicationRunListener**.
		SpringApplicationRunListeners listeners = getRunListeners(args);
    	//遍历 SpringApplicationRunListener 调用 starting 方法；
		listeners.starting(bootstrapContext, this.mainApplicationClass);
		try {
            //保存命令行参数；ApplicationArguments
			ApplicationArguments applicationArguments = new DefaultApplicationArguments(args);
            //准备环境 prepareEnvironment（）
			ConfigurableEnvironment environment = prepareEnvironment(listeners, bootstrapContext, applicationArguments);
            //返回或者创建基础环境信息对象。StandardServletEnvironment
            //配置环境信息对象
            //读取所有的配置源的配置属性值
			configureIgnoreBeanInfo(environment);
			Banner printedBanner = printBanner(environment);

            
            //创建IOC容器（createApplicationContext（））
            context = createApplicationContext();
			context.setApplicationStartup(this.applicationStartup);
			//准备ApplicationContext IOC容器的基本信息prepareContext()
            prepareContext(bootstrapContext, context, environment, listeners, applicationArguments, printedBanner);
            
            // 刷新IOC容器。refreshContext
            // 创建容器中的所有组件（Spring注解）
			refreshContext(context);
            
            // 容器刷新完成后工作afterRefresh
			afterRefresh(context, applicationArguments);
            // 停止计时
			stopWatch.stop();
			if (this.logStartupInfo) {
				new StartupInfoLogger(this.mainApplicationClass).logStarted(getApplicationLog(), stopWatch);
			}
            
            // 所有监听器调用 listeners.started(context); 通知所有的监听器started
			listeners.started(context);
            
            // 调用所有runners；callRunners()
			// 获取容器中的ApplicationRunner
            // 获取容器中的CommandLineRunner
			// 合并所有runner并且按照@Order进行排序
			// 遍历所有的runner。调用 run方法
			// 如果以上有异常，调用Listener 的 failed
			callRunners(context, applicationArguments);
		}
		catch (Throwable ex) {
			handleRunFailure(context, ex, listeners);
			throw new IllegalStateException(ex);
		}

		try {
            // 调用所有监听器的running方法listeners.running(context); 通知所有的监听器 running 
  			// running如果有问题。继续通知failed。调用所有Listener的failed；通知所有的监听器 failed
			listeners.running(context);
		}
		catch (Throwable ex) {
			handleRunFailure(context, ex, null);
			throw new IllegalStateException(ex);
		}
		return context;
	}
```

