---
layout: post
title: git rebase命令
---

rebase命令平常用的比较少，通常都用merge了，记录一下这个命令

用merge会产生非常乱的提交树，rebase在合并的时候只会产生一条直线。

假如当前分支为dev，使用 git rebase master, 则会将dev上分叉的commit重新指向master最新commit的后面。

git pull --rebase 可以让merge变成rebase的操作


---
rebase和merge的区别:

merge会产生一个新的commit，但是commit比较频繁时，分支历史很混乱。

rebase是先找公共祖先，之前的commit历史会被抹除。

不要rebase公共分支（如master分支等），不然会很容易产生冲突
