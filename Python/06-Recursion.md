# Rcursion Function:maple_leaf:

## 递归的定义:jack_o_lantern:

在一个函数里再调用这个函数本身

## 递归最大深度:jack_o_lantern:

递归函数如果不受外力的阻止就会一直执行下去，但每一次函数调用都会产生一个属于它自己的名称空间，如果一直调用下去，就会造成名称空间占用太多内存的问题，于是python为了杜绝此类现象，强制的将递归层数控制在了997

```
#测试最大递归深度

def foo(n):
    print(n)
    n += 1
    foo(n)
foo(1)
```

当然，997是python为了我们程序的内存优化所设定的一个默认值，我们还是可以通过一些方式修改默认值的

```
#修改递归最大深度

import sys
print(sys.setrecursionlimit(100000))
```

不过不推荐修改默认递归深度，因为如果用997层递归都没有解决的问题不是代码太烂那就是不适合使用递归来解决

## 递归示例:jack_o_lantern:

### 二分查找算法

定义：二分查找又称折半查找

优点：比较次数少，查找速度快，平均性能好

缺点：要求待查表为有序表，且执行插入删除操作困难

因此，折半查找方法适用于不经常变动而查找频繁的有序列表。首先，假设列表中元素是按升序排列，将列表中间位置记录的值与所需查找的值比较，如果两者相等，则查找成功；否则利用中间位置记录将列表分成前、后两个子表，如果中间位置记录的值大于需要查找的值，则进一步查找前一子表，否则进一步查找后一子表。重复以上过程，直到找到满足条件的记录，查找成功，或直到子表不存在为止，此时查找不成功

```
#简单版

l = [2,3,5,10,15,16,18,22,26,30,32,35,41,42,43,55,56,66,67,69,72,76,82,83,88]

def func(l,aim):
    mid = (len(l)-1)//2
    if l:
        if aim > l[mid]:
            func(l[mid+1:],aim)
        elif aim < l[mid]:
            func(l[:mid],aim)
        elif aim == l[mid]:
            print("bingo",mid)
    else:
        print('找不到')
func(l,66)
func(l,6)
```

```
#优化版

def find_2(l,aim,start=0,end=None):
    if end == None:end = len(l) - 1
    if start <= end:
        mid = (end-start) // 2  + start
        if l[mid] > aim:
            find_2(l,aim,start,mid-1)
        elif l[mid] < aim:
            find_2(l,aim,mid+1,end)
        else:
            print(aim,mid)
    else:
        print('找不到这个值')
l = [2,3,5,10,15,16,18,22,26,30,32,35,41,42,43,55,56,66,67,69,72,76,82,83,88]
find_2(l,32)

# 32 10
```

### 阶乘

```
def f(n):
    if n==1:
        return 1
    return n*f(n-1)
print(f(3))
 
# 6
```

### 斐波那契数列

```
def fib(n):
    if n==1 or n==2:
        return 1
    return fib(n-1)+fib(n-2)
print(fib(8))
 
# 21
```

### 三级菜单

```
menu = {
    '北京': {
        '海淀': {
            '五道口': {
                'soho': {},
                '网易': {},
                'google': {}
            },
            '中关村': {
                '爱奇艺': {},
                '汽车之家': {},
                'youku': {},
            },
            '上地': {
                '百度': {},
            },
        },
        '昌平': {
            '沙河': {
                '老男孩': {},
                '北航': {},
            },
            '天通苑': {},
            '回龙观': {},
        },
        '朝阳': {},
        '东城': {},
    },
    '上海': {
        '闵行': {
            "人民广场": {
                '炸鸡店': {}
            }
        },
        '闸北': {
            '火车战': {
                '携程': {}
            }
        },
        '浦东': {},
    },
    '山东': {},
}
 
def menu_3(menu):
    while True:
        for key in menu:
            print(key)
        choice=input('选择:')
        if choice == 'q' or choice == 'b':
            return choice
        elif choice in menu and menu_3(menu[choice]):
            borq = menu_3(menu[choice])
            if borq == 'q':
                return 'q'

menu_3(menu)
```



