---
layout: post
title: Redis big key
---

大key问题是key对应的value很大，大key会造成的问题如下：

1. 如果类型是string，由于redis单线程运行，则读写大key有可能阻塞服务。

2. 如果是hash，list，set，zset等类型，则如果删除大key也可能阻塞服务。不过新版的redis可以异步删除

3. 大key也可能导致集群的数据倾斜


如何查找大key： redis-cli -bigkeys

删除或遍历大key的方式：用scan命令迭代大key中的元素，分批删除

string 类型控制在10KB以内， hash, list, set, zset 元素不要超过5000

解决大key问题的思路大概是拆分大key。比如拆成多个key-value，用multiGet获取值。
