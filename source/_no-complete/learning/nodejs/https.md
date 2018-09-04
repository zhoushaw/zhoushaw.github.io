# https

## 概述

> 在nodejs中，提供了 https 这个模块来完成 HTTPS 相关功能。从官方文档来看，跟 http 模块用法非常相似

包含两部分内容:
1. 通过客户端、服务端的例子，对https模块进行入门讲解。
2. 如何访问安全证书不受信任的网站。（以 12306 为例子）


## 客户端例子
`跟http模块的用法非常像，只不过请求的地址是https协议的而已，代码如下：`

```
var https = require('https');

https.get('https://www.baidu.com', function(res){
    console.log('status code: ' + res.statusCode);
    console.log('headers: ' + res.headers);

    res.on('data', function(data){
        process.stdout.write(data);
    });
}).on('error', function(err){
    console.error(err);
});
```

## 生成证书

> 生成公私钥

```
# 生成服务器端私钥
openssl genrsa -out server.key 1024
# 生成服务器端公钥
openssl rsa -in server.key -pubout -out server.pem
 
 
# 生成客户端私钥
openssl genrsa -out client.key 1024
# 生成客户端公钥
openssl rsa -in client.key -pubout -out client.pem
```

> 生成 CA 证书


```
# 生成 CA 私钥
openssl genrsa -out ca.key 1024
# X.509 Certificate Signing Request (CSR) Management.
openssl req -new -key ca.key -out ca.csr
# X.509 Certificate Data Management.
openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt
```

> 生成服务器端证书和客户端证书


```
# 服务器端需要向 CA 机构申请签名证书，在申请签名证书之前依然是创建自己的 CSR 文件
openssl req -new -key server.key -out server.csr
# 向自己的 CA 机构申请证书，签名过程需要 CA 的证书和私钥参与，最终颁发一个带有 CA 签名的证书
openssl x509 -req -CA ca.crt -CAkey ca.key -CAcreateserial -in server.csr -out server.crt
 
# client 端
openssl req -new -key client.key -out client.csr
# client 端到 CA 签名
openssl x509 -req -CA ca.crt -CAkey ca.key -CAcreateserial -in client.csr -out client.crt
```

