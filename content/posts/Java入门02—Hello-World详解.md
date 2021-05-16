---
title: "Java入门02—Hello World详解"
date: 2021-05-16T21:56:56+08:00
draft: false
tags: [learning, Java]
 
---

# HelloWorld

1. 新建文件夹，存放代码

2. 新建 Java 文件
   - 后缀名为：“.java”
   
3. 编写代码

   ```java
   public class Hello{
       public static void main(String[] args){
           System.out.print("Hello,World!");
   	}
   }
   ```


4. 编译 & 运行

   ```bash
   javac Hello.java # 生成一个class文件
   
   java Hello.class # 运行 class 文件
   ```
   
   ![image-20210516233738809](https://cdn.jsdelivr.net/gh/Graundcian/images@master/blog/2021/05/16/20210516233748.png)

## 可能出现的问题

- 大小写敏感

- 尽量用中文

- 文件名 和 类名必须保持一致

  
