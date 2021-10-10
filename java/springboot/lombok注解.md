# lombok注解

## @Data

**注解在类上：**

提供类所有属性的get和set方法，此外还提供了equals、canEqual、hashCode、toString 方法。


## @Setter

@Setter

**注解在属性：**

为单个属性提供set方法

**注解在类上：**

为该类所有的属性提供set方法


## @Getter

**注解在属性上：**

为单个属性提供get方法

**注解在类上：**

为该类所有的属性提供get方法

## @Log4j

**注解在类上：**

为类提供一个属性名为log的log4j日志对象

## @AllArgsConstructor

**注解在类上：**

为类提供一个全参的构造方法，加了这个注解后，类中不提供默认构造方法了。

## @NoArgsConstructor

**注解在类上：**

为类提供一个无参的构造方法。

## @EqualsAndHashCode

**注解在类上：**

可以生成 equals、canEqual、hashCode 方法。

## @NonNull

**注解在属性上：**

会自动产生一个关于此参数的非空检查，如果参数为空，则抛出一个空指针异常

## @Cleanup

**这个注解用在变量前面：**

可以保证此变量代表的资源会被自动关闭，默认是调用资源的 close() 方法，如果该资源有其它关闭方法，可使用 @Cleanup(“methodName”) 来指定要调用的方法

## @ToString

**这个注解用在类上：**

可以生成所有参数的toString方法

## @RequiredArgsConstructor

**用在类上：**

使用类中所有带有@NonNull注解的或者带有final修饰的成员变量生成对应的构造方法。

## @Value

**这个注解用在类上：**

会生成含所有参数的构造方法，get方法，此外还提供了equals、hashCode、toString 方法

## @SneakyThrows

**这个注解用在方法上：**

可以将方法中的代码用try-catch语句包裹起来，捕获异常并在catch中用 Lombok.sneakyThrow(e) 把异常抛出，可以使用 @SneakyThrows(Exception.class) 的形式指定抛出哪种异常，也会生成默认的构造方法。

## @Synchronized

**这个注解用在类方法或者实例方法上：**

效果和 synchronized 关键字相同，区别在于锁对象不同，对于类方法和实例方法，synchronized 关键字的锁对象分别是类的 class 对象和 this 对象，而 @Synchronized 的锁对象分别是 私有静态 final 对象 lock 和 私有 final 对象 lock，当然，也可以自己指定锁对象，此外也提供默认的构造方法。
