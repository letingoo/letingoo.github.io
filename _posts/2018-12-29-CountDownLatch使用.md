---
layout: post
title: CountDownLatch使用
---

CountDownLatch是一种常用的同步工具类，属于java.util.concurrent包下，作用是使一个线程等待其他线程完成工作后再往下执行，
例如主线程使用了线程池处理N个任务，等待这N个任务执行完再往下执行就可以用CountDownLatch。

CountDownLatch使用的时候，一般是构造函数指定任务数量，然后主线程调用await等待。任务线程执行完自己的逻辑后调用countDown。
一些注意事项：
1. 任务线程的countDown()最好在finally块中执行
2. 主线程的await()最好设置超时时间

CountDownLatch是不能重用的，与CyclicBarrier不同。CountDownLatch底层是基于AQS实现的。

另外调用线程池后等待所有子任务执行完毕也可以用

