---
title: nginx配置
date: 2018-09-14 15:54:12
tags:
  - nginx
categories:
  - nginx
---

1. 远程登录服务器 使用ssh命令
在终端执行下列命令：
```
 ssh dev@39.106.111.163 注意使用dev不要使用root
```
2. 输入密码 

3. 进入nginx中
```
  cd /etc/nginx
```
4. 查看虚拟主机的目录
```
 cd sites-avaliable
```
5.  新建一个conf配置文件 
 在现有的conf文件中拷贝一份
 cp 现有的某个.conf配置文件   自己新建的文件名字.conf

 ```
  cp web.conf esharing.conf
 ```

6. 过程中遇到权限问题 请使用sudo!!
7. 先开放你新建的conf的权限
   命令 chmod 777 ehsharing.conf
8. 打开新建的conf文件
   修改server下面的listen监听端口改为80 server name域名和root路径
   vi esharing.conf 通过i命令实现修改 修改之后点击esc然后:wq保存
9.  
  cd sites-avaliable
  ln -s 源文件目录 建立软连接的目录
  例如 ln -s /etc/nginx/sites-available/esharing.conf   /etc/nginx/sites-enables/esharing.conf
10. 你配置的conf中的root路径如果不存在需要新建一个
    例如 你配置的路径为/data/esharing/web
    命令为 cd /data/esharing/ 
          mkdir web