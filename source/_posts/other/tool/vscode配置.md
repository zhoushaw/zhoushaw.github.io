---
title: vscode常用配置
date: 2018-01-14 3:18:32
tags: vscode
categories: other
---

<div><!-- more--></div>

## 引言

为加快工作效率特将vscode常用配置插件整理出来

## 配置md预览


<a href="https://github.com/raycon/vscode-markdown-css">vscode配置文件github地址</a>

打开配置文件:文件=>首选项=>设置
增加以下内容：

> 在线地址

```javascript

"markdown.styles": [
    "https://github.com/raycon/vscode-markdown-css/blob/master/markdown-pdf.css"
]

```
> 本地vscodemd.css

```javascript
"markdown.styles": [
      "file:///C:/Users/Administrator/Desktop/blog/_posts/other/工具/vscodemd.css"
    ],
```

## eslint配置

[原文](https://segmentfault.com/a/1190000009077086)

> 配置

文件 > 首选项 > 设置，在右侧用户设置中修改 ESLint 的相关配置并保存：

```
"eslint.options": {
    "configFile": "/Users/shawzhou/Desktop/meili/mgj-pay-meilijie/.eslintrc.js",
    "plugins": ["html"]
},
"eslint.validate": [
    "javascript",
    "javascriptreact",
    "html",
    "vue"
]
```

> 检测项目选装npm包

`npm install eslint babel-eslint --save-dev`

## 自定义代码片段


> 起步

`Code=>首选项=>用户代码片段`

