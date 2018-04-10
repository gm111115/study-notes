# CSS介绍🎃

**CSS**(Cascading Style Sheet，层叠样式表)定义如何显示HTML元素。

当浏览器读到一个样式表，它就会按照这个样式表来对文档进行格式化（渲染）。

# CSS语法:jack_o_lantern:

每个CSS样式由两个组成部分：选择器和声明。声明又包括属性和属性值。每个声明之后用分号结束。

![img](https://images2017.cnblogs.com/blog/867021/201712/867021-20171215115756808-909989248.png)

## CSS注释

```
/*这是注释*/
```

# 引入方式:jack_o_lantern:

## 行内样式

行内式是在标记的style属性中设定CSS样式。不推荐大规模使用。

```
<p style="color: red">Hello world.</p>
```

## 内部样式

嵌入式是将CSS样式集中写在网页的<head></head>标签对的<style></style>标签对中

```
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        p{
            background-color: #eee;
        }
    </style>
</head>
```

## 外部样式

### 链接式

将css写在一个单独的文件中，然后在HTML页面进行引入即可。推荐使用此方式。

```
<link href="mystyle.css" rel="stylesheet" type="text/css"/>
```

### 导入式

导入式使用CSS规则引入外部CSS文件，<style>标记也是写在<head>标记中    

```
<style type="text/css">
 
          @import"mystyle.css";    #此处要注意.css文件的路径
 
</style>　
```

注意：

​	 导入式会在整个网页装载完后再装载CSS文件，因此这就导致了一个问题，如果网页比较大则会儿出现先显示无样式的页面，闪烁一下之后，再出现网页的样式。这是导入式固有的一个缺陷。使用链接式时与导入式不同的是它会以网页文件主体装载前装载CSS文件，因此显示出来的网页从一开始就是带样式的效果的，它不会象导入式那样先显示无样式的网页，然后再显示有样式的网页，这是链接式的优点。

# CSS选择器:jack_o_lantern:

## 基本选择器

![img](https://images2015.cnblogs.com/blog/877318/201705/877318-20170517132804978-1482408610.png)

注意：

​	样式类名不要用数字开头(有的浏览器不认识)。

​	标签中的class属性如果有多个，要用空格分隔。

## 组合选择器

### 后代选择器

```
/*li内部的a标签设置字体颜色*/
li a {
  color: green;
}
```

### 子元素选择器

```
/*选择所有父级是 <div> 元素的 <p> 元素*/
div>p {
  font-family: "Arial Black", arial-black, cursive;
}
```

### 毗邻选择器

```
/*选择所有紧接着<div>元素之后的<p>元素*/
div+p {
  margin: 5px;
}
```

### 兄弟选择器

```
/*i1后面所有的兄弟p标签*/
#i1~p {
  border: 2px solid royalblue;
}
```

关于标签嵌套：

​	一般，块级元素可以包含内联元素或某些块级元素，但内联元素不能包含块级元素，它只能包含其它内联元素。需要注意的是，p标签不能包含块级标签。

## 属性选择器

```
#常用属性选择器

/*用于选取带有指定属性的元素。*/
p[title] {
  color: red;
}
/*用于选取带有指定属性和值的元素。*/
p[title="213"] {
  color: green;
}
```

```
#不常用属性选择器

/*找到所有title属性以hello开头的元素*/
[title^="hello"] {
  color: red;
}

/*找到所有title属性以hello结尾的元素*/
[title$="hello"] {
  color: yellow;
}

/*找到所有title属性中包含（字符串包含）hello的元素*/
[title*="hello"] {
  color: red;
}

/*找到所有title属性(有多个值或值以空格分割)中有一个值为hello的元素：*/
[title~="hello"] {
  color: green;
}
```

## 伪类选择器

伪类指的是标签的不同状态

伪类选择器格式:  标签:伪类名称{ css代码; }

anchor伪类：专用于控制链接的显示效果

```
a标签 ==> 点过状态 没有点过的状态 鼠标悬浮状态 激活状态

a:link（没有接触过的链接）,用于定义了链接的常规状态。

a:hover（鼠标放在链接上的状态）,用于产生视觉效果。
        
a:visited（访问过的链接）,用于阅读文章，能清楚的判断已经访问过的链接。

a:active（在链接上按下鼠标时的状态）,用于表现鼠标按下时的链接状

/* 未访问的链接 */
a:link {color: #FF0000} 

 /* 已访问的链接 */
a:visited {color: #00FF00}

/* 鼠标移动到链接上 */
a:hover {color: #FF00FF} 

/* 选定的链接 */ 
a:active {color: #0000FF}

/*input输入框获取焦点时样式*/
input:focus {
  outline: none;
  background-color: #eee;
  }
```

## 伪元素选择器

### first-letter

常用的给首字母设置特殊样式

```
p:first-letter {
  font-size: 48px;
  color: red;
}
```

### before

```
/*在每个<p>元素之前插入内容*/
p:before {
  content:"*";
  color:red;
}
```

### after

```
/*在每个<p>元素之后插入内容*/
p:after {
  content:"[?]";
  color:blue;
} 
```

**before和after多用于清除浮动。**

## 分组和嵌套

### 分组

当多个元素的样式相同的时候，我们没有必要重复地为每个元素都设置样式，我们可以通过在多个选择器之间使用逗号分隔的分组选择器来统一设置元素样式。 

```
div, p {
  color: red;
}
```

上面代码为div标签和p标签统一设置字体为红色。

通常，我们会分两行来写，更清晰

```
div,
p {
  color: red;
}
```

###	嵌套

多种选择器可以混合起来使用，比如：.c1类内部所有p标签设置字体颜色为红色。

```
.c1 p {
  color: red;
}
```

# 选择器的优先级:jack_o_lantern:

## CSS继承

继承是CSS的一个主要特征，它是依赖于祖先-后代的关系的。继承是一种机制，它允许样式不仅可以应用于某个特定的元素，还可以应用于它的后代。例如一个body定义了的字体颜色值也会应用到段落的文本中。

```
body {
  color: red;
}

<p>hello world！</p>
```

这段文字都继承了由body {color:red;}样式定义的颜色。然而CSS继承性的权重是非常低的，是比普通元素的权重还要低的0。

我们只要给对应的标签设置字体颜色就可覆盖掉它继承的样式。由此可见：任何显示申明的规则都可以覆盖其继承样式。　

```
p {
  color: green;
}
```

此外，继承是CSS重要的一部分，我们甚至不用去考虑它为什么能够这样，但CSS继承也是有限制的。有一些属性不能被继承，如：border, margin, padding, background等。

```
div{
  border:1px solid #222
}

<div>hello 
	<p>world</p>
</div>
```

## CSS的优先级

所谓CSS优先级，即是指CSS样式在浏览器中被解析的先后顺序。

样式表中的特殊性描述了不同规则的相对权重，它的基本规则是：

![img](https://images2018.cnblogs.com/blog/867021/201803/867021-20180305155201408-1680872107.png)

按这些规则将数字符串逐位相加，就得到最终的权重，然后在比较取舍时按照从左到右的顺序逐位比较。

```
1、文内的样式优先级为1,0,0,0，所以始终高于外部定义。
   
2、有!important声明的规则高于一切。

3、如果!important声明冲突，则比较优先权。

4、如果优先权一样，则按照在源码中出现的顺序决定，后来者居上。

5、由继承而得到的样式没有specificity的计算，它低于一切其它规则(比如全局选择符*定义的规则)。
```

虽然通过添加 !important方式可以强制让样式生效，但并不推荐使用。因为如果过多的使用!important会使样式文件混乱不易维护。

# CSS属性操作:jack_o_lantern:

## 文本属性

### 文字字体

font-family可以把多个字体名称作为一个“回退”系统来保存。如果浏览器不支持第一个字体，则会尝试下一个。浏览器会使用它可识别的第一个值。

```
body {
  font-family: "Microsoft Yahei", "微软雅黑", "Arial", sans-serif
}
```

### 字体大小

```
p {
  font-size: 14px;
}
```

如果设置成inherit表示继承父元素的字体大小值。

### 字重

font-weight用来设置字体的字重（粗细）。

| 值       | 描述                              |
| ------- | ------------------------------- |
| normal  | 默认值，标准粗细                        |
| bold    | 粗体                              |
| bolder  | 更粗                              |
| lighter | 更细                              |
| 100~900 | 设置具体粗细，400等同于normal，而700等同于bold |
| inherit | 继承父元素字体的粗细值                     |

### 文本颜色

颜色属性被用来设置文字的颜色。

颜色是通过CSS最经常的指定：

- 十六进制值 - 如: **＃**FF0000
- 一个RGB值 - 如: RGB(255,0,0)
- 颜色的名称 - 如:  red

还有rgba(255,0,0,0.3)，第四个值为alpha, 指定了色彩的透明度/不透明度，它的范围为0.0到1.0之间。

### 文字装饰

text-decoration 属性用来给文字添加特殊效果。

| 值            | 描述                         |
| ------------ | -------------------------- |
| none         | 默认。定义标准的文本。                |
| underline    | 定义文本下的一条线。                 |
| overline     | 定义文本上的一条线。                 |
| line-through | 定义穿过文本下的一条线。               |
| inherit      | 继承父元素的text-decoration属性的值。 |

常用的为去掉a标签默认的自划线

```
a {
  text-decoration: none;
}
```

### 水平对齐方式

text-align 属性规定元素中的文本的水平对齐方式。

- left      把文本排列到左边。默认值：由浏览器决定。
- right    把文本排列到右边。
- center 把文本排列到中间。
- justify 实现两端对齐文本效果。

### 首行缩进

将段落的第一行缩进 32像素

```
p {
  text-indent: 32px;
}
```

### 文本其他属性

```

line-height: 200px;   文本行高 通俗的讲，文字高度加上文字上下的空白区域的高度 50%:基于字体大小的百分比

vertical-align:－4px  设置元素内容的垂直对齐方式 ,只对行内元素有效，对块级元素无效

font-style: oblique     斜体

letter-spacing: 10px;  字母间距

word-spacing: 20px;  单词间距

text-transform: capitalize/uppercase/lowercase ; 文本转换，用于所有字句变成大写或小写字母，或每个单词的首字母大写

```

## 背景属性

```
/*背景颜色*/
background-color: red;

/*背景图片*/
background-image: url('1.jpg');

/*
 背景重复
 repeat(默认):背景图片平铺排满整个网页
 repeat-x：背景图片只在水平方向上平铺
 repeat-y：背景图片只在垂直方向上平铺
 no-repeat：背景图片不平铺
*/
background-repeat: no-repeat; 

/*背景位置*/
background-position: right top（20px 20px）;
```

支持简写

```
background:#ffffff url('1.png') no-repeat right top;
```

使用背景图片的一个常见案例就是很多网站会把很多小图标放在一张图片上，然后根据位置去显示图片。减少频繁的图片请求。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>滚动背景图</title>
    <style>
        * {
            margin: 0;
        }
        .box {
            width: 100%;
            height: 500px;
            background: url("https:图片地址自定义") no-repeat center center;
            background-attachment: fixed;
        }
        .d1 {
            height: 500px;
            background-color: tomato;
        }
        .d2 {
            height: 500px;
            background-color: steelblue;
        }
        .d3 {
            height: 500px;
            background-color: mediumorchid;
        }
    </style>
</head>
<body>
    <div class="d1"></div>
    <div class="box"></div>
    <div class="d2"></div>
    <div class="d3"></div>
</body>
</html>
```

## 边框属性

### 属性介绍

- border-width
- border-style (required)
- border-color

```
#i1 {
  border-width: 2px;
  border-style: solid;
  border-color: red;
}
```

通常使用简写方式

```
#i1 {
  border: 2px solid red;
}
```

### 边框样式

| 值      | 描述      |
| ------ | ------- |
| none   | 无边框。    |
| dotted | 点状虚线边框。 |
| dashed | 矩形虚线边框。 |
| solid  | 实线边框。   |

除了可以统一设置边框外还可以单独为某一个边框设置样式

```
#i1 {
  border-top-style:dotted;
  border-top-color: red;
  border-right-style:solid;
  border-bottom-style:dotted;
  border-left-style:none;
}
```

### border-radius

用这个属性能实现圆角边框的效果。

将border-radius设置为长或高的一半即可得到一个圆形。

```
#圆形头像

<!DOCTYPE HTML>
<html>
<head>
  <meta charset="UTF-8">
  <meta http-equiv="x-ua-compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>圆形头像</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      background-color: #eeeeee;
    }
    .header-img {
      width: 150px;
      height: 150px;
      border: 3px solid white;
      border-radius: 100%;
      overflow: hidden;
    }
    .header-img>img {
      max-width: 100%;
    }
  </style>
</head>
<body>

<div class="header-img">
  <img src="https:头像地址" alt="">
</div>

</body>
</html>
```



## display属性

用于控制HTML元素的显示效果。

| 值                      | 意义                                       |
| ---------------------- | ---------------------------------------- |
| display:"none"         | HTML文档中元素存在，但是在浏览器中不显示。一般用于配合JavaScript代码使用。 |
| display:"block"        | 内联标签设置为块级标签，默认占满整个页面宽度，如果设置了指定宽度，则会用margin填充剩下的部分。一个内联元素设置为display:block是不允许有它内部的嵌套块元素。 |
| display:"inline"       | 按行内元素显示，此时再设置元素的width、height、margin-top、margin-bottom和float属性都不会有什么影响。 |
| display:"inline-block" | 使元素同时具有行内元素和块级元素的特点。                     |

**display:"none"与visibility:hidden的区别**

visibility:hidden: 可以隐藏某个元素，但隐藏的元素仍需占用与未隐藏之前一样的空间。也就是说，该元素虽然被隐藏了，但仍然会影响布局。

display:none: 可以隐藏某个元素，且隐藏的元素不会占用任何空间。也就是说，该元素不但被隐藏了，而且该元素原本占用的空间也会从页面布局中消失。

**display:inline-block**可做列表布局，其中的类似于图片间的间隙小bug可以通过如下设置解决

```
#outer{
	border: 3px dashed;
	word-spacing: -5px;
        }
```

# CSS盒子模型:jack_o_lantern:

- **margin**:            用于控制元素与元素之间的距离；margin的最基本用途就是控制元素周围空间的间隔，从视觉角度上达到相互隔开的目的。
- **padding**:           用于控制内容与边框之间的距离；   
- **Border**(边框):     围绕在内边距和内容外的边框。
- **Content**(内容):   盒子的内容，显示文本和图像。

![img](https://images2018.cnblogs.com/blog/867021/201803/867021-20180305155247808-885981996.png)

## margin外边距

```
.margin-test {
  margin-top:5px;
  margin-right:10px;
  margin-bottom:15px;
  margin-left:20px;
}
```

推荐使用简写

```
.margin-test {
  margin: 5px 10px 15px 20px;
}
```

顺序：上右下左

常见居中

```
.mycenter {
  margin: 0 auto;
}
```

## padding内填充

```
.padding-test {
  padding-top: 5px;
  padding-right: 10px;
  padding-bottom: 15px;
  padding-left: 20px;
}
```

推荐使用简写

```
.padding-test {
  padding: 5px 10px 15px 20px;
}
```

顺序：上右下左

补充padding的常用简写方式：

- 提供一个，用于四边；
- 提供两个，第一个用于上－下，第二个用于左－右；
- 如果提供三个，第一个用于上，第二个用于左－右，第三个用于下；
- 提供四个参数值，将按上－右－下－左的顺序作用于四边

**body的外边距**

边框在默认情况下会定位于浏览器窗口的左上角，但是并没有紧贴着浏览器的窗口的边框，这是因为body本身也是一个盒子（外层还有html），在默认情况下，   body距离html会有若干像素的margin，具体数值因各个浏览器不尽相同，所以body中的盒子不会紧贴浏览器窗口的边框了

```
body{
    border: 1px solid;
    background-color: cadetblue;
}
```

解决方法如下

```
body{
    margin: 0;
}
```

**margin collapse（边界塌陷或者说边界重叠）**

1、兄弟div：
上面div的margin-bottom和下面div的margin-top会塌陷，也就是会取上下两者margin里最大值作为显示值

2、父子div：
if 父级div中没有border，padding，inlinecontent，子级div的margin会一直向上找，直到找到某个标签包括border，padding，inline content中的其中一个，然后按此div 进行margin

```
<!DOCTYPE html>
<html lang="en" style="padding: 0px">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>

        body{
            margin: 0px;
        }

        .div1{
            background-color: rebeccapurple;
            width: 300px;
            height: 300px;
            overflow: hidden;

        }
        .div2{
            background-color: green;
            width: 100px;
            height: 100px;
            margin-bottom: 40px;
            margin-top: 20px;
        }
        .div3{
            background-color:teal;
            width: 100px;
            height: 100px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
<div style="background-color: bisque;width: 300px;height: 300px"></div>

<div class="div1">

   <div class="div2"></div>
   <div class="div3"></div>
</div>

</body>

</html>
```

 解决方法

```
overflow: hidden;
```

# float属性:jack_o_lantern:

在 CSS 中，任何元素都可以浮动。

浮动元素会生成一个块级框，而不论它本身是何种元素。

关于浮动的两个特点：

- 浮动的框可以向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。
- 由于浮动框不在文档的普通流中，所以文档的普通流中的块框表现得就像浮动框不存在一样。

## 三种取值

left：向左浮动

right：向右浮动

none：默认值，不浮动

## 基本浮动规则

先了解一下block元素和inline元素在文档流中的排列方式。

　　block元素通常被现实为独立的一块，独占一行，多个block元素会各自新起一行，默认block元素宽度自动填满其父元素宽度。block元素可以设置width、height、margin、padding属性；

　　inline元素不会独占一行，多个相邻的行内元素会排列在同一行里，直到一行排列不下，才会新换一行，其宽度随元素的内容而变化。inline元素设置width、height属性无效

- 常见的块级元素有 div、form、table、p、pre、h1～h5、dl、ol、ul 等。
- 常见的内联元素有span、a、strong、em、label、input、select、textarea、img、br等

**所谓的文档流**，指的是元素排版布局过程中，元素会自动从左往右，从上往下的流式排列。

**脱离文档流**，也就是将元素从普通的布局排版中拿走，其他盒子在定位的时候，**会当做脱离文档流的元素不存在而进行定位**。

​      假如某个div元素A是浮动的，如果A元素上一个元素也是浮动的，那么A元素会跟随在上一个元素的后边(如果一行放不下这两个元素，那么A元素会被挤到下一行)；如果A元素上一个元素是标准流中的元素，那么A的相对垂直位置不会改变，也就是说A的顶部总是和上一个元素的底部对齐。此外，浮动的框之后的block元素元素会认为这个框不存在，但其中的文本依然会为这个元素让出位置。 浮动的框之后的inline元素，会为这个框空出位置，然后按顺序排列。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin: 0;
        }

        .r1{
            width: 300px;
            height: 100px;
            background-color: #7A77C8;
            float: left;
        }
        .r2{
            width: 200px;
            height: 200px;
            background-color: wheat;
            /*float: left;*/

        }
        .r3{
            width: 100px;
            height: 200px;
            background-color: darkgreen;
            float: left;
        }
    </style>
</head>
<body>

<div class="r1"></div>
<div class="r2"></div>
<div class="r3"></div>


</body>
</html>
```

## 非完全脱离文档流

左右结构div盒子重叠现象，一般是由于相邻两个DIV一个使用浮动一个没有使用浮动。一个使用浮动一个没有导致DIV不是在同个“平面”上，但内容不会造成覆盖现象，只有DIV形成覆盖现象。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin: 0;
        }

        .r1{
            width: 100px;
            height: 100px;
            background-color: #7A77C8;
            float: left;
        }
        .r2{
            width: 200px;
            height: 200px;
            background-color: wheat;

        }
    </style>
</head>
<body>

<div class="r1"></div>
<div class="r2">region2</div>


</body>
</html>
```

解决方法：要么都不使用浮动；要么都使用float浮动；要么对没有使用float浮动的DIV设置margin样式。

## 父级坍塌现象

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<style type="text/css">
         * {
             margin:0;padding:0;
         }
        .container{
            border:1px solid red;width:300px;
        }
        #box1{
            background-color:green;float:left;width:100px;height:100px;
        }
        #box2{
            background-color:deeppink; float:right;width:100px;height:100px; 
        }
         #box3{
             background-color:pink;height:40px;
         }
</style>
</head>
<body>

        <div class="container">
                <div id="box1">box1 向左浮动</div>
                <div id="box2">box2 向右浮动</div>
        </div>
        <div id="box3">box3</div>
</body>
</body>
</html>
```

如上：.container和box3的布局是上下结构，上图发现box3跑到了上面，与.container产生了重叠，但文本内容没有发生覆盖，只有div发生覆盖现象。这个原因是因为第一个大盒子里的子元素使用了浮动，脱离了文档流，导致.container没有被撑开。box3认为.container没有高度（未被撑开），因此跑上去了。

解决方法：

**1、固定高度**

给.container设置固定高度，一般情况下文字内容不确定多少就不能设置固定高度，所以一般不能设置“.container”高度(当然能确定内容多高，这种情况下“.container是可以设置一个高度即可解决覆盖问题。

或者给.container加一个固定高度的子div

```
<div class="container">
                <div id="box1">box1 向左浮动</div>
                <div id="box2">box2 向右浮动</div>
                <div id="empty" style="height: 100px"></div>
</div>
<div id="box3">box3</div>
```

但是这样限定固定高度会使页面操作不灵活，不推荐！

**2、清除浮动(推荐)**

clear属性规定元素的哪一侧不允许其他浮动元素。

| 值       | 描述                    |
| ------- | --------------------- |
| left    | 在左侧不允许浮动元素。           |
| right   | 在右侧不允许浮动元素。           |
| both    | 在左右两侧均不允许浮动元素。        |
| none    | 默认值。允许浮动元素出现在两侧。      |
| inherit | 规定应该从父元素继承 clear 属性的值 |

但是需要注意的是：clear属性只会对**自身**起作用，而不会影响其他元素。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin: 0;
        }

        .r1{
            width: 300px;
            height: 100px;
            background-color: #7A77C8;
            float: left;
        }
        .r2{
            width: 200px;
            height: 200px;
            background-color: wheat;
            float: left;
            clear: left;

        }
        .r3{
            width: 100px;
            height: 200px;
            background-color: darkgreen;
            float: left;
        }
    </style>
</head>
<body>

<div class="r1"></div>
<div class="r2"></div>
<div class="r3"></div>

</body>
</html>
```

把握住两点：1、元素是从上到下、从左到右依次加载的。

​                 2、clear: left;对自身起作用，一旦左边有浮动元素，即切换到下一行来保证左边元素不是浮动的，依据这一点解决父级塌陷问题。

解决父级塌陷

```
.clearfix:after {             <----在类名为“clearfix”的元素内最后面加入内容；
    content: ".";                 <----内容为“.”就是一个英文的句号而已。也可以不写。
    display: block;               <----加入的这个元素转换为块级元素。
    clear: both;                  <----清除左右两边浮动。
    visibility: hidden;           <----可见度设为隐藏。注意它和display:none;是有区别的。
                                       visibility:hidden;仍然占据空间，只是看不到而已；
    line-height: 0;               <----行高为0；
    height: 0;                    <----高度为0；
    font-size:0;                  <----字体大小为0；
    }
    
    .clearfix { *zoom:1;}         <----这是针对于IE6的，因为IE6不支持:after伪类，这个神
                                       奇的zoom:1让IE6的元素可以清除浮动来包裹内部元素。


整段代码就相当于在浮动元素后面跟了个宽高为0的空div，然后设定它clear:both来达到清除浮动的效果。
之所以用它，是因为，你不必在html文件中写入大量无意义的空标签，又能清除浮动。
<div class="head clearfix"></div>
```

简写

```
.clearfix:after {
  content: "";
  display: block;
  clear: both;
}
```

**3、overflow:hidden**

overflow：hidden的含义是超出的部分要裁切隐藏，float的元素虽然不在普通流中，但是他是浮动在普通流之上的，可以把普通流元素+浮动元素想象成一个立方体。如果没有明确设定包含容器高度的情况下，它要计算内容的全部高度才能确定在什么位置hidden，这样浮动元素的高度就要被计算进去。这样包含容器就会被撑开，清除浮动。

# overflow溢出属性:jack_o_lantern:

| 值       | 描述                           |
| ------- | ---------------------------- |
| visible | 默认值。内容不会被修剪，会呈现在元素框之外。       |
| hidden  | 内容会被修剪，并且其余内容是不可见的。          |
| scroll  | 内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容。 |
| auto    | 如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。 |
| inherit | 规定应该从父元素继承 overflow 属性的值。    |

- overflow（水平和垂直均设置）
- overflow-x（设置水平方向）
- overflow-y（设置垂直方向）

 # position(定位):jack_o_lantern:

## static

static 默认值，无定位，不能当作绝对定位的参照物，并且设置标签对象的left、top等值是不起作用的的。

## relative（相对定位）

定义：相对定位是相对于该元素在文档流中的原始位置，即以自己原始位置为参照物。有趣的是，即使设定了元素的相对定位以及偏移值，元素还占有着原来的位置，即占据文档流空间**。**对象遵循正常文档流，但将依据top，right，bottom，left等属性在正常文档流中偏移位置。而其层叠通过z-index属性定义。

注意：position：relative的一个主要用法：方便绝对定位元素找到参照物。

## absolute（绝对定位）

定义：设置为绝对定位的元素框从文档流完全删除，并相对于最近的已定位祖先元素定位，如果元素没有已定位的祖先元素，那么它的位置相对于最初的包含块（即body元素）。元素原先在正常文档流中所占的空间会关闭，就好像该元素原来不存在一样。元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框。

重点：如果父级设置了position属性，例如position:relative;，那么子元素就会以父级的左上角为原始点进行定位。这样能很好的解决自适应网站的标签偏离问题，即父级为自适应的，那我子元素就设置position:absolute;父元素设置position:relative;，然后Top、Right、Bottom、Left用百分比宽度表示。

另外，对象脱离正常文档流，使用top，right，bottom，left等属性进行绝对定位。而其层叠通过z-index属性定义。

## fixed（固定）

 fixed：对象脱离正常文档流，使用top，right，bottom，left等属性以窗口为参考点进行定位，当出现滚动条时，对象不会随着滚动。而其层叠通过z-index属性 定义。 注意点： 一个元素若设置了 position:absolute | fixed; 则该元素就不能设置float。这 是一个常识性的知识点，因为这是两个不同的流，一个是浮动流，另一个是“定位流”。但是 relative 却可以。因为它原本所占的空间仍然占据文档流。

​       在理论上，被设置为fixed的元素会被定位于浏览器窗口的一个指定坐标，不论窗口是否滚动，它都会固定在这个位置。

```
#返回顶部

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin: 0;
        }
        .back{
            background-color: wheat;
            width: 100%;
            height: 1200px;
        }
        span{
            display: inline-block;
            width: 80px;
            height: 50px;
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: rebeccapurple;
            color: white;
            text-align: center;
            line-height: 50px;

        }
    </style>
</head>
<body>


<div class="back">
    <span>返回顶部</span>
</div>
</body>
</html>
```

# z-index:jack_o_lantern:

```
#i2 {
  z-index: 999;
}
```

设置对象的层叠顺序，数值大的会覆盖在数值小的标签之上。z-index 仅能在定位元素上奏效。

```
#自定义模态框

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="x-ua-compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>自定义模态框</title>
  <style>
    .cover {
      background-color: rgba(0,0,0,0.65);
      position: fixed;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      z-index: 998;
    }

    .modal {
      background-color: white;
      position: fixed;
      width: 600px;
      height: 400px;
      left: 50%;
      top: 50%;
      margin: -200px 0 0 -300px;
      z-index: 1000;
    }
  </style>
</head>
<body>

<div class="cover"></div>
<div class="modal"></div>
</body>
</html>
```

# opacity:jack_o_lantern:

用来定义透明效果。取值范围是0~1，0是完全透明，1是完全不透明。

# Other:jack_o_lantern:

## 默认的高度和宽度问题

### 父子都是块级元素

```
<!DOCTYPE html>
<html>
<head>
    <title>fortest</title>
    <style>
        div.parent{
            width: 500px;
            height: 300px;
            background: #ccc;
        }
        div.son{
            width: 100%;
            height: 200px;
            background: green;
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="son"></div>
    </div>
</body>
</html>
```

这时，子元素设置为了父元素width的100%，那么子元素的宽度也是500px；但是如果我们把子元素的width去掉之后，就会发现子元素还是等于父元素的width。**也就是说，对于块级元素，子元素的宽度默认为父元素的100%。**

**当我们给子元素添加padding和margin时，可以发现宽度width是父元素的宽度减去子元素的margin值和padding值。**

**毫无疑问，如果去掉子元素的height，就会发先子元素的高度为0，故height是不会为100%的，**一般我们都是通过添加内容（子元素）将父元素撑起来。

### 父：块级元素  子：内联元素

如果内联元素是不可替换元素（除img，input以外的一般元素），元素是没有办法设置宽度的，也就谈不上100%的问题了。 即内联元素必须依靠其内部的内容才能撑开。

如果内联元素是可替换元素（img，input，本身可以设置长和宽），**不管怎么设置父元素的宽度和高度，而不设置img的宽和高时，img总是表现为其原始的宽和高。**

```
<!DOCTYPE html>
<html>
<head>
    <title>...</title>
    <style>
        div.parent{
            width: 500px;
            height: 300px;
            background: #ccc;
        }
        img{
            height: 100px;
            background: green;
        }
    </style>
</head>
<body>
    <div class="parent">
        <img class="son" src="s1.jpg"></img>
    </div>
</body>
</html>
```

由此我们可以发现，虽然没有设置宽度，但是表现在浏览器上为160px，它并没有继承父元素的100%得到500px，而是根据既定的高度来等比例缩小宽度。  同样， 如果只设置width，那么height也会等比例改变。   如果我们把img的width设置为100%，就可以发现其宽度这时就和父元素的宽度一致了。而我们一般的做法时，首先确定img的父元素的宽度和高度，然后再将img的宽度和高度设置位100%，这样，图片就能铺满父元素了。