title: AES对称加密
date: 2018-1-25 4:36:35
categories: js
tags: 
- js
- aes
---


![](http://sf.dankal.cn/tmp/wxb6cbb81471348fec.o6zAJszA0KOosUhoTLKll8Q2-ufA.46e2722ada5f99c4d6cbca3b488da45c.jpg)

<div><!--more--></div>

## 前言


> 数据安全

对于一款应用无疑非常重要,明文的数据传输对于应用而言非常致命。

> 用户的数据，接口、信息等等都暴露在攻击者的面前

1.攻击者只需要获取用户的token信息，就可以通过接口模拟<code>用户行为</code>
2.使用用户信息模拟<code>用户操作</code>


> 解决目前的安全隐患

前后端统一使用<code>Base64</code> -> <code>AES</code> (<code>key</code>:keyname, <code>iv</code>:ivnum) -> <code>gzip</code>的方式来，进行加密、解密。来确保数据安全

## 项目结构

```

util
│  
├─encryption
│  ├─Base64.js
│  ├─lock.js
│  ├─pako.js
│  ├─DataCrypt.js
│  │  
│  └─cryptojs
│      ├─lib
│      ├─cryptojs.js
│      ├─package.json
│      └─README.md
└─comutil

```


> 工具类下的工具函数封装应用

* DataCrypt.js 对AES方法进行封装实现自定义key，vi
* pako 实现数据的压缩与解压缩
* base64对数据进行64位编码
* lock.js对以上数据处理方法进行整体封装

> locak.js的封装

```javascript
// 引入AES加解密方法
import { Encrypt,Decrypt } from './DataCrypt.js'
// 引入Base64位，装换方法。
import { Base64 } from './Base64.js';
// 引入gizp，js中的压缩与解压缩
let pako = require('./pako.js');

const lock = (obj)=>{
  let jsonStringify,base64Encode,aesEncrypt,deflateString

  // 将json数据转成strting类型
  jsonStringify = JSON.stringify(obj)
  // 将jsonString数据转成base64位数据
  base64Encode = Base64.encode(jsonStringify)
  // 将base64位数据使用AES进行加密
  aesEncrypt = Encrypt(base64Encode); 
  // 将aes加密数据进行压缩
  deflateString = pako.deflate(aesEncrypt, { to: 'string' });

  return deflateString
}




const unlock = (obj)=>{
  let jsonParse,base64Decode,aesDecrypt,inflateString

  // 将压缩的数据解压缩
  inflateString = pako.inflate(obj, { to: 'string' })
  // 将数据使用AES解码
  aesDecrypt = Decrypt(inflateString)
  // 将base64位数据转成jsonstring格式
  base64Decode = Base64.decode(aesDecrypt)
  // 将jsonstringify格式数据转成JSON数据
  jsonParse = JSON.parse(base64Decode)

  return jsonParse
}

export { lock,unlock }

```



## pako.js

> 压缩模块，可以对内容进行压缩和解压缩

```javascript
npm install pako
```

模块安装完成之后使用，dist目录内的pako.js即可

> 使用

```javascript 

let pako = require('./pako.js');
let deflateString = pako.deflate(obj, { to: 'string' });
let inflateString = pako.inflate(obj, { to: 'string' })


```


## CryptoJS核心

AES加密在密码学中又称Rijndael加密法，是美国联邦政府采用的一种区块加密标准

> 起步

<pre>
	npm install cryptojs
</pre>

> 封装 DataCrypt.js,对cryptojs进行使用

```javascript

const Crypto = require('./cryptojs/cryptojs').Crypto;
const Encrypt = (word)=>{
    var mode = new Crypto.mode.CBC(Crypto.pad.pkcs7);
    var eb = Crypto.charenc.UTF8.stringToBytes(word);
    var kb = Crypto.charenc.UTF8.stringToBytes("dankal1234567891");//KEY
    var vb = Crypto.charenc.UTF8.stringToBytes("12345678");//IV
    var ub = Crypto.AES.encrypt(eb,kb,{iv:vb,mode:mode,asBpytes:true});
    return ub;
}

//解密：

const   Decrypt = (word)=>{
    var mode = new Crypto.mode.CBC(Crypto.pad.pkcs7);
    var eb = Crypto.util.base64ToBytes(word);
    var kb = Crypto.charenc.UTF8.stringToBytes("dankal1234567891");//KEY
    var vb = Crypto.charenc.UTF8.stringToBytes("12345678");//IV
    var ub = Crypto.AES.decrypt(eb,kb,{asBpytes:true,mode:mode,iv:vb});
    return ub;
}

export {
    Encrypt,
    Decrypt
}

```

## javascript base64位编码

> 由于在小程序中有诸多限制base64位转码方法有特定限制

base64文件可以自行下载，这里列出一个，我再项目中使用的


```javascript

import { Base64 } from './Base64.js';

//编码
 base64Encode = Base64.encode(jsonStringify)

//解码
 base64Decode = Base64.decode(aesDecrypt)

```

> base64源码

```javascript

;(function (global, factory) {
    typeof exports === 'object' && typeof module !== 'undefined'
        ? module.exports = factory(global)
        : typeof define === 'function' && define.amd
        ? define(factory) : null
}((
    typeof self !== 'undefined' ? self
        : typeof window !== 'undefined' ? window
        : typeof global !== 'undefined' ? global
: this
), function(global) {
    'use strict';
    // existing version for noConflict()
    var _Base64 = global.Base64;
    var version = "2.4.2";
    // if node.js, we use Buffer
    var buffer;
    if (typeof module !== 'undefined' && module.exports) {
        try {
            buffer = require('buffer').Buffer;
        } catch (err) {}
    }
    // constants
    var b64chars
        = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/';
    var b64tab = function(bin) {
        var t = {};
        for (var i = 0, l = bin.length; i < l; i++) t[bin.charAt(i)] = i;
        return t;
    }(b64chars);
    var fromCharCode = String.fromCharCode;
    // encoder stuff
    var cb_utob = function(c) {
        if (c.length < 2) {
            var cc = c.charCodeAt(0);
            return cc < 0x80 ? c
                : cc < 0x800 ? (fromCharCode(0xc0 | (cc >>> 6))
                                + fromCharCode(0x80 | (cc & 0x3f)))
                : (fromCharCode(0xe0 | ((cc >>> 12) & 0x0f))
                   + fromCharCode(0x80 | ((cc >>>  6) & 0x3f))
                   + fromCharCode(0x80 | ( cc         & 0x3f)));
        } else {
            var cc = 0x10000
                + (c.charCodeAt(0) - 0xD800) * 0x400
                + (c.charCodeAt(1) - 0xDC00);
            return (fromCharCode(0xf0 | ((cc >>> 18) & 0x07))
                    + fromCharCode(0x80 | ((cc >>> 12) & 0x3f))
                    + fromCharCode(0x80 | ((cc >>>  6) & 0x3f))
                    + fromCharCode(0x80 | ( cc         & 0x3f)));
        }
    };
    var re_utob = /[\uD800-\uDBFF][\uDC00-\uDFFFF]|[^\x00-\x7F]/g;
    var utob = function(u) {
        return u.replace(re_utob, cb_utob);
    };
    var cb_encode = function(ccc) {
        var padlen = [0, 2, 1][ccc.length % 3],
        ord = ccc.charCodeAt(0) << 16
            | ((ccc.length > 1 ? ccc.charCodeAt(1) : 0) << 8)
            | ((ccc.length > 2 ? ccc.charCodeAt(2) : 0)),
        chars = [
            b64chars.charAt( ord >>> 18),
            b64chars.charAt((ord >>> 12) & 63),
            padlen >= 2 ? '=' : b64chars.charAt((ord >>> 6) & 63),
            padlen >= 1 ? '=' : b64chars.charAt(ord & 63)
        ];
        return chars.join('');
    };
    var btoa = global.btoa ? function(b) {
        return global.btoa(b);
    } : function(b) {
        return b.replace(/[\s\S]{1,3}/g, cb_encode);
    };
    var _encode = buffer ?
        buffer.from && buffer.from !== Uint8Array.from ? function (u) {
            return (u.constructor === buffer.constructor ? u : buffer.from(u))
                .toString('base64')
        }
        :  function (u) {
            return (u.constructor === buffer.constructor ? u : new  buffer(u))
                .toString('base64')
        }
        : function (u) { return btoa(utob(u)) }
    ;
    var encode = function(u, urisafe) {
        return !urisafe
            ? _encode(String(u))
            : _encode(String(u)).replace(/[+\/]/g, function(m0) {
                return m0 == '+' ? '-' : '_';
            }).replace(/=/g, '');
    };
    var encodeURI = function(u) { return encode(u, true) };
    // decoder stuff
    var re_btou = new RegExp([
        '[\xC0-\xDF][\x80-\xBF]',
        '[\xE0-\xEF][\x80-\xBF]{2}',
        '[\xF0-\xF7][\x80-\xBF]{3}'
    ].join('|'), 'g');
    var cb_btou = function(cccc) {
        switch(cccc.length) {
        case 4:
            var cp = ((0x07 & cccc.charCodeAt(0)) << 18)
                |    ((0x3f & cccc.charCodeAt(1)) << 12)
                |    ((0x3f & cccc.charCodeAt(2)) <<  6)
                |     (0x3f & cccc.charCodeAt(3)),
            offset = cp - 0x10000;
            return (fromCharCode((offset  >>> 10) + 0xD800)
                    + fromCharCode((offset & 0x3FF) + 0xDC00));
        case 3:
            return fromCharCode(
                ((0x0f & cccc.charCodeAt(0)) << 12)
                    | ((0x3f & cccc.charCodeAt(1)) << 6)
                    |  (0x3f & cccc.charCodeAt(2))
            );
        default:
            return  fromCharCode(
                ((0x1f & cccc.charCodeAt(0)) << 6)
                    |  (0x3f & cccc.charCodeAt(1))
            );
        }
    };
    var btou = function(b) {
        return b.replace(re_btou, cb_btou);
    };
    var cb_decode = function(cccc) {
        var len = cccc.length,
        padlen = len % 4,
        n = (len > 0 ? b64tab[cccc.charAt(0)] << 18 : 0)
            | (len > 1 ? b64tab[cccc.charAt(1)] << 12 : 0)
            | (len > 2 ? b64tab[cccc.charAt(2)] <<  6 : 0)
            | (len > 3 ? b64tab[cccc.charAt(3)]       : 0),
        chars = [
            fromCharCode( n >>> 16),
            fromCharCode((n >>>  8) & 0xff),
            fromCharCode( n         & 0xff)
        ];
        chars.length -= [0, 0, 2, 1][padlen];
        return chars.join('');
    };
    var atob = global.atob ? function(a) {
        return global.atob(a);
    } : function(a){
        return a.replace(/[\s\S]{1,4}/g, cb_decode);
    };
    var _decode = buffer ?
        buffer.from && buffer.from !== Uint8Array.from ? function(a) {
            return (a.constructor === buffer.constructor
                    ? a : buffer.from(a, 'base64')).toString();
        }
        : function(a) {
            return (a.constructor === buffer.constructor
                    ? a : new buffer(a, 'base64')).toString();
        }
        : function(a) { return btou(atob(a)) };
    var decode = function(a){
        return _decode(
            String(a).replace(/[-_]/g, function(m0) { return m0 == '-' ? '+' : '/' })
                .replace(/[^A-Za-z0-9\+\/]/g, '')
        );
    };
    var noConflict = function() {
        var Base64 = global.Base64;
        global.Base64 = _Base64;
        return Base64;
    };
    // export Base64
    global.Base64 = {
        VERSION: version,
        atob: atob,
        btoa: btoa,
        fromBase64: decode,
        toBase64: encode,
        utob: utob,
        encode: encode,
        encodeURI: encodeURI,
        btou: btou,
        decode: decode,
        noConflict: noConflict
    };
    // if ES5 is available, make Base64.extendString() available
    if (typeof Object.defineProperty === 'function') {
        var noEnum = function(v){
            return {value:v,enumerable:false,writable:true,configurable:true};
        };
        global.Base64.extendString = function () {
            Object.defineProperty(
                String.prototype, 'fromBase64', noEnum(function () {
                    return decode(this)
                }));
            Object.defineProperty(
                String.prototype, 'toBase64', noEnum(function (urisafe) {
                    return encode(this, urisafe)
                }));
            Object.defineProperty(
                String.prototype, 'toBase64URI', noEnum(function () {
                    return encode(this, true)
                }));
        };
    }
    //
    // export Base64 to the namespace
    //
    if (global['Meteor']) { // Meteor.js
        Base64 = global.Base64;
    }
    // module.exports and AMD are mutually exclusive.
    // module.exports has precedence.
    if (typeof module !== 'undefined' && module.exports) {
        module.exports.Base64 = global.Base64;
    }
    else if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define([], function(){ return global.Base64 });
    }
    // that's it!
    return {Base64: global.Base64}
}));
```


