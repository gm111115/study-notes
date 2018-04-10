## MVC模型:jack_o_lantern:

MVC作为一个概念已经存在很长时间了，但是自从Internet出现以来，它已经经历了指数级的增长，因为它是设计客户机-服务器应用程序的最佳方式。所有最好的web框架都是围绕MVC概念构建的。冒着爆发战争的危险，如果你没有使用MVC设计web应用程序，那么你做错了。

作为一个概念，MVC设计模式简单易懂

​	The model(M)——数据的模型或表现

​	它不是实际的数据，而是一个数据接口。该模型允许你从数据库提取数据，且不需要了解底层数据库的复杂性。该模型通常还提供了一个带有数据库的抽象层，这样你就可以在多个数据库中使用相同的模型。

​	The view(V)——是你所看到的，是模型的表示层

​	在你的电脑上，视图是你在浏览器看到的Web应用程序或桌面应用程序的UI，视图还提供了一个收集用户输入的接口

​	The controller(C)——控制模型与视图之间的信息流

​	它使用编程逻辑来决定通过模型从数据库中提取什么信息，以及传递给视图的信息。它还通过视图和实现业务逻辑从用户那里获取信息：要么通过更改视图，要么通过模型修改数据，或者两者兼而有之。

## MTV框架:jack_o_lantern:

Django紧跟MVC模式，但是它在实现中使用了自己的逻辑。因为“C”是由框架本身来处理的，而Django中的大部分兴奋发生在模型、模板和视图中，Django通常被称为MTV框架。

在MTV发展模式中

​	M代表“Model”——数据访问层

​	这一层包含了关于数据的任何内容:如何访问它，如何验证它，它有哪些行为，以及数据之间的关系。

​	T代表“Template”——表示层

​	这一层包含与显示相关的决策：如何在Web页面或其他类型的文档中显示某些内容

​	V代表“View”——业务逻辑层

​	该层包含访问模型的逻辑，并将其提交给适当的模板。你可以把它看作是模型和模板之间的桥梁。

Django的视图更像MVC中的控制器，而MVC视图实际上是Django中的一个模板。