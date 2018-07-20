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
4. 
