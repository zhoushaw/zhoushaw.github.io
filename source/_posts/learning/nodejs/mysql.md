---
title: mysql入门
date: 2018-12-27 16:14
tags: node
categories: node
---



## 启动
> 命令行启动

* 安装完成之后
* vim ~/.zshrc，添加mysql路径`PATH=$PATH:/usr/local/mysql/bin`
* `mysql -u root -p`输入密码，进入mysql管理


## 常见问题

> 连接mysql遇到的错误

```
ER_NOT_SUPPORTED_AUTH_MODE: Client does not support authentication protocol requested by server; consider upgrading MySQL client
```

<div><!-- more--></div>

=>

everything should still work if you use the mysql_native_password plugin

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'YourRootPassword';
-- or
CREATE USER 'foo'@'%' IDENTIFIED WITH mysql_native_password BY 'bar';
```

## 查看数据库、表

```
mysql> show databases;
mysql> show tables;
```

## 创建数据库、表


```
mysql> CREATE DATABASE database_name;
mysql> show tables;
```

## 数据类型

[数据类型](https://blog.csdn.net/qq_21397217/article/details/51656783#%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)

## 执行本地sql脚本

> cmd命令执行

```
mysql –uroot –p123456 sql_path;
```

> 进入mysql命令行

```
mysql>source sql_path;
```

## 使用数据库、表

```
# 使用数据库
mysql> use database db_name;
# 使用表
mysql> use table tb_name;
```

## 删除数据库、表

```
# 删除数据库
mysql> drop database db_name;
# 删除表
mysql> drop table tb_name;
```

## 创建表


```
mysql> CREATE TABLE 数据表名
    -> (
    -> 列名1 数据类型(数据长度) PRIMARY KEY,        --主键
    -> 列名2 数据类型(数据长度) NOT NULL,        --非空约束
    -> 列名3 数据类型(数据长度) DEFAULT '默认值',        --默认值约束
    -> UNIQUE(列名a),        --唯一约束
    -> CONSTRAINT 主键名 PRIMARY KEY (列名a,列名b,...)，        --复合主键
    -> CONSTRAINT 外键名 FOREIGN KEY (列名) REFERENCES 表名(主键名)        --外键
    -> );
```

例如:


```
CREATE TABLE users (
  user_id int(11) NOT NULL AUTO_INCREMENT COMMENT 'primary key',
  name varchar(30) DEFAULT NULL COMMENT 'user name',
  email varchar(70) DEFAULT NULL COMMENT 'user email',
  created_at datetime DEFAULT NULL COMMENT 'created time',
  updated_at datetime DEFAULT NULL COMMENT 'updated time',
  PRIMARY KEY (user_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='user';
```


## 修改数据


```
# 修改列定义
ALTER TABLE table_name MODIFY [COLUMN] col_name column_definition [FIRST | AFTER col_name];
/* 例: */ ALTER TABLE users MODIFY user_id VARCHAR(255)  NOT NULL;;
```

## id自增修改起始值
设置主键id自增的数据库表删除数据后，自增id不会自动重新计算 
想要重新设置自增的id可以用如下命令

alter table table_name AUTO_INCREMENT=10;
table_name是表名,10表示自增开始的位置

