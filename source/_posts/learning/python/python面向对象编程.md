---
title: python面向对象编程
date: 2019-9-18 10:28
tags: python
categories: python
---


# 面向对象编程

## 类和实例

> 定义类

以Student类为例，在Python中，定义类是通过`class`关键字：

```
class Student(object):
    pass
```

class后面紧接着是类名，即Student，类名通常是大写开头的单词，紧接着是(object)，表示该类是从哪个类继承下来的，继承的概念我们后面再讲，通常，如果没有合适的继承类，就使用object类，这是所有类最终都会继承的类(object可省略)

根据类创造实例


```
bart = Student()
bart
```

> 类初始化

在Python中构造函数是`__int__`，第一个参数是`self`自身，后续的参数根据调用类时创建

```
class Student(object):

    def __init__(self, name, score):
        self.name = name
        self.score = score
```

实例的变量名如果以__开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问:

```
class Student(object):

    def __init__(self, name, score):
        self.__name = name
        self.__score = score

    def print_score(self):
        print('%s: %s' % (self.__name, self.__score))
```

**在Python中，变量名类似__xxx__的，也就是以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的，不是private变量，所以，不能用__name__、__score__这样的变量名**

## 继承和多态

> 继承

基类：

```
class Animal(object):
    def run(self):
        print('Animal is running...')
```

当我们需要编写Dog和Cat类时，就可以直接从Animal类继承：

```
class Dog(Animal):
    pass
dog = Dog()
dog.run()
```

> 多态

可以在子类上覆盖父类的方法

```
class Dog(Animal):
    def run(self):
        print('Dog is running...')
```

> 判断变量类型

判断一个变量是否是某个类型可以用isinstance()判断：

```
isinstance(a, list)
True
isinstance(b, Animal)
True
isinstance(c, Dog)
True
```

但是通过`isinstance`，检测出来的结果不仅仅包含父类还包含超类(父类的基类)

```
c = Dog()
isinstance(c, Animal)
True
```

## 获取对象信息

> type()

我们来判断对象类型，使用type()函数：

```
type(123)
#<class 'int'>

type('str')
#<class 'str'>

type(None)
#<type(None) 'NoneType'>
```

判断对象类型


```
type(123)==int
True
type('abc')==str
True

import types
def fn():
    pass

type(fn)==types.FunctionType
True
```

> dir()

`dir()`函数会返回对象上所有的属性和方法

```
dir('ABC')
['__add__', '__class__',..., '__subclasshook__', 'capitalize', 'casefold',..., 'zfill']
```

> getattr()、setattr()以及hasattr()，我们可以直接操作一个对象的状态


```
hasattr(obj, 'x') # 有属性'x'吗？
setattr(obj, 'y', 19) # 设置一个属性'y'
getattr(obj, 'y') # 获取属性'y'
```

## 类属性

可通过简单的声明生成类属性，当实例属性与类属性名称相同时，将会获取实例属性的值

```
class Student(object):
    name = 'Student'
    
    def __init__(self):
        pass
        self.name = 'shaw'
        
d = Student()
print(d.name) # shaw
```

只有当实例中不存在属性时返回类属性

```
class Student(object):
    name = 'Student'
d = Student()
print(d.name) # Student
```

### `__slots__`


> 限制类添加属性范围


```
class Student():
    __slots__ = ('age')
stud1 = Student()
stud1.name = 'shaw'
```

限制了`Student`类只能添加`age`属性，若添加其他属性将会报错，上述例子运行时将会报错

**使用__slots__要注意，__slots__定义的属性仅对当前类实例起作用，对继承的子类是不起作用的。除非子类添加与父类一样的__slots__**

###@property

拦截类属性的`setter`和`getter`操作

定义一个学生类，对学生类的`score`属性的读写进行校验：

```
class Student(object):

    @property
    def score(self):
        return self._score

    @score.setter
    def score(self, value):
        if not isinstance(value, int):
            raise ValueError('score must be an integer!')
        if value < 0 or value > 100:
            raise ValueError('score must between 0 ~ 100!')
        self._score = value
```

若只定义`getter`不定义`setter`时，
该类只有读操作，无法进行写入

## 多重继承

Python可以同时继承多个类


```
class Mammal()
    pass
class RunnableMixIn()
    pass
class Dog(Mammal, RunnableMixIn):
    pass
```

## 定制类

可以通过给类添加一些特殊属性来完善类的功能

### `__str__`

我们队类进行`print`打印时，打印出来的并不能让你了解类的属性和方法的细节，我们可以通过`__str__`方法来处理打印后的展示的情况，例如下面`Student`打印实例


```
class Student(object):
    def __init__(self, name):
        self.name = name

print(Student('Michael'))
#<__main__.Student object at 0x109afb190>
```

从上面的例子可以看到，无法通过过打印类来了解类具体的细节。我们可以通过`__str__`来定义类`str`化时，展示的内容

> 定义str化后的内容

```
class Student(object):
    def __init__(self, name):
        self.name = name
    def __str__(self):
        return 'Student object (name: %s)' % self.name
    __repr__ = __str__

print(Student('Michael'))
#Student object (name: Michael)
```

### `__iter__`


如果类需要被迭代可以通过`__iter__`和`__next__()`，iter是用来返回迭代对象，next是用来计算下一个迭代值的


```
class Fib(object):
    def __init__(self):
        self.a, self.b = 0, 1 # 初始化两个计数器a，b

    def __iter__(self):
        return self # 实例本身就是迭代对象，故返回自己

    def __next__(self):
        self.a, self.b = self.b, self.a + self.b # 计算下一个值
        if self.a > 100000: # 退出循环的条件
            raise StopIteration()
        return self.a # 返回下一个值
```


### `__getitem__`

定义使用下标访问类时，定义返回的值

```
class Fib(object):
    def __getitem__(self, n):
        a, b = 1, 1
        for x in range(n):
            a, b = b, a + b
        return a
# f = Fib()
# f[0]
#1
```

### `__getattr__`


当访问不存在属性、或者方法时可以通过在`__getattr__`中定义返回内容


```
class Student(object):
    def __init__(self):
        self.name = 'Michael'
    def __getattr__(self, attr):
        if attr=='age':
            return 22
# st = Student()
# st.age 
# 22
```

可以用在动态接口的情况下，做一些异常处理

### `__call__`

定义实例被调用时执行的内容


```
class Student(object):
    def __init__(self, name):
        self.name = name

    def __call__(self):
        print('My name is %s.' % self.name)

s = Student('Michael')
s() # self参数不要传入
# My name is Michael.
```

通过`callable()`函数，我们就可以判断一个对象是否是“可调用”对象。

## 枚举类

在Python中可以将类做成枚举类，可以更形象的使用枚举


```
from enum import Enum, unique

@unique # 用于检测是否有重复
class Weekday(Enum): # 继承枚举类
    Sun = 0 # Sun的value被设定为0
    Mon = 1
    Tue = 2
    Wed = 3
    Thu = 4
    Fri = 5
    Sat = 6

# day1 = Weekday.Mon
```

