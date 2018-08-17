# Core Java Learning Notes

## Chapter 4

### 4.4 静态域与静态方法
1. 静态方法可直接通过类名调用。静态方法没有this隐式参数。
2. 需要使用静态方法的2种情况：
    - 一个方法不需要访问对象状态，其所需参数都是通过显式参数提供（例如： Math.pow)。
    - 一个方法只需要访问类的静态域（例如：Employee.getNextldh

### 4.6 对象构造
1. 初始化块。
    - 下面的例子中，首先运行初始化块，然后才运行构造器的主体部分。
    ![初始化块](https://ws1.sinaimg.cn/large/e2989da6ly1fsvd6eu1uqj20840btwfd.jpg)
    - 如果对类的静态域进行初始化的代码比较复杂，那么可以使用静态的初始化块。
    ![静态初始化块](https://ws1.sinaimg.cn/large/e2989da6ly1fsvd8dns0aj20cg0bp75r.jpg)