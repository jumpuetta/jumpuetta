---
layout: post
title: 定位java进程中最消耗cpu线程，并定位问题代码
date: 2018-01-31
categories: blog
tags: [java,thread,cpu]
subtitle: 系统cpu使用率过高,java进程占用单核cpu一直保持在100%上下，原因排除
---

## 场景 ##
系统cpu使用率过高,java进程占用单核cpu一直保持在100%上下

## 问题排查 ##
  1.
 top命令查看系统资源使用情

![](/attach/20180131001.png)

  可以看到进程ID:33026的java进程占用cpu最多，基本霸占了一个cpu核心。


  2.
 继续top查看一下33026这个进程的子进程。

```shell
top -p 33026 -H  
```

![](/attach/20180131002.png)

  该名称显示对应进程下的线程资源使用情况,现在可以看到罪魁祸首为33027的线程


  3.
 将这个pid转换为16进制
  
```shell
printf "%x\n" 33027
#结果：8103
```

  4.
 用jstack打印出父进程的栈，从而找到pid为8103的这个线程的栈信息。

```shell
jstack 33026 | grep 8103 -A 10 -B 10
```

![](/attach/20180131003.png)

  可以看到8103对应的java线程为main方法主线程。

![](/attach/20180131004.png)

  在看代码可以非常好理解，因为死循环生成随机数导致cpu资源使用率过高。

  值得注意：在线程中使用类似while(true)的操作时，若线程中抛出异常，需要在catch中适当睡眠线程，防止因为代码异常而导致无阻塞死循环引起cpu耗尽。

```java
while(true) {
	try{
		// 可能会发生异常
	} catch (异常) {
	    Thread.sleep(1000);
	}
}
```