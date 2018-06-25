# Core Java Learning Notes

>20180625

## Chapter 6

### 6.3 lambda表达式
1. 如果可以推导出一个lambda表达式的参数类型，则可以忽略其类型。如果方法只有一个参数，且这个参数的类型可以推导得出，那么可以忽略小括号。
![忽略类型](https://ws1.sinaimg.cn/large/e2989da6ly1fsn7uo79baj20ct021aab.jpg)
![忽略小括号](https://ws1.sinaimg.cn/large/e2989da6ly1fsn7vr9h2jj20ed01wq3a.jpg)
2. lambda表达式的返回类型总是由上下文推导得出。
![la返回类型](https://ws1.sinaimg.cn/large/e2989da6ly1fsn7wqo26lj20do00t0sr.jpg)
3. 函数式接口。只能有一个抽象方法，但是可以有默认方法之类有实现过的方法的接口。需要这种接口时，可以提供一个lambda表达式。比如，comparator接口就是函数式接口。
![函数式接口例子](https://ws1.sinaimg.cn/large/e2989da6ly1fsn8pnab5fj20by01dglo.jpg)
4. 方法引用。已经有现成的方法可以完成想要传递到其他代码的某个动作。
    - "::"分割对象或类名和方法名。
    ![分割符](https://ws1.sinaimg.cn/large/e2989da6ly1fsnhglu9wwj207502s3yp.jpg)
    - 例子。
    ![方法引用例子](https://ws1.sinaimg.cn/large/e2989da6ly1fsnkhvrxpgj20q402t75h.jpg)
5. 构造器引用。
    - 就是方法引用中引用的方法是new，即构造器。
    ![构造引用1](https://ws1.sinaimg.cn/large/e2989da6ly1fsnodualkxj20c90210t3.jpg)
    - 让stream接口的toArray方法返回泛型类型T的数组。
    ![构造引用2](https://ws1.sinaimg.cn/large/e2989da6ly1fsnoid4j88j20a400rjrc.jpg)
6. lambda 表达式中捕获的变量必须实际上是最终变量(effectively final)。实际上的最终变量是指，这个变量初始化之后就不会再为它赋新值。非必须声明为final。但是lambda代码块外以及之内，此值都不能被改变，其实与被声明为final一样。
7. 使用lambda表达式的重点是延迟执行deferred execution)。之所以希望以后再执行代码，这有很多原因，如下图所示。
![延迟执行](https://ws1.sinaimg.cn/large/e2989da6ly1fsnoulxu4dj20jy04pq4h.jpg)
8. 常用的函数式接口。
![常用函数式接口](https://ws1.sinaimg.cn/large/e2989da6ly1fsnp3ycgh3j20pq0bd0y9.jpg)
9. 基本类型的函数式接口。
![基本类型](https://ws1.sinaimg.cn/large/e2989da6ly1fsnp62z80lj20nf0bhwig.jpg)
10. 编写需要传入lambda表达式的方法。
![例子](https://ws1.sinaimg.cn/large/e2989da6ly1fsnp7uk0qrj20cw04u74x.jpg)
11. 比较时不一定必须提供比较器。可以考虑用Comparator里提供的静态方法。
![comp静态方法](https://ws1.sinaimg.cn/large/e2989da6ly1fsnpm6219oj209e01xq35.jpg)
