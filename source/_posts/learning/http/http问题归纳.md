---
title: http常见问题
date: 2017-03-5 8:07:12
tags: http
categories: work
---


<div><!-- more--></div>

## 字节流传输

> 如何实现字节流接收并下载

// 将其定义在util.js中，需要时倒入，输入字节流对象即可进行下载
```javascript
/**
 * 下载blob的文件
 */
export const downLoadFile = (fileData)=>{
    let blob     = new Blob([fileData],{'type':'application/msexcel'});  // [文件]{类型}
    // 创建a标签模拟点击事件并下载
    let a        = document.createElement('a');
    a.download = 'excel.xls'  // 下载的文件名
    a.href     = window.URL.createObjectURL(blob);
    var evt = document.createEvent("MouseEvents");
    evt.initEvent("click", false, false);
    a.dispatchEvent(evt);
}
```

> 字节流传输

```javascript
    let formData = new FormData()
    // 设置文件内容
    formData.append('file', item.file)
    // 与后台约定的一些键值
    formData.append('type', this.qrCodeType)
```
## http请求报文

> content-type

1.text/html
2.text/plain
3.text/css
4.text/javascript
5.application/x-www-form-urlencoded
6.multipart/form-data
7.application/json
8.application/xml

> application/x-www-form-urlencoded

application/x-www-form-urlencoded是常用的表单发包方式，普通的表单提交，或者js发包

> application/json

application/json,通过json格式发送数据

## 三次握手

在TCP/IP协议中，TCP协议提供可靠的连接服务，采用三次握手建立一个连接。 

* 第一次握手：建立连接时，客户端发送syn包(syn=j)到服务器，并进入SYN_SEND状态，等待服务器确认； 
* 第二次握手：服务器收到syn包，必须确认客户的SYN（ack=j+1），同时自己也发送一个SYN包（syn=k），即SYN+ACK包，此时服务器进入SYN_RECV状态；
* 第三次握手：客户端收到服务器的SYN＋ACK包，向服务器发送确认包ACK(ack=k+1)，此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成三次握手。 完成三次握手，客户端与服务器开始传送数据.

## 四次分手

【注意】中断连接端可以是Client端，也可以是Server端。

1. 假设Client端发起中断连接请求，也就是发送FIN报文。

2. Server端接到FIN报文后，意思是说"我Client端没有数据要发给你了"，但是如果你还有数据没有发送完成，则不必急着关闭Socket，可以继续发送数据。所以你先发送ACK，"告诉Client端，你的请求我收到了，但是我还没准备好，请继续你等我的消息"。

3. 这个时候Client端就进入FIN_WAIT状态，继续等待Server端的FIN报文。当Server端确定数据已发送完成，则向Client端发送FIN报文，"告诉Client端，好了，我这边数据发完了，准备好关闭连接了"。

4. Client端收到FIN报文后，"就知道可以关闭连接了，但是他还是不相信网络，怕Server端不知道要关闭，所以发送ACK后进入TIME_WAIT状态，如果Server端没有收到ACK则可以重传。“，Server端收到ACK后，"就知道可以断开连接了"。 Client端等待了2MSL后依然没有收到回复，则证明Server端已正常关闭，那好，我Client端也可以关闭连接了。Ok，TCP连接就这样关闭了！


## 浏览器输入url发生了什么

总体来说分为以下几个过程:

DNS解析

TCP连接

发送HTTP请求

服务器处理请求并返回HTTP报文

浏览器解析渲染页面

连接结束

## http状态码

[状态码](http://www.runoob.com/http/http-status-codes.html)

协议、域名、端口有任何一个不同，都被当作是不同的域


