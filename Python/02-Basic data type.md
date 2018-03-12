# Basic data type

## str字符串:jack_o_lantern:

字符串的索引与切片

 	索引即下标，就是字符串组成的元素从第一个开始，初始索引为0以此类推

```
a = 'ABCDEFGHIJK'
print(a[0])
print(a[3])
print(a[5])
print(a[7])
```

​	切片就是通过索引（索引：索引：步长）截取字符串的一段，形成新的字符串（原则就是顾头不顾腚）

```
a = 'ABCDEFGHIJK'
print(a[0:3])
print(a[2:5])
print(a[0:]) #默认到最后
print(a[0:-1]) #-1就是最后一个
print(a[0:5:2]) #加步长
print(a[5:0:-2]) #反向加步长
```

## int数字:jack_o_lantern:

主要用于计算

```python
bit_length()　　当十进制用二进制表示时，转换成二进制时最少使用的位数
a=3
b=6
data=a.bit_length()
data1=b.bit_length()
print(data,data1)
```



## dict字典:jack_o_lantern:

​	字典是python中唯一的映射类型，采用键值对（key-value）的形式存储数据。python对key进行哈希函数运算，根据计算的结果决定value的存储地址，所以字典是无序存储的，且key必须是可哈希的。可哈希表示key必须是不可变类型，如：数字、字符串、元祖

　　字典是除列表以外python之中最灵活的内置数据结构类型。列表是有序的对象集合，字典是无序的对象集合。两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取

### 增

```
setdefault 在字典中添加键值对，如果只有键那对应的值是none,但是如果原字典中存在设置的键值对，则他不会更改或者覆盖

dic.setdefault('k','v')
print(dic)      
dic.setdefault('k','v1')     
print(dic)

# {'age': 18, 'name': 'jin', 'sex': 'male', 'k': 'v'}
# {'age': 18, 'name': 'jin', 'sex': 'male', 'k': 'v'}
```

### 删

```
dic_pop = dic.pop("a",'无key默认返回值')     # pop根据key删除键值对，并返回对应的值，如果没有key则返回默认返回值
print(dic_pop)
del dic["name"]      # 没有返回值。
print(dic)
 
dic_pop1 = dic.popitem()      # 随机删除字典中的某个键值对，将删除的键值对以元祖的形式返回
print(dic_pop1)      # ('name','jin')
 
dic_clear = dic.clear()      # 清空字典
print(dic，dic_clear)      # {} None
```

### 改

```
dic = {"name":"jin","age":18,"sex":"male"}
dic2 = {"name":"alex","weight":75}
dic2.update(dic)      # 将dic所有的键值对覆盖添加（相同的覆盖，没有的添加）到dic2中
print(dic2)
```

### 查

```
value1 = dic['name']      # 没有会报错
print(value1)
 
value2 = dic.get('djffdsafg','默认返回值')      # 没有可以返回设定的返回值
print(value2)
```

其他

```
item = dic.items()
print(item,type(item))      # dict_items([('name', 'jin'), ('sex', 'male'), ('age', 18)]) <class 'dict_items'>这个类型就是dict_items类型，可迭代的
 
keys = dic.keys()
print(keys,type(keys))      # dict_keys(['sex', 'age', 'name']) <class 'dict_keys'>
 
values = dic.values()
print(values,type(values))      # dict_values(['male', 18, 'jin']) <class 'dict_values'> 同上
```

字典循环取key，value

```
dic = {"name":"jin","age":18,"sex":"male"}
for key in dic:
     print(key)
for item in dic.items():
     print(item)
for key,value in dic.items():
     print(key,value）　
```



## list列表:jack_o_lantern:

### 增

append(在列表最后的位置添加元素)：在原列表上进行增加

```
a=['alix','wusir','xiaofang']
a.append('laozi')
print(a)       

# ['alex','wusir','xiaofang','laozi']
```

```
a=['alix','wusir','xiaofang']
while True:
    username=input('请输入员工姓名：')
    if username.lower()=='q':
        print('退出成功！')
        break
    else:
        a.append(username)
        print(a)
 
请输入员工姓名：ksdh
['alix', 'wusir', 'xiaofang', 'ksdh']
请输入员工姓名：q
退出成功！　
```

lnsert插入，可以在任意位置插入元素

insert(index,p_object)

```
a=['taibai','jinxin','wusir']
a.insert(1,'太亮')
print(a)      

# ['taibai','太亮'，'jinxin','wusir']
```

extend()：迭代的添加，加入列表的最后

```
a=['taibai','jinxin','wusir']
a.extend('太亮')
b=['taibai','太亮','wusir']
b.extend(['金星'])
print(a)　　　　　　
print(b)　　　　　　

# ['taibai','jinxin','wusir','太','亮']
# ['taibai','太亮'，'wusir','金星']
```

　　如果extend()添加的是字符串，则字符串中的每个元素都会被拆分成单个的元素添加到目的列表中

　　如果extend()添加的是列表，则该列表会被当做一个整体添加到目的列表中成为目的列表中的一个元素

### 删

pop 按照索引去删除，有返回值

```
a=['taibai', '太亮', 'wusir', '金星']
name=a.pop(2)
print(name)　　　　
print(a)　　　　　　

# wusir
# ['taibai','太亮'，‘'金星']
```

​	删除的是a[2]=‘wusir’，返回值是wusir 

remove() 按元素来删除，但是没有返回值

```
a=['taibai', '太亮', 'wusir', '金星']
name=a.remove('taibai')
print(name)　　
print(a)　　　 

# None
# ['太亮', 'wusir', '金星']
```

　　由于remove()没有返回值，则输出name时得到的是0

clear() 清空列表，将列表变成空列表

```
a=['taibai', '太亮', 'wusir', '金星']
a.clear()
print(a)　　　　

# []
```

　　独立为一条语句，列表在进行clear()操作之后返回的是一个空列表，列表还在

del() 可以按照索引删除；也可以按照切片删除，可加步长。但是没有返回值

​	可以按照索引删除

```
a=['alix','taibai','tailiang','wusir']
del a[3]
print(a)
 
['alix', 'taibai', 'tailiang']
```

　　可以按照切片删除，也可以加步长

```
b=['alix','taibai','tailiang','wusir']
del b[1:3]
print(b)
 
['alix', 'wusir']
```

### 改

​	按照索引改：适用于修改单个元素的列表中

```
a=['alix','taibai','tailiang','wusir']
a[3]='亮亮'
print(a)
 
['alix', 'taibai', 'tailiang', '亮亮']
```

　　按照切片进行修改：先删除，之后迭代着添加

```
a=['alix','taibai','tailiang','wusir']
a[1:3]='都是一个人'
print(a)
 
['alix', '都', '是', '一', '个', '人', 'wusir']
```

　　该段代码是将列表中的a[1],a[2]先删除，之后将'都是一个人'从a[1]迭代着添加到列表a当中

　　该段代码是将a[1],a[2]现删除，之后将列表['都是一个人']添加到a[1]的位置

### 查

for循环查询

```
a=['alix', 'taibai', 'tailiang','wusir']
for i in a:
    print(i)
 
alix
taibai
tailiang
wusir
```

按索引查询

```
a=['alix', 'taibai', 'tailiang','wusir']
print(a[0])
print(a[1])
print(a[2])
print(a[3])
 
alix
taibai
tailiang
wusir
```

### 列表的嵌套

列表可以被更改，字符串不可以被更改

```
a=['alix', 'taibai',[1,2,3,'yanger,old'], 'tailiang','wusir']
print(a[2])
print(a[2][2])
 
[1, 2, 3, 'yanger,old']
 3
```

 	将列表li的元素'yuanhao'的首字母变成大写，由于字符串不能被更改就只能将'yuanhao'提出之后形成一个新的首字母为大写的'Yuanhao'，之后再赋值给li[4]

```
li=[1,2,3,'taibai','yuanhao',[1,'alix',3],True]
print(li[3])  # taibai
print(li[5][1])  # alix
s=li[4].capitalize()
li[4]=s
print(li)  

# [1, 2, 3, 'taibai', 'Yuanhao', [1, 'alix', 3], True]
```

　　将li[4]中的'yuanhao'中的hao用'日天'来代替，由于'yuanhao'是字符串不能更改，所以只能是先提出li[4],之后形成一个新的字符串，将新的字符串赋值给li[4]

```
li=[1,2,3,'taibai','yuanhao',[1,'alix',3],True]
s2=li[4].replace('hao','日天')
li[4]=s2
print(li)
 
[1, 2, 3, 'taibai', 'yuan日天', [1, 'alix', 3], True]
```

对列表中的字符串进行'修改'和对列表中的元素进行修改。

```
li=[1,2,3,'taibai','yuanhao',[1,'alix',3],True]
s2=li[4].replace('hao','日天')
li[4]=s2
li[4]=li[4][0:4]+'ritian'
print(li)  

# [1, 2, 3, 'taibai', 'yuanritian', [1, 'alix', 3], True]

li[5][0]='文杰'
print(li)  

# [1, 2, 3, 'taibai', 'yuanritian', ['文杰', 'alix', 3], True]

li[5][1]=li[5][1].upper()
print(li)  

# [1, 2, 3, 'taibai', 'yuanritian', ['文杰', 'ALIX', 3], True]
```

### 列表的叠加

```
li=[1,2,3]
l2=['a','b','c']
l3=li+l2
print(l3)
 
[1, 2, 3, 'a', 'b', 'c']
```

### 其他方法

计数 count()

```
li=[1,2,3,'taibai','yuanhao',[1,'alix',3],True]
print(li.count('fsh'))  
print(li.count(1)) 

# 0
# 2
```

排序

　　正排序：sort()

```
a=[1,2,3,7,4,8,0,3,9]
a.sort()
print(a)
 
[0, 1, 2, 3, 3, 4, 7, 8, 9]
```

　　反转：reverse()  不排序，只是将原有列表中的元素按照与原来顺序相反的方式输出

```
a=[1,2,3,7,4,8,0,3,9]
a.reverse()
print(a)
 
[9, 3, 0, 8, 4, 7, 3, 2, 1]
```

## tuple元祖:jack_o_lantern:

元组被称为只读列表，即数据可以被查询，但不能被修改，但字符串的切片操作同样适用于元组。例：（1，2，3）（"a","b","c"）

```
a=(1,2,3)
print(a[0])
print(a[1])
print(a[2])
 
1
2
3
```

## set集合:jack_o_lantern:

​	集合是无序的，不重复的数据集合，它里面的元素是可哈希的（不可变类型），但集合本身是不可哈希的（所以集合做不了字典的键）

　　集合最重要的两点：

　　　　1.去重，把一个列表变成集合，就自动去重了

　　　　2.关系测试，测试两组数据之前的交集、并集、差集等关系

### 增

```
set1 = {'alex', 'wusir', 'ritian','barry'}
set1.add('景女神')　　#增加一个元素
print(set1)
 
update：迭代的增加
set1.update('A')
print(set1)
set1.update('老师')
print(set1)
set1.update([1,2,3])
print(set1)
```

### 删

```
set1 = {'alex','wusir','ritian','egon','barry'}
set1.remove('alex')    #删除一个元素
print(set1)
 
set1.pop()      #随机删除一个元素
print(set1)
 
set1.clear()    #清空集合
print(set1)
 
del set1        #删除集合
print(set1)
```

### 查

集合的查询只能用for循环操作

```
set = {1,2,3}
for i in set:
    print(i)
 
1
2
3
```

### 其他操作

交集（&或者intersectiion）

```
set1 = {1,2,3,4,5}
set2 = {4,5,6,7,8}
print(set1 & set2)
print(set1.intersection(set2))
```

并集（| 或者union）

```
set1 = {1,2,3,4,5}
set2 = {4,5,6,7,8}
print(set1 | set2)
print(set1.union(set2))
```

差集（-或者difference）

```
set1 = {1,2,3,4,5}
set2 = {4,5,6,7,8}
print(set1- set2)
print(set1.difference(set2))
```

反交集（^或者symmetric_difference）

```
set1 = {1,2,3,4,5}
set2 = {4,5,6,7,8}
print(set1 ^ set2)
print(set1.symmetric_difference(set2))
```

子集与超集

```
set1 = {1,2,3}
set2 = {1,2,3,4,5,6}
print(set1<set2)
print(set1.issubset(set2))  #这两个相同说明set1是set2的子集
 
print(set2>set1)
print(set2.issuperset(set1))#这两个相同说明set2是set1的超集
```

### frozenset

frozenset不可变集合，让集合变成不可变类型

```
s = frozenset('barry')
print(s,type(s))    #frozenset({'r', 'a', 'b', 'y'}) <class 'frozenset'>
```

## bool布尔值:jack_o_lantern:

bool只有True、真和False、假两种表现形式，就是反应条件的正确与否

　　真   1   True

　　假   0   False