---
title: vue源码中常用函数
date: 2018-06-05 6:21:35
tags: vue
categories: vue
---


## isReserved

```
function isReserved (str) {
  var c = (str + '').charCodeAt(0);
  return c === 0x24 || c === 0x5F
}
```

该函数的作用是：检查字符串是否是以 $ 或者 _ 开始的,在vue中用于检查是否该变量可以用于代理至`vm`中

我们在这里需要学习的是 charCodeAt() 这个方法。它返回的是 Unicode 编码的字符串表示的值。

比如说：

```
'abc'.charCodeAt(0);  // 97
'abc'.charCodeAt(1);  // 98
```

