---
title: python知识
date: 2019-9-11 13:14
tags: python
categories: python
---


# 基础

本文是Python的笔记，[教程文档](https://www.liaoxuefeng.com/wiki/1016959663602400)

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
print('''line1
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
'Hello, %s' % 'world'
'Hello, world'
'Hi, %s, you have $%d.' % ('Michael', 1000000)
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
classmates = ['Michael', 'Bob', 'Tracy']
classmates
['Michael', 'Bob', 'Tracy']
```

* 获取数组长度:`len(classmates)`
* 通过索引下标获取值: `classmates[0]`
    * 输出：`'Michael'`
* 指定位置插入：`classmates.insert(1, 'Jack')`
* 在最后插入：`classmates.append('Adam')`
* 在最后删除：`classmates.pop()`
* 删除指定位置 `classmates.pop(1)`
* 取list区间值：`L[star:end]`，取0到3之间的元素不包含end
    * 索引为0时可以省略`L[:3]`取前三个
    * 可以用-数序号，倒数第一个元素的索引是-1，取后十个: `L[-10:]`
    * 前10个数，每两个取一个: `L[:10:2]`
    * 字符串也可以与list类似的取值方式
* 数组反转
    * reverse，`list.reverse()`
    * 切片反转`list[::-1]`

#### 列表生成器


> 生成list

```
list(range(1, 11))
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

> 迭代元素基础上增加


```
[x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

> 迭代元素筛选，仅留下偶数

```
[x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]
```

> 两层循环

```
[m + n for m in 'ABC' for n in 'XYZ']
#['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
```

#### 生成器

* 将迭代器的`[]`更改成`()`生成的将会是迭代器，迭代器保存的数据的规则
* 生成器对象可以通过`next()`函数调用
* 生成器也可以通过`for in`迭代

### tuple(元组)

tuple与list类似，都是但是tuple初始化完成后，不可添加删除

```
classmates = ('Michael', 'Bob', 'Tracy')
```

也可以通过下标`0`、`1`访问tuple内的元素

定义一个元组时,需要增加`,`号，因为()一般也用于计算，为了区分所以要增加`,`

```
a = ('few',)
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
list(range(5))
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
d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
d['Michael']
95
```

* 添加新key-value`d['Adam'] = 67`
* 获取不存在的key会报错`d['shaw']`
* 通过in判断key是否存在`'Thomas' in d`
* `get()`方法判断是否存在
    * 如果key不存在，返回None
    * `d.get('shaw',-1)`，不存在指定返回-1
* 删除指定key`d.pop('Bob')`
* 迭代`dict`的`key`和`value`

```
d = {'x': 'A', 'y': 'B', 'z': 'C' }
for k, v in d.items():
...     print(k, '=', v)
```


## set

set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key

要创建一个set，需要提供一个list作为输入集合：

```
s = set([1, 2, 3])
s
#{1, 2, 3}
```

* 重复的将自动过滤掉
* 通过`add(key)`方法可以添加元素到set中`s.add(4)`
* 通过`remove(key)`方法可以删除元素,s.remove(4)

> set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作：

```
s1 = set([1, 2, 3])
s2 = set([2, 3, 4])
s1 & s2
{2, 3}
s1 | s2
{1, 2, 3, 4}
```


# 函数

通过`help(abs)`查看`abs`函数的帮助信息

* `abs`: 求绝对值的函数
* `max`: 比较数据
* `int`: 可以把其他数据类型转换为整数
* `float`: 转成浮点数
* `str`: 转成字符型
* `bool`: 转成boolean类型
* `hex`: 转成十六进制

通过`lambda`来定义匿名函数
匿名函数`lambda x: x * x`实际上就是：

```
def f(x):
    return x * x
```

## 定义函数

* 通过`def`关键词来声明函数
* 括号内的`x`是相应的参数
* 没有定义return值，默认返回`None`
* 返回的多个值，将会变成tuple
* `python`中函数与变量之间也存在闭包，返回函数通过对外层函数变量的引用也会导致变量闭包，与JavaScript中的闭包非常类似，不过里层变量在使用外层作用域变量时需要使用`nonlocal`对变量进行申明

```
def my_abs(x):
    if x >= 0:
        return x
    else:
        return -x
```


> 定义空函数

使用`pass`语句，若函数、条件判断不使用pass关键词又为空的会将会报错

```
def nop():
    pass
```

## 函数的参数


* 默认情况下不校验参数类型，内置函数会校验参数类型
* 会校验参数个数
* 可以给参数定义默认值
    * 必选参数在前，默认参数在后
    * 提供了默认参数，在调用函数时默认参数不传
    * 默认参数必须指向不变对象！(可变对象对此调用函数后将会导致值更改值被缓存下来了)

> 可变参数，参数传入的数量可以是不定的，通过`*`关键词可以将传入的参数变成元组,可以不传参

```
def calc(*numbers):
    print(numbers)
calc(1,2,3,4)
# 运行输出
calc(1,2,3,4)
(1,2,3,4)

# calc(*numbers) === calc((1,2,3,4))
```

> 可以将list或tuple的元素变成可变参数传进去，相当于数组解构展开

```
nums = [1, 2, 3]
calc(*nums)
(1,2,3)

# calc(*nums) === calc(1,2,3)
```

> 关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict

```
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
person('Bob', 35, city='Beijing',job='Engineer')
('name:', 'Bob', 'age:', 35, 'other:', {'city': 'Beijing', 'job': 'Engineer'})
```

简化的写法

```
extra = {'city': 'Beijing', 'job': 'Engineer'}
person('Jack', 24, **extra)
name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
```

> 命名关键字参数必须传入参数名


```
def person(name, age, *, city='Beijing', job):
    print(name, age, city, job)
person('Jack', 24, job='Engineer')
Jack 24 Beijing Engineer
```

### 函数式编程

> map

* `map`接收两个参数，第一个是`Iterable`的函数，第二个是需要迭代的list、或set数据
    * `Iterable`迭代的参数将会接收到两个参数：第一个参数是前一个，第二个参数是后一个
    * map返回的是一个新的list
* list所有元素*10

```
def f(x):
    return x * x
r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
list(r)
```

> reduce

reduce把结果继续和序列的下一个元素做累积计算，其效果就是:

```
reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
```

例如序列求和:

```
from functools import reduce
def add(x, y):
    return x + y

reduce(add, [1, 3, 5, 7, 9])
```

> filter

`filter()`函数用于过滤序列,和`map()`类似，`filter()`也接收一个函数和一个序列。和`map()`不同的是，`filter()`把传入的函数依次作用于每个元素，然后根据返回值是`True`还是`False`决定保留还是丢弃该元素。

例如删掉偶数，只保留奇数：

```
def is_odd(n):
    return n % 2 == 1

list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
# 结果: [1, 5, 9, 15]
```
> sorted

排序也是在程序中经常用到的算法。无论使用冒泡排序还是快速排序，排序的核心是比较两个元素的大小。如果是数字，我们可以直接比较，但如果是字符串或者两个dict呢？直接比较数学上的大小是没有意义的，因此，比较的过程必须通过函数抽象出来。

* `sorted()`函数也是一个高阶函数，
    * 还可以接收一个key函数来实现自定义的排序，例如: 
        * 按绝对值大小排序
`sorted([36, 5, -12, 9, -21], key=abs)`
* 默认情况下，对字符串排序，是按照ASCII的大小比较的
* 忽略大小写
    * `sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower)`
* 反向排序，传入`reverse=True`

### 装饰器

> 假设我们要增强一个函数的功能，比如，在函数调用前后自动打印日志，但又不希望修改这个函数的定义，这种在代码运行期间动态增加功能的方式，称之为“装饰器”（`Decorator`）

decorator就是一个返回函数的高阶函数。所以，我们要定义一个能打印日志的decorator，可以定义如下：

```
def log(func):
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper
```

> 使用装饰器

```
@log
def now():
    print('2015-3-25')
```

把@log放到now()函数的定义处，相当于执行了语句：

```
now = log(now)
```

* 函数拥有`__name__`属性，通过这个属性可以查看到函数的名称

> decorator本身需要传入参数，那就需要编写一个返回decorator的高阶函数

```
def log(text):
    def decorator(func):
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator
```

decorator用法如下：

```
@log('execute')
def now():
    print('2015-3-25')
```

携带参数的装饰器是这样的:

```
now = log('execute')(now)
```

但是通过自定义装饰器的包装，`__name__`属性的值已经变成了`wrapper`,Python内置的`functools.wraps`就是用来解决这个问题的。

参数的decorator:

```
import functools

def log(text):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kw):
            tprint('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator
```
### 偏函数

偏函数在Python中的定义是：把一个函数的某些参数给固定住（也就是设置默认值），返回一个新的函数，调用这个新函数会更简单

可以通过`functools.partial`创建偏函数

```
int2 = functools.partial(int, base=2)
```

## 迭代


在Python中，迭代是通过`for ... in`来完成的

```
d = {'a': 1, 'b': 2, 'c': 3}
```

> 迭代dict

`dict`迭代的是`key`。如果要迭代`value`，可以用`for value in d.values()`，如果要同时迭代`key`和`value`，可以用`for k, v in d.items()`。

> 判断对象是否是可迭代项目

```
from collections import Iterable
isinstance('abc', Iterable) # str是否可迭代
True
```

## 模块

模块内容组成，以下面代码为例:


```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

' a test module '

__author__ = 'Michael Liao'

import sys

def test():
    print('hello!')

if __name__=='__main__':
    test()
```

* 第1行注释可以让这个`*.py`文件直接在`Unix/Linux/Mac`上运行
* 第2行注释表示`.py`文件本身使用标准UTF-8编码
* 第4行是一个字符串，表示模块的文档注释，任何模块代码的第一个字符串都被视为模块的文档注释
* 第6行使用`__author__`变量把作者写进去

> 导入模块


```
import sys
```

导入`sys`模块后，我们就有了变量`sys`指向该模块，利用`sys`这个变量，就可以访问`sys`模块的所有功能


* `sys`模块有一个`argv`变量，用`list`存储了命令行的所有参数
    * 运行`python3 hello.py Michael`获得的`sys.argv`就是`['hello.py', 'Michael]`


### 作用域

模块内的私有变量和函数我们通过`_`来实现，类似`_xxx`和`__xxx`这样的函数或变量就是非公开的（`private`），不应该被直接引用，比如`_abc`，`__abc`等

private函数和变量“不应该”被直接引用，而不是“不能”被直接引用，是因为Python并没有一种方法可以完全限制访问private函数或变量，但是，从编程习惯上不应该引用private函数或变量。

### 安装python包

一般来说，第三方库都会在Python官方的pypi.python.org网站注册，要安装一个第三方库，必须先知道该库的名称，可以在官网或者pypi上搜索，比如Pillow的名称叫Pillow，因此，安装Pillow的命令就是：

```
pip install Pillow
```

> 模块搜索路径

当我们试图加载一个模块时，Python会在指定的路径下搜索对应的.py文件，如果找不到，就会报错

默认情况下，Python解释器会搜索当前目录、所有已安装的内置模块和第三方模块，搜索路径存放在sys模块的path变量中:


```
import sys
sys.path
['', '/Library/Frameworks/Python.framework/Versions/3.6/lib/python36.zip', '/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6', ..., '/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages']
```

> 添加自己的搜索目录

```
import sys
sys.path.append('/Users/michael/my_py_scripts')
```


## 安装版本

> 问题

如电脑上同时装了python2(2.7)和python3(3.5)，当使用pip安装时默认应安装到python2中，pip3安装时应安装到python3中，但奇怪的是使用pip安装时每次都定位到python3中，不知是啥原因，也不知如何将其重定向到python2中，索性手动指定pip到python2中

> 查看pip版本

pip -V pip 18.0 from /usr/local/lib/python3.5/dist-packages/pip (python 3.5)
pip2 -V pip 8.1.1 from /usr/lib/python2.7/dist-packages (python 2.7)
pip3 -V pip 18.0 from /usr/local/lib/python3.5/dist-packages/pip (python 3.5)

> pip指定python版本安装

安装到python2.7版本中：sudo pip2 install 模块名 或 python2 -m pip install 模块名
安装到python3.5版本中：sudo pip3 install 模块名 或 python3 -m pip install 模块名

