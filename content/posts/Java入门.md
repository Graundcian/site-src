---
title: "Java入门"
date: 2021-05-16T21:01:18+08:00
draft: false
toc: true
authors: [graundcian]
tags: [learning,Java]
featuredImage: https://cdn.jsdelivr.net/gh/Graundcian/images@master/blog/image.2n6uww3yo3o0.png
---
特性及优势、版本差异、环境搭建、运行机制

<!--more-->

# Java简介

## Java的特性和优势

- 简单性
- 面向对象
- 可移植性（Write ones, Run anywhere）
- 高性能
- 分布式
- 动态性（本身不具有动态性，可以通过“反射”实现）
- 多线程
- 安全性
- 健壮性

## Java的三大版本

- **JavaSE**:  标准版（桌面程序，控制台开发......)
- JavaME：嵌入式开发（基本已经废弃）
- **JavaEE**：企业级开发（web端，服务器开发.....)

## JDK、JRE、JVM

- JDK：Java Development Kit
- JRE：Java Runtime Environment
- JVM：Java Virtual Machine

![image](https://cdn.jsdelivr.net/gh/Graundcian/images@master/blog/image.v0efhp6of2o.png)





# Java开发环境搭建

## 安装JDK

1. [JDK 下载地址]([Java SE - Downloads | Oracle Technology Network | Oracle](https://www.oracle.com/java/technologies/javase-downloads.html))

2. 安装、配置环境变量

   - 变量名：JAVA_HOME  变量值：  C:\Program Files\Java\jdk1.8.0_191
   
   - 变量名：CLASSPATH   变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar
   - Path变量 中添加：%JAVA_HOME%\bin  和  %JAVA_HOME%\jre\bin
   
3. 测试环境

   ```powershell
   Java
   javac
   java -version
   ```

   如果报错，检查环境变量设置是否正确。

## 安装IDEA

- [Download IntelliJ IDEA: The Capable & Ergonomic Java IDE by JetBrains](https://www.jetbrains.com/idea/download/#section=windows)



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
   
   ![image-20210516233738809](https://cdn.jsdelivr.net/gh/Graundcian/images@master/blog/2021/05/17/20210517155425.png)

## 可能出现的问题

- 大小写敏感

- 尽量用中文

- 文件名 和 类名必须保持一致

  

# Java 程序运行机制

- 编译型：运行速度快，可移植性差
- 解释型：边解释边执行，跨平台容易，运行效率低

随着硬件的发展，编译型和解释型语言的界限再逐渐变小。



Java语言是先**编译（compile）** 后**解释（interpretation）**

![img](https://cdn.jsdelivr.net/gh/Graundcian/images@master/blog/2021/05/17/20210517145907)
