---
title: nginx
date: 2019-07-17 8:07:12
tags: http
categories: http
---

## 前言



## 配置

* [ngix参考](https://www.runoob.com/linux/nginx-install-setup.html)
* nginx 的安装目录为：/usr/local/nginx/sbin/nginx
* nginx 的配置目录为：/usr/local/nginx/conf/nginx.conf

> 启动Nginx

* 测试 nginx 配置是否正确 sudo /usr/local/nginx/sbin/nginx -t -c /usr/local/nginx/conf/nginx.conf
* 第一次启动 sudo /usr/local/nginx/sbin/nginx
* 重启 sudo /usr/local/nginx/sbin/nginx -s reload
* 建议每次重启前，都检测下配置是否正确。

> 常见问题

* nginx: [emerg] getpwnam("www") failed
    * 因为没有 www 用户组，
    * 修改 nginx.conf 配置，去掉#user www注释，改成user nobody
    * 再次启动，访问 http://10.70.96.67/，可以看到 nginx 的欢迎页面

