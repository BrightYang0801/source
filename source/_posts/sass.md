---
title: create-react-app如何使用sass
date: 2018-09-14 15:54:07
tags:
  - 前端
categories:
  - 前端
---

1. 安装
在终端执行下列命令：
```
 npm install sass-loder node-sass —save-dev
```
2. 在node_modules/react-scripts/config 下找到webpack.config.dev.js文件,在exclude中添加/.scss$/
```
 nginx
```
3. 并在loaders中添加一项
```
 { test: /\.scss$/, loaders: ['style-loader', 'css-loader', 'sass-loader'],},
```
  ![image](https://note.youdao.com/yws/api/personal/file/WEBfd6a7854cc5e94f1a1b8b65dfde5e611?method=download&shareKey=92c5d29855c89098f421e901f92c3c9a)
  至此，Sass 就配置好了。
  注意，我们只是修改了 webpack.config.dev.js ,如果要在生产环境中生效，需要在webpack.config.prod.js做同样的配置
