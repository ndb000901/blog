# junit5注解


|注解|说明|
|----|----|
|@Test|表示方法是测试方法。但是与JUnit4的@Test不同，他的职责非常单一不能声明任何属性，拓展的测试将会由Jupiter提供额外测试|
|@ParameterizedTest |表示方法是参数化测试，下方会有详细介绍|
|@RepeatedTest |表示方法可重复执行，下方会有详细介绍|
|@DisplayName |为测试类或者测试方法设置展示名称|
|@BeforeEach |表示在每个单元测试之前执行|
|@AfterEach |表示在每个单元测试之后执行|
|@BeforeAll |表示在所有单元测试之前执行|
|@AfterAll |表示在所有单元测试之后执行|
|@Tag |表示单元测试类别，类似于JUnit4中的@Categories|
|@Disabled |表示测试类或测试方法不执行，类似于JUnit4中的@Ignore|
|@Timeout |表示测试方法运行如果超过了指定时间将会返回错误|
|@ExtendWith |为测试类或测试方法提供扩展类引用|
