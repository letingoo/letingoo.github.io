---
layout: post
title: Redis Cluster
---


Redis-Cluster架构中，总共有16384个slot，每个master都分得一部分slot，算法为 clot = crc16(key) % 16384，这样找到对应的slot。
cluster至少要3主3从。正常情况下每个哈希槽只由一个主节点处理，每个主节点都有1-n个slave，当主节点down调，slave可以选举成新的主节点

Redis的主从同步是 异步复制：全量同步 + 命令传播

Redis集群里使用Gossip协议进行节点之间的同步，达到自动发现的目的。Gossip协议利用一种随机的方式将信息散播到整个网络里，分为Push-based和Pull-based两种，
push-based的流程为 一个节点随机选择其他n个节点作为传输对象，迭代地传播信息；  而pull-based的流程是 一个节点随机选择n个节点是否有最新
的信息，n个节点去拉。Gossip协议一般使用UDP协议实现

Redis-Cluster是一种去中心化的分布式实现方案。当master down掉之后，它的slave会竞争成为master，向其他master发请求，类似Raft协议？