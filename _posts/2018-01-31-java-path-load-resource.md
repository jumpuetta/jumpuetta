---
layout: post
title: java读取资源文件，路径定位
date: 2018-01-31
categories: blog
tags: [java]
subtitle: java读取资源文件，路径定位
---


```java
public class Loader {

	public static void main(String[] args) throws IOException {
		String path = Thread.currentThread().getContextClassLoader().getResource(".").getPath();
		System.out.println(path); // 程序根目录

		String string = Loader.class.getClassLoader().getResource(".").getPath();
		System.out.println(string); // 程序根目录

		String string2 = Loader.class.getResource(".").getPath();
		System.out.println(string2); // 当前类所在目录

		System.out.println(Thread.currentThread().getContextClassLoader()); // 当前线程的类加载器
		System.out.println(Loader.class.getClassLoader()); // 当前类的类加载器
		System.out.println(ClassLoader.getSystemClassLoader()); // 系统初始的类加载器

		Enumeration<URL> urls = Loader.class.getClassLoader().getResources("system.properties");
		while (urls.hasMoreElements()) {
			URL url = urls.nextElement();
			System.out.println(url.getPath());
		}	
	}
}
```

	new  File()代表的所有javaIO文件读取  
	
	new File("box.txt")： 读取的是程序（src）目录下的box.txt。它的当前目录是程序（src）所在目录；  
	
	new File("/box.txt")：读取的是程序所在磁盘下的box.txt（假设程序文件在E盘，则对应文件目录为：E:/box.txt）；  
	
	类名.class.getResource().getPath()代表的程序内部资源读取  
	
	类名.class.getResource("box.txt").getPath()：获取的是当前类同目录下的box.txt。它的当前目录是类本身所在目录；  
	
	类名.class.getResource("/box.txt").getPath()：获取的是程序根目录（src）目录下的box.txt。  
	
	类名.class.getClassLoader().getResourceAsStream()  
	
	无论要查找的资源前面是否带'/' 都会从classpath的根路径下查找。  