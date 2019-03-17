---
title: vue单元测试
date: 2018-03-13 11:07:35
tags: vue
categories: vue
---


<div><!-- more--></div>


## 起步

> 依赖安装

`npm install --save-dev @vue/test-utils babel-jest babel-preset-env jest regenerator-runtime vue-template-compile`

> 编辑package.json

```
"scripts": {
    "test": "jest"
},
"jest": {
    "moduleFileExtensions": [
      "js",
      "json",
      "vue"
    ],
    "transform": {
      ".*\\.(vue)$": "<rootDir>/node_modules/vue-jest",
      "^.+\\.js$": "<rootDir>/node_modules/babel-jest"
    },
    "snapshotSerializers": [
      "<rootDir>/node_modules/jest-serializer-vue"
    ],
    "collectCoverage": true,
    "collectCoverageFrom": [
      "**/*.{js,vue}",
      "!**/node_modules/**"
    ],
    "coverageReporters": ["html", "text-summary"]
  },
```

> .babelrc

```
{
  "presets": [
    ["env", {
      "targets:": { "node": "6" } // change this to your node version
    }]
  ]
}
```



