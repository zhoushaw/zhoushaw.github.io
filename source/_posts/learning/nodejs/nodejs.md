title: nodejs基础知识
date: 2017-8-6 6:52:35
categories: js
tags: nodejs
---

<div><!--more--></div>

##nodejs与js

在ECMAScript部分node和js其实是一样的，比如数据类型的定义语法结构，内置对象
在js中的顶层window
在node中的顶层对象global

注意:
在node中没有什么window
一个文件就是一个模块
每个模块都有自己的作用域
我们使用一个var来声明变量，他并不是全局的，而是属于当前模块下的


## 模块加载系统
requires(加载模块)
模块加载机制:
	路径:
		1.绝对路径(电脑中文件的路径)
		2.相对路径，require('./server');必须是以./开头
     	 require('2.js');//加载node中的核心模块，或者node__mdoules

### 加载优先级
1.首先按照加载的模块的文件名称进行查找
2.如果没有找到，则会在模块文件名称后面加上.js的后缀继续查找
3.如果还没有找到，则会在文件名称后加上。json的后缀，进行查找
4.如果还没找到，则会在文件名称后面加上.node的后缀进行查找
文件名称->.js>.json->.node

### 模块变量的访问
在一个模块中通过var定义的变量，其作用域范围是当前模块，外部不能直接的访问
如果我们想一个模块能访问另外一个模块中定义的变量，可以
1.把变量作为global对象的属性，但是这样的做法是不推荐的
2.使用模块对象、module
module:保存提供和当前模块有关的一些信息
在这个module对象，有一个子对象:exports对象，我们可以通过这个对象把一个模块中的局部变量
对外进行访问
如果在一个模块中通过require();引入了一个文件，可以访问这个module对象的属性
require();这个方法的返回值，其实就是被加载模块中的module.exports

api:
1.__filename:返回当前模块文件的解析后的绝对路径。其属性并非全局，而是模块作用域下的
2.__dirname:返回当前模块文件所在目录解析后的绝对路径，该属性也不是全局的，而是木块作用域下的


## module模块

一个文件就是一个模块
每个模块都有自己的作用域
我们使用var来申明的一个变量，他并不是全局的，而是属于当前模块下

在一个模块中通过var定义的变量，其作用域范围是当前模块，外部不能够直接的访问
如果我们想一个模块能够访问另外一个模块中定义的变量，可以:
1.把变量作为global对象的一个属性，但是这样的做法是不推荐
2.使用模块对象 module.exports可以将这个局部变量的属性共享出去

exports == module.exports
exports指向的空间和module.exports一样,但是exports的指向被改变之后，最终导不导出取决于module.exports的地址
module.exports等于谁就导出谁，不像exports会改变里面的地址



## http请求设置

http请求的过程

<script>Vue.http.options.emulateJSON=true;</script>

我们使用vue-resource的使用
Vue.http.headers。post['Content-Type']='application/json';
Vue.http.headers。post['Content-Type']='x-www-application-urlencoded';

对于非简单请求，Vue-resource会先发送一次method为options的请求，如果服务器能正常响应(表示服务器支持非简单类型请求)，客户端才真正的发送本次非简单请求

什么是非简单请求:请求类型为PUT、DELETE或者POST类型请求时Content-Type不为x-www-applications-urlencoded form/urlecoed??时为非简单请求


res.writeHeader({
	'Access-Control-Allow-Origin':'*',
	'Access-Control-Allow-Headers':'Content-Type',//==aplication/json
	'Access-Control-Allow-Methods':'GET,POST,PUT,DELETE,OPTIONS'
});



//可以跨域
//什么是非简单请求?
//method为PUT、DELETE、Content-Type为application/json的请求
//服务器怎么应对?
//服务器需要配置以下头
//客户端如果是vue-resource需要以下配置(也可以不配置因为vue-resource本来这些就是默认值)
//Vue.http.options.emulateJSON=false;
//Vue.http.headers.post['Content-Type']='application/json';
//客户端发之前还要JSON.stringifry(要发到服务器的json数据)


## package.json

XXXX>npm install express --save-dev
npm init创建package.json

我们不断通过npm install XXX--save安装的第三方库的名字和版本信息，会写进package.json的dependencies或devDependencies节点

npm install 会读取package.json文件里面的dependencies,和Devdependencies的配置信息，找到所有需要安装的插件，安装好，
根据package.json文件的配置自动安装第三方库，通过读取dependencies和Devdepencies里面的配置安装所需的插件

npm install body-parser --save
使用nmp 安装一个包，会在当前目录下找package。json文件，并且在dependencies:里面增加包的名字，还有版本号
dependencies:
	产品阶段(投入使用阶段)用到的第三方库,里面的插件依赖于别的插件，但是只显示最终要显示的插件，

npm install body-parser --save-dev == npm install --save-dev  body-parser
使用nmp 安装一个包，会在当前目录下找package。json文件，并且在Devdependencies:里面增加包的名字，还有版本号
Devdependencies:
	开发阶段使用的第三方库，里面的用于放一些最终使用插件所依赖的插件

script:
	里面放的是

## express

概述:express是基于Node.js下的http模块扩展的框架

### express创建服务器

express创建的服务器
```javascript
var express = require('express');
var app = express();
//use是express最底层的函数，就是express的很多功能都是在这个函数的基础上进行扩展的
//use回调函数里面的三个形参，与http创建服务器里面的形参有着本质的差别
app.use(function(req,res,next){
	res.send('express创建的服务器');
});
app.listen(8080);
console.log('server is running 8080');
```


http创建的服务器
```javascript
var http=require('http');
var server = http.createServer(function(req,res){
	res.write('server is running 8080');
});
server.listen(8080);

```

其中的使用res.write跟res.send的区别

```javascript
var app.all('*',function(req,res,next){
	//所有的methods请求都会通过这里
	res.setHeader('Access-Cross-Allow-Origin','*');//setHeader可以设置多次，但是一次只能设置一条
	res.setHeader('Access-Cross-Allow-Mehods','GET,POST,PUT,DEL');
	next();
});

```
其中获取数据的方式相同:

```javascript
del:function(req,res){
	var Qstr = '';
	req.addListener('data',function(dataPart){
		Qstr +=dataPart;
	});	
	req.addListener('end',function(){
		var temp = JSON.parse(Qstr);
		console.log(temp);
	});
		
}
```

### 获取数据的处理
如何确定用户发过来请求什么操作
//第一种方式
```javascript
app.post('/student/:aaa',function(req,res){
	console.log(req.params.aaa);
	res.send('sudent page...');//每次调用send方法会自动去设置writeHeader里面的内容，但是writeHeader只能调用一次，所以会报错，可以使用setHeader，因为setHeader可以调用多次
	res.end();

});
```
//第二种方式（express,天生就支持RESTFUR服务器）
```javascript
app.get('/student',function(req,res){
	res.send('查询信息');
});
app.put('/student',function(req,res){
	res.send('修改信息');
});
app.post('/student',function(req,res){
	res.send('新增信息');
});
app.del('/student',function(req,res){
	res.send('删除信息');
});
```

```javascript
//use第一个参数，使用的是模糊匹配，地址里面有的，就会匹配到(模糊匹配)
//使用next
app.use('/about',function(req,res,next){
	console.log('输出');
	next();
});

```

### 设置当前网站的根目录

app.use(express.static(__dirname+'/public'));
不同形式:
var path = require('path');
//path函数可以将里面的字符串拼接在一起
app.use(express.static(path.jion(__dirname,'/public')));
app.use(express.static('/public');

### 配合express一起使用的插件

```javascript

var favicon=require('favicon');
var bodyParser=require('body-parser');
var methodOverride=require('method-override');

app.use(favicon());//favicon请求,在里面填地址，可以指定当前网站的favicon
app.use(bodyParser.json());//可以将传输过来的数据变成一个对象
app.user(bodyParser.urlendcoded({extended:false}));

app.use(methodOverrided(functoin('_method'));*///把一个非put，del请求变成put、del
//如果表单里面有一个name叫做'_method'的input

```



## webpack

1.全局安装
npm install -g webpack

2.局部安装(安装到当前目录的node_modules文件夹下)

npm install webpack --save-dev


用来在webpack中打包css、vue文件(加载器)
cssloader、np
vueloader
fileloader用于处理css链入的外部文件处理

plugins插件


