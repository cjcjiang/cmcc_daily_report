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
