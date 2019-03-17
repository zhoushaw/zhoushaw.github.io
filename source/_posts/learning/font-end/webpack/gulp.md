---
title: gulp
date: 2018-04-27 12:52:35
tags: gulp
categories: js
---


<div><!-- more--></div>

## 引言
    
* 易于使用:通过代码优于配置的策略，Gulp 让简单的任务简单，复杂的任务可管理。
* 构建快速:利用 Node.js 流的威力，你可以快速构建项目并减少频繁的 IO 操作。
* 插件高质:Gulp 严格的插件指南确保插件如你期望的那样简洁高质得工作。
* 易于学习:通过最少的 API，掌握 Gulp 毫不费力，构建工作尽在掌握:如同一系列流管道。

## 依赖安装


```
npm install gulp-cli -g
npm install gulp -D
touch gulpfile.js
gulp --help
```


## 错误检测

gulp有一个插件，gulp-util，用来打印日志，看具体什么地方出错了。

在gulpfile.js打包压缩的命令里。。增加一个错误的打印。

```
var gutil = require('gulp-util');
/ 合并，压缩文件
    gulp.task('scripts',['copy'], function() {
        gulp.src('./dist/js/page/**/*.js')
            .pipe(sourcemaps.init())
            .pipe(uglify({
                mangle:true,
                compress: true
            }
            ))
            .on('error', function (err) {
                gutil.log(gutil.colors.red('[Error]'), err.toString());
            })
            .pipe(sourcemaps.write('../maps'))
            .pipe(gulp.dest('./dist/js/page'));
    });

```
这个时候，，打印的时候具体错误就会有提示。
这样的话我们就可以轻松的知道问题出在哪里。然后去修改相应的js文件即可。


## 转化es6代码到es5

> 依赖安装

```
npm install --save-dev gulp-babel
// 安装 Gulp 上 Babel 的插件。

npm install --save-dev babel-preset-es2015
// 安装 Babel 上将 ES6 转换成 ES5 的插件。

```

> config


```
//gulp 配置:

//复制代码
var gulp = require("gulp");
var babel = require("gulp-babel");

gulp.task("default", function () {
  return gulp.src("src/**/*.js")// ES6 源码存放的路径
    .pipe(babel()) 
    .pipe(gulp.dest("dist")); //转换成 ES5 存放的路径
});
//复制代码
// babel配置:

//在项目根路径创建文件 .babelrc。内容为

{
  "presets": ["es2015"]
}
```


