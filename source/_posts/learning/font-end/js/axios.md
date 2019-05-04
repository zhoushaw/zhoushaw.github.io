---
title: axios设计
date: 2019-04-28 8:45:35
categories: js
tags: js
---


## 项目初始化

[axios-ts项目地址](https://github.com/zhoushaw/axios)

使用现有的`ts脚手架`: **typescript-library-starter**

```
git clone https://github.com/alexjoverm/typescript-library-starter.git ts-axios
cd ts-axios

npm install
```


## 优秀工具集成

`typescript-library-starter`中集成了一个完整包开发的插件包

- [RollupJS](https://rollupjs.org/) 帮助我们打包。
- [Prettier](https://github.com/prettier/prettier) 和 [TSLint](https://palantir.github.io/tslint/) 帮助我们格式化代码以及保证代码风格一致性。
- [TypeDoc](https://typedoc.org/) 帮助我们自动生成文档并部署到 GitHub pages。
- [Jest](https://jestjs.io/)帮助我们做单元测试。
- [Commitizen](https://github.com/commitizen/cz-cli)帮助我们生成规范化的提交注释。
- [Semantic release](https://github.com/semantic-release/semantic-release)帮助我们管理版本和发布。
- [husky](https://github.com/typicode/husky)帮助我们更简单地使用 git hooks。
- [Conventional changelog](https://github.com/conventional-changelog/conventional-changelog)帮助我们通过代码提交信息自动生成 change log。




