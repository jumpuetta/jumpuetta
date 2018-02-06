---
layout: post
title: Spring-Boot整合jsp
date: 2018-01-26
categories: java
tags: [spring boot]
subtitle: 虽然Spring-Boot整合jsp是个简单的事,但自己确实踩了几下坑,记下来吧！总觉得spring的东西用熟了顺手，初期不熟时项目部署起来都各种心酸。
---

spring-boot官方不推荐使用jsp,自己项目中也没用到,但作为学习,还是想尝试下用spring-boot整合jsp,中间踩了很多坑，还是记录下吧。

## 配置pom.xml文件 ##
```xml
<dependencyManagement>
        <dependencies>
            <dependency>
                <!-- Import dependency management from Spring Boot -->
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>1.3.6.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
			<dependencies>
			    <dependency>
			        <groupId>org.springframework.boot</groupId>
			        <artifactId>spring-boot-starter-web</artifactId>
			    </dependency>
			
			    <!--配置servlet-->
			    <dependency>
			        <groupId>javax.servlet</groupId>
			        <artifactId>javax.servlet-api</artifactId>
			    </dependency>
			
			    <!--配置jsp jstl的支持-->
			    <dependency>
			        <groupId>javax.servlet</groupId>
			        <artifactId>jstl</artifactId>
			    </dependency>
			
			    <dependency>
			        <groupId>org.apache.tomcat.embed</groupId>
			        <artifactId>tomcat-embed-jasper</artifactId>
			    </dependency>
			</dependencies>
        </dependencies>
    </dependencyManagement>
```

## 添加WEB-INF目录 ##
在src/main目录下新建webapp/WEB-INF/jsp目录,并编写自己的jsp页面
![](/attach/20180126001.png)



## 配置application.properties ##
```properties
server.port=9100
server.contextPath=/web
server.session.timeout=1200
spring.mvc.view.prefix=/WEB-INF/jsp/ #页面默认前缀目录
spring.mvc.view.suffix=.jsp #响应页面默认后缀
```
1.当parent标签中引入的是1.3.6版本的话,那么applicaion.properties中配置jsp前缀和后缀的时候应该配置如下,一定要带上mvc
```properties
spring.mvc.view.prefix=/WEB-INF/jsp/
spring.mvc.view.suffix=.jsp
```
2.当parent标签中引入的是低版本的话,那么applicaion.properties中配置jsp前缀和后缀的时候应该配置如下,一定不要带上mvc
```properties
spring.view.prefix=/WEB-INF/jsp/
spring.view.suffix=.jsp
```
具体从哪一个版本开始变化没做研究

## 启动类继承SpringBootServletInitializer ##
这个是必须的,容易漏掉
```java
@EnableAutoConfiguration
@SpringBootApplication
@ComponentScan(value = "com.sylar.springboot.web")
public class AppServer extends SpringBootServletInitializer{
    public static void main(String[] args) {
        SpringApplication.run(AppServer.class, args);
    }
}
```

## controller ##

```java
@RequestMapping("/jsp")
public String helloJsp(Map<String,Object> map){
    map.put("value", "hello");
    return"index";
}
```

## 运行项目 ##

可以因为项目打包结构的问题,用idea直接运行项目访问 http://localhost:9100/web/hello/jsp 总是提示404错误,似乎无法找到响应的jsp页面
![](/attach/20180126001.png)

在网上看见同样问题，用mvn的spring-boot插件启动能正常访问，具体在pom.xml中添加如下配置：
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

进入pom.xml所在文件夹
执行mvn spring-boot:run
访问 http://localhost:9100/web/hello/jsp 正常
