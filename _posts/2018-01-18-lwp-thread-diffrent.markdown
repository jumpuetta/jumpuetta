---
layout: post
title:  "Dinosaurs are extinct today"
subtitle: "because they lacked opposable thumbs and the brainpower to build a space program."
date:   2017-10-26 23:45:13 -0400
background: '/img/posts/01.jpg'
author:     "jumpuetta"
---

# 轻量级进程 #

　　在计算机操作系统中,轻量级进程（LWP）是一种实现多任务的方法。与普通进程相比，LWP与其他进程共享所有（或大部分）它的逻辑地址空间和系统资源；与线程相比，LWP有它自己的进程标识符，优先级，状态，以及栈和局部存储区，并和其他进程有着父子关系；这是和类Unix操作系统的系统调用vfork()生成的进程一样的。另外，线程既可由应用程序管理，又可由内核管理，而LWP只能由内核管理并像普通进程一样被调度。Linux内核是支持LWP的典型例子。　　在大多数系统中，LWP与普通进程的区别也在于它只有一个最小的执行上下文和调度程序所需的统计信息，而这也是它之所以被称为轻量级的原因。一般来说，一个进程代表程序的一个实例，而LWP代表程序的执行线程（其实，在内核不支持线程的时候，LWP可以很方便地提供线程的实现）。因为一个执行线程不像进程那样需要那么多状态信息，所以LWP也不带有这样的信息。　　LWP的一个重要作用是提供了一个用户级线程实现的中间系统。LWP可以通过系统调用获得内核提供的服务，因此，当一个用户级线程运行时，只需要将它连接到一个LWP上便可以具有内核支持线程的所有属性。　　而因为LWP之间共享它们的大部分资源，所以它在某些应用程序就不适用了；这个时候就要使用多个普通的进程了。例如，为了避免内存泄漏（a process can be replaced by another one）和实现特权分隔（processes can run under other credentials and have other permissions）。　　使用多个进程也使得应用程序在出现进程池内的进程崩溃或被攻击的情况下变得更加健壮。
