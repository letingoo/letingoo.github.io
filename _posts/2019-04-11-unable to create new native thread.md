---
layout: post
title: unable to create new native thread
---

Java应用有时会突然报错：
>Exception in thread “main” java.lang.OutOfMemoryError: unable to create new native thread

刚开始以为是内存不足，但是free命令查了之后发现内存还比较多，这种情况下一般是用户的线程数达到了上限导致的。

ulimit -a  可以查看系统对当前用户的限制，可以注意到max user process 这一项，代表着当前用户最大进程数，
还有其他的一些参数，如最大内存限制和虚拟内存限制。这些参数可以通过ulimit命令（临时生效）或者 改配置文件 /etc/security/limits.conf（永久生效）。
因为Java创建一个线程需要占用一定的栈空间，默认是1M，可以通过 -Xss512k 设置

线程和协程的区别：

1. 线程可以说是特殊化的 1:N 协程，协程和线程的区别是协程交给程序调度而线程交给内核调度。Golang实现了自己的协程--Goroutine，
其内存消耗和切换的开销非常小，默认占用内存只有2K，

