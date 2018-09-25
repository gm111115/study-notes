# Function

## 定义

将代码封装起来

```
#函数定义
def my_len():
    s1='hello world'
    length=0
    for i in s1:
        length=length+1
    print(length)
my_len()  #函数调用
 
# 11
```

​	def关键词开头，空格之后接函数名称和圆括号(),最后还有一个“：”

​	def是固定的，不能变，必须是连续的def三个字母，不能分开

​	空格  为了将def关键字和函数名称分开，必须空

​	函数名：函数名只能包含字符串、下划线和数字且不能以数字开头。虽然函数名可以随便起，但我们给函数起名字还是要尽量简短，并表达函数功能

​	括号：必须要有

## 注释

每一个函数都应该对功能和参数进行相应的说明，应该写在函数下面第一行。以增强代码的可读性

## 调用

函数名()

## 返回值

在调用python自带的len函数时，必须用一个变量来接收这个值

```
str_len=len('hello,word')
```

使用自己写的函数也可以做到这一点

```
# 函数定义
def my_len():
    s1='hello world'
    length=0
    for i in s1:
        length=length+1
    print(length)
str_len=my_len()  #函数调用
print('str_len:%s'%str_len)

# 11
# str_len:None  说明这段代码什么都没有返回
```

​	在写函数的时候，要尽量以功能为向导，结果最好不要直接在函数中打印出来

## 关键字return

​	1、返回一个值

　　2、终止一个函数的继续

```
def my_len():  # 函数名的定义
    s1='hello world'
    length=0
    for i in s1:
        length=length+1
    return length  # 函数的返回值
str_len=my_len()  #函数的调用以及返回值的接收
print(str_len)

# 11
```

### 在没有返回值的时候

　　1、不写return与写入return None的效果相同，返回的只都是None　　　

　　2、只写一个return后面不加任何东西的时候与写return None的效果一样

### 返回多个值

​	1、当用一个变量接收返回值的时候，收到的是一个元组。这是因为在python中把用逗号分割的 多个值认为是一个元组

​	2、当返回值有多个变量接收，那么返回值的个数应该和接收变量的个数完全一致

```
#返回多个值，用一个变量接收
def f():
    return 'a','b'
c=f()
print(c)

# ('a', 'b')
 
#返回多个值，用多个变量接收(接收的变量数与返回值的个数要一致)
c,d=f()
print(c,d)

# a b
```

### return的扩展

```
def f(l):
    if len(l)>4:
        return True
    else:
        return False
s=[1,2,3,4]
dic={5,6,7,8,9}
print(f(s))
print(f(dic))

# False
# True
```

## 参数

```
#函数定义
def fun(s):
    count=0
    for i in s:
        count+=1
    return count
#函数调用
str=fun('jshdjkshkdhsk')
print(str)

#13
```

​	在上述代码中，告诉了fun函数要计算的字符串是谁，这个过程就是传递参数，简称传参；在调用函数时传递的这个'jshdjkshkdhsk'和定义函数时的s就是参数

### 实参

​	在调用函数时传递的'jshdjkshkdhsk'被称为**实际参数**，因为这个是实际要交给函数的内容，简称**实参**

### 形参

​	定义s的时候，s只是一个变量的名字，被称为**形式参数**，因为在定义函数的时候它只是一个形式，表示这里有一个参数，简称**形参**。

​	在传递多个参数：多个函数分别可以使用任意数据类型

​	按照关键之传参数和按照位置传参数是可以混用的，但是首先都是按位置传，之后再是按关键字传的；按照位置传完该接收的参数只能接收一个值，不接受或者重复接收

```
def f2(arge1,arge2):  # 站在接收、形参的角度上：位置参数
    print(arge1)
    print(arge2)
f2('abc',arge2=[1,2,3])

# abc
# [1, 2, 3]
 
def f2(arge1,arge2):
    print(arge1)
    print(arge2)
f2('abc',{'jsdj'})

# abc
# {'jsdj'}
```

### 默认参数

​	可以不传的参数，在不传参数的情况下可以使用默认值；如果传了，就会使用传的值

```
def classmate(name,sex='男'):
    print('姓名：%s,性别：%s'%(name,sex))
classmate('张三')
classmate('李四')
classmate('翠花','女')
 
# 姓名：张三,性别：男
# 姓名：李四,性别：男
# 姓名：翠花,性别：女
```

#### 默认参数魔性用法

​	默认参数尽量避免使用可变数据类型

```
def fun(l=[]):  # 相当于在def之前先定义了一个str=[],再将str赋值给l
    l.append(2)
    print(l)
fun()
fun()
fun()
fun()
 
# [2]
# [2, 2]
# [2, 2, 2]
# [2, 2, 2, 2]
```

```
def fun(l=[]):  # 相当于在def之前先定义了一个str=[],再将str赋值给l
    l.append(2)
    print(l)
fun([])
fun([])
fun([])
fun([])
 
# [2]
# [2]
# [2]
# [2]
```

### 动态参数

按位置传值多余的参数都由args统一接收，保存成一个元组或字典的形式

*args：接收所有按照位置传的参数

```
#位置参数  动态参数
def func(a,b,c,*args):  # 在参数前面加个*，这个参数就变成了动态参数
    print(a,b,c)
    print(args)  # 使用的时候，所有接收过来的参数都被组织成一个元组的形式
func(2,3,4,'jsk',[1,2,3])
 
# 2 3 4
# ('jsk', [1, 2, 3])
```

```
#位置参数  动态参数  默认参数
def func(a,b,c,*args,key='key'):  # 在参数前面加个*，这个参数就变成了动态参数
    print(a,b,c)
    print(key)
    print(args)  # 使用的时候，所有接收过来的参数都被组织成一个元组的形式
func(2,3,4,'jsk',[1,2,3],'xiaoming')
 
# 2 3 4
# key
# ('jsk', [1, 2, 3],'xiaoming')
```

#### *args魔性用法

```
def sum(*args):  # *args的作用是聚合，将传入的参数转变成元组的形式
    print(args)
    sun=0
    for i in args:
        sun+=i
    return sun
l=[1,2,34,5]
print(sum(*l))  # *l 是将列表l打散之后变成将列表中的每个元素分别输出
 
# (1, 2, 34, 5)
# 42
```

*\*kwargs：按照所有接收关键字传的参数

```
def func(a,*args,key='key',**kwargs):
    print(a)
    print(args)
    print(key)
    print(kwargs)
func(1,b=2,key='key')
func(5)
 
# 1
# ()
# key
# {'b': 2}
 
# 5
# ()
# key
# {}
```

## 三元运算

```
a=1
b=7
c=0
if a>b:
    c=a
else:
    c=b
print(c)
```

​	三元运算表达式，与以上代码的作用效果相同	

```
c=0
a=1
b=7
c=a if a>b else b  # 如果a>b成立，则c==a,否则c==b
print(c)
```

