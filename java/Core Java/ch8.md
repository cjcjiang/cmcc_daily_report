# Core Java Learning Notes

## Chapter 8 泛型
1. 类型变量使用大写形式，且比较短，这是很常见的。在Java库中，使用变量E表示集合的元素类型，K和V分别表示表的关键字与值的类型。T(需要时还可以用临近的字母U和S)表示“任意类型”。
![泛型例子](https://ws1.sinaimg.cn/large/e2989da6ly1ft3qknydzfj20gs08pabl.jpg)
2. 泛型方法。
    - 类型变量放在修饰符（这里是public static )的后面，返回类型的前面。泛型方法可以定义在普通类中，也可以定义在泛型类中。
    ![泛型方法](https://ws1.sinaimg.cn/large/e2989da6ly1ft3qzb73ejj209q04y0sx.jpg)
    - 当调用一个泛型方法时，在方法名前的尖括号中放人具体的类型。在这种情况（实际也是大多数情况）下，方法调用中可以省略<String>类型参数。编译器有足够的信息能够推断出所调用的方法。
    ![泛型方法调用1](https://ws1.sinaimg.cn/large/e2989da6ly1ft3qzn0geuj20e600vwej.jpg)
    ![泛型方法调用2](https://ws1.sinaimg.cn/large/e2989da6ly1ft3qzzzctjj20cf00tglm.jpg)
3. 类型变量的限定。
    - 设置限定的例子。
    ![类型变量限定](https://ws1.sinaimg.cn/large/e2989da6ly1ft3v2vl2flj20bn00nt8o.jpg)
    - T 和绑定类型可以是类，也可以是接口。一个类型变量或通配符可以有多个限定。限定类型用“&”分隔，而逗号用来分隔类型变量。限定中至多有一个类。如果用一个类作为限定，它必须是限定列表中的第一个。
    ![多个限定](https://ws1.sinaimg.cn/large/e2989da6ly1ft3v42w68pj207l00t0sm.jpg)
4. 泛型代码和虚拟机。
    - 类型擦除。无论何时定义一个泛型类型，虚拟机都自动提供了一个相应的原始类型（raw type)。没有限定用Object替换。有限定的话用限定中的第一个替换。切换限定：写成class Interval<T extends Serializable & Comparable>时， 原始类型用Serializable替换T, 而编译器在必要时要向Comparable插入强制类型转换。为了提高效率，应该将标签（tagging)接口（即没有方法的接口）放在边界列表的末尾。
    ![原始类型](https://ws1.sinaimg.cn/large/e2989da6ly1ft3w8u01mcj20hd0cp0uy.jpg)
    - 翻译泛型表达式。编译器把这个方法调用翻译为两条虚拟机指令。对原始方法Pair.getFirst 的调用。将返回的Object类型强制转换为Employee类型。
    ![翻译泛型](https://ws1.sinaimg.cn/large/e2989da6ly1ft3wcw98mij207q01e0ss.jpg)
    - 泛型方法同样应用类型擦除。为保持多态，编译器会生成桥方法。
    ![桥方法](https://ws1.sinaimg.cn/large/e2989da6ly1ft3woh6w0aj20dv00odfw.jpg)
    - 桥方法有时可能出现只有返回类型不同的情况。在虚拟机中，用参数类型和返回类型确定一个方法。因此，编译器可以产生两个仅返回类型不同的方法字节码，虚拟机能够正确地处理这一情况。
    ![仅返回类型不同](https://ws1.sinaimg.cn/large/e2989da6ly1ft3wqtimamj20hm01h0t2.jpg)
5. 使用泛型时的限制。
    - 不能用类型参数代替基本类型。因此，没有Pair<double>, 只有Pair<Double>。当然，其原因是类型擦除。擦除之后，Pair类含有Object类型的域，而Object不能存储double值。
    - 运行时进行类型查询，只会获得原始类型。为提醒这一风险，试图查询一个对象是否属于某个泛型类型时，倘若使用instanceof会得到一个编译器错误，如果使用强制类型转换会得到一个警告。同样的道理，getClass方法总是返回原始类型。
    ![泛型类型查询](https://ws1.sinaimg.cn/large/e2989da6ly1ftds0044thj20f1021weu.jpg)
    - 不能创建参数化类型数组。如果需要收集参数化类型对象，只有一种安全而有效的方法：使用ArrayList:ArrayList<Pair<String>>。
    - 不能实例化类型变量。
        1. 不能使用像new T(...)，new T[...]或T.class这样的表达式中的类型变量。下图中的构造器就是非法的。
        ![非法构造器](https://ws1.sinaimg.cn/large/e2989da6ly1ftdslowteej20cy00z0sq.jpg)
        2. 传统解决方法，通过反射调用Class.newInstance方法来构造泛型对象。
            - makePair工厂方法。
            ![工厂方法](https://ws1.sinaimg.cn/large/e2989da6ly1ftdsq2xxqsj20dp038jru.jpg)
            - makePair工厂方法调用方式。
            ![调用方式](https://ws1.sinaimg.cn/large/e2989da6ly1ftdsspcu4vj209q00saa0.jpg)
        3. JAVA SE8，lambda表达式解决办法。
            - makePair工厂方法。makePair方法接收一个Supplier<T>，这是一个函数式接口， 表示一个无参数而且返回类型为T的函数。
            ![se8工厂方法](https://ws1.sinaimg.cn/large/e2989da6ly1ftdt7x0zfaj20bk02ldg4.jpg)
            - makePair工厂方法调用方式。调用者提供一个构造器表达式。
            ![se8调用方式](https://ws1.sinaimg.cn/large/e2989da6ly1ftdt9tcos8j209k00xdfs.jpg)
    - 不能构造泛型数组。
    - 禁止使用带有类型变量的静态域和方法。
    - 既不能抛出也不能捕获泛型类对象。实际上，甚至泛型类扩展Throwable都是不合法的。
    - 可以利用泛型消除对受查异常的检查。
    - 类型擦除后引起的冲突。要想支持擦除的转换，就需要强行限制一个类或类型变量不能同时成为两个接口类型的子类，而这两个接口是同一接口的不同参数化。
    ![非法](https://ws1.sinaimg.cn/large/e2989da6ly1ftduxr2974j20d2026mxh.jpg)
6. 通配符类型。
    - 泛型类，pair类之间没有继承关系。无论S与T有什么联系，通常，Pair\<S>与Pair<T>没有什么联系。
    ![泛型类无继承](https://ws1.sinaimg.cn/large/e2989da6ly1ftjum2ryfrj20kv0dvwkl.jpg)
    - 完全没有继承关系意味着下面的方法调用无法实现，这很不方便。所以需要通配符来模拟继承关系。
    ```java
    public static void printBuddies(Pair<Employee> p) {}
    Pair<Manager> managerBudies = new Pair<>(ceo, cfo);
    printBuddies(managerBudies); //compile-time error
    ```
    - 使用通配符子类限定可以模拟继承关系。如下更改就可以实现上边方法的调用。
    ```java
    public static void printBuddies(Pair<? extends Employee> p) {}
    Pair<Manager> managerBudies = new Pair<>(ceo, cfo);
    printBuddies(managerBudies); //success
    ```
    ![通配符继承1](https://ws1.sinaimg.cn/large/e2989da6ly1ftjupaswagj20di01u74t.jpg)
    ![通配符继承2](https://ws1.sinaimg.cn/large/e2989da6ly1ftjupmpuj0j20fw0cwn2u.jpg)
    - 使用通配符子类限定时无法访问set方法，从而保护类内数据不被破坏。不能访问的原因是。不可能调用setFirst方法。编译器只知道需要某个Employee的子类型，但不知道具体是什么类型。因此它拒绝传递任何特定的类型。毕竟？不能用来匹配。使用getFirst就不存在这个问题，将getFirst的返回值赋给一个Employee的引用完全合法。
    ![无法调用set](https://ws1.sinaimg.cn/large/e2989da6ly1ftjuvyh7ccj20dh01zjrx.jpg)
    ![通配符子类限定的方法](https://ws1.sinaimg.cn/large/e2989da6ly1ftjux17eg0j207201fdfv.jpg)
    - 使用通配符超类限定时访问get方法只能取回object。原因是。编译器无法知道setFirst方法的具体类型，因此调用这个方法时不能接受类型为Employee或Object的参数。只能传递Manager类型的对象，或者某个子类型（如Executive）对象，从而保护数据不被破坏。如果调用getFirst，不能保证返回对象的类型，只能把它赋给一个Object。
    ![通配符超类限定](https://ws1.sinaimg.cn/large/e2989da6ly1ftjwjay15wj206j01h74a.jpg)
    - 无限定通配符。只能调用get，不能调用set方法。
    ![无限定通配符应用](https://ws1.sinaimg.cn/large/e2989da6ly1ftjwo5ntjtj20bt02mdg2.jpg)
    - 可以使用如下方法捕获通配符的类型。通配符捕获只有在有许多限制的情况下才是合法的。编译器必须能够确信通配符表达的是单个、确定的类型。例如，ArrayList<Pair<T>>中的T永远不能捕获ArrayList<Pair<?>>中的通配符。数组列表可以保存两个Pair<?>，分别针对?的不同类型。
    ![通配符捕获方法](https://ws1.sinaimg.cn/large/e2989da6ly1ftjww18414j209c03u0t0.jpg)
    ![通配符方法](https://ws1.sinaimg.cn/large/e2989da6ly1ftjwwj6mr6j20b800sq2w.jpg)
