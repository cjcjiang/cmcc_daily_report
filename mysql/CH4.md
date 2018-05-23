# MySQL Learning Notes

## Chapter 3
### 20180523
1. USE crashcourse。SHOW DATABASES。SHOW TABLES。SHOW COLUMNS FROM customers。

## Chapter 4
### 20180523
1. DISTINCT
    - SELECT DISTINCT vend_id FROM products;只返回不同（唯一）的vend_id行。
    - 不能部分使用distinct，DISTINCT关键字应用于所有列而不仅是前置它的列。如果给出SELECT DISTINCT vend_id,prod_price，除非指定的两个列都不同，否则所有行都将被检索出来。
2. LIMIT
    - SELECT prod_name FROM products LIMIT 5;。LIMIT 5指示MySQL返回不多于5行。
    - SELECT prod_name FROM products LIMIT 3, 4;。从行3开始的4行，即取出4，5，6，7行中的数据。
    - SELECT prod_name FROM products LIMIT 4 OFFSET 3;。从行3开始的4行。

## Chapter 5
### 20180523
1. order by
    - 通常，ORDER BY子句中使用的列将是为显示所选择的列。但是，实际上并不一定要这样，用非检索的列排序数据是完全合法的。
    - select * from products order by prod_price, prod_name;。重要的是理解在按多个列排序时，排序完全按所规定的顺序进行。换句话说，对于上述例子中的输出，仅在多个行具有相同的prod_price值时才对产品按prod_name进行排序。如果prod_price列中所有的值都是唯一的，则不会按prod_name排序。
    - select * from products order by prod_price desc, prod_name;。DESC关键字只应用到直接位于其前面的列名。在上例中，只对prod_price列指定DESC，对prod_name列不指定。因此，prod_price列以降序排序，而prod_name列（在每个价格内）仍然按标准的升序排序。不指定的话，默认ASC升序。
