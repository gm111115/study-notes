# CSS介绍

**CSS**(Cascading Style Sheet，层叠样式表)定义如何显示HTML元素。

当浏览器读到一个样式表，它就会按照这个样式表来对文档进行格式化（渲染）。

# CSS语法

每个CSS样式由两个组成部分：选择器和声明。声明又包括属性和属性值。每个声明之后用分号结束。

![img](https://images2017.cnblogs.com/blog/867021/201712/867021-20171215115756808-909989248.png)

## CSS注释

```
/*这是注释*/
```

# 引入方式

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

# CSS选择器

