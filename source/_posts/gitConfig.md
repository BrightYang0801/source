---
title: git的配置以及使用
date: 2018-09-14 15:54:10
tags:
  - git
categories:
  - git
---

1. ** 配置用户 **

   ```
    zhouhongdeAir:~ zhouhong$ git config --global user.name "zhouhong" //修改你的用户名
    zhouhongdeAir:~ zhouhong$ git config --global user.email "zhouhong@dongwu-inc.com"//修改你的邮箱
    zhouhongdeAir:~ zhouhong$ ssh-keygen -t rsa -C "你的邮箱地址"
    
   ```

2. ** 获取SSH公钥信息 **
   ```
    zhouhongdeAir:~ zhouhong$ ls ~/.ssh      根目录查看是否有 ssh
    id_rsa id_rsa.pub    文件
    zhouhongdeAir:~ zhouhong$ cd id_ras.pub
    zhouhongdeAir:~ zhouhong$ cat ~/.ssh/id_rsa.pub 
    通过cat命令。在命令行中敲入cat ~/.ssh/id_rsa.pub ，回车执行后命令行界面中会显示id_rsa.pub文件里的内容，复制。

   ```
3. ** 添加SSH公钥到gitlab **
 + 打开gitlab的profile Setting页面，选择SSH Keys
 + 添加SSH公钥。填写Title和Key，其中Title是Key的描述信息，Key是上面复制的SSH公钥的内容，直接粘贴到输入框中保存即可。
