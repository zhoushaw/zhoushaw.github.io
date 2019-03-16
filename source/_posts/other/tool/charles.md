---
title: charles应用
date: 2017-010-14 3:18:32
tags: charles
categories: tool
---

<div><!-- more--></div>

## charles配置

1. 首先下载charles，并破解。如果替换jar后，提示软件损坏无法打开，提升用户权限可解决当前问题
2. proxy=>proxy settings=>proxies选项 设置http port为8888，macOs选项设置Use HTTP proxy选项
3. proxy=>SSL Proxying Setting=>SSL proxying选项，添加*:443信任https端口，或双星
4. Help=>SSL Proxying=>install charles Root certificase,进行证书安装
5. 安装完成后双击证书，从弹窗里第一个选项选择始终信任
6. wifi=>open network preferences=>advanced=>proxies选项，勾选web proxy、secure web proxy选项，并设置主机名和端口分别为127.0.0.1和8888
7. 如果chrome任然提示不安全，无法进行网页访问，设置chrome代理为系统代理
8. 将手机与电脑连接同一wifi，通过wifi查看当前主机ip地址，和端口默认8888，设置手机wifi代理，将代理主机和端口进行填写
9. 填写完成后，通过Help=>SSL Proxying=>install mobile... 查看提示信息，进行证书安装。连接电脑代理后chls.pro/ssl，进入该页面。下载完证书后，将证书后缀名修改为charles.crt
10. 安装完成后，charles可以截取mobile网络请求

## ios安装后开启证书信任


设置=>通用=》关于手机=》证书信任设置



## charles破解包

[链接](https://tools.zzzmode.com/mytools/charles/)

