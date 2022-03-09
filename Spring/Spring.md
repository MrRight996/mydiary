# 1、Spring

## 1.1、简介

- Spring：春天--》给行业带来了春天！
- 2002，首次推出了Spring框架的雏形：interface21框架！
- Spring框架
- Spring理念：使现有的技术更加容易使用，本身是一个大杂烩，整合了先有的技术框架！



- SSH：Struct2+Spring+Hibernate！（全自动）mybatis半自动

- SSM：SpringMVC+Spring+Mybatis

  ```xml
  <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.3.16</version>
  </dependency>
  <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>5.3.16</version>
  </dependency>
  ```

## 1.2、优点

- Spring是一个开源的免费的框架（容器）
- Spring是一个轻量级的、非入侵式的框架！
- 控制反转（IOC）、面向切面编程（AOP）
- 支持事务的处理，对框架整合的支持



总结一句话：Spring就是一个轻量级的控制反转（IOC）和面向切面编程（AOP）框架

## 1.3、组成

![image-20220306190228179](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20220306190228179.png)

## 1.4、扩展

在Spring的官网有这个介绍：现代化的java开发！说白就是基于Spring的开发！

![image-20220306191009024](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20220306191009024.png)

- Spring Boot

  - 一个快速开发的脚手架

  - 居于SpringBoot可以快速的开发单个微服务。

  - 约定大于配置！

- Spring Cloud
  - SpringCloud是基于SpringBoot实现的。

因为现在大多数公司都在使用SpringBoot进行快速开发，学习SpringBoot的前提，需要完全掌握Spring及 SpringMVC！承上启下的作用！

**弊端：发展了太久之后，违背了原来的理念！配置十分繁琐，人称：“配置地狱！“**

# 2、IOC理论推导

1. UserDao接口



1. UserDaolmpl实现类



1. UserService业务接口



1. UserServicelmpl业务实现类



