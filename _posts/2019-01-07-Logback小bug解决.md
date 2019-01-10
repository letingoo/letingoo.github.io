---
layout: post
title: Logback小bug解决
---

发现logback的配置文件失效了，生成不了日志文件。google一番发现是因为项目引入的jar包里有logback.xml，其优先级高于
logback-spring.xml，导致项目的logback配置失效。然后在pom.xml里exclude即可。
先是把logback-spring.xml改名成logback.xml,发现配置重新生效，但是好像logback-spring.xml是鼓励的命名，于是还是继续确定问题，
用maven的命令：mvn dependency:tree 查项目的依赖，再搜logback,发现一个依赖引入了com.bytedance.logback...的jar包。
在idea的extrenal libraries里找到了这个依赖，发现里面确实存在logback.xml。于是在pom里excluede，发现配置重新生效，问题解决。
