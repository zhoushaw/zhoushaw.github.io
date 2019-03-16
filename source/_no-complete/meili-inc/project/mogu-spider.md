## 接口文档

queryChannel：


params: 

* channel 
* url

查询渠道，查询url






```
interface NightMareChannel {
    'taobao': String,
    'taobao-intl': String,
    'taobao-old': String,
    'wconcept': String,
    'farfetch': String,
    'shopbop': String,
    'netAPorter': String
}
let CheckResult: NightMareChannel = {
        'taobao': '校验通过',
        'taobao-intl': '校验通过',
        'taobao-old': '校验通过',
        'wconcept': '校验通过',
        'farfetch': '校验通过',
        'shopbop': '校验通过',
        'netAPorter': '校验通过'
}

let fn = (channel: ??) => {
    CheckResult[channel] = '未通过'
}
```


