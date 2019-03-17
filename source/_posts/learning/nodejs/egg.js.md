---
title: egg.js
date: 2018-10-27 16:14
tags: node
categories: node
---


<div><!-- more--></div>

## 起步

> 安装egg-cli，参考官方

[官方文档](https://eggjs.org/zh-cn/intro/quickstart.html)

> 核心

约定大于配置

> 目录结构

MVC结构，定义router和controller，route到多应的controller,controller来渲染对应的模板，但需要配置对应的渲染模板引擎，具体参考[模板引擎](https://eggjs.org/zh-cn/intro/quickstart.html#%E6%A8%A1%E6%9D%BF%E6%B8%B2%E6%9F%93)

```
egg-example
├── app
│   ├── controller
│   │   └── home.js
│   ├── view
│   │   └── news
│   │   │   └── list.tpl
│   └── router.js
├── config
│   └── config.default.js
└── package.json
```


## router
> 添加namespace


```
npm install egg-router-plus

// config/config.default.ts
config.routerPlus = {
    enable: true,
    package: 'egg-router-plus',
};
```

## 本地开发调试

> 注意

* vscode断点调试，必须将service文件夹当做根目录文件夹打开(这样vscode的配置才会生效)
* 在package.json的script中添加

```
  "scripts": {
    "debug": "egg-bin debug -r egg-ts-helper/register --proxy=9999",
  },
```

* proxy端口和vscode配置文件launch.json中attach端口一致

```
  "configurations": [
  
    {
      "type": "node",
      "request": "attach",
      "name": "Egg Attach to remote",
      "localRoot": "${workspaceRoot}",
      "remoteRoot": "/usr/src/app",
      "address": "localhost",
      "protocol": "auto",
      "port": 9999
    }
  ]
}
```

* 启动项目后，在启动vscode的egg attrach to remote端口

> 按照egg的本地开发从上到下配置好 [本地开发](https://eggjs.org/zh-cn/core/development.html)


## 配置跨域

> plugin配置


```
// plugin.js
cors: {
    enable: true,
    package: "egg-cors"
}
```

> 配置跨域

```
config.security= {
    csrf: {
     enable: false,
     ignoreJSON: true
    },
    domainWhiteList: ['http://localhost:7000']
}

  config.cors = {
    allowMethods: 'GET,HEAD,PUT,POST,DELETE,PATCH,OPTIONS',
  };
```

## 配置cookie属于哪个域

在进行instagram开发时，陷入了误区。主观认为，网站a.com请求b.com时，b.com可以设置cookie到a.com


