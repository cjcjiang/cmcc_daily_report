# Junit5 learning notes
1. junit5的3个子项目。
    - JUnit Platform。主要提供TestEngine API。
    - JUnit Jupiter。提供了一个TestEngine实现类，用于运行j5测试。
    - JUnit Vintage。提供了一个TestEngine实现类，用于运行j3和j4测试。
2. 所有的核心注解都位于junit-jupiter-api模块的 org.junit.jupiter.api 包中。被@Test、@TestTemplate、@RepeatedTest、@BeforeAll、@AfterAll、@BeforeEach 或 @AfterEach 注解标注的方法不可以有返回值。
![注解1](https://ws1.sinaimg.cn/large/e2989da6ly1fqz3sbbsuaj20t80jsgob.jpg)
![注解2](https://ws1.sinaimg.cn/large/e2989da6ly1fqz3tlgkphj20sm0iowhg.jpg)
![注解3](https://ws1.sinaimg.cn/large/e2989da6ly1fqz3uidcdcj20so0j6adi.jpg)
![注解4](https://ws1.sinaimg.cn/large/e2989da6ly1fqz3vav17ij20t009m0u0.jpg)
3. 可以自定义注解，用来避免@Tag("fast")的多次使用。自定义后即可使用@Fast。
4. 所有的JUnit Jupiter断言都是 org.junit.jupiter.Assertions 类中static方法。
5. 可以使用第三方断言库。
6. 所有的JUnit Jupiter假设都是 org.junit.jupiter.Assumptions 类中的静态方法。
7. 条件化测试。@Disable;  @EnabledOnOs; @DisabledOnOs; @EnabledOnJre; @DisabledOnJre; @EnabledIfSystemProperty; @DisabledIfSystemProperty; @EnabledIfEnvironmentVariable; @DisabledIfEnvironmentVariable。
8. 可以用@Tag("fast")标记测试。
9. 测试实例生命周期。
    - 测试实例默认生命周期为per-method，即为在执行每个测试方法执行之前创建一个新的实例。
    - 测试类上加上注解@TestInstance(Lifecycle.PER_CLASS)，这样就会在同一个实例上执行所有的测试方法。使用了"per-class"模式之后，你就可以在非静态方法和接口的default方法上声明@BeforeAll和 @AfterAll。因此，"per-class"模式使得在@Nested测试类中使用@BeforeAll和@AfterAll注解成为了可能。
    - 使用JUnit Platform配置文件来设置默认的测试实例生命周期模式的方法。在类路径的根目录（例如，src/test/resources）中创建一个名为junit-platform.properties的文件，并写入以下内容。junit.jupiter.testinstance.lifecycle.default = per_class。
10. 嵌套测试什么用处没懂。
11. JUnit Jupiter一个主要的改变是：允许给测试类的构造函数和方法传入参数。这带来了更大的灵活性，并且可以在构造函数和方法上使用依赖注入。
    - 三种被自动注册的内置解析器。
        1. TestInfoParameterResolver。如果一个方法参数的类型是 TestInfo，TestInfoParameterResolver将根据当前的测试提供一个TestInfo的实例用于填充参数的值。然后，TestInfo就可以被用来检索关于当前测试的信息，例如：显示名称、测试类、测试方法或相关的Tag。显示名称要么是一个类似于测试类或测试方法的技术名称，要么是一个通过@DisplayName配置的自定义名称。
        2. RepetitionInfoParameterResolver。如果一个位于@RepeatedTest、@BeforeEach或者@AfterEach方法的参数的类型是 RepetitionInfo，RepetitionInfoParameterResolver会提供一个RepetitionInfo实例。然后，RepetitionInfo就可以被用来检索对应@RepeatedTest方法的当前重复以及总重复次数等相关信息。
        3. TestReporterParameterResolver。如果一个方法参数的类型是 TestReporter，TestReporterParameterResolver会提供一个TestReporter实例。然后，TestReporter就可以被用来发布有关当前测试运行的其他数据。这些数据可以通过 TestExecutionListener 的reportingEntryPublished()方法来消费，因此可以被IDE查看或包含在报告中。在JUnit Jupiter中，你应该使用TestReporter来代替你在JUnit 4中打印信息到stdout或stderr的习惯。使用@RunWith(JUnitPlatform.class)会将报告的所有条目都输出到stdout中。
        4. 其他的参数解析器必须通过@ExtendWith注册合适的扩展来明确地开启。
        



