## 依赖环境配置


> yarn 


```
vim .zshrc
export PATH="$PATH:`yarn global bin`"
```

## npm代理设置

> 起步

`vim ~/.npmrc`

> 切换代理

```
registry=https://registry.npm.taobao.org
//registry=http://npm.f2e.mogujie.org/
//registry=https://registry.npmjs.org/
```

## 端口占用查询

> 查询端口占用

`lsof -i:3000`


> 解除端口占用(PID在查询端口出现)

`sudo kill -9 PID`





