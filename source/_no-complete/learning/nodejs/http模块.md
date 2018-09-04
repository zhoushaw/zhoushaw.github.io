## 目录

* [1.起步](#1)
* [2.request](#2)
* [3.服务端例子](#3)
* [4.response](#4)
* [5.客户端方法](#5)
* [6.https](#6)

<h3 id="1">起步</h3> 


```
var http = require('http');

// http server 例子
var server = http.createServer(function(serverReq, serverRes){
    var url = serverReq.url;
    serverRes.end( '您访问的地址是：' + url );
});

server.listen(3000);

// http client 例子
var client = http.get('http://127.0.0.1:3000', function(clientRes){
    clientRes.pipe(process.stdout);
});
```


<h3 id="2">reponse</h3>

> 重点会放在req这个对象上。前面已经提到，它其实是http.IncomingMessage实例，在服务端、客户端作用略微有差异

* 服务端处：获取请求方的相关信息，如request header等
* 客户端处：获取响应方返回的相关信息，如statusCode等


> server


```
var http = require('http');
var server = http.createServer(function(req, res) {
	console.log(req.headers);
	res.end('ok');
})
server.listen(3000);
console.log('server is runing');
```

> client


```
// 下面的res
var http = require('http');
http.get('http://127.0.0.1:3000', function(res){
    console.log(res.statusCode);
});
```

<h3 id="3">服务端案例</h3>

> 例子一：获取httpVersion/method/url


```
// getClientInfo.js
var http = require('http');

var server = http.createServer(function(req, res){
    console.log( '1、客户端请求url：' + req.url );
    console.log( '2、http版本：' + req.httpVersion );
    console.log( '3、http请求方法：' + req.method );
    console.log( '4、http请求头部' + JSON.stringify(req.headers) );

    res.end('ok');
});

server.listen(3000);

```

> 例子二：获取get请求参数


```
// getClientGetQuery.js
var http = require('http');
var url = require('url');
var querystring = require('querystring');

var server = http.createServer(function(req, res){
    var urlObj = url.parse(req.url);
    var query = urlObj.query;
    var queryObj = querystring.parse(query);
    
    console.log( JSON.stringify(queryObj) );
    
    res.end('ok');
});

server.listen(3000);
```


> 获取post请求参数


```
// getClientPostBody.js
var http = require('http');
var url = require('url');
var querystring = require('querystring');

var server = http.createServer(function(req, res){
    
    var body = '';  
    req.on('data', function(thunk){
        body += thunk;
    });

    req.on('end', function(){
        console.log( 'post body is: ' + body );
        res.end('ok');
    }); 
});

server.listen(3000);
```

<h3 id="4">response</h3>

> 概念

`
http模块四剑客之一的res，应该都不陌生了。一个web服务程序，接受到来自客户端的http请求后，向客户端返回正确的响应内容，这就是res的职责。`

返回的内容包括：状态代码/状态描述信息、响应头部、响应主体。下文会举几个简单的例子。


> 例子


```
var http = require('http');

// 设置状态码、状态描述信息、响应主体
var server = http.createServer(function(req, res){
    res.writeHead(200, 'ok', {
        'Content-Type': 'text/plain'
    });
    res.end('hello');
});

server.listen(3000);
```

> 设置响应头


```
// 方法一
res.writeHead(200, 'ok', {
    'Content-Type': 'text-plain'
});

// 方法二
res.setHeader('Content-Type', 'text-plain');
```

1. res.writeHead() 不单单是设置header。
2.已经通过 res.setHeader() 设置了header，当通过 res.writeHead() 设置同名header，res.writeHead() 的设置会覆盖之前的设置。

<h3 id="5">客户端方法</h3>

> get请求

`下面构造了个GET请求，访问 http://id.qq.com/ ，并将返回的网页内容打印在控制台下`


```
var http = require('http');
var options = {
    protocol: 'http:',
    hostname: 'id.qq.com',
    port: '80',
    path: '/',
    method: 'GET'
};

var client = http.request(options, function(res){
    var data = '';
    res.setEncoding('utf8');
    res.on('data', function(chunk){
        data += chunk;
    });
    res.on('end', function(){
        console.log(data);
    });
});

client.end();
```

> post请求


```
var http = require('http');
var querystring = require('querystring');

var createClientPostRequest = function(){
    var options = {
        method: 'POST',
        protocol: 'http:',
        hostname: '127.0.0.1',
        port: '3000',
        path: '/post',
        headers: {
            "connection": "keep-alive",
            "content-type": "application/x-www-form-urlencoded"
        }    
    };

    // 发送给服务端的数据
    var postBody = {
        nick: 'chyingp'
    };

    // 创建客户端请求
    var client = http.request(options, function(res){
        // 最终输出：Server got client data: nick=chyingp
        res.pipe(process.stdout);  
    });

    // 发送的报文主体，记得先用 querystring.stringify() 处理下
    client.write( querystring.stringify(postBody) );
    client.end();
};

// 服务端程序，只是负责回传客户端数据
var server = http.createServer(function(req, res){
    res.write('Server got client data: ');
    req.pipe(res);
});

server.listen(3000, createClientPostRequest);
```

