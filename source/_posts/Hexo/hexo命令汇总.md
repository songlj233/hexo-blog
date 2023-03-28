---
title: hexo命令汇总
tags: hexo
categories:
- hexo
abbrlink: 21521
date: 2023-03-26 12:34:44
---

# 常用命令

## 新建文章
```hexo new a```
## 新建草稿
```hexo new draft b```
## 发布草稿

`hexo publish a`

## 开启服务
hexo server

## 新建文章
hexo new a

## 新建草稿
hexo new draft b

## 发布草稿成为文章
hexo publish b

## 发布关于
hexo new page c

## 生成静态文章
hexo generate 或者是 hexo g
## 部署文章
hexo deploy 或者是 hexo d
## 一键部署-部署到后台
hexo clean && hexo generate && hexo deploy
## 一键部署-本地部署
hexo clean && hexo generate && hexo s

## 自动生成abbrlink
npm install hexo-abbrlink --save

# 备忘
## next主题错误的解决方案
npm i hexo-renderer-swig

## 主题网站
https://hexo.io/themes/

### maple
https://github.com/xbmlz/hexo-theme-maple

### fluid
引入指南：https://gitcode.net/mirrors/fluid-dev/hexo-theme-fluid
使用手册：https://hexo.fluid-dev.com/docs/guide/

## 教程
https://blog.csdn.net/qq_58608526/article/details/124652412

## 问题整理
### git部署
使用git部署，需要安装git工具，命令为`npm install hexo-deployer-git --save`。

注：部署`hexo d`部署成功，意味这会将`hexo g`生成的文件，上传到github服务器上。

