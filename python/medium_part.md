# Python Learning Notes

## 20180525
38. 列表的操作。
    - stuff是个list。stuff[-1]永远指向list中最后一个。
    - stuff是个list。'#'.join(stuff)。用#将整个list连接起来。
39. 字典。
    - 使用{}声明字典。字典与列表的最大区别。列表只能使用数字即索引取出元素。字典是使用key取出元素，而key几乎可是包括字符串与数字的任何东西。
    - 字典加东西可以直接用dic['key']='value'来往里加东西。
    ![字典加](https://ws1.sinaimg.cn/large/e2989da6ly1frqw9afihfj206u00oq2p.jpg)
    - 字典删东西使用del。
    ![dic删除](https://ws1.sinaimg.cn/large/e2989da6ly1frqwft3xurj203q01ddfl.jpg)
    - 字典的items()函数。for state, abbrev in states.items()。想遍历字典就的用这个方法。
    - 直接用['key']拿value时，如果key不存在，会报keyerror错误。
    - 字典的get()可以在没有的情况下返回默认值。state = states.get('Texas',默认值)。如不写默认值，则没有的情况下，默认为none。
40. 类。__init__(self)函数。每个函数都有入参self。
![类](https://ws1.sinaimg.cn/large/e2989da6ly1frr1piltirj20bu06o74a.jpg)
41. 面向对象术语。
    - string的strip('%')函数去除首尾中所有指定的字符。如没有入参，则默认去除首尾所有空格。
    ![首尾去除](https://ws1.sinaimg.cn/large/e2989da6ly1frr7b3mgevj20cl04j74d.jpg)
    - dict.keys()。字典(Dictionary) keys() 函数以列表返回一个字典所有的键。
    - random.shuffle (lst )。将序列的所有元素随机排序。
    - random.sample(c, 5)。在c这个list中，随机去除5个。
    - str.capitalize()。将字符串的第一个字母变成大写,其他字母变小写。对于 8 位字节编码需要根据本地环境。
    - random.randint(a, b)。Return a random integer N such that a <= N <= b。
    - str.replace(old, new[, max])。把字符串中的 old（旧字符串） 替换成 new(新字符串)，如果指定第三个参数max，则替换不超过 max 次。
    - list slicing。列表切片。就是list[1:4]，取出其中第1,2,3个的值。[:]就是全取出来，就是复制。

## 20180529
42. 对象及类。
    - class name(object)。为了支持旧类，创建新类时需要加object。
    - super(type[, object-or-type])这个用处就是用来调用父类方法。前边的type就是这个类自己。后边就是self。
    ![spex](https://ws1.sinaimg.cn/large/e2989da6ly1frs1eea2n0j2083044q2s.jpg)

## 20180601
43. 无。
44. 继承与合成。
    - 隐式继承。如果你将函数放到基类中（也就是这里的 Parent ），那么所有的子类（也就是 Child 这样的类）将会自动获得这些函数功能。如果你需要很多类的时候，这样可以让你避免重复写很多代码。
    - 显式覆盖。子类中相同的方法会覆盖父类。
    - 使用super调用父类方法。
    - 合成就是直接调用别的模块和类。

