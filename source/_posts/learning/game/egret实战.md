---
title: Egret实战-母亲节活动
date: 2019-5-6 7:42
tags: egret
categories: game
---

## 目录结构

```
|—— bin-debug   <-编译后运行代码
|—— libs        <-第三方库
|—— resource    <-资源文件
    |—— default.res.json    <-资源索引目录
    └── default.thm.json    <-主题索引目录
|—— scripts     <-构建脚本
|—— resource    <-资源文件
|—— src         <-项目源代码
└── template    <-项目模板
```

## h5活动构建思路

如何制作一个类似于中国女子图鉴的项目呢。

> 扫码访问：

<img width="200" src="https://s10.mogucdn.com/mlcdn/c45406/190506_2dl50cg7c5b79kf58a050fgch92ib_400x400.png" />

> 主要思路

通过龙骨场景动画将将所有动画做成帧动画到龙骨中，通过滑动事件来控制帧切换的位置，具体实现代码：

```
const dragonbonesData = RES.getRes( "dragonbones@listen_mother_ske_json" );  
const textureData = RES.getRes( "dragonbones@listen_mother_tex_json" );  
const texture = RES.getRes( "listen_mother_png" );

let egretFactory: dragonBones.EgretFactory = dragonBones.EgretFactory.factory;
egretFactory.parseDragonBonesData(dragonbonesData);  
egretFactory.parseTextureAtlasData(textureData, texture);

let armatureDisplay: dragonBones.EgretArmatureDisplay = egretFactory.buildArmatureDisplay("listen_mother");

this.addChild(armatureDisplay);
armatureDisplay.x = 0;
armatureDisplay.y = 0;

   	
const myScroller = new eui.Scroller();
//注意位置和尺寸的设置是在Scroller上面，而不是容器上面
   
const group = new eui.Group();
const img = new eui.Image("bg_png");
group.addChild(img);
img.height = this.stage.stageHeight * 2;
   
myScroller.width = this.stage.stageWidth;
myScroller.height = this.stage.stageHeight;
myScroller.viewport = group;
myScroller.bounces = false;
this.addChild(myScroller);   
myScroller.addEventListener(
  egret.Event.CHANGE, 
  () => {
      let scrollRate = myScroller.viewport.scrollV/(img.height - this.stage.stageHeight);
     
      console.log(myScroller.viewport.scrollV,scrollRate);
      armatureDisplay.animation.gotoAndStopByFrame ('newAnimation',scrollRate*80);
  },
  this
)
```

功能流程：

* 获取龙骨资源、并创建`dragonBones`实例对象
* 将龙骨场景对象添加至画布
* 创建`Image`对象，设置宽度设置为视窗宽度，高度设置为**龙骨场景高度+视窗高度**并添加至场景中
* 创建`scroll`对象，将其设置为视窗大小，设置`Image`对象为`scroll`的视域组件组件
* 使用`scroll`监听滚动高度，计算当前滚动条占总可滚动高度的百分比=“已滚动高度/(图片高度-视窗高度)”
* 获取`dragonBones`场景一共拥有多少帧，通过总帧数*当前百分比，得到用户滑动到当前所在帧数

