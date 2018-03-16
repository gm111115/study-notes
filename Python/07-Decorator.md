# Decorator

## 本质

装饰器的本质——一个闭包函数

## 功能

装饰器的功能——在不修改原函数本身及其调用方式的前提下在函数前后添加功能

## 形成

```
#装饰器简单版

import time

def func1():
    print('in func1')

def timer(func):
    def inner():
        start = time.time()
        func()
        print(time.time() - start)
    return inner

func1 = timer(func1)
func1()
```

为了省略上面那一次赋值调用，python为我们提供了一句语法糖来解决这个问题

```
#装饰器————语法糖

import time
def timer(func):
    def inner():
        start = time.time()
        func()
        print(time.time() - start)
    return inner

@timer   #==> func1 = timer(func1)
def func1():
    print('in func1')


func1()
```

```
#带参数的装饰器

def timer(func):
    def inner(a):
        start = time.time()
        func(a)
        print(time.time() - start)
    return inner

@timer
def func1(a):
    print(a)

func1(1)
```

```
#hold所有函数传参

import time
def timer(func):
    def inner(*args,**kwargs):
        start = time.time()
        re = func(*args,**kwargs)
        print(time.time() - start)
        return re
    return inner

@timer   #==> func1 = timer(func1)
def func1(a,b):
    print('in func1')

@timer   #==> func2 = timer(func2)
def func2(a):
    print('in func2 and get a:%s'%(a))
    return 'fun2 over'

func1('aaaaaa','bbbbbb')
print(func2('aaaaaa'))
```

```
#带返回值的装饰器

import time
def timer(func):
    def inner(*args,**kwargs):
        start = time.time()
        re = func(*args,**kwargs)
        print(time.time() - start)
        return re
    return inner

@timer   #==> func2 = timer(func2)
def func2(a):
    print('in func2 and get a:%s'%(a))
    return 'fun2 over'

func2('aaaaaa','bbbbbb')
print(func2('aaaaaa'))
```

```
#多个装饰器装饰同一个函数

def wrapper1(func):
    def inner():
        print('wrapper1 ,before func')
        func()
        print('wrapper1 ,after func')
    return inner

def wrapper2(func):
    def inner():
        print('wrapper2 ,before func')
        func()
        print('wrapper2 ,after func')
    return inner

@wrapper2
@wrapper1
def f():
    print('in f')

f()
```

正常情况下一些查看函数信息的方法都会在装饰器这里失效

```
#查看函数信息

def index():
    '''这是一个主页信息'''
    print('from index')

print(index.__doc__)    #查看函数注释的方法
print(index.__name__)   #查看函数名的方法
```

为了不让它们失效，需要在装饰器上加上一点来完善

```
#装饰器————wraps

from functools import wraps

def deco(func):
    @wraps(func) #加在最内层函数正上方
    def wrapper(*args,**kwargs):
        return func(*args,**kwargs)
    return wrapper

@deco
def index():
    '''哈哈哈哈'''
    print('from index')

print(index.__doc__)
print(index.__name__)
```

## 开放封闭原则

​	**对扩展是开放的**

​	任何一个程序，不可能在设计之初就已经想好了所有的功能并且在未来不做任何关心和修改，所以必须允许代码扩展、添加新功能

​	**对修改是封闭的**

​	我们所写的程序都是要交给用户使用的，如果我们随意对其进行修改，很有可能影响已经在使用程序的用户

​	**装饰器完美的遵循了开放封闭原则**