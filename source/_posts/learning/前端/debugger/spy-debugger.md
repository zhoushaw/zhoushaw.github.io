---
title: spy-debugger
date: 2019-02-4 8:52:35
tags: debugger
categories: debugger
---




## 前言

移动端web调试十分麻烦，chrome调试工具不支持ios，在ios端出现兼容问题将十分难易调试，普通的log方式调试时间大量损耗，有没有一个方便易用的方式呢，spy-debugger可以很好的解决的这个问题，跨多端webview调试也非常方便快捷


<div><!-- more--></div>

## 起步

> 安装

```
npm install spy-debugger -g
```

> 启动

`spy-debugger`


> 环境配置

手机与pc保持同一个局域网
ios代理设置：设置 - 无线局域网 - 选中网络 - HTTP代理手动

代理配置信息为，启动命令行窗口中会暴露ip地址和端口号

> 安装正式

浏览器访问：http://s.xxx(真实域名就是这个不用怀疑)
按照操作步骤完成安装

> 信任证书

设置 - 通用 - 证书信任设置 - 设置node-mitmproxy为信任证书



