---
layout: post
title: lsof命令
---


在Linux系统中，任何事物都是文件，网络连接和硬件也被当做硬件。lsof命令是一个系统级的监控、诊断工具。
lsof文件可以查看

* 普通文件
* 目录
* 网络文件系统的文件
* 字符或者设备文件

直接lsof会列出系统内所有打开的文件

lsof -p pid 可以列出pid进程打开的所有文件

lsof -u user 可以列出user打开的所有文件

lsof比较常用的是查看网络信息

lsof -i 是查看所有的网络信息。 lsof -i TCP 可以只显示TCP协议的连接信息

lsof -i:port 可以查看port端口的占用情况，但是有时候会查到对端的端口信息。比如lsof -i:80 可能不是本地的80端口，而是对到了对端的80端口。
netstat -anp 也可以查看端口占用的情况。
