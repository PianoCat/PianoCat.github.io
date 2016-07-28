---
layout: post
title: 聊聊Java中的异常吧
category: 编程语言
tags: [Java]
---

![exception](https://raw.githubusercontent.com/PianoCat/Blog_imgs/master/images_2016/java_exception.jpg)

---

在Java的异常体系中，`Throwable `类是所有错误或异常的超类，`Error`和`Exception`两个类是他的子类。

`Error`类是应用程序一般不会出现的问题，通常由JVM自己处理。这个类又包含了`VirtulMachineError`和`AWTError`，`VirtulMachineError`类包括`StackOverFlowError`和`OutOfMemoryError`两个类。

`Exception`类包含了合理地应用程序想要捕获的异常，包括`IOException`和`RuntimeException`两个异常，这两个异常都很常见。

---

关于异常，我们还应该知道，Java中的异常可以分为`可查的异常(checked exceptions)`和`不可查的异常(unchecked exceptions)`两种。

* **可查异常**（编译器要求必须处理的异常）：正确的程序在运行中，很容易出现的、情理可容的异常状况。可查异常虽然是异常状况，但在一定程度上他的发生是可以预计的，而且一旦发生这种异常状况，就必须采取某种方式进行处理。

除了`RuntimeException`及其子类以外，其他的`Exception`类及其子类都属于可查异常。这种异常的特点是Java编译器会检查他，也就是说，当程序中可能出现这种异常，要么用`try-catch`语句捕获他，要么用`throws`子句声明抛出他，否则编译不会通过。

* **不可查异常**（编译器不要求强制处理的异常）：包括`运行时异常（RuntimeException与其子类）`和`错误（Error）`。
