---
layout: post
title: sed 使用
---

sed 是一种在线编辑器 主要用来编辑一个或者多个文件，简化对文件的反复操作


sed [-nefr] [动作]

-n: silent模式, 一般的sed用法中 所有来自STDIN的数据一般会列出在终端上 但是加上-n参数后，只有sed特殊处理的那一行会列出

-e: 直接在命令行模式上进行sed的动作编辑

-f: 直接将sed的动作卸载一个文件内  -f fileName 可以运行fileName里的sed动作

-r: sed的动作支持的是延伸的正规表达式的语法 默认的是基础的正规表达式语法

-i: 直接修改读取的文件内容


function:

a: 新增 新增的字符串在新的一行出现

c: 取代

d: 删除

i: 插入 在上一行出现


例子:

1. 删除某一行: sed '2d' file   删除第2行到末尾所有行:  sed '2,$d' file    删除文件中所有开头是test的行 sed '/^test/d' file

2. 替换 s    sed 's/book/books' file    全面替换  sed 's/book/books/g' file     从第N处开始替换 /Ng  如 sed 's/book/books/2g' file

3. 已匹配字符串标记 &

sed 's/^192.168.0.1/&localhost' file
