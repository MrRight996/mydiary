# Mybatis-9.28

环境：

- JDK1.8
- Mysql 5.7 或者 8.0
- maven 3.6.1（无）
-  IDEA

回顾：

- JDBC
- Mysql
- Java基础
- Maven
- Junit



SSM框架：配置文件的。最好的方式：看官网文档；

# 1、简介

## 1.1、什么是Mybatis

- MyBatis 是一款优秀的**持久层框架**
- 它支持自定义 SQL、存储过程以及高级映射。
- MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。
- MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

如何获得Mybatis？

- maven仓库：

- ```xml
  <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
  <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.9</version>
  </dependency>
  ```

- Github：

- 中文文档

## 1.2、持久化

数据持久化

- 持久化就是将程序的数据在持久状态和瞬时状态转化的过程
- 内存：**断电即失**
- 数据库（jdbc），io文件持久化。

**为什么需要持久化**

- 有一些对象，不能让他丢掉

- 内存太贵了

## 1.3、持久层

Dao层，Service层，Controler层...

- 完成持久化工作的代码块
- 层界限十分明显

## 1.4、为什么需要Mybatis

- 方便
- 传统的JDBC代码太复杂了。简化。框架。自动化
- 帮助程序员将数据存入到数据库中
- 不用Mybatis也可以。更容易上手。 **技术没有高低之分**
- 优点
  - 简单易学
  - 灵活
  - sql和代码的分离，提高了可维护性
  - 提供映射标签，支持对象与数据库的orm字段关系映射
  - 提供对象关系的映射标签，支持对象关系组建维护
  - 提供xml标签，支持编写动态sql
  - 最重要的还是使用的人多

# 2、第一个Mybatis程序

思路：搭建环境-->导入Mybatis-->编写代码-->测试！

## 2.1、搭建环境

搭建数据库

```mysql
CREATE DATABASE `mybatis`;
USE `mybatis`;
CREATE TABLE `user`(
`id` INT(20) NOT NULL PRIMARY KEY,
`name`VARCHAR(30) DEFAULT NULL,
`pwd`VARCHAR(30) DEFAULT NULL
 
)ENGINE=INNODB DEFAULT CHARSET=utf8;

```

新建项目