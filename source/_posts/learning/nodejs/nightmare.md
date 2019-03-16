---
title: nightmare
date: 2019-03-06 5:05
tags: node
categories: ndoe
---


<div><!-- more--></div>


## 前言

待补充....


## 起步


> 安装依赖

```
npm install --save nightmare
```

> 模拟手机环境

**前置条件**


```
const Nightmare = require('nightmare');
const nightmare = new Nightmare({
  show: false, // 是否打开模拟器
  openDevTools: {
    mode: 'detach'// 开发者工具模式
  },
  load_policy: Nightmare.CONTINUE_DOMREADY
});
```

**设置终端**

```
// 模拟器终端
const userAgent = "Mozilla/5.0 (iPhone; CPU iPhone OS 6_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Mobile/10A5376e";

// 设置模拟终端
nightmare.useragent(userAgent)
```

**模仿设备尺寸**


```
const mobilesettings = { // 设备参数
  screenPosition: 'mobile',
  screenSize: { width: 375, height: 667 },
  deviceScaleFactor: 0,
  viewPosition: { x: 0, y: 0 },
  viewSize: { width: 375, height: 667 },
  fitToView: true,
  offset: { x: 0, y: 0 }
};

// 自定义方法,模仿设备
Nightmare.action('emulateDevice',
  //define the action to run inside Electron
  function(name, options, parent, win, renderer, done) {
    // This task runs in the remote process
    parent.respondTo('emulateDevice', function(settings, done) {// <---- See settings
        win.webContents.on('did-finish-load', function(){
          win.webContents.enableDeviceEmulation(settings);// Set settings here...
        });
        done();//call done
    });
    //call the action creation `done`
    done();//call done
  },
  // use the IPC child's `call` to call the action added to the Electron instance
  function(settings, done) {
    this.child.call('emulateDevice', settings, done);
});

// 应用到nightmare上
nightmare.emulateDevice(mobilesettings)
```

## 页面是否渲染完成


> 渲染完成事件


``` 
Nightmare.on("did-stop-loading", () => {
    console.log('页面加载完成');
})
```

> 多次重定向

跳转到指定页时，指定页面可能会发生重定向，通过判断"did-stop-loading"判断页面加载完成并且页面指定元素已被渲染，执行后续爬取逻辑

```
Nightmare
.on("did-stop-loading", () => {
      console.log('页面加载完成');
})
.wait('.present-price .o-t-price')
.evaluate(() => {
     return window.detect();
})
```


