---
layout: post
title: JVM的metaspace
---

JDK8以后，JVM不再有PermGen（永久代），取而代之的是Metaspace。

Metaspace由这两部分组成： Klass Metaspace：存Klass，Klass是class文件在jvm里运行时的数据结构。但是A.class实际上是存在heap里。该内存不是必须的
NoKlass Metaspace: 存Klass相关的其他内容，如method，ConstantPool等，这块内存是不连续的，是必须的，有的情况下是可以存Klass的。


Metaspace和永久代类似，都是对JVM规范中方法区的实现。不过Metaspace不在JVM中，而是在内地内存里