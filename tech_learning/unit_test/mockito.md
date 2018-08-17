# Mockito Learning Notes

1. Mock就是做一个假的object，对这个object里的方法的调用，都会被Mockito拦截，然后返回用户预设的行为。这样可以绕过需要从其它地方拿数据的地方，直接返回用户预设的数据，进行单元测试。
2. Mockito可以验证行为确实发生。
    ```java
    //Let's import Mockito statically so that the code looks clearer
    import static org.mockito.Mockito.*;
    //mock creation
    List mockedList = mock(List.class);
    //using mock object
    mockedList.add("one");
    mockedList.clear();
    //verification
    verify(mockedList).add("one");
    verify(mockedList).clear();
    ```
3. Mockito可以预设方法返回值，称为stubbing。如果这个方法没被stubbing，则默认返回null，0，false，空集合之类的。
    ```java
    //You can mock concrete classes, not just interfaces
    LinkedList mockedList = mock(LinkedList.class);
    //stubbing
    when(mockedList.get(0)).thenReturn("first");
    when(mockedList.get(1)).thenThrow(new RuntimeException());
    //following prints "first"
    System.out.println(mockedList.get(0));
    //following throws runtime exception
    System.out.println(mockedList.get(1));
    //following prints "null" because get(999) was not stubbed
    System.out.println(mockedList.get(999));
    ```
4. 可以利用Argument matchers使用一条语句为多种情况给出可能的返回值。
    ```java
    //stubbing using built-in anyInt() argument matcher
    when(mockedList.get(anyInt())).thenReturn("element");
    //stubbing using custom matcher (let's say isValid() returns your own matcher implementation):
    when(mockedList.contains(argThat(isValid()))).thenReturn("element");
    //following prints "element"
    System.out.println(mockedList.get(999));
    //you can also verify using an argument matcher
    verify(mockedList).get(anyInt());
    //argument matchers can also be written as Java 8 Lambdas
    verify(mockedList).add(argThat(someString -> someString.length() > 5));
    // 需要注意的是，如果使用Argument matchers，那么所有参数都必须由其提供。
    verify(mock).someMethod(anyInt(), anyString(), eq("third argument"));
    //above is correct - eq() is also an argument matcher
    verify(mock).someMethod(anyInt(), anyString(), "third argument");
    //above is incorrect - exception will be thrown because third argument is givenwithout an argument matcher.
    ```
5. 可以以多种形式验证方法被调用的次数。示例见ch4-Verifying exact number of invocations / at least x / never。
6. 可以使用InOrder object来验证调用发生的顺序。
    ```java
    // A. Single mock whose methods must be invoked in a particular order
    List singleMock = mock(List.class);
    //using a single mock
    singleMock.add("was added first");
    singleMock.add("was added second");
    //create an inOrder verifier for a single mock
    InOrder inOrder = inOrder(singleMock);
    //following will make sure that add is first called with "was added first, thenwith "was added second"
    inOrder.verify(singleMock).add("was added first");
    inOrder.verify(singleMock).add("was added second");
    // B. Multiple mocks that must be used in a particular order
    List firstMock = mock(List.class);
    List secondMock = mock(List.class);
    //using mocks
    firstMock.add("was called first");
    secondMock.add("was called second");
    //create inOrder object passing any mocks that need to be verified in order
    InOrder inOrder = inOrder(firstMock, secondMock);
    //following will make sure that firstMock was called before secondMock
    inOrder.verify(firstMock).add("was called first");
    inOrder.verify(secondMock).add("was called second");
    // Oh, and A + B can be mixed together at will
    ```
7. 有2种启用Mockito注解的方法。
    - 写个@Before(JUnit4)方法，里边调用MockitoAnnotations.initMocks(this)方法。
    ```java
    @Before public void initMocks() {
        MockitoAnnotations.initMocks(this);
    }
    ```
    - 可以直接使用built-in runner: MockitoJUnitRunner。
    ```java
    @RunWith(MockitoJUnitRunner.class)
    ```
8. 使用@Mock注解直接创建假对象。
    ```java
    public class ArticleManagerTest {
       @Mock private ArticleCalculator calculator;
       @Mock private ArticleDatabase database;
       @Mock private UserProvider userProvider;
       private ArticleManager manager;
    ```
9. 可以将结果设定串联起来。
    ```java
    when(mock.someMethod("some arg"))
    .thenThrow(new RuntimeException())
    .thenReturn("foo");
    //First call: throws runtime exception:
    mock.someMethod("some arg");
    //Second call: prints "foo"
    System.out.println(mock.someMethod("some arg"));
    //Any consecutive call: prints "foo" as well (last stubbing wins).
    System.out.println(mock.someMethod("some arg"));
    // 可以写到一起，达成简写的目的
    when(mock.someMethod("some arg")).thenReturn("one", "two", "three");
    // 这样写是不对的，只会被后边的two全部覆盖
    //All mock.someMethod("some arg") calls will return "two"
    when(mock.someMethod("some arg")).thenReturn("one")
    when(mock.someMethod("some arg")).thenReturn("two")
    ```
10. 当方法的返回值为空时，需要用do开头的方法，来设置动作。
    ```java
    doThrow(new RuntimeException()).when(mockedList).clear();
    //following throws RuntimeException:
    mockedList.clear();
    ```
11. 除直接造假Object之外，还可以监视真Object。拦截需要设置返回值的方法，让其余方法直接调用真方法。
    ```java
    List list = new LinkedList();
    List spy = spy(list);
    //optionally, you can stub out some methods:
    when(spy.size()).thenReturn(100);
    //using the spy calls *real* methods
    spy.add("one");
    spy.add("two");
    //prints "one" - the first element of a list
    System.out.println(spy.get(0));
    //size() method was stubbed - 100 is printed
    System.out.println(spy.size());
    // 于spy的对象上使用when来做假方法有时行不通，需使用doReturn等方法代替
    List list = new LinkedList();
    List spy = spy(list);
    //Impossible: real method is called so spy.get(0) throws    IndexOutOfBoundsException (the list is yet empty)
    when(spy.get(0)).thenReturn("foo");
    //You have to use doReturn() for stubbing
    doReturn("foo").when(spy).get(0);
    ```
