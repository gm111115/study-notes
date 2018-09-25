# Object-Oriented Advanced

## isinstance和issubclass:jack_o_lantern:

isinstance(obj,cls)检查obj是否是cls的对象

```
class Foo(object):
     pass
   
obj = Foo()
   
isinstance(obj, Foo)
```

issubclass(sub,super)检查sub类是否是super类的派生类

```
class Foo(object):
    pass
  
class Bar(Foo):
    pass
  
issubclass(Bar, Foo)
```

## 反射:jack_o_lantern:

**什么是反射  **

反射的概念是由Smith在1982年首次提出的，主要是指程序可以访问、检测和修改它本身状态或行为的一种能力（自省）这一概念的提出很快引发了计算机科学领域关于应用反射性的研究，它首先被程序语言的设计领域所采用，并在Lisp和面向对象方面取得了成绩

**python面向对象中的反射：通过字符串的形式操作对象相关的属性，python中一切事物都是对象（都可以使用反射）**

四个可以实现自省的函数，适用于类和对象（python一切皆对象，类本身也是一个对象）

```
#hasattr

def hasattr(*args, **kwargs): # real signature unknown
    """
    Return whether the object has an attribute with the given name.
    
    This is done by calling getattr(obj, name) and catching AttributeError.
    """
    pass
```

```
#getattr

def getattr(object, name, default=None): # known special case of getattr
    """
    getattr(object, name[, default]) -> value
    
    Get a named attribute from an object; getattr(x, 'y') is equivalent to x.y.
    When a default argument is given, it is returned when the attribute doesn't
    exist; without it, an exception is raised in that case.
    """
    pass
```

```
#setattr

def setattr(x, y, v): # real signature unknown; restored from __doc__
    """
    Sets the named attribute on the given object to the specified value.
    
    setattr(x, 'y', v) is equivalent to ``x.y = v''
    """
    pass
```

```
#delattr

def delattr(x, y): # real signature unknown; restored from __doc__
    """
    Deletes the named attribute from the given object.
    
    delattr(x, 'y') is equivalent to ``del x.y''
    """
    pass
```

```
#四个方法的使用

class Foo:
    f = '类的静态变量'
    def __init__(self,name,age):
        self.name=name
        self.age=age

    def say_hi(self):
        print('hi,%s'%self.name)

obj=Foo('egon',73)

#检测是否含有某属性
print(hasattr(obj,'name'))
print(hasattr(obj,'say_hi'))

#获取属性
n=getattr(obj,'name')
print(n)
func=getattr(obj,'say_hi')
func()

print(getattr(obj,'aaaaaaaa','不存在啊')) #报错

#设置属性
setattr(obj,'sb',True)
setattr(obj,'show_name',lambda self:self.name+'sb')
print(obj.__dict__)
print(obj.show_name(obj))

#删除属性
delattr(obj,'age')
delattr(obj,'show_name')
delattr(obj,'show_name111')#不存在,则报错

print(obj.__dict__)
```

```
#类本身也是一个对象

class Foo(object):
 
    staticField = "old boy"
 
    def __init__(self):
        self.name = 'wupeiqi'
 
    def func(self):
        return 'func'
 
    @staticmethod
    def bar():
        return 'bar'
 
print getattr(Foo, 'staticField')
print getattr(Foo, 'func')
print getattr(Foo, 'bar')
```

```
#反射当前模块成员

import sys

def s1():
    print 's1'

def s2():
    print 's2'


this_module = sys.modules[__name__]

hasattr(this_module, 's1')
getattr(this_module, 's2')
```

导入其他模块，利用反射查找该模块是否存在某个方法

```
def test():
    print('from the test')
```

```
"""
程序目录：
    module_test.py
    index.py
 
当前文件：
    index.py
"""

import module_test as obj

#obj.test()

print(hasattr(obj,'test'))
getattr(obj,'test')()
```

## __str__和__repr__:jack_o_lantern:

改变对象的字符串显示__str__，__repr__

自定制格式化字符串__format__

```
format_dict={
    'nat':'{obj.name}-{obj.addr}-{obj.type}',#学校名-学校地址-学校类型
    'tna':'{obj.type}:{obj.name}:{obj.addr}',#学校类型:学校名:学校地址
    'tan':'{obj.type}/{obj.addr}/{obj.name}',#学校类型/学校地址/学校名
}
class School:
    def __init__(self,name,addr,type):
        self.name=name
        self.addr=addr
        self.type=type

    def __repr__(self):
        return 'School(%s,%s)' %(self.name,self.addr)
    def __str__(self):
        return '(%s,%s)' %(self.name,self.addr)

    def __format__(self, format_spec):
        # if format_spec
        if not format_spec or format_spec not in format_dict:
            format_spec='nat'
        fmt=format_dict[format_spec]
        return fmt.format(obj=self)

s1=School('oldboy1','北京','私立')
print('from repr: ',repr(s1))
print('from str: ',str(s1))
print(s1)

'''
str函数或者print函数--->obj.__str__()
repr或者交互式解释器--->obj.__repr__()
如果__str__没有被定义,那么就会使用__repr__来代替输出
注意:这俩方法的返回值必须是字符串,否则抛出异常
'''
print(format(s1,'nat'))
print(format(s1,'tna'))
print(format(s1,'tan'))
print(format(s1,'asfdasdffd'))
```

```
#%s和%r

class B:

     def __str__(self):
         return 'str : class B'

     def __repr__(self):
         return 'repr : class B'


b=B()
print('%s'%b)
print('%r'%b)
```

## __del__:jack_o_lantern:

析构方法，当对象在内存中被释放时，自动触发执行

析构方法无需定义，python是一门高级语言，程序员在使用时无需关心内存的分配和释放，因为此工作都是交给python解释器来执行，析构函数的调用时由解释器在进行垃圾回收是自动触发执行的

```
# class A:
#     def __del__(self):   # 析构函数: 在删除一个对象之前进行一些收尾工作
#         self.f.close()
# a = A()
# a.f = open()   # 打开文件 第一 在操作系统中打开了一个文件 拿到了文件操作符存在了内存中
                        # a.f 拿到了文件操作符消失在了内存中
# del a   # del 既执行了这个方法，又删除了变量
```

## item系列:jack_o_lantern:

__getitem__\__setitem__\__delitem__

```
class Foo:
    def __init__(self,name):
        self.name=name

    def __getitem__(self, item):
        print(self.__dict__[item])

    def __setitem__(self, key, value):
        self.__dict__[key]=value
    def __delitem__(self, key):
        print('del obj[key]时,我执行')
        self.__dict__.pop(key)
    def __delattr__(self, item):
        print('del obj.key时,我执行')
        self.__dict__.pop(item)

f1=Foo('sb')
f1['age']=18
f1['age1']=19
del f1.age1
del f1['age']
f1['name']='alex'
print(f1.__dict__)
```

## __new__:jack_o_lantern:

构造方法：创建一个对象

```
class A:
    def __init__(self):
        self.x = 1
        print('in init function')
    def __new__(cls, *args, **kwargs):
        print('in new function')
        return object.__new__(A, *args, **kwargs)

# a1 = A()
# a2 = A()
# a3 = A()
# print(a1)
# print(a2)
# print(a3)
# print(a.x)
```

```
class A:
    def __init__(self):
        self.x = 1
        print('in init function')
    def __new__(cls, *args, **kwargs):
        print('in new function')
        return object.__new__(A, *args, **kwargs)

a = A()
print(a.x)
```

```
#单例模式

class Singleton:
    def __new__(cls, *args, **kw):
        if not hasattr(cls, '_instance'):
            cls._instance = object.__new__(cls, *args, **kw)
        return cls._instance

one = Singleton()
two = Singleton()

two.a = 3
print(one.a)
# 3
# one和two完全相同,可以用id(), ==, is检测
print(id(one))
# 29097904
print(id(two))
# 29097904
print(one == two)
# True
print(one is two)
```

## __call__:jack_o_lantern:

对象后面加括号，触发执行

析构方法的执行时由创建对象触发的，即：对象=类名() ，而对于__call__方法的执行时由对象后加括号触发的，即：对象() 或者 类()()

```
class Foo:

    def __init__(self):
        pass
    
    def __call__(self, *args, **kwargs):

        print('__call__')


obj = Foo() # 执行 __init__
obj()       # 执行 __call__
```

```
class A:
    def __init__(self,name):
        self.name = name
    def __call__(self):
        '''
        打印这个对象中的所有属性
        :return:
        '''
        for k in self.__dict__:
            print(k,self.__dict__[k])
a = A('alex')()
```

## __len__:jack_o_lantern:

```
class A:
    def __init__(self):
        self.a = 1
        self.b = 2

    def __len__(self):
        return len(self.__dict__)
a = A()
print(len(a))
```

## __hash__:jack_o_lantern:

```
class A:
    def __init__(self):
        self.a = 1
        self.b = 2

    def __hash__(self):
        return hash(str(self.a)+str(self.b))
a = A()
print(hash(a))
```

## __eq__:jack_o_lantern:

```
class A:
    def __init__(self):
        self.a = 1
        self.b = 2

    def __eq__(self,obj):
        if  self.a == obj.a and self.b == obj.b:
            return True
a = A()
b = A()
print(a == b)
```

```
#Card Games

class FranchDeck:
    ranks = [str(n) for n in range(2,11)] + list('JQKA')
    suits = ['红心','方板','梅花','黑桃']

    def __init__(self):
        self._cards = [Card(rank,suit) for rank in FranchDeck.ranks
                                        for suit in FranchDeck.suits]

    def __len__(self):
        return len(self._cards)

    def __getitem__(self, item):
        return self._cards[item]

deck = FranchDeck()
print(deck[0])
from random import choice
print(choice(deck))
print(choice(deck))
```

```
#Card Games2

class FranchDeck:
    ranks = [str(n) for n in range(2,11)] + list('JQKA')
    suits = ['红心','方板','梅花','黑桃']

    def __init__(self):
        self._cards = [Card(rank,suit) for rank in FranchDeck.ranks
                                        for suit in FranchDeck.suits]

    def __len__(self):
        return len(self._cards)

    def __getitem__(self, item):
        return self._cards[item]

    def __setitem__(self, key, value):
        self._cards[key] = value

deck = FranchDeck()
print(deck[0])
from random import choice
print(choice(deck))
print(choice(deck))

from random import shuffle
shuffle(deck)
print(deck[:5])
```