title: ajax知识梳理
date: 2017-5-1 6:52:35
categories: js
tags: ajax
---

<div><!--more--></div>



### 搭配环境

服务器工具:
	http://www.php100.com/html/plugin/ser/2013/0905/91.html
    
把我们做的文件放到指定目录下

我安装在了c:/wamp 开启服务器工具后 浏览器中输入localhost，将访问c:/wamp/www这个环境中的文件。

### 什么是ajax

ajax : Asynchronous JavaScript and XML 异步JavaScript和XML

用javascript异步形式去操作xml


### 同步和异步

#### 什么是同步
```javascript

<script src="jquery.js"></script>//必须将jq文件读取结束后才能执行后面的调用，按照从上到下的原则执行
$(function(){})	//阻塞 -> 同步

```
#### 什么是异步
```javascript

	setTimeout(function() {
		alert(1);
	}, 2000);//在这段代码中以异步的形式执行，先弹出2，然后过两秒钟弹出1.这种是非阻塞模式
	
	alert(2);//	非阻塞 - 异步。正是这种异步原理，不需要获取

```

### ajax的工作原理

模拟原理
```javascript
			var xhr = null;
			//打开浏览器
			//创建一个ajax对象ie6以下new ActiveXObject('Microsoft.XMLHTTP')
			
			if (window.XMLHttpRequest) {
					xhr = new XMLHttpRequest();
				} else {
					xhr = new ActiveXObject('Microsoft.XMLHTTP');
			}//两种创建模式，第一种判断,第二种try ，catch方式。两种方式都实现了兼容


			try {
					xhr = new XMLHttpRequest();
			} catch (e) {
					xhr = new ActiveXObject('Microsoft.XMLHTTP');
			}
						
			//在地址栏输入地址
		/*
			open方法
			参数
				1.打开方式
				2.地址
				3.是否异步
					异步:非阻塞 前面的代码不会影响后面代码的执行
					同步:阻塞 前面的代码会影响后面代码的执行
		*/
		xhr.open('get','1.txt',true);
		//提交 发送请求
		xhr.send();
		//等待服务器返回内容

		xhr.onreadystatechange = function() {
			
			if ( xhr.readyState == 4 ) {
				alert( xhr.responseText );
			}
			
		}

		//responseText就是向ajax后台的程序发送xmlhttp请求的时候, 后台程序接到请求会进行处理,处理结束后,可以返回一串数据给前台,这个就是responseText
```

### 异常

```javascript
	try {
		//代码尝试执行这个块中的内容,如果有错误，则会执行catch{}，	并且传入错误信息参数
		//alert(a);
		//new throw();
		//throw new Error('错了错了');
	} catch (e) {
		alert(e);
	}
```

### onreadystatechange事件

当 readyState 等于 4 且状态为 200 时，表示响应已就绪:
```javascript
	xmlhttp.onreadystatechange=function()
	  {
	  if (xmlhttp.readyState==4 && xmlhttp.status==200)
	    {
	    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
	    }
	  }
```
等待服务器返回内容

```javascript
			readyState : ajax工作状态
			responseText : ajax请求返回的内容就被存放到这个属性下面
			on readystate change : 当readyState改变的时候触发
			status : 服务器状态，http状态码

			xml.setRequestHeader('content-type', 'application/x-www-form-urlencoded');//申明发送的数据类型
		//post没有缓存问题
		//无需编码
```

### 表单:数据的提交

	action : 数据提交的地址，默认是当前页面
     method : 数据提交的方式，默认是get方式
        	1.get
            	把数据名称和数据值用=连接，如果有多个的话，那么他会把多个数据组合用&进行连接，然后把数据放到url?后面传到指定页面
				使用get方式，后台接收也必须设置成get方式，或者request
            2.post
				使用post方式，后台接收也必须设置成post方式，或者request

      enctype : 提交的数据格式，默认application/x-www-form-urlencoded
		
```javascript
	
	<form action="1.get.php" enctype="application/x-www-form-urlencoded">
    	<input type="text" name="username" />
        <input type="text" name="age" />
        <input type="submit" value="提交" />
    </form>


```

### 字符型的数组

eval() 函数可计算某个字符串，并执行其中的的 JavaScript 代码。使用该函数将字符串数组变成数组，就可以使用了``