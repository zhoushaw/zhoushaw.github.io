---
title: node查询ip
date: 2018-10-28 16:14
tags: dns
categories: node
---


## 查询ip

> 比如我们要查询域名 www.qq.com 对应的ip，可以通过 dns.lookup() 

```
var dns = require('dns');

dns.lookup('www.qq.com', function(err, address, family){
    if(err) throw err;
    console.log('例子A: ' + address);
});
```


> 一个域名对应多个ip


```
var dns = require('dns');
var options = {all: true};

dns.lookup('www.qq.com', options, function(err, address, family){
    if(err) throw err;
    console.log('例子B: ' + address);
});
```

> resolve4


```
var dns = require('dns');

dns.resolve4('id.qq.com', function(err, address){
    if(err) throw err;
    console.log( JSON.stringify(address) );
});
```

> dns.lookup()跟dns.resolve4()的区别


从上面的例子来看，两个方法都可以查询域名的ip列表。那么，它们的区别在什么地方呢？
可能最大的差异就在于，当配置了本地Host时，是否会对查询结果产生影响。

* dns.lookup():有影响。
* dns.resolve4():没有影响。


