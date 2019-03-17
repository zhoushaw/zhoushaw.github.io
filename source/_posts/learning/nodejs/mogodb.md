---
title: mongodb使用
date: 2017-08-9 8:52:35
tags: mongodb
categories: js
---


<div><!-- more--></div>

## 安装

[菜鸟教程](http://www.runoob.com/mongodb/mongodb-osx-install.html)

## 数据库进入
mongod --dbpath E:\mongodb\db -directoryperdb

## 基本操作

进入使用:
- mongo 进入数据库操作
- show dbs :展示所有的数据库
- use ‘local’:使用哪一个数据库

## ObjectId

mongodb中提供了Id

分别组成
 Time/Machine/PID/INC

### 插入操作

db.people.insert({name:'leo',age:'23'});	:插入数据
==
var model ={name:'leo',age:'23'}
db.people.insert(model);

### 查找:(支持正则表达式)

- db.people.find({$where:function(){return this.name!='zs'}});	:查找名字不为zs的数据
- db.people.findOne();	:找到第一条数据
- 
- db.people.find({"name":/^[^z]/,"address.provice":"guangzhou"});	:找到数据name开头不为z，并且地址省份为guangzhou的数据
- db.people.find({$or:[{"name":"zs"},{"address.provice":"guangzhou"}]});	:找到name为zs或者address。provice为guangzhoju的数据
- db.people.find().pretty();// 将查找到的数据格式化显示
- 
- db.people.find({"name":{$in;["zs","ls"]});	:找到name里面有zs和li的数据
- db.people.find({"name":{$nin;["zs","ls"]});	:找到name里面不是zs和li的数据


db.student.find({age:{$gt:20}});	:大于20
db.student.find({age:{$gte:20}});	:大于等于20
db.student.find({age:{$lt:20}});	:小于20
db.student.find({age:{$lte:20}});	:小于等于20
db.student.find({age:{$ne:20}});	:不等于20

$gt : >
$lt : <
$gte: >=
$lte: <=
$ne : !=、<>
$in : in
$nin: not in


db.people.find().limit(2);  		:找到前两条，找到后面所有的
db.people.find().skip(2).limit(1);	:跳过前两条，往后找一条

db.people.find({},{name:1,_id:0})	:id不要，name要一列

db.people.find({},{_id:0});			:id不要，其他都要

db.people.count({name:{$in:['zx','li']});	:找到有zx，li的行

db.people.update({naem:'ls',{$set{"address.provice":"jiangxi"}}});






### 删除:

db.people.remove({});		:删除people的所有数据

db.people.drop();//删除这张表了

### 修改

db.student.update({},{},false,false);
第一个参数修改的参数，
第二个参数修改成什么样子
第三个默认false，true没有找到修改的数据，插入
第四个数据:默认false，找到后只修改一条，true修改所有的


db.student.update({name:'ls'},{$set:{age:'22'}});	:只修改我们想修改的

db.student.update({name:'ls'},{age:'22'});	:使用后只留下了要改的数据

db.student.update({},{$set:{age:'22'}});	:所有数据年龄变成22

db.student.update({},{$inc:{age:2}});	:所有年龄的基础上加2


## 表操作

show collections



## 存储过程

db.system.js		:芒果数据库中有这样的一张表，用来存放js函数

db.system.js.find();	:查找当前的存储过程的方式


db.student.find().explain();
可以查看当前查找的计划


建立索引
db.dormitory.ensureIndex({name:1});		:表示升序的索引，-1表示降序的索引
对于经常查询的列，加一个索引可以降低成本


确定唯一的索引:
db.dormitory.ensureIndex({name:1},(unique:true));


删除索引:
db.dormitory.dropIndex('name_1');

排序:
db.dormitory.find().sort({name:1},{sex:1});按照name来升序，第二条件是性别
db.dormitory.find().sort({name:-1});按照name来降序


分组:
db.dormitory.group({
	key:{type:true},//可以联合分组，增加多个条件	
	initial:{count:0,names:[]},//每次进来初始化这两个参数，
	reduce:function(cur,end){//end进来都是上一次的状态
		end.names.push(cur.name);
		end.count++
		return end;	
	},
	condition:{type:'male'}
});
key:分组的关键词
initial:进行操作的数据初始化
reduce进行的操作
db.dormitory.group({
	key:{type:true},
	initial:{count:0,names:[]},
	reduce:function(cur,end){
		end.names.push(cur.name);
		end.count++
		return end;	
	},
	condition:{type:'male'}
});

## 创建索引

// 将名字当做唯一索引，使用索引使用空间去换取时间。索引创建完成之后，表将根据索引进行排序
db.user.createIndex({name:1},{unique:1});

// 删除索引
db.user.dropIndex({name:1})


