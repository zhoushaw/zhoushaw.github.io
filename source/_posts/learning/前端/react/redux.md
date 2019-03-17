---
title: redux
date: 2017-07-9 7:52:35
tags: react
categories: js
---


<div><!-- more--></div>


## 技术栈

npm install react@2.0 --save-dev

chrome安装react调试插件
mdn官网	新的教学官网
掘金官网	可以搜索比较全面的技术信息
sass 扩展性的css

## redux

概念性跟Vuex的功能相似，主要用于存放数据，作为数据仓库使用，不过在用法上有很大的差别

- 1.使用redux需要先安装redux模块，
- 2.import {createStore} from redux
- 3.引出createStore函数，用来初始化store仓库的
- 4.初始化仓库之前，要给初始化函数一个参数，这个参数也是一个函数reducer(一般命名)
- 5.reducer函数需要为其提供两个参数，第一个参数是初始化的数据(state),第二个参数仓库的方法(action)
	- 1.这里需要注意的是，仓库的方法下，有两个参数，一个是方法名(type),另一个是调用方法时，传过来的值(payload)
	- 2.根据传过来的type看需要进行什么操作
- 6.var store = createStore(reducer);初始函数配置完成后，构建数据仓库
- 7.检测数据发生的变化，将最后的挂载ReactDOM.render(），放在函数里，store.subscribe(render);使用对函数进行实时更新



### reducer

用于存放一个函数，这个函数会返回一个state对象，这个对象就是数据仓库存放的内容

解构:
const type = action.type
const payload = action.payload
const {type,payload} = action;


defaultState
命名可随意:
主要用于存放初始化state数据的地方

var defaultState ={
    msg:'这里是显示内容',
    isShow:true
};

```javascript
var reducer=(state=defaultState,action={})=>{
    const {type,payload} = action;
    switch(type){
        case 'ALERT_SHOW':
            return Object.assign(
                {},
                state,
                {msg:payload,isShow:true}
            );
            break;
        case 'ALERT_HIDE':
            return Object.assign(
                {},
                state,
                {msg:'',isShow:false}
            )
            break;
        default:return state;break;
    }
} 
```

## createStore

将已经配置好了的初始化函数，放到createStore里面进行数据仓库的构建
var store = createStore(reducer);



## 使用数据仓库的数据

引入数据仓库
import store from './store/store.js'

store.getState().msg	:可以获取数据仓库的msg数据
store.dispatch(type:'ALERT_SHOW',payload:'显示的信息');

type:对应要操作的方法，payload要传递过去的数据


