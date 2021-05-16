---
title: "Java入门01—环境搭建"
date: 2021-05-16T21:01:18+08:00
draft: false
tags: [learning,Java]
---

# Java的特性和优势

- 简单性
- 面向对象
- 可移植性（Write ones, Run anywhere）
- 高性能
- 分布式
- 动态性（本身不具有动态性，可以通过“反射”实现）
- 多线程
- 安全性
- 健壮性

# Java的三大版本

- **JavaSE**:  标准版（桌面程序，控制台开发......)
- JavaME：嵌入式开发（基本已经废弃）
- **JavaEE**：企业级开发（web端，服务器开发.....)

# JDK、JRE、JVM

- JDK：Java Development Kit
- JRE：Java Runtime Environment
- JVM：Java Virtual Machine

![image](https://cdn.jsdelivr.net/gh/Graundcian/images@master/blog/image.v0efhp6of2o.png)





# Java开发环境搭建

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

