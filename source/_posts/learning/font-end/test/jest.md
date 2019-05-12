---
title: Jest
date: 2019-05-4 11:01:35
categories: js
tags: js
---

## 起步

> 安装

```
npm install --save-dev jest
```

> `pageckage.json`配置

```
{
  "scripts": {
    "test": "jest"
  }
}
```


## Expect

`Expect`是一个函数，第一个参数接收`value`,后面可接链式属性判断

* `expect(value)`
    * `expect(value).not.toEqual`: 与后面等式取反比较
    * `toEqual(compareValue)`: `value` 与 `compareValue`必须完全相等

> 自定义校验方法

```
// 查询对象key值是否存在对象中
expect.extend({
    toContainKeys(received, keys) {
        const receivedKeys = Object.keys(received);
        const pass = keys.every((val => receivedKeys.includes(val)));
        if (pass) {
            return {
                message: () =>
                `expected ${JSON.stringify(received)} have contain ${receivedKeys}`,
                pass: true,
            };
        } else {
            return {
                message: () =>
                `expected ${JSON.stringify(received)} don't have contain ${receivedKeys}`,
                pass: false,
            };
        }
    }
});
```

