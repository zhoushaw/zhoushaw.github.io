---
title: grid
date: 2018-07-15 11:07:35
tags: css
categories: css
---

## 原文地址
[大漠postcss](https://www.w3cplus.com/PostCSS/postcss-deep-dive-shortcuts-and-shorthand.html)

## 知识杂点

a标签添加属性顺序:LVHA
link、visited、hover、active


<div><!-- more--></div>

## 语法

### 别名


```
// 属性设置别名:
@alias {
    bsz: border-size;
    bst: border-style;
    bcl: border-color;
}
// 然后添加以下代码来测试使用的新别名:
.set_border {
    bsz: 1px;
    bst: solid;
    bcl: #ccc;
}
```

### 定义速写

```
// 例如，将以下代码添加到您的src/style.css 文件，其中包含的 margin-top 、 margin-right 、 margin-bottom 和 margin-left 属性的简写:
.crip_shorthand {
    mt: 1rem;
    mr: 2rem;
    mb: 3rem;
    ml: 4rem;
}
// 编译您的代码，您应该看到你的dest/style.css代码是扩展后的:
.crip_shorthand {
    margin-top: 1rem;
    margin-right: 2rem;
    margin-bottom: 3rem;
    margin-left: 4rem;
}
```

### 定义圆形和三角形

> 圆形

```
// 若要创建一个圆，使用的语法 circle: size color; 。 将以下代码添加到您的src/style.css文件:
.circle {
    circle: 8rem #c00;
}
// 编译它，你就会看到下面的代码添加到您的dest/style.css 文件中:
.circle {
    border-radius: 50%;
    width: 8rem;
    height: 8rem;
    background-color: #c00;
}
```

> 三角形

```
// 我们会添加一个等腰三角形，它的语法是:
triangle: pointing-<up|down|left|right>;
width: <length>;
height: <length>;
background-color: <color>;
// 让我们将这个等腰三角形示例添加到src/style.css文件:
.isosceles-triangle {
    triangle: pointing-right;
    width: 7rem;
    height: 8rem;
    background-color: #c00;
}
// 编译的文件，现在您应该看到三角形的CSS代码在dest/style.css文件:
.isosceles-triangle {
    width: 0;
    height: 0;
    border-style: solid;
    border-color: transparent;
    border-width: 4rem 0 4rem 7rem;
    border-left-color: #c00;
}
```

### 清浮动


```
.clearfixed {
    clear: fix;
}
通过编译，您将看到它生成了清除浮动的代码:

.clearfixed:after {
    content: '';
    display: table;
    clear: both;
}
```

### Component


创建一个组件，可以使用@component ComponentName{...}语法。

```
@component SearchForm {
    padding: 0;
    margin: 0;
}
// 编译出来的结果是:
.SearchForm {
  padding: 0;
  margin: 0;
}
```

生成一个Descendent
通过@descendent descName{...}语法在组件中嵌套，可以创建一个Descendent。
在SearcForm组件中嵌套一个textField，添加一个Descendent，如下所示:
    
```

// @component SearchForm {
    padding: 0;
    margin: 0;

    /* Nest descendent under component */
    @descendent textField {
        border: 1px solid #ccc;
    }

}
// 编译出来是这样的:

.SearchForm {
    padding: 0;
    margin: 0;
}

.SearchForm-textField {
    border: 1px solid #ccc;
}
/
```

