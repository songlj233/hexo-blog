---
title: Flutter搭建web
tags:
  - 原创
  - Flutter
categories:
  - Flutter
abbrlink: 5bb06
date: 2024-04-06 12:15:00
---

# 编译运行web项目

## 问题汇总

### 问题1 Http请求跨域问题
解决方案
1. 在flutter安装路径`flutter\bin\cache`中找到`flutter_tools.stamp`文件，然后删掉
2. 在flutter安装路径`packages\flutter_tools\lib\src\web`中找到`chrome.dart`文件，然后编辑
在`--disable-extensions`后面增加一行`--disable-web-security`
>以上方案能解决本地调试的跨域问题，打包release版本部署到服务器上还是存在跨域问题

### 问题2 webview不支持web
判断如果是web，则不启用webview，直接做url跳转

## 坑点
编译的产物太大，浏览器加载时间很长，用户体验极差，放弃

