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


