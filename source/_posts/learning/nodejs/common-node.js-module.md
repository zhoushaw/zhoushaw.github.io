title: 常用的npm包
date: 2018-01-23 6:52:35
categories: js
tags: nodejs
---


## **前言**

为提供工作效率我们常常需要使用到npm包，集成工具来加快开发效率，这里将列出我再实际开发中常用的一些插件、npm包

<div><!--more--></div>

## browser-sync

> 起步

npm install -g browser-sync

> 监听文件

```javascript

browser-sync start --server --files "css/*.css"

// --files 路径是相对于运行该命令的项目（目录） 
browser-sync start --server --files "css/*.css, *.html"
// 如果你的文件层级比较深，您可以考虑使用 **（表示任意目录）匹配，任意目录下任意.css 或 .html文件。 
browser-sync start --server --files "**/*.css, **/*.html"

```


