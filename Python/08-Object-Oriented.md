# Object-Oriented

## 面向过程vs面向对象:jack_o_lantern:

面向过程的程序设计核心是过程（流水线式思维），过程即解决问题的步骤，面向过程的设计就好比精心设计好一条流水线，考虑周全什么时候处理什么东西

优点：极大的降低了写程序的复杂度，只需要顺着要执行的步骤，堆叠代码即可

缺点：一套流水线或者流程就是用来解决一个问题，代码牵一发而动全身

面向对象的程序设计的核心是对象（上帝式思维），要理解对象为何物，必须把自己当成上帝，上帝眼里世间存在的万物皆为对象，不存在的也可以创造出来。面向对象的程序设计好比如来设计西游记，如来要解决的问题是把经书传给东土大唐，如来想了想解决这个问题需要四个人：唐僧，沙和尚，猪八戒，孙悟空，每个人都有各自的特征和技能（这就是对象的概念，特征和技能分别对应对象的属性和方法），然而这并不好玩，于是如来又安排了一群妖魔鬼怪，为了防止师徒四人在取经路上被搞死，又安排了一群神仙保驾护航，这些都是对象。然后取经开始，师徒四人与妖魔鬼怪神仙互相缠斗着直到最后取得真经。如来根本不会管师徒四人按照什么流程去取。

优点：解决了程序的扩展性，对某一个对象单独修改，会立刻反映整个体系中，如对游戏中一个人物参数的特征和技能修改都很容易

缺点：可控性差，无法像面向过程的程序设计流水线式的可以很精准的预测问题的处理流程与结果，面向对象的程序一旦开始就由对象之间的交互解决问题，即便是上帝也无法预测最终结果。于是我们经常看到一个游戏人物一参数的修改极有可能导致bug技能的出现，一刀砍死多个人，这个游戏就失去平衡 

应用场景：需求经常变化的软件，一般需求的变化都集中在用户层，互联网应用，企业内部软件，游戏等都是面向对象的程序设计大显身手的好地方。

在python 中面向对象的程序设计并不是全部。

 面向对象编程可以使程序的维护和扩展变得更简单，并且可以大大提高程序开发效率 ，另外，基于面向对象的程序可以使它人更加容易理解你的代码逻辑，从而使团队开发变得更从容。

了解一些名词：类、对象、实例、实例化

类：具有相同特征的一类事物(人、狗、老虎)

对象／实例：具体的某一个事物（隔壁阿花、楼下旺财）

实例化：类——>对象的过程

**初始类和对象**

python中一切皆为对象，类型的本质就是类

```
类：一类具有相同属性和方法的事物
字典 _ 类
d1 = {'k1':'v1'}  #对象
#动物园：老虎 狮子 猴
```

在python中，用变量表示特征，用函数表示技能，因而具有相同特征和技能的一类事物就是类，对象则是这一类事物中具体的一个

**类**

```
lass Person:  #类名有两个作用
     country = '中国'   #静态属性、数据属性
     def walk(self):    #动态属性、函数属性、方法
        print('walk')
```

​	**类的两种作用：属性引用和实例化**

**属性引用（类名.属性）**

```
class Person:
    country = '中国'
    def walk(self): 
        print('walk')
 
1.属性引用
print(Person.country) #静态属性的查看
print(Person.walk)
Person.role = '人'  #添加一个新静态属性
Person.country = '印度'  #修改一个新静态属性
del Person.role #删除一个静态属性
print(Person.__dict__)
print(Person.walk())  #报错 少self参数
Person.__dict__['country'] = '印度'  #报错 不能改变
print(Person.__dict__['country'])
print(Person.country)
```

**实例化（类名加括号就是实例化，会自动触发__init__函数的运行，可以用它来为每个实例定制自己的特性）**

```
class Person:  #类名有两个作用
    country = '中国'   #静态属性、数据属性
    def walk(self):    #动态属性、函数属性、方法
        print('walk')
 
#类能完成的第二个功能：实例化对象
#实例化：从一个类中创造一个具体的对象的过程
p = Person()
print(p)  #Person的对象
```

　　实例化的过程就是类——对象的过程

**对象**

```
class Person:
    def __init__(self,life_value,aggr,name,job):
        self.life = life_value
        self.aggressive = aggr
        self.name = name
        self.job = job
 
    def attack(self,dog_obj):   #boss_gold,tiedan
        print('%s 攻击了 %s'%(self.name,dog_obj.name))
        dog_obj.life = dog_obj.life - self.aggressive
```

​	对象是关于类而实际存在的一个例子，即实例

​	对象/实例只有一种作用：属性引用

```
boss_gold = Person(100,2.5,'太黑','old_driver')
print(boss_gold.life)
```

**对象之间的交互**

```
#人类 ：
# 属性 ：life_value,aggr,name,job
# 方法： attack
class Person:
    def __init__(self,life_value,aggr,name,job):
        self.life = life_value
        self.aggressive = aggr
        self.name = name
        self.job = job
 
    def attack(self,dog_obj):   #boss_gold,tiedan
        print('%s 攻击了 %s'%(self.name,dog_obj.name))
        dog_obj.life = dog_obj.life - self.aggressive
 
#狗类:
# 属性：life_value,aggr,name,kind
# 方法：bite
class Dog:
    def __init__(self,life_value,aggr,name,kind):
        self.life = life_value
        self.aggressive = aggr
        self.name = name
        self.kind = kind
 
    def bite(self,person_obj):
        print('%s 咬了 %s' % (self.name, person_obj.name))
        person_obj.life -= self.aggressive
 
 
tiedan = Dog(1000,100,'铁蛋','土狗')
boss_gold = Person(100,2.5,'太黑','old_driver')
# boss_gold.attack(tiedan)  #Person.attack(boss_gold,tiedan)
# print(tiedan.life)
# tiedan.bite(boss_gold)
# print(boss_gold.life)
```

**类命名空间与对象、实例的命名空间**

**创建一个类就会创建一个类的名称空间，用来存储类中定义的所有名字，这些名字称为类的属性**

类有两种属性：静态属性和动态属性

　　　　静态属性就是直接在类中定义的变量

　　　　动态属性就是定义在类中的方法

**其中类的数据属性是共享给所有对象的**

**而类的动态属性是绑定到所有对象的**

**创建一个对象/实例就会创建一个对象/实例的名称空间，存放对象/实例的名字，称为对象/实例的属性**

在obj.name会先从obj自己的名称空间里找name，找不到则去类中找，类也找不到就找父类...最后都找不到就抛出异常

### 组合用法

软件重用的重要方式除了继承之外还有另外一种方式，即：组合

组合指的是，在一个类中以另外一个类的对象作为数据属性，称为类的组合

```
class Person:  # 定义一个人类
    def __init__(self, name, aggressivity, life_value, money):
        self.name = name  # 每一个角色都有自己的昵称;
        self.aggressivity = aggressivity  # 每一个角色都有自己的攻击力;
        self.life_value = life_value  # 每一个角色都有自己的生命值;
        self.money = money
 
    def attack(self,dog):
        dog.life_value -= self.aggressivity
 
    def get_weapon(self,weapon_obj):
        if self.money > weapon_obj.price:
            self.money -= weapon_obj.price  # 金老板花钱买武器
            self.weapon = weapon_obj  # 金老板装备打狗棒
            self.aggressivity += weapon_obj.aggr  # 金老板的攻击力增加了
 
# boss_gold = Person('金老板',5,250,100)
# huang = Dog('大黄','藏獒',100,3000)
# huang.bite(boss_gold)
# print(boss_gold.life_value)
# boss_gold.attack(huang)
# print(huang.life_value)
#武器装备
#人 有 武器 —— 组合
#武器：攻击力，名字，价格
class Weapon:
    def __init__(self,name,price,aggr):
        self.name = name
        self.price = price
        self.aggr = aggr
dgb = Weapon('打狗棒',99.8,100)
boss_gold = Person('金老板',5,250,100)
huang = Dog('大黄','藏獒',100,3000)
boss_gold.get_weapon(dgb)
boss_gold.attack(huang)
print(huang.life_value)
```

**圆环是由两个圆组成的，圆环的面积是外面圆的面积减去内部圆的面积。圆环的周长是内部圆的周长加上外部圆的周长。**
**这个时候，我们就首先实现一个圆形类，计算一个圆的周长和面积。然后在"环形类"中组合圆形的实例作为自己的属性来用**

```
#圆形类
from math import pi
class Circle:
    def __init__(self,r):
        self.radius = r
    def perimeter(self):
        return 2*pi*self.radius
    def area(self):
        return pi*(self.radius**2)
#环形类
class Ring:
    def __init__(self,outer_r,inner_r):
        self.outer_circle = Circle(outer_r)
        self.inner_circle = Circle(inner_r)
    def perimeter(self):
        return self.outer_circle.perimeter()+self.inner_circle.perimeter()
    def area(self):
        return self.outer_circle.area() - self.inner_circle.area()
```

**用组合的方式建立了类与组合的类之间的关系，它是一种‘有’的关系,比如老师有生日**

```
class Teacher:
    def __init__(self,name,age,sex):
        self.name = name
        self.age = age
        self.sex = sex
        # self.birth_year = year
class Birthday:
    def __init__(self,year,month,day):
        self.year = year
        self.month = month
        self.day = day
birthay1 = Birthday(1968,12,31)
boss_gold = Teacher('太亮',40,'不详')
boss_gold.birth = birthay1
boss_gold.birth.year  #boss_gold.bith.year
#老师有生日 ： 年月日
#将一个类的对象拥有的属性 再将其定义成一个类以提高代码的复用
class Teacher:
    def __init__(self,name,age,sex,year,month,day):
        self.name = name
        self.age = age
        self.sex = sex
        self.birth = Birthday(year,month,day)
class Birthday:
    def __init__(self,year,month,day):
        self.year = year
        self.month = month
        self.day = day
boss_gold = Teacher('太亮',40,'不详',1968,12,31)
print(boss_gold.birth)
```

​	**当类之间有显著不同，并且较小的类是较大的类所需要的组件时，用组合比较好**

## 三大特性:jack_o_lantern:

### 继承

继承是一种创建新类的方式，在python中，新建的类可以继承一个或多个父类，父类又可称为基类或超类，新建的类称为派生类或子类

python中类的继承分为：单继承和多继承

```
# 继承 ：至少两个类 ： 什么 是 什么 的关系,为了避免几个类之间有相同的代码
# 父类 ： Animal
# 子类 ： Dog、Person
#动物
class Animal:
    def __init__(self,name,aggressivity,life_value):
        self.name = name
        self.aggressivity = aggressivity
        self.life_value = life_value
#狗
class Dog(Animal):  # 定义一个狗类
    def bite(self,people):
        people.life_value -= self.aggressivity
#人
class Person(Animal):  # 定义一个人类
    def attack(self,dog):
        dog.life_value -= self.aggressivity
 
    def get_weapon(self,weapon_obj):
        if self.money > weapon_obj.price:
            self.money -= weapon_obj.price  # 金老板花钱买武器
            self.weapon = weapon_obj  # 金老板装备打狗棒
            self.aggressivity += weapon_obj.aggr  # 金老板的攻击力增加了
huang = Dog('大黄',100,3000)   #__init__ 找父类
print(huang.life_value)
boss_gold = Person('金老板',5,250)  #__init__ 自己没有 找父类
print(boss_gold.life_value)
# Dog.bite(Person)
print(Dog.__bases__)
print(Animal.__bases__)
```

#### 继承与抽象（先抽象再继承）

抽象即抽取类似或者说比较像的部分。

抽象分成两个层次： 

1.将奥巴马和梅西这俩对象比较像的部分抽取成类； 

2.将人，猪，狗这三个类比较像的部分抽取成父类。

抽象最主要的作用是划分类别（可以隔离关注点，降低复杂度）

**![img](https://images2017.cnblogs.com/blog/1260329/201711/1260329-20171120171342086-1570258713.png)**

 

 

**继承：是基于抽象的结果，通过编程语言去实现它，肯定是先经历抽象这个过程，才能通过继承的方式去表达出抽象的结构**

抽象只是分析和设计的过程中，一个动作或者说一种技巧，通过抽象可以得到类

![img](https://images2017.cnblogs.com/blog/1260329/201711/1260329-20171120171342086-1570258713.png)

#### 继承与重用性

在开发程序的过程中，如果我们定义了一个类A，然后又想新建立另外一个类B，但是类B的大部分内容与类A的相同时

我们不可能从头开始写一个类B，这就用到了类的继承的概念。

通过继承的方式新建类B，让B继承A，B会‘遗传’A的所有属性(数据属性和函数属性)，实现代码重用 

```
# 猫类 抓老鼠
# 狗类 看门
# 动物 吃 喝 睡
class Animal:
    def eat(self):
        print('eating')
 
    def drink(self):
        print('drinking')
 
    def sleep(self):
        print('sleeping')
 
class Cat(Animal):
    def catch_mouse(self):
        print('yeah')
 
class Dog(Animal):
    def watch_door(self):
        print('wangwangwang')
 
kitty = Cat()
kitty.eat()
snoopy = Dog()
snoopy.eat()
```

#### 派生

当然子类也可以添加自己新的属性或者在自己这里重新定义这些属性（不会影响到父类），需要注意的是，一旦重新定义了自己的属性且与父类重名，那么调用新增的属性时，就以自己为准了

派生属性 ： 在自己的init方法里 使用父类的init方法 —— 指名道姓调用方法

派生方法 ： 在子类中增加父类没有的

只要子类有，就有子类的

只要想用父类，Animal.eat(snoopy) 父类名.父类的方法(子类对象)

2.7经典类中

```
#人 狗 相同属性的同时 还有一些不同的属性
class Animal:
    def __init__(self,aggressivity, life_value,name):
        self.name = name  # 每一个角色都有自己的昵称;
        self.aggressivity = aggressivity  # 每一个角色都有自己的攻击力;
        self.life_value = life_value  # 每一个角色都有自己的生命值;
    def eat(self):
        self.life_value += 10
 
class Person(Animal):
    def __init__(self, name, aggressivity, life_value, money):
        Animal.__init__(self, name, aggressivity, life_value)
        self.money = money    #派生属性：父类没有的属性
 
    def attack(self,dog):
        dog.life_value -= self.aggressivity
 
    def get_weapon(self,weapon_obj):
        if self.money > weapon_obj.price:
            self.money -= weapon_obj.price  # 金老板花钱买武器
            self.weapon = weapon_obj  # 金老板装备打狗棒
            self.aggressivity += weapon_obj.aggr  # 金老板的攻击力增加了
class Dog(Animal):
    def __init__(self, name, breed, aggressivity, life_value):
        Animal.__init__(self,aggressivity,life_value,name)
        self.breed = breed  # 每一只狗都有自己的品种; #派生属性：父类没有的属性
 
    def bite(self,people):  # 派生方法 ：父类没有的方法
        people.life_value -= self.aggressivity
 
    def eat(self):
        Animal.eat(self)
        print('dog is eating')
 
snoopy = Dog('太白','京巴',250,500)
print(snoopy.breed)
print(snoopy.name)
# Animal.eat(snoopy)
snoopy.eat()
print(snoopy.life_value)
snoopy.eat()
print(snoopy.life_value)
```

在新式类中

```
class Animal:
    def __init__(self,aggressivity, life_value,name):
        self.name = name  # 每一个角色都有自己的昵称;
        self.aggressivity = aggressivity  # 每一个角色都有自己的攻击力;
        self.life_value = life_value  # 每一个角色都有自己的生命值;
    def eat(self):
        self.life_value += 10
 
class Person(Animal):
    def __init__(self, name, aggressivity, life_value, money):
        # Animal.__init__(self, name, aggressivity, life_value)
        super().__init__(name, aggressivity, life_value)  #新式类
        self.money = money    #派生属性：父类没有的属性
 
    def attack(self,dog):
        dog.life_value -= self.aggressivity
 
    def get_weapon(self,weapon_obj):
        if self.money > weapon_obj.price:
            self.money -= weapon_obj.price  # 金老板花钱买武器
            self.weapon = weapon_obj  # 金老板装备打狗棒
            self.aggressivity += weapon_obj.aggr  # 金老板的攻击力增加了
class Dog(Animal):
    def __init__(self, name, breed, aggressivity, life_value):
        # Animal.__init__(self,aggressivity,life_value,name)
        # super(Dog,self).__init__(aggressivity,life_value,name)
        super().__init__(aggressivity,life_value,name)
        self.breed = breed  # 每一只狗都有自己的品种; #派生属性：父类没有的属性
 
    def bite(self,people):  # 派生方法 ：父类没有的方法
        people.life_value -= self.aggressivity
 
    def eat(self):
        # Animal.eat(self)
        super().eat()
        print('dog is eating')
snoopy = Dog('太白','京巴',250,500)
print(snoopy.breed)
print(snoopy.name)
snoopy.eat()
print(snoopy.life_value)
super(Dog,snoopy).eat()   #Animal.eat(snoopy)
print(snoopy.life_value)
```

用子类的对象，调用父类的方法：

如果子类中没有这个方法，直接就使用父类的

如果子类中有同名方法：

　　　　　　经典类 指名道姓 类名.方法名(子类对象) 类内外一致

　　　　　　新式类 super方法 super(子类名，子类对象).方法名() 类内可以省略super的参数

 **钻石继承**

　　经典类和新式类的多继承问题，继承顺序问题

　　　　新式类：广度优先

　　　　经典类：深度优先

```
class F(object):
    pass
    def f(self):
        print('F')
class E(F):
    pass
    def f(self):
        print('E')
class D(F):
    pass
    # def f(self):
    #     print('D')
class B(D):
    pass
    # def f(self):
    #     print('B')
class C(E):
    pass
    def f(self):
        print('C')
class A(B,C):
    pass
    # def f(self):
    #     print('A')
 
a = A()
a.f()
print(A.mro()) #新式类：查看继承顺序
# class A(object):pass #新式类
```

**继承的作用**

　　减少代码的重用

　　提高代码可读性 

　　规范编程模式

### 多态

多态指的是一类事物有多种形态

动物有多种形态：人，狗，猪

```
class Animal:pass
 
class Person(Animal):
    def attack(self):
        pass
 
class Dog(Animal):
    def attack(self):
        pass
 
def attack(obj):  #多态
    obj.attack()
 
d = Dog()
p = Person()
attack(d) #d.attack()
attack(p) #p.attack()
```

**鸭子类型**

　　Python崇尚鸭子类型，即‘如果看起来像、叫声像而且走起路来像鸭子，那么它就是鸭子python程序员通常根据这种行为来编写程序。例如，如果想编写现有对象的自定义版本，可以继承该对象也可以创建一个外观和行为像，但与它无任何关系的全新对象，后者通常用于保存程序组件的松耦合度。

　　例1：利用标准库中定义的各种‘与文件类似’的对象，尽管这些对象的工作方式像文件，但他们没有继承内置文件对象的方法

　　例2：序列类型有多种形态：字符串，列表，元组，但他们直接没有直接的继承关系

　　list tuple是一对鸭子类型

　　切片 ： 字符串 列表 元组

​	+：字符串 列表 数字

```
#二者都像鸭子,二者看起来都像文件,因而就可以当文件一样去用
class TxtFile:
    def read(self):
        pass
 
    def write(self):
        pass
 
class DiskFile:
    def read(self):
        pass
    def write(self):
        pass
```

#### 抽象类与接口类

##### 接口类

继承有两种用途：

　　　　1、继承基类的方法，并且做出自己的改变或者扩展（代码重用）  

　　　　2、声明某个子类兼容于某基类，定义一个接口类Interface，接口类中定义了一些接口名（就是函数名）且并未实现接口的功能，子类继承接口类，并且实现接口中的功能

```
from abc import ABCMeta,abstractmethod
class Fly_Animal(metaclass=ABCMeta):   #规范
    @abstractmethod
    def fly(self):pass
 
class Swim_Animal(metaclass=ABCMeta):
    @abstractmethod
    def swim(self): pass
 
class Walk_Animal(metaclass=ABCMeta):
    @abstractmethod
    def walk(self): pass
 
class Frog(Walk_Animal,Swim_Animal):
    def walk(self):
        print('自己实现walk功能')
 
    def swim(self): pass
 
class Swan(Walk_Animal,Swim_Animal,Fly_Animal):
    pass
 
class Bird(Walk_Animal,Fly_Animal):
    pass
```

　　接口类：

　　　　是规范子类的一个模板，只要接口类中定义，就应该在子类中实现

　　　　接口类不能被实例化，只能被继承

　　　　支持多继承

```
class Payment(metaclass=ABCMeta): #模板，接口类
    @abstractmethod  #装饰接口类中方法的，加上这个装饰器，自动检测子类中的方法名
    def pay(self,money):pass
 
    @abstractmethod
    def get(self):pass
 
class Apple_Pay(Payment):
    def pay(self,money):
        print('您使用苹果支付支付了%s元'%money)
 
class Ali_Pay(Payment):
    def pay(self, money):
        print('您使用支付宝支付了%s元' % money)
 
class WeChat_Pay(Payment):
    def pay(self,money):
        print('您使用微信支付了%s元' % money)
 
def pay(obj,money):
    return obj.pay(money)
 
apple = Apple_Pay()
ali = Ali_Pay()
wechat = WeChat_Pay()
pay(apple,100)   #apple.pay(100)
pay(wechat,200)
```

##### 抽象类

**什么是抽象类**

​    　　与java一样，python也有抽象类的概念但是同样需要借助模块实现，**抽象类是一个特殊的类，它的特殊之处在于只能被继承，不能被实例化**

**为什么要有抽象类**

​    　　如果说**类是从**一堆**对象**中抽取相同的内容而来的，那么**抽象类**就**是从**一堆**类**中抽取相同的内容而来的，内容包括数据属性和函数属性。

　　　 比如我们有香蕉的类，有苹果的类，有桃子的类，从这些类抽取相同的内容就是水果这个抽象的类，你吃水果时，要么是吃一个具体的香蕉，要么是吃一个具体的桃子。。。。。。你永远无法吃到一个叫做水果的东西。

​    　　从设计角度去看，如果类是从现实对象抽象而来的，那么抽象类就是基于类抽象而来的。

　 　　从实现角度来看，抽象类与普通类的不同之处在于：抽象类中有抽象方法，该类不能被实例化，只能被继承，且子类必须实现抽象方法。这一点与接口有点类似，但其实是不同的

```
　　抽象类可以实现一些子类共有的功能和属性\抽象类不鼓励多继承
　　　　文件操作 ：打开文件 关闭文件 写文件 读文件
　　　　硬盘操作：打开，关闭，写 读
　　　　进程文件：打开 关闭，读 写
　　　　python 没有接口的概念
　　　　只能借助抽象类的模块 来实现接口类
　　　　接口 —— java : 没有多继承 —— Interface
```

在python中实现抽象类　

```
from abc import ABCMeta,abstractmethod
class Base(metaclass=ABCMeta):
    def __init__(self,filename):
        self.filename = filename
    @abstractmethod #抽象方法
    def open(self):
        return 'file_handler'
 
    @abstractmethod
    def close(self):pass
 
    @abstractmethod
    def read(self):pass
 
    @abstractmethod
    def write(self):pass
 
 
class File(Base):
    def open(self):pass
    def close(self):pass
    def read(self):pass
    def write(self):pass
```

​	抽象类不能被实例化

　　这个抽象类可以规范子类必须实现抽象类中的抽象方法

**名词**

　　抽象：抽象即抽取类似或者说比较像的部分。是一个从具题到抽象的过程

　　 继承：子类继承了父类的方法和属性

　　 派生：子类在父类方法和属性的基础上产生了新的方法和属性

**抽象类与接口类**

```
　　1.多继承问题
　　在继承抽象类的过程中，我们应该尽量避免多继承；
　　而在继承接口的时候，我们反而鼓励你来多继承接口

　　2.方法的实现
　　在抽象类中，我们可以对一些抽象方法做出基础实现；
　　而在接口类中，任何方法都只是一种规范，具体的功能需要子类实现
```

### 封装

封装

​         隐藏对象的属性和实现细节，仅对外提供公共访问方式。

优点：

​	1.将变化隔离

​	2.便于使用

​	3.提高复用性 

​	4.提高安全性

封装原则

​	1.将不需要对外提供的内容都隐藏起来

​	2.把属性都隐藏，提供公共方法对其访问

#### 私有变量和私有方法

　　在python中用双下划线开头的方式将属性隐藏起来（设置成私有的）

##### 私有变量

```
class Dog:
    __role = 'dog'   #私有的静态属性
    def __discount(self): #私有的方法
        print('in __func')
 
    def price(self):
        self.__discount()
 
print(Dog.__dict__)
print(Dog._Dog__role)

从类的外面不能直接调用，在类内的使用加上了一层密码：_类名
```

```
d = Dog()
d.__func()
```

　　定义一个私有变量\属性\方法 ： __名字

　　在类的内部可以直接用 : __名字

　　在类的外部不能直接使用，如果一定要用，在私有方法之前加上：_类名,变成 _类名__名字

　　在类外的名字 通过__dict__就可以查看

##### 私有方法

　　在继承中，父类如果不想让子类覆盖自己的方法，可以将方法定义为私有的

```
class A:
    def __func(self):
        print('__a_func')
 
class B(A):
    def __init__(self):
        self.__func()
 
b = B()
```

```
私有的静态属性、方法、对象属性
使用__名字的方式调用，保证在类内部可以调用，外部不行
私有的 不能被继承
当有一个名字，不想被外部使用也不想被子类继承，只想在内部使用的时候就定义私有的
```

**封装与扩展性**

封装在于明确区分内外，使得类实现者可以修改封装内的东西而不影响外部调用者的代码；而外部使用用者只知道一个接口(函数)，只要接口（函数）名、参数不变，使用者的代码永远无需改变。这就提供一个良好的合作基础——或者说，只要接口这个基础约定不变，则代码改变不足为虑

```
class Room:
    def __init__(self,name,price,length,width):
        self.name = name
        self.price = price
        self.__length =length  #私有的对象属性
        self.__width = width
 
    def area(self):
        return self.__length*self.__width
 
house = Room('小超超',1000000,2,1)
print(house.area())
```

**property属性**

　　 property是一种特殊的属性，访问它时会执行一段功能（函数）然后返回值

```
class Person:
    def __init__(self,name,height,weight):
        self.name = name
        self.height = height
        self.__weight = weight
 
    @property
    def bmi(self):
        return self.__weight / (self.height ** 2)
 
li = Person('李岩',1.75,85)
print(li.bmi())
```

**为什么要用property**

将一个类的函数定义成特性，对象再去使用的时候obj.name根本无法察觉自己的name是执行了一个函数然后计算出来的，这种特性的使用方式遵循了统一访问原则

```
面向对象的封装有三种方式:
【public】
这种其实就是不封装,是对外公开的
【protected】
这种封装方式对外不公开,但对朋友(friend)或者子类(形象的说法是“儿子”,但我不知道为什么大家 不说“女儿”,就像“parent”本来是“父母”的意思,但中文都是叫“父类”)公开
【private】
这种封装对谁都不公开
```

python并没有在语法上把它们三个内建到自己的class机制中，在C++里一般会将所有的数据都设置为私有的，然后提供set和get方法（接口）去设置和获取，在python中通过property方法可以实现

```
class Foo:
    def __init__(self,val):
        self.__NAME=val #将所有的数据属性都隐藏起来
 
    @property
    def name(self):
        return self.__NAME #obj.name访问的是self.__NAME(这也是真实值的存放位置)
 
    @name.setter
    def name(self,value):
        if not isinstance(value,str):  #在设定值之前进行类型检查
            raise TypeError('%s must be str' %value)
        self.__NAME=value #通过类型检查后,将值value存放到真实的位置self.__NAME
 
    @name.deleter
    def name(self):
        raise TypeError('Can not delete')
 
f=Foo('egon')
print(f.name)
# f.name=10 #抛出异常'TypeError: 10 must be str'
del f.name #抛出异常'TypeError: Can not delete'　　
```

@property 把一个方法 伪装成一个属性zzzzzzzd

​	1.属性的值 是这个方法的返回值

​	2.这个方法不能有参数了

```
圆形类 ： 面积 周长
from math import pi
class Circle:
    def __init__(self,r):
        self.r = r
    @property
    def area(self):
        return self.r*self.r*pi
 
    @property
    def perimeter(self):
        return self.r*pi*2
c1 = Circle(5)
print(c1.area)
print(c1.perimeter)
```

```
class Goods:
    __discount = 0.8   #静态属性
    def __init__(self,name,price):
        self.__name = name
        self.__price = price  #原价
    @property
    def name(self):
        return self.__name
 
    @name.setter
    def name(self,new_name):
        self.__name = new_name
 
    @property
    def price(self):   #折后价
        return self.__price * Goods.__discount
 
    @price.setter
    def price(self,new_price):   #修改原价
        if type(new_price) is int:
            self.__price = new_price
apple = Goods('苹果',10)
apple.price = '10'   #settrt
print(apple.price)   #property
```

　　封装

　　__私有+property

　　让对象的属性变得更安全了

　　获取到的对象的值可以进行一些加工

　　修改对象的值的同时可以进行一些验证

```
class Foo:
    @property
    def AAA(self):
        print('get的时候运行我啊')
 
    @AAA.setter
    def AAA(self,value):
        print('set的时候运行我啊')
 
    @AAA.deleter
    def AAA(self):
        print('delete的时候运行我啊')
 
#只有在属性AAA定义property后才能定义AAA.setter,AAA.deleter
f1=Foo()
print(f1.AAA)     #property
f1.AAA='aaa'  #setter
del f1.AAA    #deleter
```

​	一个静态属性property本质就是实现了get，set，delete三种方法

```
class Goods:
    __discount = 0.8   #静态属性
    def __init__(self,name,price):
        self.__name = name
        self.__price = price  #原价
    @property
    def name(self):
        return self.__name
 
    @name.setter
    def name(self,new_name):
        self.__name = new_name
 
    @name.deleter
    def name(self):
        del self.__name
 
    @property
    def price(self):   #折后价
        return self.__price * Goods.__discount
 
    @price.setter
    def price(self,new_price):   #修改原价
        if type(new_price) is int:
            self.__price = new_price
 
 
apple = Goods('苹果',10)
# del apple.name
# print(apple.name)　
```

**classmethod**

把一个方法变成一个类中的方法，这个方法就直接可以被类调用，不需要依托任何对象

　　定义一个类

　　类里面的方法

　　并没有用到self

当一个方法的操作只涉及静态属性的时候，就应该使用classmethod来装饰这个方法

```
class Goods:
    __discount = 0.8
    @classmethod   #类方法
    def change_discount(cls,new_discount):
        cls.__discount = new_discount
    @classmethod
    def get_discount(cls):
        return cls.__discount
# apple = Goods()
Goods.change_discount(0.75)
print(Goods.get_discount())
```

```
类方法
    调用：不需要实例化 直接用类名调用就好
    定义：不用接受self参数，默认传cls，cls就代表当前方法所在的类

什么时候用类方法？
    需要使用静态变量且不需要和对象相关的任何操作的时候

静态方法
如果这个方法 既不需要操作静态变量
           也不需要使用对象相关的操作，
　　　　　　 就使用静态方法
```

**staticmethod**

在完全面向对象的程序中，如果一个函数既和对象没有关系，也和类没有关系，那么就用staticmethod将这个函数变成一个静态方法

```
class A:
    @staticmethod
    def func(name):  #静态方法
        print(123)
A.func('alex')
```

　　staticmethod是一个专门为面向对象编程提供的方法

　　它完全可以当做普通函数去用，只不过这个函数要通过类名.函数名调用

　　其他 传参 返回值 完全没有区别

绑定方法 和 非绑定方法

```
class A:
    @staticmethod
    def func1(name):  #静态方法
        print(123)
 
    @classmethod
    def func2(cls):  # 静态方法
        print(123)
 
    def func3(self):pass
a = A()
print(a.func1)  #静态方法
print(a.func2)  #类方法 ： 绑定到A类的func
print(a.func3)  #普通方法：绑定到A类对象的func
```

　　类里面，一共可以定义这三种方法：

　　普通方法 self

　　类方法 cls

　　静态方法

静态方法和类方法 都是直接可以使用类名调用

普通方法：对象调用