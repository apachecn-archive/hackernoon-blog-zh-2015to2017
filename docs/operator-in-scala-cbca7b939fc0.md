# | > Scala 中的运算符

> 原文：<https://medium.com/hackernoon/operator-in-scala-cbca7b939fc0>

在本周早些时候的一次代码交流中，一位同事在我的代码中看到这个*奇怪的*符号，他马上问这是什么。他似乎很惊讶地发现了 **F#** 拥有的管道转发运算符( **| >** )。

我的朋友正在学习 **Scala** ，他想在上面使用 **| >** ，Scala 缺少的一个构造。让我们看看如何将这个构造添加到每个 **Scala** 对象。

# 操作组合

使用 **| >** 可以非常容易地编写函数。代码变得更容易编写和被他人理解。

让我们看一个例子:

我们能不能利用 **| >** 这样这篇作文就更好写了？嗯，我们可以这样写:

我们刚刚重新定义了 **s** ,因此我们不再使用嵌套的函数调用，而是将一个函数应用到一个对象，然后是另一个对象，以此类推，线性进行。

我不知道在 **Scala** 中加入这样的东西是否有意义，但我们可以轻松实现它。

# Scala 中的管道运算符

我们来看看 **F#** 是如何定义 **| >** 的。

我们可以在 **Scala 中模仿同样的功能，**让我们看看如何实现:

我们已经定义了一个类 **Pipe** ，它接收类型 **A** 的值 **a** ，因此我们可以在调用方法 **| >** 时将函数 **f** 应用于 **a** 。

我们还定义了一个对象 **PipeOps** 来完成我们想要的任何*对象*到**管道**的*隐式转换。请看看文章[c#开发者 Scala 中的隐式转换](/@anicolaspp/implicit-conversions-in-scala-for-c-developers-92ea6c7902fa#.so89cekhv)，了解更多关于*隐式*的信息。*

一旦定义了这个，我们就可以在任何对象中使用 **| >** 。让我们在实践中看到它。

***原写法后增加:*** 定义管道的新方式是

***原文写到此处结束后添加。***

在这里，我们将 **5** 转换为**管道(5)** ，然后我们将传递的函数 **f: x = > x + 1** 应用于它。 **Scala** *隐式*在这个过程中帮助很大。

# 地图

让我们看看如何定义一个**映射**函数。

**map** 将函数 **f** 应用于**项**中的每一项。这个签名有点令人不安，因为通常我们会将 **f** 作为第二个参数，将 **items** 作为第一个参数，以便利用一些 **Scala** 语法糖。但是，这并没有错，只是另外一种定义**地图**的方式。

我们可以通过执行以下操作来调用**地图**:

让我们看另一个例子，它有各种各样的 **| >** 操作符。

注意我们是如何定义**正方形**的。它由**过滤器**和**贴图**使用 **| >** 操作符合成。如果我们不得不使用 **| >** 在不使用的情况下完成这个*，代码应该如下所示:*

同样，这不是我们通常在 **Scala** 中定义这类函数的方式，但本质上是一样的。

让我们比较一下我们当前的定义和另一种方式，后者对 Scala 语言来说更自然。

# 结论

我们已经看到 **Scala** 如何组合函数，以及 **F#** 中如何使用 **| >** 组合函数。我们还看到了如何在 **Scala** 中实现 **| >** 操作符，并比较了我们如何通过使用或不使用管道转发操作符来定义这些函数。我不确定人们是否真的在使用 **| >** ，因为 **Scala** 有另一个构造函数和代码样式来实现另一组可能性，然而，我们仍然可以使用 **| >** 及其好处。

希望这篇文章对你有用，如果你喜欢它，请推荐它(**绿心**)，这样其他人也能从中受益。

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 要了解更多信息，[请阅读我们的“关于”页面](https://goo.gl/4ofytp) , [喜欢/在脸书给我们发消息](http://bit.ly/HackernoonFB)，或者简单地，[发推文/DM @HackerNoon。](https://goo.gl/k7XYbx)
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！