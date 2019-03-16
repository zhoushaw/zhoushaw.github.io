---
title: charles应用
date: 2017-10-14 3:18:32
tags: charles
categories: tool
---

<div><!-- more--></div>


## charles破解包

[破解包下载地址](https://tools.zzzmode.com/mytools/charles/)

## 如何访问HTTPS请求内容
如果需要抓取https内容需要通过,通过设置SSL端口，为所有的可以访问https接口内容。

> step1

![](https://s10.mogucdn.com/mlcdn/c45406/190316_7klf427a2g3162djc8fiel8h4b56g_650x428.jpg)

> step2

![](https://s10.mogucdn.com/mlcdn/c45406/190316_0aa0j8dddll335g2ad35ch8838k54_592x442.jpg)

## 关注部分请求

在通过Charles抓包时，会抓取到很多http请求，这个时候所需关注的内容**往往不容易找到**。

![](https://s10.mogucdn.com/mlcdn/c45406/190316_5lkd46ijlllhfj4ehg962d9c79glk_1179x726.png)

右击你需要关注的http请求，选择focus后，将会显示的更加全面，将http请求分成两类，可以让你**更容易关注**你所需的http请求

## 如何修改请求头，返回报文

> 选中需要断点的http，

点击上面的断点按钮，并右击选中BrackPoints。

* step1
![](https://s10.mogucdn.com/mlcdn/c45406/190316_1egk5039j05akc7acf6377lkfb584_1178x727.png)

* step2
![](https://s10.mogucdn.com/mlcdn/c45406/190316_1igl6l4b4kld0ccll1gb2gcb06lkh_1176x723.png)


```
1. 选中需要断点的http，点击上面的断点按钮，并右击选中BrackPoints。之后再进行这个http请求之后，分别在
2. 请求的时候可以点击=> Edit Request可以对发送请求头，进行编辑，修改请求头。
3. Execute跳过当前断点，跳入响应请求断点。可以修改返回的内容
```

可以将断点修改请求头，将http的response存储下来，并且使用map映射到http请求上，这样子。每当内容进行响应的时候，将自动返回应用的请求内容

```
1. 右击对应http请求=>Save response..
2. 右击应用httpResponse的http=>Map Local..
3. 关闭映射菜单栏Tool=>Map Local..关闭或删除对应映射
```

## 如何抓取chrome浏览器请求

设置代理，ifconfig查看对应的ip，
在Charles设置中设置对应端口

* step1

![](https://s10.mogucdn.com/mlcdn/c45406/190316_288g40j79j72lfbgf1akk55khf3bf_640x488.png)

* step2

![](https://s10.mogucdn.com/mlcdn/c45406/190316_5i9b93b8aek34lfe4jcj0g892ejc7_592x505.png)


## ios安装后开启证书信任


设置=>通用=》关于手机=》证书信任设置


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


