## refs节点获取

```
// template
<button ref="myButton" @click="clickedButton">点击偶</button>

// script
let app = new Vue({ 
    methods: { 
        clickedButton: function () { 
            console.log(this.$refs.myButton); 
        } 
    } 
})
```

## directives


> 简介

自定义指令，类似v-for,v-if，可将复用操作简化，封装直接操作dom

> 用法一，组件使用


```
# 作为vue组件，参数传入
export default {
    data: {
        msg: 'hello world'
    },
    directives: {
        // 定义link指令
        link: {
            bind: function(el, binding, vnode){
                // 第一次绑定事件时调用，第一次被初始化               
                let url = binding.value
                if(url) {
                    el.onclick = () => {
                        window.logger.goTo(url)
                    }
                }
            },
            inserted: function(){
                // 插入父节点时调用
            },
            update: function(){
                // 组件更新
            }
        }
    }
}
```

> 用法二，全局注入

```
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
```

> 指令传参

当指令子组件内部定义时，指令的生命周期内也无法获取到定义的数据、方法，唯有通过传参方式，获取外层数据

* 传递一个参数

```
<template>
    <div v-link="'www.baidu.com'"></div>
</template>
```

* 传递多个参数

```
<template>
    <div v-link="{name:'百度',link:'www.baidu.com'}"></div>
</template>
```


* 获取传递参数

```
export default {
    directives: {
        link: {
            bind: function(el, binding, vnode){  
                // 获取跳转地址，名称
                let {name,link} = binding.value
            }
        }
    }
}
```


## Vue中使用动画


> 前言

之前一直对vue动画使用抱有很多疑问，官方介绍的vue动画使用，是怎么都没学会

> 可通过自定义指令，直接操作dom简单就可以实现，通过v-if，控制dom重复渲染


```
<template>
    <div class="loading" v-animationGroup="{animation,goToNextLayer}"></div>
</template>

<script type="text/ecmascript-6">
export default {
    data() {
        return {
            animation: {
                "animationName": "loading",
                "animationDuration": "2.5s",
                "animationFillMode": "both",
                "animationDelay": "0s",
                "animationIterationCount": "1",
                "animationDirection": "normal",
                "animationTimingFunction": "linear"
            }
        }
    },
    props: {
        goToNextLayer: Function
    },
    directives: {
        animationGroup: {
            inserted: function(el, binding, vnode) {
                let animation = binding.value.animation
                el.style.animationName = animation.animationName
                el.style.animationDuration = animation.animationDuration
                el.style.animationIterationCount = animation.animationIterationCount
                el.style.animationFillMode = animation.animationFillMode
                el.style.animationTimingFunction = animation.animationTimingFunction
                el.style.animationDelay = animation.animationDelay
                el.style.animationDirection = animation.animationDirection

                el.addEventListener('animationend', () => {
                    binding.value.goToNextLayer()
                })
            },
            unbind: function(el, binding, vnode) {
                const clearData = () => {
                    el.style.animationName = ""
                    el.style.animationDuration = ""
                    el.style.animationIterationCount = ""
                    el.style.animationFillMode = ""
                    el.style.animationTimingFunction = ""
                    el.style.animationDelay = ""
                    el.style.animationDirection = ""
                }

                clearData()
            }
        }
    },
    components: {

    }
}
</script>
```


