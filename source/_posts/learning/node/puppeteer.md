---
title: puppeteer爬虫实战
date: 2019-4-23 4:18:35
categories: node
tags: node
---

## 前言

待补充....


## centOs7.0无法运行问题

centos必须升级到7.0以上否则会遇到依赖版本缺失问题

```
yum install ipa-gothic-fonts xorg-x11-fonts-100dpi xorg-x11-fonts-75dpi xorg-x11-utils xorg-x11-fonts-cyrillic xorg-x11-fonts-Type1 xorg-x11-fonts-misc -y

yum install pango.x86_64 libXcomposite.x86_64 libXcursor.x86_64 libXdamage.x86_64 libXext.x86_64 libXi.x86_64 libXtst.x86_64 cups-libs.x86_64 libXScrnSaver.x86_64 libXrandr.x86_64 GConf2.x86_64 alsa-lib.x86_64 atk.x86_64 gtk3.x86_64 -y

# 再安装NSS的依赖：
yum install nss.x86_64

# puppeteer的执行文件中去沙箱运行：
browser = await puppeteer.launch({
  headless: true,
  args: ['--no-sandbox', '--disable-setuid-sandbox']
});
```

## puppeteer启动配置

```
const puppeteer = require('puppeteer');
const browser = await puppeteer.launch([options]);
```

* options
    * headless `<boolean>` 以界面形式运行
    * devtools `<boolean>` 打开开发者工具栏

## emulate仿真

```
const puppeteer = require('puppeteer');
const devices = require('puppeteer/DeviceDescriptors')
await page.emulate(devices['iPhone X'])
```

