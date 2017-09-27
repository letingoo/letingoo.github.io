---
layout: post
title: Lambda表达式
---


Lambda表达式是Java 8中引入的，为Java添加了缺失的函数式编程特点。
Lambda表达式是一种匿名函数，通常用 >(argument) -> (body)语法书写。

一些Lambda表达式的例子：
1. 匿名实现Runnable接口：
```
new Thread(
	() -> System.out.println("Hello world")
).start();
```


2.遍历列表：
```
//old style
List<Integer> list = Arrays.asList(1,2,3,4,5);
for (int n : list) {
	System.out.println(n);
}

// Lambda
List<Integer> list = Arrays.asList(1,2,3,4,5);
list.foreach(n -> System.out.println(n));
```

