---
title: Egret
date: 2018-1-26 18：14
tags: egret
categories: game
---

## 更改文件刷新

Egret自动编译刷新：


项目目录下：

1.egret run -a，启动项目修改自动编译
2.全局安装：

`npm install -g browser-sync`

进入项目文件夹、命令行输入：

```
browser-sync start --server --files "bin-debug/**/*.js, *.html"
```


<div><!-- more--></div>

## 雪碧图


在egret中当做纹理集使用

具体参考：http://developer.egret.com/cn/github/egret-docs/Engine2D/bitmapTexture/useTexture/index.html

可使用bigshear工具，将雪碧图转换成egret纹理集

## 动画相关

在egret扩展库中提供

> game库

* 可将纹理集做成帧动画

> tween

* 动画库
* 移动、变形



## MovieClip元素设置大小

> 因MovieClip元素无法设置height、width苦恼了很久

解决贴： https://bbs.egret.com/forum.php?mod=viewthread&tid=109&highlight=width

简单来说就是在egret中width/height和scaleX/scaleY ：

相当于给一个div元素设置了大小与背景图，但背景图设置的属性(没有设置background-size: 100% 100%)大小与当前元素大小相同，这时给div设置了宽高内部的背景图大小也不会发生变化，要使内部图像发生变化，则使用scaleX和scaleY。div和背景图都会发生大小比例变化

## 不是EUI项目

需要手动增加配置

```
//注入自定义的素材解析器
let assetAdapter = new AssetAdapter();
egret.registerImplementation("eui.IAssetAdapter", assetAdapter);
egret.registerImplementation("eui.IThemeAdapter", new ThemeAdapter());
```

