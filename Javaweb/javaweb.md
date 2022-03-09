# JavaWeb

java web

## 1、基本概念

### 1.1、前言

web开发：

- web，网页的意思，www.baidu.com
- 静态web
  - html，css
  - 提供给所有人看的数据始终不会发生变化！
- 动态web
  - 淘宝，几乎是所有的网站；
  - 提供给所有人看的数据始终会发生变化！每个人在不同的时间，不同的地点看到的信息各不相同！
  - 技术栈：Servlet/JSP,ASP,PHP

在java中，动态web资源开发的技术统称为javaweb；

### 1.2、web应用程序

web应用程序：可以提供浏览器访问的程序；

- a.html b.html....多个web资源，这些web资源可以被外界访问，对外界提供服务；
- 你们能访问到的任何一个网页或者资源，都存在于这个世界的某一个角落的计算机上。
- URL
- 这个统一的web资源会被放在同一个文件夹下，web应用程序-->Tomcat：服务器
- 一个web应该由多部分组成（静态web，动态web）
  - html，css，js
  - jsp，servlet
  - java程序
  - jar包
  - 配置文件（properties）

web应用程序编写完毕之后，若想提供给外界访问：需要一个服务器来统一管理；

### 1.3、静态web

*.htm,  *.html,这些都是网页的后缀，然后服务器上一直存在这些东西，我们就可以直接进行读取。通络；

![image-20210407170557365](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210407170557365.png)

request 请求 response 相应

- 静态web存在的缺点
  - web页面无法动态更新，所有用户看到的都是同一个页面
    - 轮播图，点击特效：伪动态
    - JavaScript[实际开发中，它用的最多]
    - VBScript
  - 它无法和数据库交互（数据无法持久化，用户无法交互）

### 1.4、动态web

页面会动态展示：“web的页面

![image-20210408012044779](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210408012044779.png)

缺点

- 假如服务器的动态web资源出现了错误，我们需要重新编写我们的**后台程序**，重新发布；
  - 停机维护

优点：

- Web页面可以动态更新，所有用户看到都不是同一个页面
- 它可以和数据库交互（数据持久化：注册，商品信息，用户信息.....）

![image-20210408012609420](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210408012609420.png)

## 2、web服务器

### 2.1、技术讲解

ASP：

- 微软：国内最早流行的就是ASP；
- 在HTML中嵌入了VB脚本 ASP+COM
- 在ASP开发中，基本一个页面都有几千行的业务代码，页面极其混乱
- 维护成本高！
- C#
- IIS



PHP

- PHP开发速度很快，功能强大，跨平台，代码很简单（70%，WP）
- 无法承载大访问量的情况（局限性）



JSP/Servlet

B/S：浏览器和服务器

C/S：客户端和服务器

- sun公司主推的B/S架构
- 基于java语言的（所有的大公司，或者一些开源的组件，都是用java写的）
- 可以承载三高带来的影响；（高并发，高可用，高性能）
- 语法像ASP，ASP-->JSP，加强市场强度；

### 2.2、web服务器

服务器是一种被动的操作，用来处理用户的一些请求和给用户一些响应信息；

**IIS**

微软的；ASP...,Windows自带的

**Tomcat**

面向百度编程；

**工作3-5年之后，可以尝试手写Tomcat服务器；**

下载Tomcat：

1、安装或者解压

2、了解配置文件及目录结构

3、这个东西的作用

## 3、Tomcat

### 3.1安装Tomcat

tar.gz是linux的

### 3.2、Tomcat的启动和配置

文件夹作用：

![image-20210408135550289](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210408135550289.png)

启动，关闭Tomcat

![image-20210408142408194](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210408142408194.png)

访问测试：localhost:8080

可能遇到的问题：

1、java环境变量没有配置

2、闪退问题：需要配置兼容性

3、乱码问题：配置文件中设置

### 3.3、Tomcat配置

![image-20210408144135308](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210408144135308.png)

可以配置启动的端口号

- Tomcat的默认端口号为：8080
- mysql：3306
- http：80
- https：443

```xml
<Connector port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
```
可以配置主机的名称

- 默认的主机名为：localhost --> 127.0.0.1
- 默认网站应用存放的位置为：webapps

```xml
  <Host name="localhost"  appBase="webapps"
        unpackWARs="true" autoDeploy="true">
```
**高难度面试题：**	

请你探探网站是如何进行访问的！

1. 输入一个域名；回车

2. 检查本机的C:\Windows\System32\drivers\etc\hosts配置文件下有没有这个域名映射；

   1. 如果有：直接返回对应的ip地址,这个地址中，有我们需要访问的web程序，可以直接访问

      ``` java
      127.0.0.1    iristech.co
      127.0.0.1    www.czl.com
      192.168.124.2 windows10.microdone.cn
      ```

      ![image-20210408154959830](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210408154959830.png)

   2. 如果没有：去DNS服务器,找的话就返回，找不到就返回找不到；

   ![image-20210408155622281](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210408155622281.png)

4、配置环境变量（可选项）

### 3.4、发布一个web网站

不会就先模仿

- 将自己写的网站，放在服务器（Tomcat）中指定的web应用的文件夹（webapps）下，就可以访问了

网站应该有的结构

``` java
--webapps：Tomcat服务器的web目录
	-ROOT
	-czl：网站的目录名
		-WEB-INF
			-classes：java程序
			-lib：web应用所依赖的jar包
			-web.xml：网站的配置文件
		-index.html默认的首页
		-static
			-css
				-style.css
			-js
			-img
    	-.....
```

HTTP协议：面试

Maven：构建工具

- Maven安装包

Servlet入门

- helloworld！
- Servlet配置
- 原理

## 4、Http

### 4.1、什么是http

超文本传输协议（Hypertext Transfer Protocol，HTTP）是一个简单的请求-响应协议，它通常运行在[TCP](https://baike.baidu.com/item/TCP/33012)之上。它指定了客户端可能发送给服务器什么样的消息以及得到什么样的响应。

- 文本：html，字符串，...
- 超文本：图片，音乐，视频，定位，地图....
- 默认端口80

https:安全

- 默认端口：443

### 4.2、两个时代

- http1.0
  - HTTP/1.0:客户端可以与web服务器连接后，只能获得一个web资源，断开链接
- http2.0
  - HTTP/1.1：客户端可以与web服务器连接后，可以获得多个web资源。

### 4.3、HTTP请求

- 客户端--发请求--服务器

百度：

``` java
Request URL: https://www.baidu.com/ 请求地址
Request Method: GET		get方法/post方法
Status Code: 200 OK		状态码：200
Remote（远程） Address: 14.215.177.39:443
Referrer Policy: unsafe-url
```

``` java
Accept: text/html
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9		语言
Cache-Control: max-age=0
Connection: keep-alive
```

#### **1、请求行**

- 请求行中的方式：GET
- 请求方式：**GET，POST**，HEAD,DELETE,PUT,PACT....
  - get：请求能够携带的参数比较少，大小有限制，会在浏览器的URL地址栏显示数据内容，不安全，但高效
  - post：请求能够携带的参数没有限制，大小有限制，不会在浏览器的URL地址栏显示数据内容，安全，但不高效

#### **2、消息头**

``` 
Accept:告诉浏览器，它所支持的数据类型
Accept-Encoding:支持哪种编码格式 GBK UTF-8 GB2312 ISO8859-1
Accept-Language:告诉浏览器，它的语言环境
Cache-Control:缓存控制
Connection:告诉浏览器，请求完成是断开还是保持连接
HOST：主机
```

### 4.4、http响应

- 服务器--发请求--客户端

百度：

``` java
Cache-Control: private		缓存控制
Connection: keep-alive		连接
Content-Encoding: gzip		编码
Content-Type: text/html;	类型
```

#### 1、响应体

``` java
Accept:告诉浏览器，它所支持的数据类型
Accept-Encoding:支持哪种编码格式 GBK UTF-8 GB2312 ISO8859-1
Accept-Language:告诉浏览器，它的语言环境
Cache-Control:缓存控制
Connection:告诉浏览器，请求完成是断开还是保持连接
HOST：主机
Refrush:告诉客户端，多久刷新一次
Location:让网页重新定位 
```

#### 2、响应状态码

202：请求响应成功 200

3XX：请求重定向 

- 重定向：你重新到我给你的新位置去

404：找不到资源 404

- 资源不存在；

5XX：服务器代码错误 500 502：网关错误



**常见面试题：**

当你的浏览器中地址栏输入地址并回车的一瞬间到页面能够展示回来，经历了什么？



## 5、Maven

为什么要学习这个技术？

1.在javaweb学习过程中，需要使用大量的jar包，我们手动去导入

2.如何能够让一个东西自动帮我们导入和配置这个jar包

​	由此，Maven诞生了!



### 5.1、Maven项目架构管理工具

我们目前用来就是方便导入jar包的！

Maven的核心思想：**约定大于配置**

- 有约束不用去违反。

Maven会规定好你该如何去编写我们的Java代码，必须要按照这个规范来；

### 5.2、下载安装Maven

下载完成后，解压即可；

友情建议：电脑上的所有环境都放在一个文件夹里面，方便管理。

###  5.3、配置环境变量

在我们的系统环境变量中

配置如下配置：

- M2_HOME	maven目录下的bin目录

- MAVEN_HOME    maven的目录
- 在系统的path中配置 %MAVEN_HOME%\bin

![image-20210410161532235](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210410161532235.png)

测试Maven是否配置成功，保证必须配置完毕！

### 5.4、阿里云镜像

- 镜像：mirrors

  - 作用：加速我们的下载

- ​	国内建议使用阿里云的镜像

  ``` xml
  <mirror>
      <id>aliyunmaven</id>
      <mirrorOf>*</mirrorOf>
      <name>阿里云公共仓库</name>
      <url>https://maven.aliyun.com/repository/public</url>
  </mirror>
  ```

### 5.5、本地仓库

在本地的仓库，远程仓库；

**建立个本地仓库**：localrepository

``` xml
<localRepository>D:\Maven\apache-maven-3.8.1\maven_repo</localRepository>
```

### 5.6、在IDEA中使用Maven

1、使用IDEA

2、创建一个Maven Web项目

![image-20210410171301320](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210410171301320.png)

3、等待项目

![image-20210410170228845](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210410170228845.png)

4、观察Maven仓库中多了什么东西？

5、IDEA中的Maven设置

​	IDEA项目创建成功后，看一眼Maven的配置，

![](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210410170704678.png)

6.到这里，Maven在IDEA中的配置和使用就OK了

### 5.7、创建一个普通的Maven项目

![image-20210410171839569](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210410171839569.png)

这个只有在Web应用下才会有！

![image-20210420162936089](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420162936089.png)

### 5.8、在idea中标记文件夹功能

项目结构配置

![image-20210420163458997](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420163458997.png)

### 5.9、在IDEA中配置tomcat

![image-20210420164458439](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420164458439.png)

![image-20210420164700924](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420164700924.png)

解决警告问题

必须要的配置：**为什么会有这个问题：我们访问一个网站，需要指定一个文件夹的名字**

![image-20210420165154599](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420165154599.png)

点击运行

![image-20210420165727725](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420165727725.png)

![image-20210420165715869](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420165715869.png)

![image-20210420170108783](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420170108783.png)

### 5.10、pom文件

pom.xml是maven的核心配置文件

![image-20210420172934253](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420172934253.png)

maven由于他的约定大于配置，我们之后可以能遇到我们写的配置文件，无法被导出或者生效的问题，解决方案：

``` xml
<!--    在build中配置resources，来防止我们资源导出失败的问题-->
    <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <excludes>
                    <exclude>**/*.properties</exclude>
                    <exclude>**/*.xml</exclude>
                </excludes>
                <filtering>true</filtering>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>
```

### 5.12IDEA操作

Maven中jar包的联系关联图

![image-20210420173511721](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420173511721.png)

### 5.13、解决遇到的问题（未完成）

1.Maven3.6.2

2.Tomcat闪退

3.IDEA中每次都要重复配置Maven

4.Maven项目中Tomcat无法配置

## 6、Servlet

### 6.1、Servlet简介

- Servlet就是sun公司开发动态web的一门技术
- Sun在这些API中提供一个接口叫做：Servlet，如果你想开发一个Sevlet程序，只需要完成两个小步骤
  - 编写一个类，实现Servlet接口
  - 把开发好的java类部署到web服务器中

**把实现了Servlet接口的Java程序叫做，Servlet**

### 6.2、HelloServlet

Servlet接口Sun公司有两个默认的实现类：HttpServlet

1.构建一个普通的Maven项目，删掉里面的src目录，以后我们的学习就在这个项目里面建立module

这个空的工程就是Maven的主工程

2.关于Maven父子工程的理解：

父项目会有

```xml
<modules>
    <module>servelt-1</module>
</modules>
```

子项目会有

parent（目前版本没有）

父项目中的java子项目可以直接使用

3.Maven环境优化

​		1.修改web.xml为最新的

​		2.将maven的结构搭建完整

4.编写一个servlet程序

​		1.编写一个普通类

​		2.实现Servlet接口，这里我们直接继承HttpServlet

![image-20210420220820501](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420220820501.png)

``` java
package com.czl.servlet;

import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

public class Helloservlet extends HttpServlet {
    //由于get和post只是请求实现的不同方式，可以相互调用，业务逻辑都一样

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        PrintWriter writer = resp.getWriter();//相应流
//        ServletOutputStream outputStream = resp.getOutputStream();
        writer.print("Hello,Servlet");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }
}
```

5.编写Servlet的映射

​	为什么需要映射：我们写的是Java程序，但是要通过浏览器访问，而浏览器需要连接web服务器，所以我们需要在web服务中注册我们写的Servlet，还需要给他一个浏览器能够访问的路径

```xml
<!--    注册servlet-->
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.czl.servlet.Helloservlet</servlet-class>
    </servlet>
<!--    /////-->
<!--    Servlet的请求路径-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>hello</url-pattern>
    </servlet-mapping>
```

6.配置Tomcat

​	注意：配置项目发布的路径就可以了

​	创一个本地的tomcat server，

7.启动测试，ok

### 6.3、Servlet原理

Servlet是由web服务器调用，web服务器

![image-20210420221715205](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420221715205.png)

![image-20210420221939527](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210420221939527.png)

这里面的web容器就是tomcat

### 6.4、Mapping问题

1、一个servlet可以指定一个映射路径

``` xml
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
```

2、一个servlet可以指定多个映射路径

```xml
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello2</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello3</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello4</url-pattern>
</servlet-mapping>
```

3、一个servlet可以指定通用映射路径

```xml
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello/*</url-pattern>
</servlet-mapping>
```

4、默认请求路径

``` xml
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/*</url-pattern>
</servlet-mapping>
```

5.指定一些后缀或者前缀等等...

``` xml
<!--    可以自定义后缀实现请求映射
        注意点，*前面不能加映射的路径
-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>*.czl</url-pattern>
    </servlet-mapping>
```

6.优先级问题

​	指定了固有的路径优先级最高，如果找不到就会走默认的处理请求；

```xml
<!--404-->
    <servlet>
        <servlet-name>error</servlet-name>
        <servlet-class>com.czl.servlet.errorservlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>error</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>
```

### 6.5、ServletContext

web容器在启动的时候，它会为每个web程序都创建一个对应的ServletContext对象，它代表了当前的web应用。

![image-20210422162233130](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210422162233130.png)

#### 1、共享数据

我在这个Servlet中保存的数据，可以在另一个servlet中拿到

``` java
public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//        this.getInitParameter();//初始化参数
//        this.getServletConfig();//Servlet配置
        ServletContext context = this.getServletContext();//Servlet上下文
        String username="陈志龙";//数据
        context.setAttribute("username",username);//将一个数据保存在了sevletcontext中，名字为：username，值为username
        System.out.println("hello");
    }
}
```

``` java
public class GetServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        String username = (String) context.getAttribute("username");

//        resp.setContentType("text/html;charset=utf-8");
        resp.setContentType("text/html");
        resp.setCharacterEncoding("utf-8");
        resp.getWriter().print("名字"+username);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req,resp);
    }
}
```

``` xml
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.czl.servlet.HelloServlet</servlet-class>
<!--        <init-param>-->
<!--            <param-name></param-name>-->
<!--            <param-value></param-value>-->
<!--        </init-param>-->
    </servlet>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
    <servlet>
        <servlet-name>getc</servlet-name>
        <servlet-class>com.czl.servlet.GetServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>getc</servlet-name>
        <url-pattern>/get</url-pattern>
    </servlet-mapping>
```

测试访问结果：



#### 2、获取初始化参数

```xml
	<!--    配置一些web应用初始化参数-->
    <context-param>
        <param-name>url</param-name>
        <param-value>jdbc:mysql://localhost:3306/mybatis</param-value>
    </context-param>
```

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    ServletContext context=this.getServletContext();
    String url = context.getInitParameter("url");
    resp.getWriter().print(url);
}
```

#### 3、请求转发

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    ServletContext context=this.getServletContext();
    System.out.println("进入了servlet demo 04");
    //        RequestDispatcher requestDispatcher = context.getRequestDispatcher("/gp");//转发的请求路径
    //        requestDispatcher.forward(req,resp);//调用forward转发
    context.getRequestDispatcher("/gp").forward(req,resp);
}
```

![image-20210510155656448](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210510155656448.png)

#### 4、读取资源文件

```
Properties
```

- 在java目录下新建properties
- 在resource目录下新建properties

发现：都被打包到了同一个路径下面：classes，我们俗称这个路径为classpath;

思路：需要一个文件流

``` properties
username=czl
password=123456
```

```java
public class ServletDemo05 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        InputStream is = this.getServletContext().getResourceAsStream("/WEB-INF/classes/com/czl/servlet/11.properties");
        Properties properties = new Properties();
        properties.load(is);
        String username = properties.getProperty("username");
        String password = properties.getProperty("password");
        resp.getWriter().print(username+":"+password);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

访问测试即可OK

### 6.6、HttpServletResponse

web服务器接收到客户端的http请求，针对这个请求，分别创建一个代表请求的HttpServletRequest对象，代表响应的HttpServletResponse；

- 如果要获取我们客户端请求过来的参数：找HttpServletRequest
- 如果要给客户端响应一些信息：找HttpServletResponse

#### 1、简单分类

负责向浏览器发生数据的方法

```java
public ServletOutputStream getOutputStream() throws IOException;
//中文用writer
public PrintWriter getWriter() throws IOException;
```

负责向浏览器发送响应头的方法

```java
public void setCharacterEncoding(String charset);

public void setContentLength(int len);

public void setContentLengthLong(long len);

public void setContentType(String type);

public void setDateHeader(String name, long date);

public void addDateHeader(String name, long date);

public void setHeader(String name, String value);

public void addHeader(String name, String value);

public void setIntHeader(String name, int value);

public void addIntHeader(String name, int value);
```

响应的状态码

```java
public static final int SC_CONTINUE = 100;

/**
 * Status code (101) indicating the server is switching protocols
 * according to Upgrade header.
 */
public static final int SC_SWITCHING_PROTOCOLS = 101;

/**
 * Status code (200) indicating the request succeeded normally.
 */
public static final int SC_OK = 200;

/**
 * Status code (201) indicating the request succeeded and created
 * a new resource on the server.
 */
public static final int SC_CREATED = 201;

/**
 * Status code (202) indicating that a request was accepted for
 * processing, but was not completed.
 */
public static final int SC_ACCEPTED = 202;

/**
 * Status code (203) indicating that the meta information presented
 * by the client did not originate from the server.
 */
public static final int SC_NON_AUTHORITATIVE_INFORMATION = 203;

/**
 * Status code (204) indicating that the request succeeded but that
 * there was no new information to return.
 */
public static final int SC_NO_CONTENT = 204;

/**
 * Status code (205) indicating that the agent <em>SHOULD</em> reset
 * the document view which caused the request to be sent.
 */
public static final int SC_RESET_CONTENT = 205;

/**
 * Status code (206) indicating that the server has fulfilled
 * the partial GET request for the resource.
 */
public static final int SC_PARTIAL_CONTENT = 206;

/**
 * Status code (300) indicating that the requested resource
 * corresponds to any one of a set of representations, each with
 * its own specific location.
 */
public static final int SC_MULTIPLE_CHOICES = 300;

/**
 * Status code (301) indicating that the resource has permanently
 * moved to a new location, and that future references should use a
 * new URI with their requests.
 */
public static final int SC_MOVED_PERMANENTLY = 301;

/**
 * Status code (302) indicating that the resource has temporarily
 * moved to another location, but that future references should
 * still use the original URI to access the resource.
 *
 * This definition is being retained for backwards compatibility.
 * SC_FOUND is now the preferred definition.
 */
public static final int SC_MOVED_TEMPORARILY = 302;

/**
* Status code (302) indicating that the resource reside
* temporarily under a different URI. Since the redirection might
* be altered on occasion, the client should continue to use the
* Request-URI for future requests.(HTTP/1.1) To represent the
* status code (302), it is recommended to use this variable.
*/
public static final int SC_FOUND = 302;

/**
 * Status code (303) indicating that the response to the request
 * can be found under a different URI.
 */
public static final int SC_SEE_OTHER = 303;

/**
 * Status code (304) indicating that a conditional GET operation
 * found that the resource was available and not modified.
 */
public static final int SC_NOT_MODIFIED = 304;

/**
 * Status code (305) indicating that the requested resource
 * <em>MUST</em> be accessed through the proxy given by the
 * <code><em>Location</em></code> field.
 */
public static final int SC_USE_PROXY = 305;

 /**
 * Status code (307) indicating that the requested resource 
 * resides temporarily under a different URI. The temporary URI
 * <em>SHOULD</em> be given by the <code><em>Location</em></code> 
 * field in the response.
 */
public static final int SC_TEMPORARY_REDIRECT = 307;

/**
 * Status code (400) indicating the request sent by the client was
 * syntactically incorrect.
 */
public static final int SC_BAD_REQUEST = 400;

/**
 * Status code (401) indicating that the request requires HTTP
 * authentication.
 */
public static final int SC_UNAUTHORIZED = 401;

/**
 * Status code (402) reserved for future use.
 */
public static final int SC_PAYMENT_REQUIRED = 402;

/**
 * Status code (403) indicating the server understood the request
 * but refused to fulfill it.
 */
public static final int SC_FORBIDDEN = 403;

/**
 * Status code (404) indicating that the requested resource is not
 * available.
 */
public static final int SC_NOT_FOUND = 404;

/**
 * Status code (405) indicating that the method specified in the
 * <code><em>Request-Line</em></code> is not allowed for the resource
 * identified by the <code><em>Request-URI</em></code>.
 */
public static final int SC_METHOD_NOT_ALLOWED = 405;

/**
 * Status code (406) indicating that the resource identified by the
 * request is only capable of generating response entities which have
 * content characteristics not acceptable according to the accept
 * headers sent in the request.
 */
public static final int SC_NOT_ACCEPTABLE = 406;

/**
 * Status code (407) indicating that the client <em>MUST</em> first
 * authenticate itself with the proxy.
 */
public static final int SC_PROXY_AUTHENTICATION_REQUIRED = 407;

/**
 * Status code (408) indicating that the client did not produce a
 * request within the time that the server was prepared to wait.
 */
public static final int SC_REQUEST_TIMEOUT = 408;

/**
 * Status code (409) indicating that the request could not be
 * completed due to a conflict with the current state of the
 * resource.
 */
public static final int SC_CONFLICT = 409;

/**
 * Status code (410) indicating that the resource is no longer
 * available at the server and no forwarding address is known.
 * This condition <em>SHOULD</em> be considered permanent.
 */
public static final int SC_GONE = 410;

/**
 * Status code (411) indicating that the request cannot be handled
 * without a defined <code><em>Content-Length</em></code>.
 */
public static final int SC_LENGTH_REQUIRED = 411;

/**
 * Status code (412) indicating that the precondition given in one
 * or more of the request-header fields evaluated to false when it
 * was tested on the server.
 */
public static final int SC_PRECONDITION_FAILED = 412;

/**
 * Status code (413) indicating that the server is refusing to process
 * the request because the request entity is larger than the server is
 * willing or able to process.
 */
public static final int SC_REQUEST_ENTITY_TOO_LARGE = 413;

/**
 * Status code (414) indicating that the server is refusing to service
 * the request because the <code><em>Request-URI</em></code> is longer
 * than the server is willing to interpret.
 */
public static final int SC_REQUEST_URI_TOO_LONG = 414;

/**
 * Status code (415) indicating that the server is refusing to service
 * the request because the entity of the request is in a format not
 * supported by the requested resource for the requested method.
 */
public static final int SC_UNSUPPORTED_MEDIA_TYPE = 415;

/**
 * Status code (416) indicating that the server cannot serve the
 * requested byte range.
 */
public static final int SC_REQUESTED_RANGE_NOT_SATISFIABLE = 416;

/**
 * Status code (417) indicating that the server could not meet the
 * expectation given in the Expect request header.
 */
public static final int SC_EXPECTATION_FAILED = 417;

/**
 * Status code (500) indicating an error inside the HTTP server
 * which prevented it from fulfilling the request.
 */
public static final int SC_INTERNAL_SERVER_ERROR = 500;

/**
 * Status code (501) indicating the HTTP server does not support
 * the functionality needed to fulfill the request.
 */
public static final int SC_NOT_IMPLEMENTED = 501;

/**
 * Status code (502) indicating that the HTTP server received an
 * invalid response from a server it consulted when acting as a
 * proxy or gateway.
 */
public static final int SC_BAD_GATEWAY = 502;

/**
 * Status code (503) indicating that the HTTP server is
 * temporarily overloaded, and unable to handle the request.
 */
public static final int SC_SERVICE_UNAVAILABLE = 503;

/**
 * Status code (504) indicating that the server did not receive
 * a timely response from the upstream server while acting as
 * a gateway or proxy.
 */
public static final int SC_GATEWAY_TIMEOUT = 504;

/**
 * Status code (505) indicating that the server does not support
 * or refuses to support the HTTP protocol version that was used
 * in the request message.
 */
public static final int SC_HTTP_VERSION_NOT_SUPPORTED = 505;
```

#### 2、常见应用

​	1、向浏览器输出消息（一直在讲，不说了）

​	2、下载文件 

​			1.要获取下载文件的路径

​			2.下载的文件名是啥？

​			3.设置想办法让浏览器能够支持下载我们需要的东西

​			4.获取下载文件的输入流

​			5.创建缓冲区

​			6.获取OutputStream对象

​			7.将FileOutputStream流写入到buffer缓冲区

​			8.使用OutputStream将缓冲区中的数据输出到客户端！



### 6.7、HttpServletRequest