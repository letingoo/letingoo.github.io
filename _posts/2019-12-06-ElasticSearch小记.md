---
layout: post
title: ElasticSearch 小记
---

目前线上和测试环境使用的是 6.3.1 版本, 最新版是7+, 明显的改动应该是版本7去掉了type的概念, 版本6里一个index只能有一个type。


创建 ES 索引:

  put index {
    "settings": {
      "index": {
        "number_of_shards": 3,
        "number_of_replicas": 2
      }
    },
    "mappings": {
      "<type>": {
        "properties": {
          "field1": {"type": "text"},
          "myKeyWord": {"type": "keyWord"}
        }
      }
    }
  }


  ES中的若干属性, _source属性： _source属性默认是开启的，如果某个字段的内容很多，业务只需要能对该字段进行搜索，最后返回文档id，查看文档内容需要在mysql中或HBase或者其他DB
  中取数据，如果把大字段的内容也存在ES里只会增大索引，浪费空间, 如果需要关闭 _source, 可以这样设置

  "<type>": {
    "_source": {"enabled": false}
  }

  这样是全局生效，如果指向存储某几个字段的原始值到ES，可以通过include参数来设置， "_source":{"includes": ["field1", "field2"]}

  ES使用kibana做可视化客户端
