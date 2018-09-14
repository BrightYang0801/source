---
title: git修改分支名字
date: 2018-09-03 15:54:11
tags:
  - git
categories:
  - git
---

# git 修改分支名称

假设分支名称为 oldName
想要修改为 newName

1. ** 本地分支重命名(还没有推送到远程) **

```
git branch -m oldName newName
```

2. ** 远程分支重命名 (已经推送远程-假设本地分支和远程对应分支名称相同) **
   a. ** 重命名远程分支对应的本地分支 **
   ```
   git branch -m oldName newName
   ```
   b. ** 删除远程分支 **
   ```
   git push --delete origin oldName
   ```
   c. ** 上传新命名的本地分支 **
   ```
   git push origin newName
   ```
   d. ** 把修改后的本地分支与远程分支关联 **
   ```
   git branch --set-upstream-to origin/newName
   ```
