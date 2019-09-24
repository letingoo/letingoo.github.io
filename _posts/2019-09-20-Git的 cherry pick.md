---
layout: post
title: git的cherry-pick
---

git的cherry-pick命令，可以理解为挑选提交的意思, 可以获取一个分支的单此提交，作为一个新的提交合并到当前分支上。

git cherry-pick [<options>] <commit-ish>


用git log显示出 git commit的hash值，然后 git cherry-pick 哈希值即可

如果有冲突，解决后再commit即可
