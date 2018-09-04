##csp

> 简介


```
CSP是网页安全政策(Content Security Policy)的缩写。是一种由开发者定义的安全性政策申明，通过CSP所约束的责任指定可信的内容来源，（内容可以是指脚本、图片、style 等远程资源）。通过CSP协定，可以防止XSS攻击，让web处一个安全运行的环境中。
       CSP 的实质就是白名单制度，开发者明确告诉客户端，哪些外部资源可以加载和执行，等同于提供白名单。它的实现和执行全部由浏览器完成，开发者只需提供配置。CSP 大大增强了网页的安全性。攻击者即使发现了漏洞，也没法注入脚本，除非还控制了一台列入了白名单的可信主机。
```


> 开启方式

　　一种是：通过 HTTP 头信息的Content-Security-Policy的字段。
　　一种是：在网页中设置<meta>标签，如：


```

 <meta http-equiv= <meta http-equiv=""Content-Security-PolicyContent-Security-Policy" content="script-src 'self'; object-src 'none'; style-src cdn.example.org third-party.org; child-src https:">
```

> 栗子


```
<script type="text/javascript" src="https://code.jquery.com/jquery-3.2.1.min.js"></script>　　
```

> script-src 的特殊值


```
'unsafe-inline'：允许执行页面内嵌的<script>标签和事件监听函数
'unsafe-eval'：允许将字符串当作代码执行，比如使用eval、setTimeout、setInterval等函数。
'nonce'值：每次HTTP回应给出一个授权token，页面内嵌脚本必须有这个token，才会执行
'hash'值：列出允许执行的脚本代码的Hash值，页面内嵌脚本的哈希值只有吻合的情况下，才能执行
```

