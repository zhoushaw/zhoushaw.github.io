---
title: npm配置
date: 2018-06-22 8:07:33
tags: npm
categories: command
---


<div><!-- more--></div>

## 依赖环境配置


> yarn 


```
vim .zshrc
export PATH="$PATH:`yarn global bin`"
```

## npm代理设置

> 起步

`vim ~/.npmrc`

> 切换代理

```
registry=https://registry.npm.taobao.org
//registry=http://npm.f2e.mogujie.org/
//registry=https://registry.npmjs.org/
```

## 端口占用查询

> 查询端口占用

`lsof -i:3000`


> 解除端口占用(PID在查询端口出现)

`sudo kill -9 PID`





