---
title: sequelize基础
date: 2018-10-15 16:14
tags: sequelize
categories: node
---


## sequelize简介

sequelize是Node的ORM框架，用于操作mysql数据库


<div><!-- more--></div>

## 在egg中定义model


```
module.exports = app => {
  const {STRING, INTEGER, DATE, NOW} = app.Sequelize;

  const Discuss = app.model.define('topic', {
    discuss_id: {type: INTEGER(10), primaryKey: true, autoIncrement: true},//帖子id
    topic_id: {type: INTEGER(10)},//用户id
    user_id: {type: STRING(255)},//用户id
    topic_title: {type: STRING(255), allowNull: true}, // 帖子标题
    topic_img: {type: STRING(1000), allowNull: false},// 图片地址，
    address: {type: STRING(255), allowNull: true}, // 发表地址
    created_at: {type: DATE, defaultValue: NOW},// 创建时间
    updated_at: {type: DATE, defaultValue: NOW}// 更新时间
  });

  return Discuss;
};
```

## 类型


```
STRING(255) # 不定长字符串(最长字符长度)
INTEGER # 整型
DATE # 日期
```

## 字段属性


```
Type # 字符串类型
primaryKey # 是否主键Boolean
autoIncrement # 是否自增Boolean
allowNull # 是否可为空Boolean  
defaultValue # 默认值String
```


## sequelize-cli

> 新建Migration创建表

`npx sequelize migration:generate --name=init-users`

执行完后会在 database/migrations 目录下生成一个 migration 文件(${timestamp}-init-users.js)，我们修改它来处理初始化 users 表


```
'use strict';

module.exports = {
  // 在执行数据库升级时调用的函数，创建 users 表
  up: async (queryInterface, Sequelize) => {
    const { INTEGER, DATE, STRING } = Sequelize;
    await queryInterface.createTable('users', {
      id: { type: INTEGER, primaryKey: true, autoIncrement: true },
      name: STRING(30),
      age: INTEGER,
      created_at: DATE,
      updated_at: DATE,
    });
  },
  // 在执行数据库降级时调用的函数，删除 users 表
  down: async queryInterface => {
    await queryInterface.dropTable('users');
  },
};
```

> 执行 migrate 进行数据库变更

`npx sequelize db:migrate`

执行之后，我们的数据库初始化就完成了。

> 定义model


```
# app/model/ 目录下编写 user的model

module.exports = app => {
  const { STRING, INTEGER, DATE } = app.Sequelize;

  const User = app.model.define('user', {
    id: { type: INTEGER, primaryKey: true, autoIncrement: true },
    name: STRING(30),
    age: INTEGER,
    created_at: DATE,
    updated_at: DATE,
  });

  return User;
};
```

这个 Model 就可以在 Controller 和 Service 中通过 app.model.User 或者 ctx.model.User 访问到了

## config


```
const Bar = sequelize.define('bar', { /* bla */ }, {
 
  # 不自动为表名添加复数+s或es
  freezeTableName: true
})
```


