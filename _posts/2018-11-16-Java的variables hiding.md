---
layout: post
title: Java的variable hiding
---

Java的多态在变量上是不体现的，引用变量时，只根据声明的类型绑定变量而不是根据实例。
当子类和父类有同名变量时，子类的变量将会 hide 父类的变量。

	class Parent {
		String x = "parent";
	}

	class Child extends Parent {
		String x = "child";
	}

	public void test() {
		Parent instance = new Child();
		System.out.println(instance.x);
	}

这段代码打印出的是parent。