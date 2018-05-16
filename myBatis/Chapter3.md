# MyBatis Learning

## Chapter3
### 20180516
1. 直接将sql语句写进DAO接口。坏处是每次改动语句，都得重新编译代码。
2. @Select注解。参数可是字符串数组，也可是字符串。
![select1](https://ws1.sinaimg.cn/large/e2989da6ly1frd11he4lij20gh04laav.jpg)
![select2](https://ws1.sinaimg.cn/large/e2989da6ly1frd11pwg7dj20gn04qmxz.jpg)
3. 处理属性字段映射。
    - 直接在sql语句中使用别名。
    - 使用@Results注解。
    ![Results注解](https://ws1.sinaimg.cn/large/e2989da6ly1frd1a8k9kjj20kf05kmyp.jpg)
    - MyBatis 3.3.1后可重复使用定义好的@Results。即加id。
    ![rt-id](https://ws1.sinaimg.cn/large/e2989da6ly1frd1bztrszj20io03cgm2.jpg)
    ![复用1](https://ws1.sinaimg.cn/large/e2989da6ly1frd1cw799mj209b010wef.jpg)
    ![复用2](https://ws1.sinaimg.cn/large/e2989da6ly1frd1d1bt8dj20be01ndg1.jpg)
4. @Insert时返回主键。
    - 返回自增主键。
    ![返回自增](https://ws1.sinaimg.cn/large/e2989da6ly1frd6kxugsbj20os04gwg5.jpg)
    - 返回非自增主键。
    ![返回非自增](https://ws1.sinaimg.cn/large/e2989da6ly1frd6q23q2uj20or06n76e.jpg)
5. @Update注解。
![update](https://ws1.sinaimg.cn/large/e2989da6ly1frd6vzksxhj20l006o0u9.jpg)
6. @Delete注解。
![delete](https://ws1.sinaimg.cn/large/e2989da6ly1frd6wnpdgzj20gm01kweq.jpg)
7. 使用带provider的注解。
    - 提供sql语句的类。
    ![p类1](https://ws1.sinaimg.cn/large/e2989da6ly1frd842hk23j20jt09v40a.jpg)
    ![p类2](https://ws1.sinaimg.cn/large/e2989da6ly1frd84b0uv7j20is03adgl.jpg)
    - DAO接口类。
    ![接口类](https://ws1.sinaimg.cn/large/e2989da6ly1frd87212zoj20nz01t0t7.jpg)








