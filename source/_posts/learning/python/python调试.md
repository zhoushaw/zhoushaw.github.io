---
title: python错误、调试和测试
date: 2019-9-18 4:14
tags: python
categories: python
---



## 错误处理

Python通过`try...except...finally...`的错误处理机制

[错误原因表](https://www.runoob.com/python/python-exceptions.html)

```
try:
    正常的操作
   ......................
except:
    发生异常，执行这块代码
   ......................
else:
    如果没有异常执行这块代码
```

> 检测所有异常


```
import traceback

try:
　　1/0
except Exception as e:
　　print(e) # 错误原因
　　traceback.print_exc() # 错误的具体行数
```

> 捕获指定错误


```
try:
    正常的操作
   ......................
except(Exception1[, Exception2[,...ExceptionN]]]):
   发生以上多个异常中的一个，执行这块代码
   ......................
else:
    如果没有异常执行这块代码
```

例如捕获用户退出操作：

```
try:
    s=input()
except (KeyboardInterrupt):
    print('用户中断输入')
```

> 不捕获原因


```
try:
    n=10/0
except:
    # print(e)
    traceback.print_exc()
```

## 调试



> print

通过打印内容来进行调试

```
print('>>> n = %d' % n)
```

* 缺点
    * 运行时含有大量垃圾信息
    * 还得删除

> 断言

格式：`assert expression [, arguments]`

```
assert n != 0, 'n is zero!'
```

断言`n`是0，如果是会报错

```
n = 0 
assert n != 0, 'n is zero!'
#AssertionError: n is zero!
```

运行时携带`-O`不报错


> logging

`logging`输入日志形式，可以输出到文件


-------
对应的log类型和权重


* NOTSET（0）
* DEBUG（10）
* INFO（20）
* WARNING（30）
* ERROR（40）


使用：


```
import logging

logging.basicConfig(filename="test.log", filemode="w", format="%(asctime)s %(name)s:%(levelname)s:%(message)s", datefmt="%d-%M-%Y %H:%M:%S", level=logging.DEBUG)

logging.debug('This is a debug message')
logging.info('This is an info message')
logging.warning('This is a warning message')
logging.error('This is an error message')
logging.critical('This is a critical message')
```

basicConfig函数接收参数：

* filename: 日志保存的文件名
* filemode：文件模式
* format: 日志格式
    * [formatter参数格式](https://docs.python.org/3.7/library/logging.html#logrecord-attributes)


## 单元测试

在Python中我们可以通过`unittest`模块来编写单元测试，我们将自身的类继承了`unittest.TestCase`后，将会自动运行类中带有`test_`开头的函数


```
import unittest
class Dict(dict):

    def __init__(self, **kw):
        super().__init__(**kw)

    def __getattr__(self, key):
        try:
            return self[key]
        except KeyError:
            raise AttributeError(r"'Dict' object has no attribute '%s'" % key)

    def __setattr__(self, key, value):
        self[key] = value
        
class TestDict(unittest.TestCase):

    def test_init(self):
        d = Dict(a=1, b='test')
        self.assertEqual(d.a, 1)
        self.assertEqual(d.b, 'test')
        self.assertTrue(isinstance(d, dict))

    def test_key(self):
        d = Dict()
        d['key'] = 'value'
        self.assertEqual(d.key, 'value')
```

通过继承类上面的`assertEqual`方法进行断言判断

> 如何运行单元测试

* 在最后加上两行代码
    
```
if __name__ == '__main__':
    unittest.main()
```

* 在命令行通过参数`-m unittest`直接运行单元测试：

```
python -m unittest mydict_test
```


## 文档测试

通过编写文档的形式，指定函数调用，并确定函数的输入和输出值

```
def abs(n):
    '''
    Function to get absolute value of number.
    
    Example:
    
    >>> abs(1)
    1
    >>> abs(-1)
    1
    >>> abs(0)
    0
    '''
    return n if n >= 0 else (-n)
```

Python内置的“文档测试”（doctest）模块可以直接提取注释中的代码并执行测试。

doctest严格按照Python交互式命令行的输入和输出来判断测试结果是否正确。只有测试异常的时候，可以用...表示中间一大段烦人的输出。

