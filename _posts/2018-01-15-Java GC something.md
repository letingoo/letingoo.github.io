---
layout: post
title: 2018-01-15-Java GC something
---

从年轻代空间回收内存称为Minor GC，从老年代回收内存是Major GC，Full GC 是清理整个堆空间。

如果应用中存在大量的短期对象，应该选择调大年轻代的空间。如果存在较多的持久对象，应该选择调大老年代的空间。

JVM一些常用参数：

Xmx：堆内存的最大值

Xms：堆内存的初始值

Xmn：新生代的大小

Xss：栈的大小

PretenureSizeThreshold: 直接分配到老年代的对象大小，大于此阈值的对象将直接在老年代中分配

MaxTenuringThresold： 新生代晋升到老年代的年龄，每个对象经历过一次 Minor GC之后，年龄会加一，超过次阈值后对象会进入老年代

SurvivorRatio：新生代和老年代区域的容量之比，默认为8


Java的收集器：
1.Serial收集器：会产生STW。是client模式下的默认的新生代收集器。采用标记-整理算法，
2.ParNew收集器：Serial的多线程实现。也会产生STW
3.Parallel Scavenge收集器：采用复制算法。
4.CMS收集器：是一种获取最短回收停顿时间为目标的收集器，是基于标记清除算法。共分四个步骤：
①初始标记
②并发标记
③重新标记
④并发清除

①和③仍然会STW