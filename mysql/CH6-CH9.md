# MySQL Learning Notes

## Chapter 6
### 20180524
1. MySQL在执行匹配时默认不区分大小写，所以fuses与Fuses匹配。
2. select * from products where prod_price between 5 and 10;
3. select cust_id from customers where cust_email is null;。在匹配过滤或不匹配过滤时数据库不返回带null的行。因此，在过滤数据时，一定要验证返回数据中确实给出了被过滤列具有NULL的行。

## Chapter 7
### 20180524
1. select * from a where b = 4 and c = 5;可添加多条，每条前边一个and。
2. select * from a where b = 4 or c = 5;
3. AND优先于OR。故需使用()定义优先级。
4. select * from products where ven_id not in (1002, 1003);

## Chapter 8
### 20180524
1. like操作符后跟通配符组成的搜索模式。
2. %通配符代表搜索模式中给定位置的0个、1个或多个字符。
3. _通配符代表搜索模式中给定位置的1个字符。

## Chapter 9
### 20180524
1. REGEXP操作符后所跟的东西作为正则表达式处理。
    - select * from products where prod_name regexp '1000';只要prod_name中出现1000就会被拿出来。
    - select * from products where prod_name like '1000';只有完全匹配才会取出。比如prod_name是'JetPack 1000'就不会被选出来。
2. .是正则表达式语言中一个特殊的字符。它表示匹配任意一个字符，因此，1000和2000都匹配且返回。
3. 正则表达式默认不区分大小写。where prod_name regexp binary '.000'就区分大小写。

### 20180525
4. |为正则表达式的OR操作符。它表示匹配其中之一。1|2|3 Ton的意思是'1'或'2'或'3 ton'。
5. 正则表达式[123] Ton。[123]定义一组字符，它的意思是匹配1或2或3。
6. 字符集合也可以被否定。尽管[123]匹配字符1、2或3，但[^123]却匹配除这些字符外的任何东西。
7. 定义一个匹配的范围。[1-5]匹配1到5。[a-z]匹配任意字母字符。
8. 为了匹配特殊字符，必须用\\为前导。\\-表示查找-，\\.表示查找.。

### 20180528
9. 字符类见表。字符类匹配时外边还需要套一层中括号。
![字符类](https://ws1.sinaimg.cn/large/e2989da6ly1frr4pyur90j20hh0bhwg3.jpg)
10. 重复元字符只对其前边一个字符生效。
    - 重复元字符见表。
    ![重复元字符](https://ws1.sinaimg.cn/large/e2989da6ly1frr6e0fjh7j20gk06zt9a.jpg)
    - 例子。
    ![e1](https://ws1.sinaimg.cn/large/e2989da6ly1frr6f9rlemj20c606nglm.jpg)
    ![e2](https://ws1.sinaimg.cn/large/e2989da6ly1frr6fh1yrcj20an06g3yi.jpg)
11. 定位元字符见表。LIKE和REGEXP的不同在于，LIKE匹配整个串而REGEXP匹配子串。利用定位符，通过用^开始每个表达式，用$结束每个表达式，可以使REGEXP的作用与LIKE一样。
![定位](https://ws1.sinaimg.cn/large/e2989da6ly1frr6updaduj20d3063wen.jpg)
12. 使用SELECT来测试正则表达式。REGEXP检查总是返回0（没有匹配）或1（匹配）。可以用带文字串的REGEXP来测试表达式，并试验它们。这个例子显然将返回0（因为文本hello中没有数字）。select 'hello' regexp '[0-9]';。

