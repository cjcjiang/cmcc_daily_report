# Learn Pythoin the Hard Way Notes

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

## 20180611
45. 无。
46. 无。
47. dict.update(dict2)。把字典dict2的键/值对更新到dict里。

## 20180612
48. 更复杂的用户输入。
    - 元组。用圆括号括起来。所有东西都跟list一样。只是创建之后就不能进行更改。
    ![元组](https://ws1.sinaimg.cn/large/e2989da6ly1fs8ig6huicj20de00xjr6.jpg)
    - 异常处理。
    ![异常处理](https://ws1.sinaimg.cn/large/e2989da6ly1fs8ikc083nj208i04da9y.jpg)
49. 创建句子。
    - 自定义异常。
    ![自定义](https://ws1.sinaimg.cn/large/e2989da6ly1fs8jjiunkmj20b201ndfn.jpg)
    - 抛出异常。
    ![抛出](https://ws1.sinaimg.cn/large/e2989da6ly1fs8jk2o0rvj20g100la9v.jpg)
    - 使用assert_raises(exception,callable,parameters)于nose单元测试中测试是否正确抛出异常。
53. 基本命令行。
    - pwd。打印工作目录。即用户当前所在目录。
    - cd ~。返回home路径。
    - mkdir。创建目录。目录名带空格需要用双引号括起来。
    - cd。更改目录。cd ..。返回上一层。cd ../../..。返回上3层。cd -返回前一个目录。
    - ls。列出目录下的内容。ls -lr。列出的带权限大小日期啥的。
    - rmdir john。john为目录名。
    - pushd,popd,dirs。
        1. pushd：切换到作为参数的目录，并把原目录和当前目录压入到一个虚拟的栈中。如果不指定参数，则会回到前一个目录，并把栈中最近的两个目录作交换。popd： 弹出栈中最近的目录。dirs: 列出当前栈中保存的目录列表。
        2. 说明: dirs的 -p参数可以每行一个目录的形式显示栈中的目录列表。-v参数可以在目录前加上编号。注意:有 -v时，不添加 -p也可以每行一个目录的形式显示。
        3. 说明之二:我们可以看到:最近压入栈的目录位于最上面。
        4. 在多个目录之间切换。用 pushd +n即可。说明:n是一个数字,有此参数时，是切换到栈中的第n个目录,并把此目录以栈循环的方式推到栈的顶部。需要注意: 栈从第0个开始数起。
    - touch。创建空文件。
    - cp a.txt b.txt。把a复制成b。cp -r a b。复制文件夹。
    - mv a b。将a移动成(重命名为)b。
    - less a.txt。查看文件a的内容。会有分页。
    - cat a.txt。查看文件a的内容。不会有分页。
    - rm a.txt。删除文件。rm -rf newplace。强制删除newplace。rm is command to remove/delete stuff. -rf is two options joined together: -r for recursive removal ( typically used with directories) and -f to force the action。
