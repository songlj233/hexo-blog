---
title: 部署web服务
tags:
  - 服务器搭建
categories:
  - 服务器
abbrlink: 43381
date: 2024-04-06 15:52:00
---

1. 安装Apache及其扩展包
```
yum install -y httpd httpd-manual mod_SSL mod_perl mod_auth_mysql
```

2. 启动Apache并设置自启动
```
systemctl start httpd
systemctl enable httpd
```

3. 查看Apache运行状态
```
systemctl status httpd
```

4. 浏览器地址栏中输入IP，能打开网页说明成功了

5. 上传需求的文件到服务器的`/var/www/html/`目录即可

