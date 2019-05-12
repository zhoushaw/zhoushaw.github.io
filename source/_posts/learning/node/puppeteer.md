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

## 页面对象附带

> page.emulate

模仿真实手机

```
const puppeteer = require('puppeteer');
const devices = require('puppeteer/DeviceDescriptors')

const page = await browser.newPage();
await page.emulate(devices['iPhone X'])
await page.goto('https://www.baidu.com'});
```

> page.waitFor

```
page.waitFor(selectorOrFunctionOrTimeout[, options[, ...args]])
```

等待指定dom节点内容渲染完成

```
let selector = '.price';
await page.waitFor(selector =>{
    return (document.querySelector(selector)||{}).innerText;
}, {}, selector);
```

> page.goto(`url`[, `options`])

* url `<string>` : 指定跳转地址
* options `<Object> `:
    * `networkidle0`: 500毫秒内没有任何一个网络请求
    * `networkidle2`:  500毫秒内没有超过任何二个网络请求
    * `domcontentloaded`: dom装载完成




## 页面环境执行脚本

```
await page.evaluate(() => {
    let name = window.name;
    return name;
});
```

> page.evaluate(pageFunction[, ...args])

* `pageFunction`: `<Function>` 执行脚本，函数在浏览器环境执行，拥有`window`、`document`访问权限
* `...args`: `<...Serializable|JSHandle>`,传入参数，`pageFunction`无法访问函数外部变量，因为`pageFunction`内容将会直接当做脚本注入页面

由于`pageFunction`函数会直接被注入到页面中，所以无法获取函数外部作用域，只能讲外部参数通过`args`传入，不能直接将`Function`传入，只能将函数通过`toString`后，在通过`eval`来执行`string`化后的函数。

```
let detect = () => {
    // ... do some thing
    return 'res';
};
 const html = await page.evaluate((fn) => {
        let res = eval(fn)();
        return res;
}, detect.toString());
```

**注意**：

页面注入脚本，监听事件失效

```
let renderReady = () => {
      return new Promise((resolve) => {
          document.onreadystatechange = () => {
              if (document.readyState === 'complete') {
                  resolve();
              }
          };
      });
};

(async () => {
    await renderReady()
    console.log('complete') // 永远也不会走到这一块来，进入到renderReady后就失效了
})()
```


## jest-puppeteer

[官方文档](https://jestjs.io/docs/zh-Hans/puppeteer)

使用puppeteer与jest搭配测试：

* 依赖安装`npm install --save-dev jest-puppeteer puppeteer jest`
* `package.json`添加`"jest": {"preset": "jest-puppeteer"}`依赖

### TypeScript

在使用TypeScript中使用`puppeteer`测试需要注意一下几点：

> 由于TypeScript需要进行类型检测所以需要在全局环境注入变量

依赖安装：

`@types/puppeteer`, `@types/jest-environment-puppeteer`

配置文件：

```
{
    jest: {
        "globalSetup": "jest-environment-puppeteer/setup",
        "globalTeardown": "jest-environment-puppeteer/teardown",
        "testEnvironment": "jest-environment-puppeteer"
    }
}
```
> 指定输出版本

若输出目标为`"target": "es5"`，则会报各种依赖无法查找错误

```
ReferenceError: __awaiter is not defined
```

解决方案：

```
// tsconfig.json,文件配置
{
  "compilerOptions": {
    "target": "es2017",
    // ...
  }
}
```


