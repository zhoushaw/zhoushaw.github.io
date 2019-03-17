---
title: webpack
date: 2018-04-26 8:52:35
tags: tool
categories: tool
---


<div><!-- more--></div>

# wepback 4.0

## 零配置快速构建

> 创建文件夹

    mkdir webpack-4-quickstart && cd $_

>  初始化

`npm init -y`

> 安装依赖

`npm i webpack-cli --save-dev`
`npm i webpack --save-dev`

> 增加快速构建

在package.json中添加build命令
`"scripts": {
  "build": "webpack"
}`

> 注意

webpack4.0后默认必须
在根目录新建./src/index.js为默认，否则无法build

> 实例

1. 新建./src/index.js，内容为console.log('test build');
2. `npm run build`后将在根目录生成dist/main.js

## 生产环境和开发环境的mode

> 风格

webpack4.0有两种项目风格
1.a configuration file for development
2.a configuration file for production

> 设置项目打包环境

在package.json中添加命令，区分dev，和product
`"scripts": {
  "dev": "webpack --mode development",
  "build": "webpack --mode production"
}`

> 特点

`npm run dev`得到的模块是未压缩的
`npm run build`得到的模块是压缩后的

## 修改默认输入输出文件

> 特点

webpack的零配置优点显著，但如何自定义导入导出文件目录

> 自定义导入导出

配置package.json

```
"scripts": {
    "dev": "webpack --mode development ./test/from/js/index.js --output ./test/to/main.js",
    "build": "webpack --mode production ./test/from/js/index.js --output ./test/to/main.js"
}
```

## 添加babel

> 引言

并不是所有浏览器都能能好支持es6特性，webpack自身不具备将es6或者更高ECMAscript转换成es5，但webpack提供loader可以将其转换成es5特性。尽管webpack零配置的特性，但是对于loader的使用任然需要通过配置来发挥其特效

> 安装依赖

* babel-core
* babel-loader
* babel-preset-env for compiling Javascript ES6 code down to ES5

`npm i babel-core babel-loader babel-preset-env --save-dev`

> 配置

webpack提供两种配置babel的方式:

1. 使用babel的loader和配置文件
新建 **.babelrc**文件名，并且在文件中添加

```
{
    "presets": [
        "env"
    ]
}
```
使用webpack.config.js

```
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  }
};
```

2. 配置package.json和配置文件
使用**--module-bind**在**npm**脚本中

```
"scripts": {
    "dev": "webpack --mode development --module-bind js=babel-loader",
    "build": "webpack --mode production --module-bind js=babel-loader"
  }
```

## 配置react

> 安装react

`npm i react react-dom --save-dev`

> 安装babel预处理

`npm i babel-preset-react --save-dev`

> 配置**.babelrc**

```
{
  "presets": ["env", "react"]
}
```
> 配置webpack.json

```
module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  }
};
```

> 案例

1.新建React component在./src/App.js

```
import React from "react";
import ReactDOM from "react-dom";
const App = () => {
  return (
    <div>
      <p>React here!</p>
    </div>
  );
};
export default App;
ReactDOM.render(<App />, document.getElementById("app"));
```
2.导入react组件，在./src/index.js中
`import App from "./App";`
3.构建
`npm run build`
4.新建html，引入压缩代码

```
<body>
    <div id="app"></div>
    <script src="./dist/main.js"></script>
</body>
```

## HTML plugin

> 安装依赖

`npm i html-webpack-plugin html-loader --save-dev`

> 配置webpack.config.js


```
const HtmlWebPackPlugin = require("html-webpack-plugin");
module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./src/index.html",
      filename: "./index.html"
    })
  ]
};
```

## 提取css

> 安装依赖

`npm i mini-css-extract-plugin css-loader --save-dev`

> 新建css文件


```
/* CREATE THIS FILE IN ./src/main.css */
body {
    line-height: 2;
}
```
> 配置webpack.config.js和plugin


```
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, "css-loader"]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./src/index.html",
      filename: "./index.html"
    }),
    new MiniCssExtractPlugin({
      filename: "[name].css",
      chunkFilename: "[id].css"
    })
  ]
};
```
> 导入css


```
// PATH OF THIS FILE: ./src/index.js
import style from "./main.css";
```

## 热更新

> 概念

在项目开发过程中，修改代码后，需要手动刷新项目十分不便。通过配置热更新达到自动更新项目的目的并且启动项目自动打开浏览器，修改代码后会产生局部更新，项目会自动重新构建

> 安装依赖

`npm i webpack-dev-server --save-dev`

> 修改webpack.config.js配置

```
"scripts": {
  "start": "webpack-dev-server --mode development --open",
  "build": "webpack --mode production"
}
```

# webpack demos

## 起步

> 基础依赖

```
npm i -g webpack webpack-dev-server
npm i webpack-dev-server --save-dev // 热更新
```

> 常用webpack命令行

* webpack – building for development
* webpack -p – building for production (minification)
* webpack --watch – for continuous incremental building
* webpack -d – including source maps
* webpack --colors – making building output pretty

> 配置快速启动

```
// package.json
{
  // ...
  "scripts": {
    "dev": "webpack --mode development",
    "build": "webpack --mode production",
    "start": "webpack-dev-server --mode development --open"
  },
  // ...
}
```

## 单入口

demo01配置

> webpack.config

```
// webpack.config.js
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  }
};
```

> mian.js入口文件

```
// main.js
document.write('<h1>Hello World</h1>');
```
> index.html,引用bundle

```
<html>
  <body>
    <script type="text/javascript" src="bundle.js"></script>
  </body>
</html>
```

## 多入口

demo02配置
> webpack.config

```
module.exports = {
  entry: {
    bundle1: './main1.js',
    bundle2: './main2.js'
  },
  output: {
    filename: '[name].js'
  }
};
```

> mian.js入口文件

```
// main1.js
document.write('<h1>Hello World</h1>');

// main2.js
document.write('<h2>Hello Webpack</h2>');
```
> index.html,引用bundle

```
<html>
  <body>
    <script src="bundle1.js"></script>
    <script src="bundle2.js"></script>
  </body>
</html>
```

## css loader

> scss依赖

`npm install sass-loader node-sass webpack --save-dev`
`npm install style-loader css-loader --save-dev`

> 配置package.config.js

```
module.exports = {
    entry: './main.js',
    output: {
        filename: 'bundle.js'
    },
    module: {
        rules: [
            {
                test: /\.css$/,
                use: [ 'style-loader', 'css-loader' ]
            },
            {
                test: /\.scss$/,
                use: [{
                    loader: "style-loader" // creates style nodes from JS strings
                }, {
                    loader: "css-loader" // translates CSS into CommonJS
                }, {
                    loader: "sass-loader" // compiles Sass to CSS
                }]
            }
        ],
    },
};
```

## image loader

> 安装依赖

`npm install --save-dev url-loader file-loader `

> 配置webpack.config

```
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  },
  module: {
    rules:[
      {
        test: /\.(png|jpg)$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 8192
            }
          }
        ]
      }
    ]
  }
};
```

## 设置别名

> webpack.config.js


```
module.exports = {
    resolve: {
             extensions: [‘.js‘, ‘.vue‘],
             alias: {
                 ‘@‘: path.resolve(__dirname, ‘src‘),
                 ‘@scss‘: path.resolve(__dirname, ‘src‘, ‘scss‘),
             }
    }
}
```

> 配置了resolve.alias 后，在js中我们可以这样用


```
// 原本这样写
import hongAlert from ‘./../src/scss/icon.scss‘

// 现在可以这样写
import hongAlert from ‘@scss/icon.scss‘
```

> 在scss中需要这样写，注意是~@


```
// 原本这样写
@import ‘./../../../scss/mixin.scss‘;

// 现在可以这样写，注意是~@
@import ‘~@scss/icon.scss‘;
```


