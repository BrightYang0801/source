---
title: nginx配置
date: 2018-09-14 15:54:08
tags:
  - nginx
categories:
  - nginx
---

1. 安装
在终端执行下列命令：
```
 brew install nginx
```
2. 启动
```
 nginx
```
3. 重启
```
 nginx -s reload
```
4. 关闭
查看主进程号 ps -ef | grep nginx
从容停止 kill -QUIT 主进程号
快速停止 kill -TERM 主进程号
强制停止 kill -9 nginx

5. 配置步骤
 + 把build后的包放到/usr/local/Cellar/nginx/1.15.0目录下
 + 修改/usr/local/etc/nginx/nginx.conf文件配置
 + 
 ```
 location / {
      root   build;
      index  index.html index.htm;
      try_files $uri $uri/ /index.html;
  }

  location ^~ /api/ {
      proxy_pass http://47.92.88.235:8082/;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";
      proxy_set_header   Host             $host;
      proxy_set_header   X-Real-IP        $remote_addr;
      proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
  }
  
  location ~* /.html$ { 
      add_header Cache-Control "no-store, no-cache";
  }
  location ~* /.(?:jpg|jpeg|gif|png|ico|cur|gz|svg|svgz|mp4|ogg|ogv|webm|htc|eot|ttf)$ { expires max;}
  location ~* /.(?:css|js|js/.map)$ { expires max;}
 ```
    1.root 为根目录默认路径
    2.try_files $uri $uri/ /index.html;
    因为browserRouter的原因，需要将每个uri指向index.html
    3.location ~* /.html$ 为html设置不缓存
