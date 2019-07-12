---
layout: post
title: Spring Cloud Gatewway 路由转发
---


对于Spring Cloud Gateway的路由转发机制一直比较迷，简单研究一下。

Gateway基于 Spring5，Reactor和Spring Boot2，使用非阻塞API。大量Reactor的代码让gateway比较难懂....

顺序是 RoutePredicateHandlerMapping -> FilterWebHandler -> 各种Filter

在RouteRredicateHandlerMapping中，getHandlerInternal的lookupRoute会遍历所有Route列表，选择合适的Route节点进行转发。

Gateway依赖的Reactor方式: Reactor是基于JVM的一个经典的异步库。Flux和Mono是Reactor两个重要的概念。
Flux代表的是0-N个元素的异步序列，
在这一序列中可以包括三种不同类型的消息: 正常的包含元素的消息，序列结束的消息和序列出错的消息。当消息通知产生时，订阅者对应方法的onNext, 
onComplete和onError会被调用。
Mono代表的是0或者1个元素的异步序列，该序列中同样可以包含与Flux相同的三种类型通知。Flux和Mono之间可以进行转换。

Mono和Flux都实现了org。reactivestreams.Publisher接口

