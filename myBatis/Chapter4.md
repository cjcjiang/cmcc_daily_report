# MyBatis Learning

## Chapter4
### 20180518
1. if标签。
    - 在where中使用if。
    ![s-if1](https://ws1.sinaimg.cn/large/e2989da6ly1frfkekh7t7j20ok05cmy3.jpg)
    ![s-if2](https://ws1.sinaimg.cn/large/e2989da6ly1frfketl04dj20ie0590tp.jpg)
    - 在update中使用if。感觉if最大好处就是可以将所有与update和insert有关的sql全写进一个sql里。最后加id=id是为了防止拼接之后出错。
    ![up-if1](https://ws1.sinaimg.cn/large/e2989da6ly1frfkrqop7zj20lc0jptdh.jpg)
    ![up-if2](https://ws1.sinaimg.cn/large/e2989da6ly1frfks0nx8kj206s01uglj.jpg)
    - 在insert中使用if。
    ![in-if](https://ws1.sinaimg.cn/large/e2989da6ly1frfl2ybu79j20lc0cftbv.jpg)
2. choose标签。choose里有when和otherwise。
![choose](https://ws1.sinaimg.cn/large/e2989da6ly1frflxjxupmj20or0guq6h.jpg)
3. where标签。当if条件都不满足时，where元素中没有内容。当if条件满足时，where会自动去掉开头的and。
![where-1](https://ws1.sinaimg.cn/large/e2989da6ly1frfn5givmqj20ok06ygne.jpg)
![where-2](https://ws1.sinaimg.cn/large/e2989da6ly1frfn5p0kp7j20jg0723zw.jpg)
4. set标签。update时某些字段可能不存在更新。set会自动把最后一个字段后面的逗号去掉。但是set标签里如果是空的，即判断全部失败，还是不行，故必须准备id=#{id}这种必有项。
![set1](https://ws1.sinaimg.cn/large/e2989da6ly1friyt7s99rj20fc0b4mz3.jpg)
![set2](https://ws1.sinaimg.cn/large/e2989da6ly1friytizf2pj20ds04d74n.jpg)
5. where和set标签的底层实现就是trim标签。
    - where对应的trim。
    ![trim1](https://ws1.sinaimg.cn/large/e2989da6ly1friz2i9tfxj20c201vmx5.jpg)
    - set对应的trim。
    ![trim2](https://ws1.sinaimg.cn/large/e2989da6ly1friz2rrf0ej209r022q2v.jpg)
    - trim标签的属性。
    ![trim3](https://ws1.sinaimg.cn/large/e2989da6ly1friz2zdwrvj20he034my9.jpg)
6. foreach标签的使用。
    - foreach实现in集合。
        1. 例子。
        ![ea1](https://ws1.sinaimg.cn/large/e2989da6ly1frj0vjnjprj20ow0bk41c.jpg)
        ![ea2](https://ws1.sinaimg.cn/large/e2989da6ly1frj0vrjljxj204x01r3yd.jpg)
        2. 属性解析。
        ![属性](https://ws1.sinaimg.cn/large/e2989da6ly1frj0wm0yqcj20o707q0vi.jpg)
        3. collection里面其实应该填参数的名字，与多参时用来指定名字的@Param指定的名字相对应。单参时默认的名字是list和array。
    - foreach实现批量插入。
        1. 例子。
        ![exi](https://ws1.sinaimg.cn/large/e2989da6ly1frj2nm7z3bj20ly0algod.jpg)
    - foreach实现动态update。本身就没有批量update。
        1. 例子。
        ![upex](https://ws1.sinaimg.cn/large/e2989da6ly1frj38qzsccj20os06gmyg.jpg)
        2. DAO里的接口方法应传入Map。
        ![dqoMap](https://ws1.sinaimg.cn/large/e2989da6ly1frj39xeqz4j20e700vaa3.jpg)
        3. foreach标签里的index设为key。Map里的key对应数据库字段。value对应要更新的值。
7. bind标签的使用。使用OGNL表达式创建一个变量并将其绑定到上下文中。2个属性均必选。name为绑定到上下文的变量名。value为ONGL表达式。
![bind](https://ws1.sinaimg.cn/large/e2989da6ly1frj3sr00psj20kk03dgme.jpg)
8. 多数据库支持。详见书。
10. ONGL用法。有一种可以打印出映射xml中方法执行的参数。
![ongl](https://ws1.sinaimg.cn/large/e2989da6ly1frj92vbo7xj20ok016t8y.jpg)










