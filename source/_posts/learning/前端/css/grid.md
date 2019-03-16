---
title: grid
date: 2017-06-15 11:07:35
tags: css
categories: css
---


## 概念

grid目前支持并不是很全面，低版本chrome也不支持这一特性。但grid必然会和flex一同成为主流布局模式，grid标准不是用来替代flex的，flex和grid相辅相成互相铺垫刚好可以发挥其最大的优势。grid主要用于二维，而flex则是一维，当你只需要对一行或者一列进行布局是flex无疑是比较好的选择，而多行多列有对应关系时grid则更胜一筹。

尽管市面上的主流浏览器已经支持grid这一特性，但稍低版本的浏览器任然不支持，其中便包括IE、低版本chrome，直接将grid网格布局推至生产环境目前并不是个十分明智的选择，但这并不妨碍我们学习网格布局，相信在下面的学习中你将会感受到网格布局的威力


<div><!-- more--></div>

## 起步

1.设置网格布局也十分简单：

`display: grid`一旦给容器使用grid属性，容器的所有子元素都将进入grid布局文档流

2.其中三个属性都可以使容器进入grid文档流
display: `grid` | `inline-grid` | `subgrid`


## 网格属性

**词法：**

```
grid-template-columns：<track-size>.... | <line-name> <track-size> ...;

grid-template-rows：<track-size>.... | <line-name> <track-size> ...;
```

**网格线定义名称：**


```
grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end];   

grid-template-rows: [row1-start] 25% [row1-end] 100px [third-line] auto [last-line];  

```


**重复声明:**

```
grid-template-columns: repeat(3, 20px [col-start]) 5%;  

/* 等价于 */
grid-template-columns: 20px [col-start] 20px [col-start] 20px [col-start] 5%;  

```


**特殊单元 fr**

`将container容器分为三列，第一列宽度为50px,剩余两列平分剩余空间。自由空间是在固定子项确定后开始计算的`

```
.container {
    grid-teamplte-columns: 50px 1fr 1fr;
}
```


## 网格布局实例


> 响应式布局

**目标效果**

![reactive](https://mdn.mozillademos.org/files/14749/11-responsive-areas.png)

`通过grid-area属性设置对应的area名称`

```
.main-head {
  grid-area: header;
}
.content {
  grid-area: content;
}
.main-nav {
  grid-area: nav;
}
.side {
  grid-area: sidebar;
}
.ad {
  grid-area: ad;
}
.main-footer {
  grid-area: footer;
}
```

`grid-template-areas设置area块所在位置`


```
/* 小于500px适配方案 */
.wrapper {
        display: grid;
        grid-gap: 20px;
        grid-template-areas: 
            "header"
            "nav"
            "content"
            "sidebar"
            "ad"
            "footer";
    }

    /* 700px大小布局 */
    @media (min-width: 500px) {
        .wrapper {
            grid-template-columns: 1fr 3fr;
            grid-template-areas: 
            "header  header"
            "nav     nav"
            "sidebar content"
            "ad      footer";
        }
        nav ul {
            display: flex;
            justify-content: space-between;
        }
    }

    @media (min-width: 700px) {
        .wrapper {
            grid-template-columns: 1fr 4fr 1fr;
            grid-template-areas: 
            "header header  header"
            "nav    content sidebar"
            "nav    content ad"
            "footer footer  footer"
        }
        nav ul {
            flex-direction: column;
        }
    }
```

> 栅格系统

`很多人都喜欢通过栅格系统来进行布局，使用grid能非常轻松制作一个栅格系统`


```
.wrapper {
      display: grid;
      grid-template-columns: repeat(12, [col-start] 1fr);
      grid-gap: 20px;
}
.item1 {
    grid-column: col-start / span 3;
}
.item2 {
    grid-column: col-start 6 / span 4 ;
    grid-row: 1 / 3;
}
.item3 {
    grid-column: col-start 2 / span 2;
    grid-row: 2;
}
.item4 {
    grid-column: col-start 3 / -1;
    grid-row: 3;
}
```

![](https://mdn.mozillademos.org/files/14753/11-grid-inspector-12col.png)



