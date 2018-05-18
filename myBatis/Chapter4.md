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










