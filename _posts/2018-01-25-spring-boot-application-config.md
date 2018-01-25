---
layout: post
title: SpringBoot常用配置 application.yml /application.properties常用配置介绍
date: 2018-07-25
categories: java
tags: [SpringBoot]
subtitle: SpringBoot常用配置 application.yml /application.properties常用配置介绍
---

前言：springboot集成了主流的第三方框架，但是需要使用springboot那一套配置方式。但是我这里只列举了非常非常常用的。当然官方文档里也有相应的配置，可惜没有注释。

### mvc ###
```properties
spring.mvc.async.request-timeout
设定async请求的超时时间，以毫秒为单位，如果没有设置的话，以具体实现的超时时间为准，比如tomcat的servlet3的话是10秒.
spring.mvc.date-format
设定日期的格式，比如dd/MM/yyyy.
spring.mvc.favicon.enabled
是否支持favicon.ico，默认为: true
spring.mvc.ignore-default-model-on-redirect
在重定向时是否忽略默认model的内容，默认为true
spring.mvc.locale
指定使用的Locale.
spring.mvc.message-codes-resolver-format
指定message codes的格式化策略(PREFIX_ERROR_CODE,POSTFIX_ERROR_CODE).
spring.mvc.view.prefix
指定mvc视图的前缀.
spring.mvc.view.suffix
指定mvc视图的后缀.
```

### messages ###
```properties
spring.messages.basename
指定message的basename，多个以逗号分隔，如果不加包名的话，默认从classpath路径开始，默认: messages
spring.messages.cache-seconds
设定加载的资源文件缓存失效时间，-1的话为永不过期，默认为-1
spring.messages.encoding
设定Message bundles的编码，默认: UTF-8
```