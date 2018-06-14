# MyBatis Learning Notes

## Chapter6

### 20180614

1. 一对一关系。直接在sql语句中将值绑定到对象上。
    - 情景：一个用户拥有一个角色。
    - 定义bean。SysUser中加SysRole这个对象作为属性。
    ![对属1](https://ws1.sinaimg.cn/large/e2989da6ly1fsaqxzwe2uj207o01ndft.jpg)
    ![对属2](https://ws1.sinaimg.cn/large/e2989da6ly1fsaqy7eoz7j20c60cdwfn.jpg)
    - sql语句中直接将值绑定到SysRole这个对象内。需要绑定到对象的列的别名需要用双引号括起来。
    ![sql1](https://ws1.sinaimg.cn/large/e2989da6ly1fsar1suxzoj20iq0cggo4.jpg)
    ![sql2](https://ws1.sinaimg.cn/large/e2989da6ly1fsar20nnirj20hu0570tr.jpg)
2. 一对一关系。使用resultMap将值绑定到对象上。
    - 情景与bean定义与1相同。
    - 配置resultMap。property中有role.的前缀。
    ![rsmap](https://ws1.sinaimg.cn/large/e2989da6ly1fsarew555ej20n50czq83.jpg)
    - sql语句。
    ![rsmsql1](https://ws1.sinaimg.cn/large/e2989da6ly1fsarl3iy5lj20kp04n754.jpg)
    ![rsmsql2](https://ws1.sinaimg.cn/large/e2989da6ly1fsarl8sxpdj20hj09xmz2.jpg)
    - resultMap可以继承。
    ![rsm继承1](https://ws1.sinaimg.cn/large/e2989da6ly1fsarmsqjflj20jh04l767.jpg)
    ![rsm继承2](https://ws1.sinaimg.cn/large/e2989da6ly1fsarn1ku4xj20lt028gm5.jpg)
3. 使用resultMap的association标签配置一对一映射。
    - association标签包含的属性。
    ![aso属性](https://ws1.sinaimg.cn/large/e2989da6ly1fsasneokrwj20ot05bgnw.jpg)
    - 情景与bean定义与1相同。
    - 将roleMap单独写出去。
    ![rolemap](https://ws1.sinaimg.cn/large/e2989da6ly1fsasskgsr2j20ov058jto.jpg)
    - 直接在association中指定resultMap。
    ![rsma](https://ws1.sinaimg.cn/large/e2989da6ly1fsasu0cua9j20ma03swfq.jpg)
4. association标签内嵌套查询
    - association标签内的嵌套查询常用的属性。
    ![嵌查常用属](https://ws1.sinaimg.cn/large/e2989da6ly1fsauec6q01j20oy051tbt.jpg)
    - 带association标签的resultMap。
    ![rsmaqc1](https://ws1.sinaimg.cn/large/e2989da6ly1fsauh01vpuj20ie02daar.jpg)
    ![rsmaqc2](https://ws1.sinaimg.cn/large/e2989da6ly1fsauh92cxwj20ms01f74j.jpg)
    - 主sql方法。
    ![主sql](https://ws1.sinaimg.cn/large/e2989da6ly1fsay7rxck7j20od0aoacb.jpg)
    - 嵌套的sql方法。传入参数是在association标签内的column属性配置的。配置多个参数用逗号隔开即可。
    ![嵌套sql](https://ws1.sinaimg.cn/large/e2989da6ly1fsay962t30j20gp02fmxl.jpg)
    - 开启延迟查询首先要将association标签内的fetchType属性配置为lazy。
    ![延迟lazy](https://ws1.sinaimg.cn/large/e2989da6ly1fsay9y3qh5j20oi05djt0.jpg)
    - 开启延迟查询第二步需要将Mybatis全局配置中的aggressiveLazyLoading配置为false。
    ![延迟false](https://ws1.sinaimg.cn/large/e2989da6ly1fsayawcbmhj20jf030q3h.jpg)
    - 在和spring集成时，要确保只能在service层调用延迟加载的属性。当结果从service层返回至controller层时，如果获取延迟加载的属性值，会因为SqlSession已经关闭而抛出异常。
5. 如需在定义为延迟加载后，需要立刻加载数据。当lazyLoadTriggerMethods参数为默认值时。调用这个对象的equals，clone，hashCode和toString方法就可以立刻加载全部数据。
