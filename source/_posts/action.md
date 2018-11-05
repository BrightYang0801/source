---
title: git
date: 2018-09-14 15:54:13
tags:
  - git
categories:
  - git
---

1. 多人开发需要创建分支
在终端执行下列命令：
```
 git checkout -b create_product //创建分支 create_product 为创建的分支的名字
 git add .
 git commit -m 'init'
 git push  复制出来的git push 链接
```
 ![image](https://note.youdao.com/yws/api/personal/file/WEB65905f73ff8c6c0f882b952f48417526?method=download&shareKey=400be717732b86e49cdaf9a2013bfcfa)
2. 切换分支
 ```
 git branch -a
 git checkout 你要去的分支的名字
```
3. 将其他分支的修改合并到当前分支
```
 git merge Invoicing //Invoicing分支的名字
 git status
 git add —a
 git commit
 git push
```
4. 拉取主干代码
 ```
 git pull origin develop //develop 为主分支名字
```
