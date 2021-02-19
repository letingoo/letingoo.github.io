---
layout: post
title: select poll epoll
---

select poll epoll都属于IO多路复用，其优势就是单个process可以同时处理多个网络连接的IO，其基本原理原理是process会不断地轮询其负责的所有socket，当某个socket有数据到达时，就通知用户进程。select/epoll/poll的优势是能处理更多的连接。

1. select
select具有良好的跨平台支持，一个缺点是单个进程能够见识的文件描述符存在最大限制，Linux默认是1024.

2. poll
poll没有文件描述符的限制，但是poll和select都需要遍历文件描述符以获取就绪的socket，但是同时连接的大量客户端在同一时刻只会有少量处于就绪状态，因此随着描述符的数量增加，效率也会大大下降。

3. epoll
epoll是poll和select的增强版本，相对于select和poll来说，epoll更加灵活，没有描述符限制，epoll使用一个文件描述符管理多个描述符，将用户关系的文件描述符的时间存放到内核的一个事件表中。epoll相当于是有个注册了回调机制。

