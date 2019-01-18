---
layout: post
title: SimpleDateFormat线程不安全问题
---


Date转String时经常使用SimpleDateFormat这个类，但是这个类并不是线程安全的，在该类的format方法中，
会对一个calendar成员变量setTime，然后再根据这个calendar拼字符串，这一过程不是线程安全的，多线程环境下
可能造成错误的输出。

解决方法是：

1. 用ThreadLocal包装。

ThreadLocal<SimpleDateFormat> safe = new ThreadLocal() {

	@Override
	protected Object initialValue() {
		return new SimpleDateFormat("yyyy-MM-dd");
	}
}


2. 用JDK8提供的DateTimeFormatter

3. 用apache-common提供的FastDateFormat
