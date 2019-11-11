---
layout: post
title: git commit 规范
---

AngularJS的提交规范,格式:


type(scope): subject
<BLANK LINE>
<BODY>
<BLANK LINE>
<footer>


1. type(必须) commit的类别 有以下选项

1.1  feat(feature): 新功能
1.2  fix: 修补bug
1.3  docs: 文档(documents)
1.4  style: 格式, 不懂是什么意思
1.5  refactor 重构
1.6  test 增加测试
1.7  chore  构建过程或者辅助工具的变动
1.8  revert  撤销之前的commit


2. scope(可选) 说明commit影响的范围，如数据层/控制层/视图层  当然也可以有不同的划分


3. subject  是commit的简短描述 不超过50字符，


4. body   是对本次commit的具体描述
