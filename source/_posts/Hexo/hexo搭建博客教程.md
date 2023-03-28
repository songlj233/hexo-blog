---
title: hexo搭建博客教程
tags: hexo
categories:
- hexo
abbrlink: a6efda57
date: 2023-03-28 15:20:00
---
## 环境准备
需要node、git的环境

## 项目部署
### 1. 安装node、git环境
```
略
```

### 2. 拉取项目
```
git clone https://github.com/songlj233/hexo-blog.git
cd hexo-blog
```

### 3. 部署项目
#### 安装node模块
```
npm install 
```

#### 本地一键运行
```
hexo clean && hexo g && hexo s
```
运行结果在浏览器`http://localhost:4000`查看

#### 部署到服务器
本操作可选，部署的路径为`_config.yml`文件中的`deploy`配置项中的git地址和分支
```
hexo d
```
