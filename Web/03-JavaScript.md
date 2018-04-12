# JavaScript概述

## JavaScript历史

JavaScript 是脚本语言。

JavaScript 是一种轻量级的编程语言。

JavaScript 是可插入 HTML 页面的编程代码。

JavaScript 插入 HTML 页面后，可由所有的现代浏览器执行。

JavaScript 很容易学习。

- 1992年Nombas开发出C-minus-minus(C--)的嵌入式脚本语言(最初绑定在CEnvi软件中).后将其改名ScriptEase.(客户端执行的语言)
- Netscape(网景)接收Nombas的理念,(Brendan Eich)在其Netscape Navigator 2.0产品中开发出一套livescript的脚本语言.Sun和Netscape共同完成.后改名叫Javascript
- 微软随后模仿在其IE3.0的产品中搭载了一个JavaScript的克隆版叫Jscript.
- 为了统一三家,ECMA(欧洲计算机制造协会)定义了ECMA-262规范.国际标准化组织及国际电工委员会（ISO/IEC）也采纳 ECMAScript 作为标准（ISO/IEC-16262）。从此，Web 浏览器就开始努力（虽然有着不同的程度的成功和失败）将 ECMAScript 作为 JavaScript 实现的基础。EcmaScript是规范.

## ECMAScript

| 年份   | 名称             | 描述                                    |
| ---- | -------------- | ------------------------------------- |
| 1997 | ECMAScript 1   | 第一个版本                                 |
| 1998 | ECMAScript 2   | 版本变更                                  |
| 1999 | ECMAScript 3   | 添加正则表达式添加try/catch                    |
|      | ECMAScript 4   | 没有发布                                  |
| 2009 | ECMAScript 5   | 添加"strict mode"严格模式添加JSON支持           |
| 2011 | ECMAScript 5.1 | 版本变更                                  |
| 2015 | ECMAScript 6   | 添加类和模块                                |
| 2016 | ECMAScript 7   | 增加指数运算符（**）增加Array.prototype.includes |

*注：ES6就是指ECMAScript 6。*

尽管 ECMAScript 是一个重要的标准，但它并不是 JavaScript 唯一的部分，当然，也不是唯一被标准化的部分。实际上，一个完整的 JavaScript 实现是由以下 3 个不同部分组成的：

- 核心（ECMAScript） 
- 文档对象模型（DOM） Document object model (整合js，css，html)
- 浏览器对象模型（BOM） Broswer object model（整合js和浏览器）
- Javascript 在开发中绝大多数情况是基于对象的.也是面向对象的. 

简单地说，ECMAScript 描述了JavaScript语言本身的相关内容

- 语法 
- 类型 
- 语句 
- 关键字 
- 保留字 
- 运算符 
- 对象 (封装 继承 多态) 基于对象的语言.使用对象.

# JavaScript基础

## 引入方式

### Script标签内写代码

```
<script>
  // 在这里写你的JS代码
</script>
```

### 引入额外的JS文件

```
<script src="myscript.js"></script>
```

## 语言规范

### 注释

```
// 单行注释

/*多行注释*/
```

### 结束符

JavaScript中的语句要以分号（;）为结束符。

### 输出

**alert()**

​	有阻塞作用，不点击确定，后续代码无法继续执行

​	alert()只能输出string,如果alert输出的是对象会自动调用toString()方法

​	alert不支持多个参数的写法,只能输出第一个值

```
alert([1,2,3]); //'1,2,3'
alert(1,2,3); //1
```

**console.log()**

​	在打印台输出

​	可以打印任何类型的数据

​	支持多个参数的写法

```
console.log([1,2,3]); //[1,2,3]
console.log(1,2,3); // 1 2 3
```

### 变量

1、JavaScript的变量名可以使用_，数字，字母，$组成，不能以数字开头。

2、声明变量使用 var 变量名; 的格式来进行声明

```
var name = "Timo";
var age = 3;
```

3、一行可以声明多个变量.并且可以是不同类型

```
var name="Timo", age=3, job="ad";
```

4、声明变量时 可以不用var. 如果不用var 那么它是全局变量

注意：

​	变量名是区分大小写的。

​	推荐使用驼峰式命名规则。

​	保留字不能用做变量名。

```
#保留字

abstract
boolean
byte
char
class
const
debugger
double
enum
export
extends
final
float
goto
implements
import
int
interface
long
native
package
private
protected
public
short
static
super
synchronized
throws
transient
volatile
```

### 常量

**常量** ：直接在程序中出现的数据值

标识符：

​	1.由不以数字开头的字母、数字、下划线(_)、美元符号($)组成

​	2.常用于表示函数、变量等的名称

​	3.例如：_abc,$abc,abc,abc123是标识符，而1abc不是

​	4.JavaScript语言中代表特定含义的词称为保留字，不允许程序再定义为标识符

![img](https://images2015.cnblogs.com/blog/877318/201610/877318-20161020152532717-389530735.png)

# 数据类型

**JavaScript拥有动态类型**

```
var x;  // 此时x是undefined
var x = 3;  // 此时x是数字
var x = "timo";  // 此时x是字符串 
```

## 数字类型(Number)

- 不区分整型数值和浮点型数值;
- 所有数字都采用64位浮点格式存储，相当于Java和C语言中的double格式
- 能表示的最大值是±1.7976931348623157 x 10308
- 能表示的最小值是±5 x 10 -324 　

整数：
​           在JavaScript中10进制的整数由数字的序列组成
​           精确表达的范围是-9007199254740992 (-253) 到 9007199254740992 (253)
​           超出范围的整数，精确度将受影响
浮点数：
​           使用小数点记录数据
​           例如：3.4，5.6
​           使用指数记录数据
​           例如：4.3e23 = 4.3 x 1023

16进制和8进制数的表达:
​           16进制数据前面加上0x，八进制前面加0;16进制数是由0-9,A-F等16个字符组成;8进制数由0-7等8个数字组成

​           16进制和8进制与2进制的换算:

```
2进制: 1111 0011 1101 0100   <-----> 16进制:0xF3D4 <-----> 10进制:62420
2进制: 1 111 001 111 010 100 <-----> 8进制:0171724
```

还有一种NaN，表示不是一个数字（Not a Number）。

```
parseInt("123")  // 返回123
parseInt("ABC")  // 返回NaN,NaN属性是代表非数字值的特殊值。该属性用于指示某个值不是数字。
parseFloat("123.456")  // 返回123.456
```

## 字符串类型(String)

由Unicode字符、数字、标点符号组成的序列；字符串常量首尾由单引号或双引号括起；JavaScript中没有字符类型；常用特殊字符在字符串中的表达；
字符串中部分特殊字符必须加上右划线\；常用的转义字符 \n:换行 \':单引号 \":双引号 \\:右划线

```
var a = "Hello"
var b = "world;
var c = a + b; 
console.log(c);  // 得到Helloworld
```



字符串创建(两种方式)
​       1、变量 = “字符串”
​       2、字串对象名称 = new String (字符串)

```
var str1="hello world";
var str1= new String("hello world");
```

常用方法

| 方法                                       | 说明                                |
| ---------------------------------------- | --------------------------------- |
| .length                                  | 获取字符串的长度                          |
| .trim()                                  | 去除字符串两边空格                         |
| .trimLeft()                              | 移除字符串左边的空白                        |
| .trimRight()                             | 移除字符串右边的空白                        |
| .charAt(index)                           | 获取指定位置字符，其中index为要获取的字符索引         |
| .concat(value, ...)                      | 拼接                                |
| .indexOf(findstr,start) .lastIndexOf(findstr) | 子序列位置                             |
| .slice(start, end)                       | 切片操作字符串                           |
| .toLowerCase()                           | 转为小写                              |
| .toUpperCase()                           | 转为大写                              |
| .split(delimiter, limit)                 | 分割字符串                             |
| .match(regexp)                           | 返回匹配字符串的数组，如果没有匹配则返回null          |
| .search(regexp)                          | 返回匹配字符串的首字符位置索引                   |
| .substring(start,length) .substring(start, end) | start表示开始位置，length表示截取长度，end是结束位置 |
| .replace(findstr,tostr)                  | 字符串替换                             |

拼接字符串一般使用“+”

```
string.slice(start, stop)和string.substring(start, stop)区别

两者的相同点：
如果start等于end，返回空字符串
如果stop参数省略，则取到字符串末
如果某个参数超过string的长度，这个参数会被替换为string的长度

substirng()的特点：
如果 start > stop ，start和stop将被交换
如果参数是负数或者不是数字，将会被0替换

silce()的特点：
如果 start > stop 不会交换两者
如果start小于0，则切割从字符串末尾往前数的第abs(start)个的字符开始(包括该位置的字符)
如果stop小于0，则切割在从字符串末尾往前数的第abs(stop)个字符结束(不包含该位置字符)
```

## 布尔类型(Boolean)

Boolean类型仅有两个值：true和false，也代表1和0，实际运算中true=1,false=0。

区别于Python，true和false都是小写。布尔值也可以看作on/off、yes/no、1/0对应true/false。

```
var a = true;
var b = false;
```

Boolean值主要用于JavaScript的控制语句。

```
if (x==1){
      y=y+1;
}else{
      y=y-1;
      }
```

## Null和Undefined类型

**Undefined类型**

Undefined 类型只有一个值，即 undefined。当声明的变量未初始化时，该变量的默认值是 undefined。

当函数无明确返回值时，返回的也是值 "undefined";

**Null类型**

另一种只有一个值的类型是 Null，它只有一个专用值 null，即它的字面量。值 undefined 实际上是从值 null 派生来的，因此 ECMAScript 把它们定义为相等的。

尽管这两个值相等，但它们的含义不同。undefined 是声明了变量但未对其初始化时赋予该变量的值，null 则用于表示尚未存在的对象。如果函数或方法要返回的是对象，那么找不到该对象时，返回的通常是 null。

## 数组(Array)

类似于Python中的列表。

创建数组的三种方式

```
创建方式1:
var arrname = [元素0,元素1,…];          // var arr=[1,2,3];

创建方式2:
var arrname = new Array(元素0,元素1,….); // var test=new Array(100,"a",true);

创建方式3:
var arrname = new Array(长度); 
            //  初始化数组对象:
                var cnweek=new Array(7);
                    cnweek[0]="星期日";
                    cnweek[1]="星期一";
                    ...
                    cnweek[6]="星期六";
```

常用方法

| 方法                 | 说明          |
| ------------------ | ----------- |
| .length            | 数组的大小       |
| .push(ele)         | 尾部追加元素      |
| .pop()             | 获取尾部的元素     |
| .unshift(ele)      | 头部插入元素      |
| .shift()           | 头部移除元素      |
| .slice(start, end) | 切片          |
| .reverse()         | 反转          |
| .join(seq)         | 将数组元素连接成字符串 |
| .concat(val, ...)  | 连接数组        |
| .sort()            | 排序          |

关于sort

```
如果调用sort方法时没有传入参数，将按字母顺序对数组中的元素进行排序，说得更精确点，是按照字符编码的顺序进行排序。要实现这一点，首先应把数组的元素都转换成字符串（如有必要），以便进行比较。

如果想按照其他标准进行排序，就需要提供比较函数，该函数要比较两个值，然后返回一个用于说明这两个值的相对顺序的数字。比较函数应该具有两个参数 a 和 b，其返回值如下：

若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。
若 a 等于 b，则返回 0。
若 a 大于 b，则返回一个大于 0 的值。
*/

// 根据上面的规则自行实现一个排序函数：


function sortNumber(a,b) {
  return a - b
}

// 调用sort方法时将定义好的排序函数传入即可。
stringObj.sort(sortNumber)
```

二维数组

```
var cnweek=new Array(7);
for (var i=0;i<=6;i++){
    cnweek[i]=new Array(2);
}
cnweek[0][0]="星期日";
cnweek[0][1]="Sunday";
cnweek[1][0]="星期一";
cnweek[1][1]="Monday";
...
cnweek[6][0]="星期六";
cnweek[6][1]="Saturday";
```

可以使用for循环遍历数组中的元素

```
var a = [10, 20, 30, 40];
for (var i=0;i<a.length;i++) {
  console.log(i);
}
```

```
#js中数组的特性
         
//java中数组的特性,  规定是什么类型的数组,就只能装什么类型.只有一种类型.
//js中的数组特性1: js中的数组可以装任意类型,没有任何限制.
//js中的数组特性2: js中的数组,长度是随着下标变化的.用到多长就有多长.
	var arr5 = ['abc',123,1.14,true,null,undefined,new String('1213'),new Function('a','b','alert(a+b)')];
     /*  alert(arr5.length);//8
         arr5[10] = "hahaha";
         alert(arr5.length); //11
         alert(arr5[9]);// undefined */
```

# 运算符

```
算术运算符：
    +   -    *    /     %       ++        -- 

比较运算符：
    >   >=   <    <=    !=    ==    ===   !==

逻辑运算符：
     &&   ||   ！

赋值运算符：
    =  +=   -=  *=   /=

字符串运算符：
    +  连接，两边操作数有一个或两个是字符串就做连接运算

```

## 算术运算符

**自加自减**

假如x=2，那么x++表达式执行后的值为3，x--表达式执行后的值为1；i++相当于i=i+1，i--相当于i=i-1；
递增和递减运算符可以放在变量前也可以放在变量后：--i

```
var i=10;
console.log(i++);
console.log(i);
console.log(++i);
console.log(i);
console.log(i--);
console.log(--i);
```

**单元运算符**

```
- 除了可以表示减号还可以表示负号  例如：x=-y
 
+ 除了可以表示加法运算还可以用于字符串的连接  例如："abc"+"def"="abcdef"
```

**JS不同于Python，是一门弱类型语言**

```
#静态类型语言
一种在编译期间就确定数据类型的语言。大多数静态类型语言是通过要求在使用任一变量之前声明其数据类型来保证这一点的。Java 和 C 是静态类型语言。 
动态类型语言
一种在运行期间才去确定数据类型的语言，与静态类型相反。VBScript 和 Python 是动态类型的，因为它们确定一个变量的类型是在您第一次给它赋值的时候。 

#强类型语言
一种总是强制类型定义的语言。Java 和 Python 是强制类型定义的。您有一个整数，如果不明确地进行转换 ，不能将把它当成一个字符串去应用。 

#弱类型语言
一种类型可以被忽略的语言，与强类型相反。JS 是弱类型的。在JS中，可以将字符串 '12' 和整数 3 进行连接得到字符串'123'，然后可以把它看成整数 123 ，所有这些都不需要任何的显示转换。 
所以说 Python 既是动态类型语言 (因为它不使用显示数据类型声明)，又是强类型语言 (因为只要一个变量获得了一个数据类型，它实际上就一直是这个类型了)。
```

NaN

```
var d="timo";
    d=+d;
    alert(d);//NaN:属于Number类型的一个特殊值,当遇到将字符串转成数字无效时,就会得到一个NaN数据
    alert(typeof(d));//Number

    //NaN特点:
    
    var n=NaN;
    
    alert(n>3);
    alert(n<3);
    alert(n==3);
    alert(n==NaN);
    
    alert(n!=NaN);//NaN参与的所有的运算都是false,除了!=
```

## 比较运算符

用于控制语句时

```
if (2>1){       
            console.log("Hello World!")
        }
```

等号和非等号的同类运算符是全等号和非全等号。这两个运算符所做的与等号和非等号相同，只是它们在检查相等性前，不执行类型转换。

```
console.log(2==2);
console.log(2=="2");
console.log(2==="2");
console.log(2!=="2");
```

```
#Attention

var bResult = "Blue" < "alpha";
alert(bResult); //输出 true　　
在上面的例子中，字符串 "Blue" 小于 "alpha"，因为字母 B 的字符代码是 66，字母 a 的字符代码是 97。

比较数字和字符串

另一种棘手的状况发生在比较两个字符串形式的数字时，比如：

var bResult = "25" < "3";
alert(bResult); //输出 "true"
上面这段代码比较的是字符串 "25" 和 "3"。两个运算数都是字符串，所以比较的是它们的字符代码（"2" 的字符代码是 50，"3" 的字符代码是 51）。

不过，如果把某个运算数该为数字，那么结果就有趣了：

var bResult = "25" < 3;
alert(bResult); //输出 "false"

这里，字符串 "25" 将被转换成数字 25，然后与数字 3 进行比较，结果不出所料。

总结：
	比较运算符两侧如果一个是数字类型,一个是其他类型,会将其类型转换成数字类型.
	比较运算符两侧如果都是字符串类型,比较的是最高位的asc码,如果最高位相等,继续取第二位比较。
```

```
#Attention

等性运算符：执行类型转换的规则如下：

如果一个运算数是 Boolean 值，在检查相等性之前，把它转换成数字值。false 转换成 0，true 为 1。 
如果一个运算数是字符串，另一个是数字，在检查相等性之前，要尝试把字符串转换成数字。 
如果一个运算数是对象，另一个是字符串，在检查相等性之前，要尝试把对象转换成字符串。 
如果一个运算数是对象，另一个是数字，在检查相等性之前，要尝试把对象转换成数字。 
在比较时，该运算符还遵守下列规则：

值 null 和 undefined 相等。 
在检查相等性时，不能把 null 和 undefined 转换成其他值。 
如果某个运算数是 NaN，等号将返回 false，非等号将返回 true。 
如果两个运算数都是对象，那么比较的是它们的引用值。如果两个运算数指向同一对象，那么等号返回 true，否则两个运算数不等。 
```

## 逻辑运算符

```
if (2>1 && [1,2]){
    console.log("条件与")
}

// 思考返回内容
console.log(1 && 3);   //与
console.log(0 && 3);
console.log(0 || 3);   //或
console.log(2 || 3);
```

## 三元运算

```
var a = 1;
var b = 2;
var c = a > b ? a : b
```

# 流程控制

- 顺序结构(从上向下顺序执行)
- 分支结构
- 循环结构

## 顺序结构

```
 <script>
        console.log(“星期一”);
        console.log(“星期二”);
        console.log(“星期三”);
    </script>
```

## 分支结构

### if-else结构

```
if (表达式){
   语句１;
   ......
   } else{
   语句２;
   .....
   }
```

功能说明：如果表达式的值为true则执行语句1,否则执行语句2

```
var x= (new Date()).getDay();
        //获取今天的星期值，0为星期天
        var y;

        if ( (x==6) || (x==0) ) {
            y="周末";
        }else{
            y="工作日";
            }  
        console.log(y);

        /*等价于
        y="工作日";
        if ( (x==6) || (x==0) ) {
        y="周末";
        }
        console.log(y);  */
```

### if-elif-else结构

```
if (表达式1) {
    语句1;
}else if (表达式2){
    语句2;
}else if (表达式3){
    语句3;
} else{
    语句4;
}
```

```
var score=window.prompt("您的分数:");

if (score>90){
    ret="优秀";
}else if (score>80){
    ret="良";
}else if (score>60){
    ret="及格";
}else {
    ret = "不及格";
}
alert(ret);
```

### switch-case结构

```
switch (表达式) {
    case 值1:语句1;break;
    case 值2:语句2;break;
    case 值3:语句3;break;
    default:语句4;
}
```

switch比else if结构更加简洁清晰，使程序可读性更强，效率更高。

```
switch(x){
case 1:y="星期一";    break;
case 2:y="星期二";    break;
case 3:y="星期三";    break;
case 4:y="星期四";    break;
case 5:y="星期五";    break;
case 6:y="星期六";    break;
case 7:y="星期日";    break;
default: y="未定义";         //如果前面都不执行就执行default
}
```

switch中的case子句通常都会加break语句，否则程序会继续执行后续case中的语句。

## 循环结构

### for循环

```
语法规则：

    for(初始表达式;条件表达式;自增或自减)
    {
         执行语句
         ...
    }
```

功能说明：实现条件循环，当条件成立时，执行语句，否则跳出循环体

```
for (var i=0;i<10;i++) {
  console.log(i);   //如果i<10这个条件成立，就执行console.log，否则跳出循环
}
```

**for循环的另一种形式**

```
for( 变量 in 数组或对象)
    {
        执行语句
        ...
    }
```

### while循环

```
语法规则：

while (条件){
    语句1；
    ...
}
```

功能说明：运行功能和for类似，当条件成立循环执行语句花括号{}内的语句，否则跳出循环；同样支持continue与break语句。

```
var i = 0;
while (i < 10) {
  console.log(i);
  i++;
}
```

### 异常处理

```
try {
    //这段代码从上往下运行，其中任何一个语句抛出异常该代码块就结束运行
}
catch (e) {
    // 如果try代码块中抛出了异常，catch代码块中的代码就会被执行。
    //e是一个局部变量，用来指向Error对象或者其他抛出的对象
}
finally {
     //无论try中代码是否有异常抛出（甚至是try代码块中有return语句），finally代码块中始终会被执行。
}
```

**主动抛出异常 throw Error('...')**

# 函数

## 函数的定义

JavaScript中的函数和Python中的非常类似，只是定义方式有点区别。

```
function 函数名 (参数){
	函数体;
	return 返回值;
}
```

功能说明：

可以使用变量、常量或表达式作为函数调用的参数
函数由关键字function定义
函数名的定义规则与标识符一致，大小写是敏感的
返回值必须使用return
Function 类可以表示开发者定义的任何函数。

用 Function 类直接创建函数的语法

```
var 函数名 = new Function("参数1","参数n","function_body");
```

虽然由于字符串的关系，第二种形式写起来有些困难，但有助于理解函数只不过是一种引用类型，它们的行为与用 Function 类明确创建的函数行为是相同的。

```
function func1(name){
    alert('hello'+name);
    return 8
}

    ret=func1("timo");
    alert(ret);

var func2=new Function("name","alert(\"hello\"+name);")
func2("ali")

```

**JS的函数加载执行与Python不同，它是整体加载完才会执行，所以执行函数放在函数声明上面或下面都可以**

```
<script>
    f(); // --->OK

    function f(){
        console.log("hello")

    }

    f(); //----->OK
</script>
```

```
// 普通函数定义
function f1() {
  console.log("Hello world!");
}

// 带参数的函数定义
function f2(a, b) {
  console.log(arguments);  // 内置的arguments对象
  console.log(arguments.length);
  console.log(a, b);
}

// 带返回值的函数定义
function sum(a, b){
  return a + b;
}

// 立即执行函数
(function(a, b){
  return a + b;
})(1, 2);
```

## 属性

函数属于引用类型，所以它们也有属性和方法。
ECMAScript 定义的属性 length 声明了函数期望的参数个数。

```
console.log(func1.length)
```

## 调用

```
function func1(a,b){

    console.log(a+b);
}

    func1(1,2);   //3
    func1(1,2,3); //3
    func1(1);     //NaN
    func1();      //NaN

//只要函数名写对即可,参数怎么填都不报错.
```

```
#扩展

function a(a,b){
    alert(a+b);
}

   var a=1;
   var b=2;
   a(a,b)
```

## 内置arguments

```
function add(a,b){

        console.log(a+b);//3
        console.log(arguments.length);//2
        console.log(arguments);//[1,2]

}
add(1,2)

#arguments的用处1
function nxAdd(){
	var result=0;
	for (var num in arguments){
	result+=arguments[num]
	}
	console.log(result)
}

nxAdd(1,2,3,4,5)

#arguments的用处2

function f(a,b,c){
	if (arguments.length!=3){
	throw new Error("function f called with "+arguments.length+" arguments,but it just need 3 arguments")
	}
	else {
		alert("success!")
	}
}

f(1,2,3,4,5)
```

## 匿名函数

```
// 匿名函数
var func = function(arg){
	return "tony";
}

// 匿名函数的应用
(function(){
	alert("tony");
} )()

(function(arg){
console.log(arg);
})('123')
```

## 全局变量和局部变量

**局部变量**：

在JavaScript函数内部声明的变量（使用 var）是局部变量，所以只能在函数内部访问它（该变量的作用域是函数内部）。只要函数运行完毕，本地变量就会被删除。

**全局变量：**

在函数外声明的变量是*全局*变量，网页上的所有脚本和函数都能访问它。

**变量生存周期：**

JavaScript变量的生命期从它们被声明的时间开始。

局部变量会在函数运行以后被删除。

全局变量会在页面关闭后被删除。

## 作用域

首先在函数内部查找变量，找不到则到外层函数查找，逐步找到最外层。

```
var city = "BeiJing";
function f() {
  var city = "ShangHai";
  function inner(){
    var city = "ShenZhen";
    console.log(city);
  }
  inner();
}

f();  //输出结果是？
```

```
var city = "BeiJing";
function Bar() {
  console.log(city);
}
function f() {
  var city = "ShangHai";
  return Bar;
}
var ret = f();
ret();  // 打印结果是？
```

闭包

```
var city = "BeiJing";
function f(){
    var city = "ShangHai";
    function inner(){
        console.log(city);
    }
    return inner;
}
var ret = f();
ret();
```

# 词法分析

JavaScript中在调用函数的那一瞬间，会先进行词法分析。

**词法分析的过程：**

当函数调用的前一瞬间，会先形成一个激活对象：Avtive Object（AO），并会分析以下3个方面：

1:函数参数，如果有，则将此参数赋值给AO，且值为undefined。如果没有，则不做任何操作。
2:函数局部变量，如果AO上有同名的值，则不做任何操作。如果没有，则将此变量赋值给AO，并且值为undefined。
3:函数声明，如果AO上有，则会将AO上的对象覆盖。如果没有，则不做任何操作。

函数内部无论是使用参数还是使用局部变量都到AO上找。

```
var age = 18;
function foo(){
  console.log(age);
  var age = 22;
  console.log(age);
}
foo();  // 问：执行foo()之后的结果是？
```

```
var age = 18;
function foo(){
  console.log(age);
  var age = 22;
  console.log(age);
  function age(){
    console.log("呵呵");
  }
  console.log(age);
}
foo();  // 执行后的结果是？
```

```
词法分析过程：
1、分析参数，有一个参数，形成一个 AO.age=undefine;
2、分析变量声明，有一个 var age, 发现 AO 上面已经有一个 AO.age，因此不做任何处理
3、分析函数声明，有一个 function age(){...} 声明， 则把原有的 age 覆盖成 AO.age=function(){...};

最终，AO上的属性只有一个age，并且值为一个函数声明

执行过程：
注意：执行过程中所有的值都是从AO对象上去寻找

1、执行第一个 console.log(age) 时，此时的 AO.age 是一个函数，所以第一个输出的一个函数
2、这句 var age=22; 是对 AO.age 的属性赋值， 此时AO.age=22 ，所以在第二个输出的是 2
3、同理第三个输出的还是22, 因为中间再没有改变age值的语句了
```

# 对象和方法

在JavaScript中除了null和undefined以外其他的数据类型都被定义成了对象，也可以用创建对象的方法定义变量，String、Number、Math、Array、Date、RegExp都是JavaScript中重要的内置对象，在JavaScript程序大多数功能都是基于对象实现的。在JavaScript中，对象是拥有属性和方法的数据。

```
<script language="javascript">
var aa=Number.MAX_VALUE; 
//利用数字对象获取可表示最大数
var bb=new String("hello JavaScript"); 
//创建字符串对象
var cc=new Date();
//创建日期对象
var dd=new Array("星期一","星期二","星期三","星期四"); 
//数组对象
</script>
```

注意var s1 = "abc"和var s2 = new String("abc")的区别：typeof s1 --> string而 typeof s2 --> Object

| 类型   | 内置对象     | 介绍      |
| :--- | -------- | :------ |
| 数据对象 | Number   | 数字对象    |
|      | String   | 字符串对象   |
|      | Boolean  | 布尔值对象   |
| 组和对象 | Array    | 数组对象    |
|      | Math     | 数学对象    |
|      | Date     | 日期对象    |
| 高级对象 | Object   | 自定义对象   |
|      | Error    | 错误对象    |
|      | Function | 函数对象    |
|      | RegExp   | 正则表达式对象 |
|      | Global   | 全局对象    |







