---
layout: post
title: nginx location截断的问题
---

nginx配置文件中，proxy_pass里如果尾部带/，则会截断匹配的url，
如果尾部不带/，则不会截断匹配的url。

