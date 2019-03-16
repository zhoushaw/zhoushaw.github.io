---
title: node-fs模块
date: 2018-11-27 16：14
tags: fs
categories: node
---


<div><!-- more--></div>

## 目录

* [1.文件读取] (#1)
* [2.写文件] (#2)
* [3.判断文件是否存在](#3)
* [4.创建目录](#4)
* [5.删除文件](#5)
* [6.遍历目录](#6)
* [7.判断是文件还是文件夹](#7)
* [8.文件重命名](#8)
* [9.监听文件修改](#9)
* [10.修改文件权限](#10)
* [11.追加文件内容](#11)
* [12.删除文件夹](#12)


## fs

<h3 id="1">文件读取</h3>

1.同步

```
var fs = require('fs');
const data = fs.readFileSync('./fileForRead.txt', 'utf8');
console.log('文件内容: ' + data);
```

2.异步


```
var fs = require('fs');
fs.readFile('./fileForRead.txt', 'utf8', function(err, data){
    console.log('文件内容: ' + data);
});
```

3.文件流读取


```
var fs = require('fs');
var readStream = fs.createStream('./xiaoshuo.txt','utf8');
readStream.on('data', function (chunk){
    console.log('文件读取', chunk)
})
.on('close',function (){
    console.log('文件读取结束');
});
```

<h3 id="2">写文件</h3> 

1.同步


```
var fs = require('fs');

fs.writeFile('./file.txt', 'hello world', 'utf8', function (err) {
    console.log('写入文件错误', err）;
});
```

2.文件流写入


```
var fs = require('fs');
var writeStream = fs.createWriteStream('./test1.txt', 'utf8');
writeStream
	.on('close', function() {
		console.log('已经关闭');
	})
writeStream.write('这是创建的第一个文件');
writeStream.write('文件名称取什么好呢!!');
writeStream.end('');
```

3.异步写入


```
var fs = require('fs');
fs.writeFile('./test1.txt', 'hello wrold', 'utf8', function(err) {
    console.log('文件读写错误', err);
});
```


<h3 id="3">文件是否存在</h3>

```
var fs = require('fs');
fs.access('./fileForRead.txt', function(err){
    console.log(err || 'fileForRead.txt存在');
});
```

<h3 id="4">创建目录</h3> 


```
var fs = require('fs');

fs.mkdir('./hello', function(err){
    console.log(err || '目录创建成功');
});
```

<h3 id="5">删除文件</h3>


```
var fs = require('fs');

fs.unlink('./fileForUnlink.txt', function(err){
    console.log(err || '文件删除成功');
});
```

<h3 id="6">遍历目录</h3>

**注意**:只会遍历一层目录


```
var fs = require('fs');
var path = require('path');

var getFilesInDir = function(dir){
    var results = [ path.resolve(dir) ];
    var files = fs.readdirSync(dir, 'utf8');
}
```

<h3 id="7">判断是文件还是文件夹</h3>


```
var fs = require('fs');
var path = require('path');

var getFilesInDir = function(dir){
    var results = [ path.resolve(dir) ];
    var files = fs.readdirSync(dir, 'utf8');
    files.forEach((file)=>{
        // 判断是文件还是文件夹
        var stats = fs.statSync(file);
         if(stats.isFile()){
            console.log(file, '是文件')
        }else if(stats.isDirectory()){
            console.log(file, '是文件夹');
        }
    });
}
```

<h3 id="8">文件重命名</h3>

```
// fs.rename(oldPath, newPath, callback)
var fs = require('fs');

fs.rename('./hello', './world', function(err){
    console.log(err || '重命名成功');
});
```

<h3 id="9">监听文件修改</h3>


> fs.watch()虽然性能较高，但是在多平台上标准不一致，一般使用fs.watchFile


`实现原理：轮询。每隔一段时间检查文件是否发生变化。所以在不同平台上表现基本是一致的。`

```
var fs = require('fs');

var options = {
    persistent: true,  // 默认就是true
    interval: 2000  // 多久检查一次
};

// curr, prev 是被监听文件的状态, fs.Stat实例
// 可以通过 fs.unwatch() 移除监听
fs.watchFile('./fileForWatch.txt', options, function(curr, prev){
    console.log('修改时间为: ' + curr.mtime);
});
```

文件在被访问的时候也会触发，回调事件，想要规避掉这个文件，增加触发条件 `curr.mtime===prev.mtime`时不触发，上次修改时间与当前修改时间相同表明没有修改

<h3 id="10">修改文件权限</h3>

> 文件访问权限

`Linux的访问权限分为 读、写、执行三种，可以使用 ls -l进行查看：`


```
r：可读(4)
w：可写(2)，对于目录来说表示可在目录中新建文件
x：可执行(1)，对于目录来说为可进入到该目录中
-：表示无对应位上的权限
```

<h3 id="11">追加文件内容</h3>

> fs.appendFile(file, data[, options], callback)


```
var fs = require('fs');
fs.appendFile('./extra/fileForAppend.txt', 'helo', 'utf8', function(err){
    if(err) throw err;
    console.log('append成功');
});
```

<h3 id="12">删除文件夹</h3>

> fs.rmdir(path, callback) fs.rmdirSync(path)

```
var fs = require('fs');
fs.rmdir('./dirForRemove', function(err){
    if(err) throw err;
    console.log('目录删除成功');
});
```

