---
title: 第二章
description:
toc: true
authors: []
date: 2021-07-01T18:16:42+08:00
lastmod: 2021-07-01T18:16:42+08:00
draft: false
weight: 2
---

# 单表数据检索

<!--more-->

> ！注意！子句是有顺序的，语序错误会导致语法错误。
>
> SELECT -> FROM ->  WHERE -> ORDER BY ->  LIMIT



## 2.1 选择子句

SELECT 是列/字段选择语句，可选择列，列间数学表达式，特定值或文本，可用AS关键字设置列别名（AS可省略）。

~~~sql
SELECT 
	last_name, 
    first_name, 
    points, 
    points * 10 + 100 AS 'discount factor'
FROM customers
~~~

### 【练习】

单价涨价10%作为新单价

~~~sql
USE sql_store;
SELECT 
	name,
    unit_price,
    unit_price * 1.1 AS new_price
FROM products
~~~



## 2.2 WHERE 子句

WHERE 是行筛选条件，实际是一行一行/一条条记录依次验证是否符合条件，进行筛选

~~~sql
SELECT *
FROM customers
WHERE points > 3000
~~~

###  2.2.1 比较运算符
- \>
- <
- =
- \>=
- <=
- != 或 <>


### 【练习】

SQL语句中的日期是字符串，需要用 ‘ ’。

~~~sql
SELECT * 
FROM orders
WHERE order_date >= '2018-01-01'
~~~



## 2.3 逻辑运算符 AND OR NOT 

```sql
SELECT *
FROM order_items
WHERE order_id = 6 AND (quantity * unit_price) > 30 
```

**AND优先级高于OR，但最好加括号，更清晰**

```sql
WHERE birth_date > '1990-01-01' OR 
      (points > 1000 AND state = 'VA')
```

NOT的用法：

```sql
WHERE NOT (birth_date > '1990-01-01' OR points > 1000)
```

上述代码等效于：

```sql
WHERE birth_date <= '1990-01-01' AND points <= 1000
```



## 2.4 *IN 运算符* 

```sql
USE sql_store;

SELECT * 
FROM customers
-- WHERE state = 'va' OR state = 'fl' OR state = 'ga'
WHERE state IN ('va', 'fl', 'ga') -- 等效于上述操作
-- 加 NOT 筛选不在给定集合中的值
WHERE state NOT IN ('va', 'fl', 'ga')
```

### 【练习】

库存量刚好为49、38或72的产品

```sql
USE sql_store;

SELECT *
FROM products
WHERE quantity_in_stock in (49, 38, 72)
```



## 2.5 BETWEEN 运算符

```sql
SELECT *
FROM customers
WHERE points BETWEEN 1000 AND 3000
```

### 【练习】
选出90后的顾客

```sql
SELECT *
FROM customers
WHERE birth_date BETWEEN '1990-01-01' AND '2000-01-01' 
```



## 2.6 LIKE 运算符

- 模糊查找，查找具有某种模式的字符串的记录/行
- “ % ” 任何个数（包括0个）的字符，“_” 单个字符


电话号码以 9 结束
~~~sql
SELECT * 
FROM customers
WHERE phone NOT LIKE '%9'
~~~

地址包含 'TRAIL' 或 'AVENUE'
~~~sql
SELECT *
FROM customers
WHERE address LIKE  '%trail%' OR
		 address LIKE '%avenue%'
~~~



## 2.7 REGEXP 运算符

- regexp 是 regular expression（正则表达式） 的缩写。
- 部分语法：

| 符号  | 意义       |
| ----- | ---------- |
| ^     | 开头       |
| $     | 结尾       |
| [abc] | 含abc      |
| [a-c] | 含a到c     |
| \|    | logical or |

~~~sql
SELECT *
FROM customers
WHERE last_name REGEXP 'b[ru]'
~~~

正则表达式可以组合来表达更复杂的字符串模式。

~~~sql
SELECT *
FROM customers
WHERE last_name REGEXP '^my|se'
/ WHERE last_name REGEXP 'ey$|on$'
/ WHERE first_name REGEXP 'elka|ambur'
~~~



## 2.8 IS NULL 运算符

找出电话号码缺失的顾客。

~~~sql
SELECT *
FROM customers 
WHERE phone IS NOT NULL
~~~

找出还没发货的订单
~~~sql
SELECT *
FROM orders
WHERE shipped_date IS NULL
~~~



## 2.9 ORDER BY 子句

1. 可多列。
2. **可以是列间的数学表达式。**
3. **可包括任何列，包括没选择的列（MySQL特性，其它DBMS可能报错）。**
4. **可以是之前定义好的别名列（MySQL特性，甚至可以是用一个常数设置的列别名）。**
5. 任何一个排序依据列后面都可选加 DESC 降序排列。

> 注：workbench 中扳手图标可打开表格的设计模式，查看或修改表中各列（属性），可以看到谁是主键。省略排序语句的话会默认按主键排序

```sql
USE sql_store;

SELECT
	name,
	unit_price * 1.1 + 10 as new_price 
FROM products
ORDER BY new_price DESC, product_id
-- 这两个分别是 别名列 和 未选择列，都用到了 MySQL 特性
```

### 【练习】

订单2的商品按总价降序排列

~~~sql

SELECT *, quantity * unit_price AS total_price 
FROM order_items
WHERE order_id = 2 
ORDER BY total_price DESC
~~~


## 2.10 LIMIT 子句

~~~sql
SELECT *
FROM customers
LIMIT 6, 3
-- 6, 3 表示跳过前6个，取第7~9个，6是偏移量，
-- 如：网页分页 每3条记录显示一页 第3页应该显示的记录就是 limit 6, 3
~~~

### 【练习】

找出积分排名前三的死忠粉

~~~sql
SELECT * 
FROM customers
ORDER BY points DESC
LIMIT 3
~~~

