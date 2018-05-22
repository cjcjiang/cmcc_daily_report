# Python Learning

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






