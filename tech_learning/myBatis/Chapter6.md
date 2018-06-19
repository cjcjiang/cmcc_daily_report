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

### 20180615

6. 一对多映射，使用collection集合的嵌套结果映射。单层嵌套。
    - 情景：一个用户拥有多个角色。需要把所有角色存进同一个用户中。
    - 定义bean。SysUser中加SysRole这个对象的list作为属性。
    ![colbean](https://ws1.sinaimg.cn/large/e2989da6ly1fsbn5v3t8bj20bz05d74t.jpg)
    - resultMap。
    ![rsmcol](https://ws1.sinaimg.cn/large/e2989da6ly1fsbn6uzeagj20o904dta3.jpg)
    - sql语句。
    ![colsql](https://ws1.sinaimg.cn/large/e2989da6ly1fsbn7widfyj20ln0do782.jpg)
    - 上面sql语句会把一个用户的2个不同角色当做2条结果查回。mybatis会自动将其合并成一个对象中的2个角色对象。合并的根据是resultMap中配置的id标签。如果没有id标签，就会查看所有条目，全部一样才合并。
7. 一对多映射，使用collection集合的嵌套结果映射。2层嵌套。
    - 情景：一个用户拥有多个角色。需要把所有角色存进同一个用户中。同时一个角色还拥有多个权限，同角色的权限要存进同一个角色中。
    - 权限的resultMap。
    ![qxrsm](https://ws1.sinaimg.cn/large/e2989da6ly1fsbo6w72haj20ou03xabm.jpg)
    - 角色的bean定义中增加权限list。
    ![qxbean](https://ws1.sinaimg.cn/large/e2989da6ly1fsbo9bz0vwj20bf038wep.jpg)
    - 增加权限相关的嵌套resultMap。这个也可以在其它嵌套查询中单独使用。
    ![qxrsmqt](https://ws1.sinaimg.cn/large/e2989da6ly1fsboc0h3fsj20n2054jt3.jpg)
    - 这个增加权限相关的嵌套也可以在其它嵌套查询中单独使用。如下面的sql语句。
    ![单嵌sql1](https://ws1.sinaimg.cn/large/e2989da6ly1fsbojpjt5vj20os094mz1.jpg)
    ![单嵌sql2](https://ws1.sinaimg.cn/large/e2989da6ly1fsboke5sywj20jl03hjrz.jpg)
    - 将外层查找的resultMap里的嵌套换成带权限嵌套的resultMap。
    ![外层嵌套](https://ws1.sinaimg.cn/large/e2989da6ly1fsboevcbw6j20mt056dhb.jpg)
    - 查询的sql语句。
    ![双层嵌sql](https://ws1.sinaimg.cn/large/e2989da6ly1fsboh2yiddj20lp0hhjvl.jpg)
8. collection标签和association标签可以混合使用。
    - 情景：角色对象中的创建信息可以进一步抽象为对象（即于2张表中分开存储）。
    - 创建信息bean。
    ![创建信息bean](https://ws1.sinaimg.cn/large/e2989da6ly1fsbos1ni93j209j09o3z3.jpg)
    - 用创建信息bean替换角色对象中对应的字段。
    ![替换](https://ws1.sinaimg.cn/large/e2989da6ly1fsbperlxrbj20ao03o0sv.jpg)
    - 更改角色对象的resultMap的配置。
    ![更改1](https://ws1.sinaimg.cn/large/e2989da6ly1fsbpg2ijivj20lq077di2.jpg)
    ![更改2](https://ws1.sinaimg.cn/large/e2989da6ly1fsbpgblqrxj205t01lglj.jpg)
9. 一对多映射。将查询嵌套进collection集合。
    - 添加根据角色来选出权限的sql方法。
    ![选权限](https://ws1.sinaimg.cn/large/e2989da6ly1fsbpsap7zaj20ld05bq48.jpg)
    - 角色对象的resultMap中将选出权限的sql方法嵌套进来。
    ![角色套权限](https://ws1.sinaimg.cn/large/e2989da6ly1fsbptpxcd2j20ny07wgnh.jpg)
    - 查询角色的sql方法。
    ![角色sql方法](https://ws1.sinaimg.cn/large/e2989da6ly1fsbpuf5sw8j20og09rjtk.jpg)
    - 查询用户的resultMap。
    ![查用户](https://ws1.sinaimg.cn/large/e2989da6ly1fsbv442p2ej20oq062gnc.jpg)
    - 查用户的sql方法。
    ![用户sql](https://ws1.sinaimg.cn/large/e2989da6ly1fsbv4xz0xsj20og0ak407.jpg)
10. 鉴别器映射。
    - discriminator标签常用的两个属性。
    ![鉴别属性](https://ws1.sinaimg.cn/large/e2989da6ly1fsbvxdyjbsj20mc026gmf.jpg)
    - case标签包含的属性。
    ![case属性](https://ws1.sinaimg.cn/large/e2989da6ly1fsbw1ycx9tj20oy058tas.jpg)
    - 鉴别器例子。利用鉴别器选用最终使用的resultMap。
    ![鉴别器例](https://ws1.sinaimg.cn/large/e2989da6ly1fsbw2vrczqj20ll05cjt0.jpg)
    - 取出角色对象，带禁用状态。
    ![禁用sql1](https://ws1.sinaimg.cn/large/e2989da6ly1fsbw7ia9omj20ow03w0tj.jpg)
    ![禁用sql2](https://ws1.sinaimg.cn/large/e2989da6ly1fsbw7qgjy9j20ht04fdgf.jpg)
