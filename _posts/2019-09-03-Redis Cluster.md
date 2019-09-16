---
layout: post
title: Redis Cluster 小记
---

Redis Cluster 中，每个节点都是有若干slave的，每个节点之间都是两两通信的，所以每个节点需要两个TCP端口，一个用于相应client端的交互，
另一个用户节点之间通信，两个端口的差值默认为10000。节点之间的连接用于宕机检测等。

hash clots是redis cluster的一个重要概念，一个cluster中有16384个hash clot，每个key通过CRC16哈希取模之后决定key所属的slot，
每个节点负责一部分clot。一个节点下线后，它上面原有的clot会被其他节点均分。

节点的fail是通过集群里超过半数master节点检测失败失效时生效的，集群将失效节点的一个slave选为新的master。用的什么协议还在研究

Redis Cluster是不支持 multi-key操作的，即Cluster不能进行跨Node的操作

Redis集群中，Master和Slave是异步replication的，可能在 Master发送异步写之后，Master挂掉导致这次写失败。

Redis Cluster使用gossip协议传播协同自动化修复集群的状态，不同于集中式将节点信息、故障等集中存储在某个节点上，而是互相之间不断通信保持整个集群之间的节点数据是完整的。Redis Cluster用gossip协议交换的信息有 故障信息、节点的增加和移除、hash slot信息等
