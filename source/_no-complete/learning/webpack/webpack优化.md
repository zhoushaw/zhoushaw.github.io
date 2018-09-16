## 体积优化

插件：
`yarn install webpack-bundle-analyzer --save-dev`


webpack.prod.conf.js配置:


```
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;

module.exports = {

  plugins: [

    new BundleAnalyzerPlugin()

  ]

}

```

启动：
在package.json中的script上添加
`“analyz”: “NODE_ENV=production npm_config_report=true npm run build”`


使用npm run analyz

## 检测打包时间

在package.json内加入--profile，它会告诉你编译过程中哪些步骤耗时最长。

