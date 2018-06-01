# BOM对象

BOM（Browser Object Model）是指浏览器对象模型，它使 JavaScript 有能力与浏览器进行“对话”。

## window对象

window对象是客户端JavaScript最高层对象之一，由于window对象是其它大部分对象的共同祖先在调用window对象的方法和属性时，可以省略window对象的引用。如：window.document.write()可以简写成document.write()

所有JavaScript全局对象、函数以及变量均自动成为window对象的成员，全局变量是window对象的属性，全局函数是window对象的方法。

没有应用于window对象的标准，但所有浏览器都支持window对象。

概念上讲：一个html文档对应一个window对象

功能上讲：控制浏览器窗口的

使用上讲：window对象不需要创建对象，直接使用即可

常用的Window方法：

- window.innerHeight - 浏览器窗口的内部高度
- window.innerWidth - 浏览器窗口的内部宽度
- window.open() - 打开新窗口
- window.close() - 关闭当前窗口

### window对象方法

#### navigator对象

浏览器对象，通过这个对象可以判定用户所使用的浏览器，包含了浏览器相关信息

```
navigator.appName　　// Web浏览器全称
navigator.appVersion　　// Web浏览器厂商和版本的详细字符串
navigator.userAgent　　// 客户端绝大部分信息
navigator.platform　　　// 浏览器运行所在的操作系统
```

#### screen对象

屏幕对象，不常用。

一些属性：

- screen.availWidth - 可用的屏幕宽度
- screen.availHeight - 可用的屏幕高度

#### history对象

浏览历史对象，包含了用户当前页面的浏览历史，但我们无法查看具体的地址，可以简单的用来前进或后退一个页面

```
history.forward()  // 前进一页
history.back()  // 后退一页
```

#### location对象

用于获得当前页面的URL，并把浏览器重定向到新的页面

常用属性和方法

```
location.href  获取URL
location.href="URL" // 跳转到指定页面
location.reload() 重新加载页面
```

#### window常用方法

```
alert()            显示带有一段消息和一个确认按钮的警告框。
confirm()          显示带有一段消息以及确认按钮和取消按钮的对话框。
prompt()           显示可提示用户输入的对话框。

open()             打开一个新的浏览器窗口或查找一个已命名的窗口。
close()            关闭浏览器窗口。

setInterval()      按照指定的周期（以毫秒计）来调用函数或计算表达式。
clearInterval()    取消由 setInterval() 设置的 timeout。
setTimeout()       在指定的毫秒数后调用函数或计算表达式。
clearTimeout()     取消由 setTimeout() 方法设置的 timeout。
scrollTo()         把内容滚动到指定的坐标。
```

##### 弹出框

可以在 JavaScript 中创建三种消息框：警告框、确认框、提示框。

警告框经常用于确保用户可以得到某些信息。

当警告框出现后，用户需要点击确定按钮才能继续进行操作。

```
alert("你看到了吗？");
```

确认框用于使用户可以验证或者接受某些信息。

当确认框出现后，用户需要点击确定或者取消按钮才能继续进行操作。

如果用户点击确认，那么返回值为 true。如果用户点击取消，那么返回值为 false。

```
confirm("你确定吗？")
```

提示框经常用于提示用户在进入页面前输入某个值。

当提示框出现后，用户需要输入某个值，然后点击确认或取消按钮才能继续操纵。

如果用户点击确认，那么返回值为输入的值。如果用户点击取消，那么返回值为 null。

```
prompt("请在下方输入","你的答案")
```

##### 计时相关

通过使用 JavaScript，我们可以在一定时间间隔之后来执行代码，而不是在函数被调用后立即执行。我们称之为计时事件。

**setTimeout() **

```
#语法
var t=setTimeout("JS语句",毫秒)
```

setTimeout() 方法会返回某个值。在上面的语句中，值被储存在名为 t 的变量中。假如你希望取消这个 setTimeout()，你可以使用这个变量名来指定它。

setTimeout() 的第一个参数是含有 JavaScript 语句的字符串。这个语句可能诸如 "alert('5 seconds!')"，或者对函数的调用，诸如 alertMsg()"。

第二个参数指示从当前起多少毫秒后执行第一个参数（1000 毫秒等于一秒）。

**clearTimeout()**

```
#语法
clearTimeout(setTimeout_variable)
```

```
// 在指定时间之后执行一次相应函数
var timer = setTimeout(function(){alert(123);}, 3000)
// 取消setTimeout设置
clearTimeout(timer);
```

**setInterval()**

setInterval() 方法可按照指定的周期（以毫秒计）来调用函数或计算表达式。

setInterval() 方法会不停地调用函数，直到 clearInterval() 被调用或窗口被关闭。由 setInterval() 返回的 ID 值可用作 clearInterval() 方法的参数。

```
#语法
setInterval("JS语句",时间间隔)
```

返回值

一个可以传递给 Window.clearInterval() 从而取消对 code 的周期性执行的值。

**clearInterval()**

clearInterval() 方法可取消由 setInterval() 设置的 timeout。

clearInterval() 方法的参数必须是由 setInterval() 返回的 ID 值。

```
#语法
clearInterval(setinterval返回的ID值)
```

```
/ 每隔一段时间就执行一次相应函数
var timer = setInterval(function(){console.log(123);}, 3000)
// 取消setInterval设置
clearInterval(timer);
```

```
#定时器

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="x-ua-compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>定时器</title>
  <script>
    var intervalId;

    function f() {
      var timeStr = (new Date()).toLocaleString();
      var inputEle = document.getElementById("i1");
      inputEle.value = timeStr;
    }

    function start() {
      f();
      if (intervalId === undefined) {
        intervalId = setInterval(f, 1000);
      }
    }
    function end() {
      clearInterval(intervalId);
      intervalId = undefined;
    }

  </script>
</head>
<body>

<input type="text" id="i1">
<input type="button" value="开始" id="start" onclick="start();">
<input type="button" value="结束" id="end" onclick="end();">
</body>
</html>
```

# DOM对象

DOM（Document Object Model）是一套对文档的内容进行抽象和概念化的方法。 

当网页被加载时，浏览器会创建页面的文档对象模型（Document Object Model）。

HTML DOM 定义了访问和操作HTML文档的标准方法。

HTML DOM 把 HTML 文档呈现为带有元素、属性和文本的树结构（节点树)。

![img](https://images2015.cnblogs.com/blog/877318/201705/877318-20170524162619154-241270145.png)

DOM树是为了展示文档中各个对象之间的关系，用于对象的导航。

## DOM节点

### 节点类型

DOM标准规定HTML文档中的每个成分都是一个节点(node)：

- 文档节点(document对象)：代表整个文档
- 元素节点(element 对象)：代表一个元素（标签）
- 文本节点(text对象)：代表元素（标签）中的文本
- 属性节点(attribute对象)：代表一个属性，元素（标签）才有属性
- 注释是注释节点(comment对象)　

JavaScript 可以通过DOM创建动态的 HTML：

- JavaScript 能够改变页面中的所有 HTML 元素
- JavaScript 能够改变页面中的所有 HTML 属性
- JavaScript 能够改变页面中的所有 CSS 样式
- JavaScript 能够对页面中的所有事件做出反应

![img](https://images2015.cnblogs.com/blog/877318/201705/877318-20170524181750638-251706028.png)

**其中，document与element节点是重点。**

## 节点关系



