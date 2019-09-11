---
title: python基础
date: 2019-9-11 13:14
tags: ptyhon
categories: python
---


# 基础
## 输入

```
name = input('please enter your name: ')
print('hello,', name)
```

命令行展示:

```
C:\Workspace> python hello.py
please enter your name: Michael
hello, Michael
```
## 数据类型

* 整型
* 浮点型
* 字符串
* 布尔值
* 空值

`int()`函数可以将字符类型的数字转成int型

> 字符串

`某些特殊字符进行“转义”，Python 字符串用 \ 进行转义`

```
\n 表示换行
\t 表示一个制表符
\\ 表示 \ 字符本身
```

* 对特殊字符串进行转义，使用\，对多个特殊字符进行转换是使用r'特殊字符'
* 多行'''.....''',类似js``模板字符串

```
>>> print('''line1
... line2
... line3''')
line1
line2
line3
```

**读取中文**

```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```
由于 Python 源代码也是一个文本文件，所以，当你的源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为 UTF-8 编码。当Python 解释器读取源代码时，为了让它按 UTF-8 编码读取

> 布尔型



* 布尔值可以用 and、or 和 not 运算。
* and 运算是与运算，只有所有都为 True，and 运算结果才是 True。
* or 运算是或运算，只要其中有一个为 True，or 运算结果就是 True。
* not 运算是非运算，它是一个单目运算符，把 True 变成 False，False 变成 True。

## 编码

ASCII：不包含中文
Unicode：国际标准编码
UTF-8：对Unicode进行了优化

```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```

* 第一行注释是为了告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释；
* 第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。


## 字符串拼接

```
>>> 'Hello, %s' % 'world'
'Hello, world'
>>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
'Hi, Michael, you have $1000000.'
```

| 占位符 | 替换内容 |
| --- | --- |
| %d | 整数 |
| %f | 浮点数 |
| %s | 字符串 |
| %x | 十六进制整数 |

## 数组

### list

Python内置的一种数据类型是列表：list。list是一种有序的集合，可以随时添加和删除其中的元素。

```
>>> classmates = ['Michael', 'Bob', 'Tracy']
>>> classmates
['Michael', 'Bob', 'Tracy']
```

* 获取数组长度:`len(classmates)`
* 通过索引下标获取值: `classmates[0]`
    * 输出：`'Michael'`
* 指定位置插入：`classmates.insert(1, 'Jack')`
* 在最后插入：`classmates.append('Adam')`
* 在最后删除：`classmates.pop()`
* 删除指定位置 `classmates.pop(1)`



### tuple(元组)

tuple与list类似，都是但是tuple初始化完成后，不可添加删除

```
>>> classmates = ('Michael', 'Bob', 'Tracy')
```

也可以通过下标`0`、`1`访问tuple内的元素

定义一个元组时,需要增加`,`号，因为()一般也用于计算，为了区分所以要增加`,`

```
>>> a = ('few',)
```


## 条件判断

```
age = 3
if age >= 18:
    print('adult')
elif age >= 6:
    print('teenager')
else:
    print('kid')
```

or

```
if <条件判断1>:
    <执行1>
elif <条件判断2>:
    <执行2>
elif <条件判断3>:
    <执行3>
else:
    <执行4>
```

if判断条件还可以简写，比如写：

```
if x:
    print('True')
```

只要x是非零数值、非空字符串、非空list等，就判断为True，否则为False


## 循环

> 循环数组

```
names = ['Michael', 'Bob', 'Tracy']
for name in names:
    print(name)
```

输出结果：

```
Michael
Bob
Tracy
```


for in 就是按顺序迭代

`range()`函数可以生成一个整数序列，再通过list()函数可以转换为list

```
>>> list(range(5))
[0, 1, 2, 3, 4]
```

> while循环

输出1+2+...+10结果

```
sum = 0
n = 10
while n > 0:
    sum = sum + n
    n = n - 1
print(sum)
```

提前终止

```
sum = 0
n = 10
while n > 0:
    if n<5:
        break
    sum = sum + n
    n = n - 1
print(sum)
```

continue，跳过当前循环，执行下一循环，例：不加偶数

```
sum = 0
n = 10
while n > 0:
    n = n - 1
    if n%2==0:
        continue
    sum = sum + n
print(sum)
```

## 字典dict

dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储

dict的key必须是不可以变的所以，key不可以是list或另一个dict，字符、整数这些就是不可变的

```
>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> d['Michael']
95
```

* 添加新key-value`d['Adam'] = 67`
* 获取不存在的key会报错`d['shaw']`
* 通过in判断key是否存在`'Thomas' in d`
* `get()`方法判断是否存在
    * 如果key不存在，返回None
    * `d.get('shaw',-1)`，不存在指定返回-1
* 删除指定key`d.pop('Bob')`


## set

set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key

要创建一个set，需要提供一个list作为输入集合：

```
>>> s = set([1, 2, 3])
>>> s
{1, 2, 3}
```

* 重复的将自动过滤掉
* 通过add(key)方法可以添加元素到set中`s.add(4)`


