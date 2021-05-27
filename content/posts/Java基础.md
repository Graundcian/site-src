---
title: "Java基础"
date: 2021-05-17T16:02:53+08:00
draft: false
tags: [learning, Java]
---



Java 基础知识总结：标识符、基本数据类型、类型转换、变量、常量、运算符、包机制、JavaDoc使用

<!--more-->

# 注释、标识符、 关键字

## 注释

书写注释是一个很好的习惯，平时写代码一定要注意规范。

Java中有三种注释：

```java
// 单行注释

//多行注释
/*
* 这是一个
* 多行注释
* 可以注释
* 一段文字
*/

//JavaDoc:文档注释
/**
 * @Description HelloWorld
 * @Auther Graundcian
 */
```

## 标识符

| JAVA关键字                                            |FFrom|百度百科|||
| :---------------------------------------------------- | :-------------------------------------------------------- | :-------------------------------------------------- | :---------------------------------------------------- | :-------------------------------------------- |
| [abstract](https://baike.baidu.com/item/abstract)     | [assert](https://baike.baidu.com/item/assert)             | [boolean](https://baike.baidu.com/item/boolean)     | break                                                 | [byte](https://baike.baidu.com/item/byte)     |
| case                                                  | [catch](https://baike.baidu.com/item/catch)               | [char](https://baike.baidu.com/item/char)           | [class](https://baike.baidu.com/item/class)           | const                                         |
| continue                                              | [default](https://baike.baidu.com/item/default)           | [do](https://baike.baidu.com/item/do)               | [double](https://baike.baidu.com/item/double)         | [else](https://baike.baidu.com/item/else)     |
| [enum](https://baike.baidu.com/item/enum)             | [extends](https://baike.baidu.com/item/extends)           | [final](https://baike.baidu.com/item/final)         | [finally](https://baike.baidu.com/item/finally)       | float                                         |
| [for](https://baike.baidu.com/item/for)               | goto                                                      | [if](https://baike.baidu.com/item/if)               | [implements](https://baike.baidu.com/item/implements) | [import](https://baike.baidu.com/item/import) |
| [instanceof](https://baike.baidu.com/item/instanceof) | [int](https://baike.baidu.com/item/int)                   | [interface](https://baike.baidu.com/item/interface) | long                                                  | native                                        |
| new                                                   | [package](https://baike.baidu.com/item/package)           | [private](https://baike.baidu.com/item/private)     | [protected](https://baike.baidu.com/item/protected)   | [public](https://baike.baidu.com/item/public) |
| [return](https://baike.baidu.com/item/return)         | [strictfp](https://baike.baidu.com/item/strictfp)         | [short](https://baike.baidu.com/item/short)         | [static](https://baike.baidu.com/item/static)         | [super](https://baike.baidu.com/item/super)   |
| [switch](https://baike.baidu.com/item/switch)         | [synchronized](https://baike.baidu.com/item/synchronized) | [this](https://baike.baidu.com/item/this)           | [throw](https://baike.baidu.com/item/throw)           | throws                                        |
| [transient](https://baike.baidu.com/item/transient)   | try                                                       | [void](https://baike.baidu.com/item/void)           | [volatile](https://baike.baidu.com/item/volatile)     | [while](https://baike.baidu.com/item/while)   |

类名、变量名、方法名称为标识符。

- 所有标识符以字母、$、或者下划线 _ 开始
- **标识符大小写敏感**
- 不能使用关键字作为变量名或方法名

# **数据类型**

- 强类型语言：Java、 C/C++
- 弱类型语言：JavaScript、Python

Java 属于强类型语言，要求变量的使用严格符合规定，所有的变量必须先定义后使用。

Java的数据类型分为两大类：

## 基本类型（Primitive Type）

### 八大基本数据类型

```java
        // 八大基本数据类型

        //整数
        int num1=10; //最常用
        byte num2 = 20;
        short num3 = 30;
        long num4 = 30L; //Long类型要在数字后面加一个 L

        //小数：浮点数
        float num5 = 50.1F; //float类型要在数字后面加一个 F
        double num6 = 3.141592653589793238462643;

        //字符
        char name1 = 'A';
        char name2 = '中';
        //字符串 String 不是关键字，是类
        String name3 = "中国";

        //布尔值
        boolean flag = true;
        boolean flag1 = false;
```

### 拓展内容

#### 整数拓展

- 二进制 0b   
- 十进制0    
- 十六进制0x

```java
int i = 10;
int i2 = 010; //八进制 0
int i3 = 0x10; //十六进制 0x
System.out.println(i); //10
System.out.println(i2); //8
System.out.println(i3); //16
```

#### 浮点数拓展

**面试题**：银行业的钱怎么表示？ （BigDecimal类 – Java数学工具）

```java
//float 是离散的，存在舍入误差
//最好避免使用浮点数进行比较
//最好避免使用浮点数进行比较
//最好避免使用浮点数进行比较

float f = 0.1f; //0.1
double d = 1.0/10; //0.1
System.out.println(f);
System.out.println(d);
System.out.println(f==d); //false

float d1 = 234553656;
float d2 = d1 + 1;
System.out.println(d1==d2); //true
```

#### 字符拓展

##### Unicode编码 

所有的字符本质还是数字，Unicode编码 表：(97=a  65=A) ，每个编码占2字节  0 - 65536

```java
char c1 = 'a';
char c2 = '中';

System.out.println(c1); //97

System.out.println((int)c1); //强制类型转换

System.out.println(c2); //20013

System.out.println((int)c2);//强制类型转换

char c3 = '\u0061';
System.out.println(c3); //a
```

##### 转义字符

| 转义字符 | 意义                                    | ASCII码值（十进制） |
| :------- | :-------------------------------------- | :-----------------: |
| \b       | 退格(BS) ，将当前位置移到前一列         |         008         |
| \f       | 换页(FF)，将当前位置移到下页开头        |         012         |
| **\n**   | **换行(LF) ，将当前位置移到下一行开头** |         010         |
| **\r**   | **回车(CR) ，将当前位置移到本行开头**   |         013         |
| **\t**   | **水平制表(HT) （跳到下一个TAB位置）**  |         009         |
| \v       | 垂直制表(VT)                            |         011         |
| **\\**   | **代表一个反斜线字符''\'**              |         092         |
| **\'**   | **代表一个单引号（撇号）字符**          |         039         |
| **\"**   | **代表一个双引号字符**                  |         034         |
| \0       | 空字符(NULL)                            |         000         |
| \ddd     | 1到3位八进制数所代表的任意字符          |     三位八进制      |
| \uhhhh   | 1到2位十六进制所代表的任意字符          |    二位十六进制     |

#### 布尔值拓展

```java
boolean flag = true;
if (flag==true){} //新手写法
if (flag){} //这样是标准写法
```

#### 思考题（未解决）

讲到 对象 部分时，从内存分析

```Java
// 遗留问题
String sa = new String("Hello World");
String sb = new String("Hello World");
System.out.println(sa==sb);

String sc = "Hello World";
String sd = "Hello World";
System.out.println(sc==sd);
// 在 对象 部分，从内存分析
```

## 引用类型（Reference Type）

- 类
- 方法
- 变量

# 类型转换

Java 是强类型语言，进行有些运算时，需要用到类型转换

```java 
// 低容量 ---------------------------> 高容量
  byte, short,char -> int -> long -> float -> double
```

## 强制类型转换 

方法：（类型名）变量名 

 高容量 --> 低容量转换，存在 <u>内存溢出问题</u>，以及 <u>精度丢失问题</u>。

```java
int i = 128;
byte b = (byte)i; //-128 内存溢出

System.out.println(i);
System.out.println(b);
```

## 自动类型转换  

直接可以转换 ，低容量 --> 高容量

```java
int i = 128;
double b1 = i; //128.0

System.out.println(i);
System.out.println(b1);
```

## 注意事项

1. 不能对 <u>布尔值</u>（boolean）进行类型转换。
2. 不能把 <u>对象类型</u> 转换为不相干类型。
3. 在把高容量转换为低容量的时候，要强制转换。
4. 转换的时候可能存在内存泄漏，或精度问题

```java
System.out.println("===============================");
System.out.println((int)23.7); //23
System.out.println((int)-49.56F); //49

       System.out.println("===============================");
        char a = 'a';// 'a'=97
        int d = a + 1; //98
        System.out.println(d); 
        System.out.println((char)d); //b
```

## 拓展知识

在操作比较大的数时，要注意溢出问题。

```java
int money = 10_0000_0000;
int years = 20;
int total1 = money*years; //-1474836480, 计算溢出，超出 int 的范围（20亿）

long total2 = money*years; //默认是 int，在long转换之前就存在问题
long total3 = (long)money*years; //先把一个数转换为long （返回值为高容量的类型，long 和 int运算，返回long）
System.out.println(total1);
System.out.println(total2);
System.out.println(total3);
```

# 变量、常量

## 变量(Variable)

Java变量是程序中最基本的存储单元，其要素包括 变量名、变量类型和作用域。

### 声明变量

每个变量都有类型，可以是基本类型，也可以是应用类型。变量声明是一条完整的语句，因此每一个声明都得以分号结束。

```java
  type   varName  [=value]；
//数据类型  变量名 =  值；

// 基本类型
      int a = 3;
//引用类型
	  String name = "Graundcian"
```

### 变量作用域

```java
public class Variable {
    static int allClicks=0;  //类变量
    String str = "Hello World"; //实例变量
    
    puplic void method(){
        int i = 0;  //局部变量
    }
}
```

#### 类变量

使用关键字 **static** 声明

```java
public class Variable {
    static int allClicks=0;  //类变量
}
```

#### 实例变量

从属于对象（class）, 如果不自行初始化，这个类型的**默认值为 0**，布尔值的默认值为 **false**，除了基本类型，其它的默认值为 **null。**

```java
public class Variable {
    String str = "Hello World"; //实例变量
}
```

#### 局部变量

在方法中声明的变量，必须初始化值。

```java
public class Variable {

    puplic void method(){
        int i = 0;  //局部变量
    }
}
```

## 常量(Constant)

常量初始化(initialize)后不能在改变值，常量名一般使用 **大写字母**

```java
// final 常量名 = 值；
final double PI = 3.14;
```

## 命名规范

- 所用变量、方法、类名，见名知意
- 常量使用 大写字母和下划线：MAX_VALUE
- 类名：首字母大写和驼峰原则  Man、GoodMan
- 其它的命名都应符合 首字母小写和驼峰原则 run() 、 monthSalary

# 运算符😢

- **算数运算符：+,	-,	*,	/,	%(模),	++, 	- -**
- **赋值运算符：=**
- **关系运算符：>,   <,   >=,    <=,    ==,    !=,   instanceof**
- **逻辑运算符：&&,    ||,   !**
- 位运算符:  &,   |,    ^,    ~,    >>,    <<,   >>>
- 条件运算符：？
- 扩展运算符：+=,     -=,     *=,    /=



# 包机制、JavaDoc
