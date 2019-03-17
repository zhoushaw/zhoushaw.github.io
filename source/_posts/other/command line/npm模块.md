---
title: npm包开发
date: 2018-04-22 8:07:33
tags: npm
categories: command
---


<div><!-- more--></div>


##发布npm

> 初始化项目

```
mkdir npmtest
cd npmtest
npm init
//填入初始化信息
// git repository不填写将放入npm仓库，可以存放到自己的github仓库 

```


> 项目目录

.
├── lib
│   ├── index.js
│   ├── module.js
├── test
├── index
│   ├── check-versions.js
│   ├── dev-client.js
│   ├── dev-server.js
│   ├── utils.js
├── package.json
├── README.md

把封装好的代码都扔在lib里面，所以，index.js里面也就一句话:
module.exports=require('./lib')


> 发布npm包

npm adduser
npm login
// 登录成功后，如果Logged in as shawzhou on http://npm.f2e.mogujie.org/.
// 后面的地址不是https://registry.npmjs.org/

使用:`npm config set registry https://registry.npmjs.org/`进行修改

package.json中的mian配置入口主文件

> 切换回公司环境


```
vim ~/.npmrc
prefix=/usr/local
registry=http://npm.f2e.mogujie.org/
```


> 撤回发布

`npm --force  unpublish pkgname`

