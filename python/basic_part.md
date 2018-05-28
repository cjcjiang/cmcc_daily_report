# Python Learning Notes

## 20180515
0. python文档里的[, arg2]，表示这个传入参数是可选的。逗号是因为有这个参数时必须加逗号。
1. python2的print直接上双引号。无分号。
2. 注释是#。

## 20180516
3. print可以加个逗号，直接数学运算。

## 20180517
4. =给变量赋值，python用下划线。
5. 格式化字符串。双引号里加%，后面变量前面加%，多个变量可加空格。
![格式化字符串](https://ws1.sinaimg.cn/large/e2989da6ly1fre3n9xu00j20g60163yd.jpg)

## 20180518
6. 字符串和文本。
    - 格式化字符串中 %r 和 %s 不同。%r显示的信息会比%s更详细，会自动添加一些东西。
    - 会替换变量中的格式化字符串。
    ![变量格式](https://ws1.sinaimg.cn/large/e2989da6ly1frfasvnd8sj20h1033mx3.jpg)
    - 可以用加号连接2个变量内的字符串。
    ![变量加号](https://ws1.sinaimg.cn/large/e2989da6ly1frfaugmzooj20bc02mq2s.jpg)
7. 打印。
    - print "jiang" * 10。打印10次jiang，不换行。
    - print中的逗号相当于空格。当用逗号隔开上下2行print语句时，2行print语句被视为同一行，中间有空格，多用于要打印的字太多，1行装不下。
    ![打印逗号](https://ws1.sinaimg.cn/large/e2989da6ly1frfhrlejm7j20mq029weh.jpg)
8. %s和%r的区别。
9. 换行仍是"\n"。用3个引号把字符串圈起来，想打印多少打多少。
![三引号](https://ws1.sinaimg.cn/large/e2989da6ly1frfi2t7f18j20e703saa2.jpg)
10. \转义。\tTAB。\\反斜杠。\r回车。
11. raw_inpit()接收用户输入，返回string。input()函数会把输入的东西当做python代码进行处理，这么做会有安全问题，应该避开这个函数。

## 20180521
12. input("How old are you")里面的string是对输入者的提示。
13. from ... import ...引入模块。将参数变量argv解包的方法。argv是个字符串数组。第0个一定是这个脚本的文件名。故解包时，就算运行时只有一个入参，也会解出2个。
![argv解包](https://ws1.sinaimg.cn/large/e2989da6ly1fritalyavcj20ek02et8k.jpg)
14. 没啥好记的。
15. file=open(filename)打开文件，返回file object。file.read()读取file object里的内容。

## 20180522
16. 读写文件
    - 关于文件的命令。
    ![文件命令](https://ws1.sinaimg.cn/large/e2989da6ly1frk5ede3yhj20hw04tdgp.jpg)
    - open(filename, 'w')以写模式打开文件，会首先truncate()文件。
17. 更多文件操作。
    - exists(filename)文件存在返回true。from os.path import exists。
    - len(string)返回string这个字符串的长度。
    - open(filename).read()如果这样写不把file赋值给变量的话，call过read()之后，这个file会直接被关闭，就不能call文件的close()。
18. 定义函数。def function_name(arg1, arg2):。*args更像接收了一个数组。**args更像接收了一个dict。
19. python的参数传递既不是值传递也不是引用传递。而是passed by assignment。
    1. the parameter passed in is actually a reference to an object (but the reference is passed by value)
    2. some data types are mutable, but others aren't
    3. If you pass a mutable object into a method, the method gets a reference to that same object and you can mutate it to your heart's delight, but if you rebind the reference in the method, the outer scope will know nothing about it, and after you're done, the outer reference will still point at the original object.
    4. If you pass an immutable object to a method, you still can't rebind the outer reference, and you can't even mutate the object.
20. fp.seek(offset, from_what)。
    - where fp is the file pointer you're working with; offset means how many positions you will move; from_what defines your point of reference:
    - 0: means your reference point is the beginning of the file
    - 1: means your reference point is the current file position
    - 2: means your reference point is the end of the file
    - if omitted, from_what defaults to 0.
21. return返回返回值。
22. 无。
23. 无。

## 20180523
24. 函数多返回值。
    - python的函数是可以有多个返回值的。
    ![多返回值](https://ws1.sinaimg.cn/large/e2989da6ly1frl1nzg797j20b3049glj.jpg)
    - 多返回值函数可以直接应用于格式化字符串。
    ![多返回值格式化字符串](https://ws1.sinaimg.cn/large/e2989da6ly1frl2hn6yfrj20i900oa9v.jpg)
25. 零散知识点。
    - 函数里使用"""注释"""，注释就是文档注释。命令行中help(module.function)就可以查看这个函数的文档注释。
    ![文档注释](https://ws1.sinaimg.cn/large/e2989da6ly1frl24bsszwj20bc023glg.jpg)
    - string分割在python中依然是split(' ')。
    - 返回值可以返回函数。
    - sorted(string_array)对字符串数组进行排序。
    - string_array.pop(0)意思是取出字符串数组的第一个，并把其从数组中移除。-1是对最后一个操作。
    - import ex25是直接引入模块，想使用模块里的函数需要ex25.function()。from ex25 import *就是直接引入全部函数，这样就可以直接用这个函数，而不用ex25这个模块名。
26. 无。

## 20180524
27. 无。
28. 布尔运算先后顺序。
![布尔运算](https://ws1.sinaimg.cn/large/e2989da6ly1frm6p7mvdyj20rr0ixwfe.jpg)
29. if后面如果不缩进，会报intended block错。
30. 有if,elif和else。如果多个 elif 区块都是 True，Python 只会运行它碰到的是 True 的第一个区块，所以只有第一个为True的区块会被运行。
31. 1<x<10,x in range(1, 10)。
32. 循环和列表。
    - 中括号包起来的是列表list。
    ![列表](https://ws1.sinaimg.cn/large/e2989da6ly1frmoanmr42j207b01mdfn.jpg)
    - 列表可以使用append('i')来增加元素。
    - for number in the_count:是循环。the_count是列表。
    - for i in range(0,6):。i是从0到5。range(6)等价于range(0,6)。没有start的值的话，start默认就是0。
33. while i<6:循环while的写法。
34. 列表是0基。
35. 在很多类型的操作系统里，``exit(0)`` 可以中断某个程序，而其中的数字参数则用来表示程序是否是碰到错误而中断。 exit(1) 表示发生了错误，而 exit(0) 则表示程序是正常退出的。这和我们学的布尔逻辑 0==False 正好相反，不过你可以用不一样的数字表示不同的错误结果。比如你可以用 exit(100) 来表示另一种和 exit(2)` 或 exit(1) 不同的错误。
36. 无。
37. 一些关键字。
    - del。删除这个变量对内存中实际数值的引用。但是其它变量仍可引用这个内存中的数值。
    ![del](https://ws1.sinaimg.cn/large/e2989da6ly1frnd6kbyczj20nv03taab.jpg)
    - global。python与java的区别之一就是，python如果想在函数中使用全局变量，就需要使用global关键字。
    ![global](https://ws1.sinaimg.cn/large/e2989da6ly1frndcfxfonj20o707zwew.jpg)
    - with。用with打开的这种类似file的文件，在with代码块执行完成后，不管是否抛出异常，最后一定都会将file关闭。
    ![with](https://ws1.sinaimg.cn/large/e2989da6ly1frndrqzcrgj20ac01jwec.jpg)
    - yield。yield替代return在函数中的作用。yield返回的永远是一个生成器(generator)。生成器是一个object。生成器其实就是生成一个列表(可迭代的对象,iterable)，但是列表中的数据只能用一次。
        1. 关于yield的详细网址。http://pyzh.readthedocs.io/en/latest/the-python-yield-keyword-explained.html
        2. 列表生成器。是方括号。
        ![列表生成](https://ws1.sinaimg.cn/large/e2989da6ly1frnespce8cj20b402o746.jpg)
        3. 生成器。是圆括号。只在用时计算数值，节省内存。
        ![生成器](https://ws1.sinaimg.cn/large/e2989da6ly1frnetroq2dj20cm02gq2v.jpg)
        4. yield用法。yield不必要在代码块的结尾。因为yield不会中断这个代码块的执行。
        ![yield](https://ws1.sinaimg.cn/large/e2989da6ly1frnevncv1ij208203ea9z.jpg)
        ![yield在中间](https://ws1.sinaimg.cn/large/e2989da6ly1frneyi62edj208b055746.jpg)
        5. 当使用yield返回生成器object时，可以直接用生成器object的next()函数输出值。
        ![next输出值](https://ws1.sinaimg.cn/large/e2989da6ly1frnf0hy5qej20cy0aj74g.jpg)
    - as。








