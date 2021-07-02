---
title: 第三章
description:
toc: true
authors: []
date: 2021-07-01T18:17:36+08:00
lastmod: 2021-07-01T18:17:36+08:00
draft: false
weight: 3
---

# 表的连接与查询

<!--more-->


## 3.1 内连接(Inner Joins)

~~~sql
SELECT order_id, o.customer_id,first_name, last_name
FROM orders o -- 别名 o
JOIN customers c
    ON o.customer_id = c.customer_id
~~~

### 【练习】

~~~sql
 SELECT order_id, p.product_id, p.name, oi.quantity, oi.unit_price
 FROM order_items oi
 JOIN products p ON oi.product_id = p.product_id
~~~

## 3.2 跨数据库链接(Joining Across Databases)

~~~sql
USE sql_store;

SELECT *
FROM order_items oi
JOIN sql_inventory.products p ON oi.product_id = p.product_id
~~~

## 3.3 自连接(Self Joins)

~~~sql
USE sql_hr; 
SELECT 
	e.employee_id,
    e.first_name,
    m.first_name AS manger
FROM employees e
JOIN employees m
	ON e.reports_to = m.employee_id
~~~

## 3.4 多表连接(Joining Multiple Tables)

~~~sql
USE sql_store;

SELECT 
	o.order_id,
    o.order_date,
    c.first_name,
    c.last_name,
    os.name AS status
FROM orders o
JOIN customers c
	ON o.customer_id = c.customer_id
JOIN order_statuses os
	ON o.status = os.order_status_id
~~~

### 【练习】

~~~sql
USE sql_invoicing;

SELECT 
	c.name,
    p.date,
    pm.name AS payment_method,
    i.number AS invice_number
FROM payments p
JOIN payment_methods pm
	ON p.payment_method = pm.payment_method_id
JOIN clients c
	ON p.client_id = c.client_id
JOIN invoices i
	ON p.invoice_id = i.invoice_id
~~~

## 3.5 复合连接条件(Compound Join Conditions)

有时候通过一列标识符无法准确定位，因为可能存在重复值，因此需要同两列标识符来准确定位。

~~~sql
USE sql_store;

SELECT *
FROM order_items oi
JOIN order_item_notes oin
	ON oi.order_id = oin.order_id
    AND oi.product_id = oin.product_id
~~~

## 3.6 隐式连接语法(Implicit Join Syntax)

### 3.6.1 显式连接

~~~sql
USE sql_store; 
SELECT *
FROM orders o
JOIN customers c
	ON o.customer_id = c.customer_id
~~~

### 3.6.2 隐式连接(不建议使用）

容易忘记写WHERE子句，查询结果会变成 “交叉连接”--笛卡尔积的形式。

~~~sql
USE sql_store;

SELECT *
FROM orders o, customers c
WHERE o.customer_id = c.customer_id
~~~

## 3.7 外连接(Outer Joins)

~~~sql
USE sql_store;

SELECT
	c.customer_id,
    c.first_name,
    o.order_id
FROM customers c
-- LEFT JOIN 会显示左边customer表的全部内容
LEFT JOIN orders o
-- RIGHT JOIN 会显示右边orders表的全部内容
-- RIGHT JOIN orders o  
	ON o.customer_id = c.customer_id
ORDER BY c.customer_id
~~~

### 【练习】

~~~sql
USE sql_store;
SELECT
	p.product_id,
    p.name,
    oi.quantity
FROM products p
LEFT JOIN order_items oi
	ON p.product_id = oi.product_id
~~~

## 3.8 多表外连接(Outer Joins Between Multiple Tables)

~~~sql
USE sql_store;

SELECT
		c.customer_id,
	    c.first_name,
     o.order_id,
     sh.name AS shipper
FROM customers c
LEFT JOIN orders o
	ON o.customer_id = c.customer_id
LEFT JOIN shippers sh
	ON o.shipper_id = sh.shipper_id
ORDER BY c.customer_id
~~~

### 【练习】

~~~sql
USE sql_store;

SELECT
	o.order_date,
    o.order_id,
    c.first_name AS customer,
    s.name AS shipper,
    os.name AS status
FROM orders o
JOIN customers c
	ON o.customer_id = c.customer_id
LEFT JOIN shippers s
	ON o.shipper_id = s.shipper_id
LEFT JOIN order_statuses os
	ON o.status = os.order_status_id
ORDER BY o.order_date
~~~

## 3.9 自外连接(Self Outer Joins)

manager本身也是employee，但使用Inner Join无法列出没有manager的employee。因此使用Self Outer Join

~~~sql
USE sql_hr;
SELECT
	e.employee_id,
    e.first_name AS employee,
    m.first_name AS manager
FROM employees e
LEFT JOIN employees m
	ON e.reports_to = m.employee_id
~~~

## 3.10 USING子句

对有相同‘列名’的不同表进行连接时，可以使用 USING 子句 代替 ON 进行限制。

~~~sql
USE sql_store;
SELECT
	o.order_id,
    c.first_name,
    sh.name AS shipper
FROM orders o
JOIN customers c
	-- ON o.customer_id = c.customer_id
    USING (customer_id)
LEFT JOIN shippers sh
	USING (shipper_id)
~~~

对于“3.5 复合连接条件”也可以使用USING子句，用","分隔多个列名即可。

~~~sql
USE sql_store;
SELECT *
FROM order_items oi
JOIN order_item_notes oin
	-- ON oi.order_id = oin.order_id
	-- AND oi.product_id = oin.product_id
	USING (order_id, product_id)
~~~

### 【练习】

~~~sql
USE sql_invoicing;
SELECT
 	p.date,
    c.name AS client,
    p.amount,
    pm.name AS payment_method
FROM payments p
JOIN clients c USING (client_id)
JOIN payment_methods pm
	ON p.payment_method = pm.payment_method_id
ORDER BY p.date
~~~

## 3.11 自然连接(Natural Joins)

**！！不建议使用！！**
数据库引擎会自己连接两个表，我们无法进行控制，可能出现意外结果。

~~~sql
USE sql_store;
SELECT 
	o.order_id,
    c.first_name
FROM orders o
NATURAL JOIN customers c
~~~

## 3.12 交叉连接(Cross Joins)

**【使用场景】**
一个产品有不同的规格和颜色，需要将所有规格和所有颜色组合，这时“交叉连接”就派上用场了。

| 规格 | 颜色 |
|:---:|:---:|
| 大  |  红  |
| 大  |  绿  |
| 小  |	 红  |
| 小  |  绿  |

### 3.12.1 显式语句

~~~sql
USE sql_store;
SELECT
	c.first_name AS customer,
    p.name AS product
FROM customers c
CROSS JOIN products p
ORDER BY c.first_name
~~~

### 3.12.2 隐式语句

**!!不建议使用!!** 语法不够清晰

~~~sql
USE sql_store;
SELECT
	c.first_name AS customer,
    p.name AS product
FROM customers c, products p
ORDER BY c.first_name
~~~

### 【练习】

**隐式表达**

~~~sql
USE sql_store;
SELECT
	   sh.name AS shipper,
    p.name AS product
FROM shippers sh, products p
~~~

**显式表达**

~~~sql
USE sql_store;
SELECT
	sh.name AS shipper,
    p.name AS product
FROM shippers sh
CROSS JOIN products p
ORDER BY sh.name
~~~

## 3.13 联合(Unions)

1.合并多个查询结果到一个结果集中，但每个查询语句返回的列数得是一样的。

2.第一段查询语句中的列名决定结果集的列名。

~~~sql
USE sql_store;
SELECT
	order_id,
    order_date,
    'ACtive' AS status
FROM orders
WHERE order_date >= '2019-01-01'
UNION
SELECT
	order_id,
    order_date,
    'Archive' AS status
FROM orders
WHERE order_date < '2019-01-01'
~~~

### 【练习】

~~~sql
USE sql_store;
SELECT
	customer_id,
    first_name,
    points,
    'Bronze' AS thpe
FROM customers
WHERE points < 2000
UNION
SELECT
	customer_id,
    first_name,
    points,
    'Silver' AS type
FROM customers
-- WHERE points < 3000 AND points >= 2000
WHERE points BETWEEN 2000 AND 3000
UNION
SELECT
	customer_id,
    first_name,
    points,
    'Gold' AS type
FROM customers
WHERE points > 3000
ORDER BY first_name
~~~