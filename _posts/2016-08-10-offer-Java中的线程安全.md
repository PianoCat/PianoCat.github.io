---
layout: post
title: Java中的线程安全
category: 编程语言
tags: [线程]
---

### Java中的线程安全 ###

* 什么是线程安全？

如果你的代码进程中有多个线程在同时运行，而这些线程可能会同时运行这段代码。如果每次运行结果和单线程运行的结果是一样的，而且其他的变量值也和预期的是一样的，就是线程安全的。

线程安全问题都是由`全局变量`和`局部变量`引起的。

若每个线程中对全局变量、静态变量只有读操作，而无写操作，一般来说，这个全局变量是线程安全的；若有多个线程同时执行写操作，一般都需要考虑线程同步，否则的话就可能影响线程安全。

---

下面来讲讲Java中的容器类有哪些是线程安全的，哪些不是线程安全的？

首先，Java中容器类的关系是这样的：

Collection:{List{LinkedList;ArrayList;Vector{Stack}};set};

Map:{Hashtable;HashMap;WeakHashMap}.

>LinkedList和ArrayList都是不同步的，线程不安全；

>Vector（相当于是一个线程安全的List）和Stack都是同步的，线程安全；

>Set是线程不安全的；

>Hashtable的方法是同步的，线程安全；

>HashMap的方法不是同步的，线程不安全。

另外，StringBuffer是线程安全的，相当于一个线程安全的StringBuilder; Properties实现了Map接口，是线程安全的。
