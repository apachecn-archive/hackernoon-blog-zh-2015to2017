# 现实世界尼姆历险记

> 原文：<https://medium.com/hackernoon/read-world-nim-adventures-5dc85ac7d9d6>

这个周末，我在 Nim 开始了我的第一个项目，并想与社区分享我的经验。这包括那些对 Nim 好奇但还没有尝试过的人，以及更多类似的人。所以，先说后面的故事吧！

# 背景

我是计算机科学学士。匈牙利学生德布勒森(Debrecen)，主要是 Java 和 JavaScript 方面的经验，并有一些函数式[编程](https://hackernoon.com/tagged/programming)(准确地说是 F#)的背景。

这些可以被看作是主流语言，拥有优秀的工具和大量的第三方库。基本上，你能想到的每个任务都有一个库。在大多数情况下，不只是一个库，而是至少有几个库。除了实际的语言特性之外，可用的库和工具在比较语言时也起着至关重要的作用。我稍后会谈到这一点，但我想先从它开始。

## 尼姆是什么？

Nim 是一种通用的静态类型和编译的编程语言，具有强大的元编程支持。它的速度非常快(编译和执行都非常快)，并且有一个漂亮、干净的语法。该语言竭尽全力通过外部函数接口支持与其他语言(例如 C 或 C++)的互操作性。这样，尽管 Nim 有自己的包管理器，但人们可以很容易地利用用其他语言编写的库。

这只是一个简短的介绍，我还可以写更多关于 Nim 的内容，但如果您查看官方网站会更好:

[](https://nim-lang.org/) [## 程序设计语言

### Nim 编程语言是一种简洁、快速的编程语言，可以编译成 C、C++和 JavaScript。

nim-lang.org](https://nim-lang.org/) 

## 真实世界

RealWorld 是 Thinkster 的一个相当新的项目。它旨在向您展示如何使用不同的前端和后端编写完全相同的应用程序(实际上是一个中型克隆)。这些都遵循相同的 API 规范，因此可以自由混合和匹配。更多信息请点击此处:

[](/@ericsimons/introducing-realworld-6016654d36b5) [## 介绍真实世界🙌

### 🏅由 React、Angular、Node、Django 等提供支持的示例性 fullstack 博客应用——它类似于 TodoMVC，但用于…

medium.com](/@ericsimons/introducing-realworld-6016654d36b5) 

这提供了一个很好的方式来比较各种平台，并了解您选择的技术的最佳实践。

任何人都可以贡献，但只有经验丰富的开发人员被建议这样做。RealWorld 非常强调可读性和使用公认的最佳实践。没有经验的开发人员可能无法产生遵循这些原则的实现。

# 周末黑客马拉松

## 动机

接近大学学习的尾声时，我有点被更重要的事情淹没了，但我想把这作为周末黑客马拉松的挑战。正如我以前写的，我已经很久没有真正使用过母语了(除了作为一名计算机图形学助教和使用 C 语言)。尼姆的特征确实吸引了我，我想尝试一下。当然，我写过强制的 *Hello Word & co* 程序，但那不是认真的试驾。然而，想出小规模的项目对我来说并不容易，这就是为什么我立即被现实世界的想法所吸引。

尽管如此，我不应该仅仅因为这个原因就开始官方的 Nim 实现。"*我如何在缺乏经验的情况下运用最佳实践*？"我问自己。这个问题的答案是我项目的真正动力:“*目前还没有最佳实践。*”。因此，我依赖我的直觉和 Java/JavaScript 经验。

GitHub 上的实现位于:

[](https://github.com/battila7/nim-realworld-example-app) [## battila 7/nim-real world-example-app

### nim-realworld-example-app -现实世界示例应用的 nim 实现

github.com](https://github.com/battila7/nim-realworld-example-app) 

## 环境

我直接从官方网站下载了 Nim 的最新发布版本。编译器是 nim 0.16.0，包管理器是 nimble 0.8.2。开发机器运行的是 64 位的 Ubuntu 15.10。

## 选择框架

人们可以直接使用 Java 中的 Servlets，或者在 node 中编写普通的 http 代码。但事实就是这样，在大多数情况下，我们选择一个框架来为我们做繁重的工作。在 Java 中，我一直分别在 node 中使用 Spring/Spark 和 hapi/express。当然，有大量的框架，但在我看来，这些是一些流行的。

Nim 提供了同样的东西:我们可以选择普通的(异步服务器)或者选择合适的工具。然而我们只能找到两个 web 框架， [Jester](https://github.com/dom96/jester) 和 [Rosencrantz](https://github.com/andreaferretti/rosencrantz) 。

Jester 是更受欢迎的选择，由 Nim 核心贡献者张秀坤·皮切塔(他写了优秀的《Nim in Action》一书)积极开发。似乎是个明智的选择，但我还是和罗森格兰兹达成了和解。据我所知，Jester 不会让我拆分我的路由定义，它们必须坐在同一个文件中(见[本期](https://github.com/dom96/jester/issues/51))。这可以看作是一个优点，但是当开发一个更大甚至中等规模的应用程序时，这显然是没有好处的。Rosencrantz 的组合方法及其更广泛的现成特性也帮助了我的决定。

# 最佳实践

本文的本质是启动一个社区进程，该进程可以产生一组关于 Rosencrantz 和一般 Nim 代码的一致认可的最佳实践，并且可以进入——目前是简短的— [Nim 风格指南](https://nim-lang.org/docs/nep1.html)。

## 明智地进口

我们导入其他模块的方式对于使我们的代码可读至关重要。我想到了以下几点:

*   首先使用`from module import x, y, z`。这样，不同的过程和类型来自哪里总是很清楚的。对于自己编写的代码，这条规则几乎总是适用的。
*   在导入标准库，或者从**同**框架中导入大量条目时，为了简洁起见，使用裸`import`。
*   使用`except`来支持你实际使用的模块。从标准库中排除。
*   当你发现自己有很多例外，或者使用限定名时，使用`from module import nil`语句并在任何地方强制限定。
*   别名导入仅使用以前的语法:`from module as m import nil`。

## 进口订单

按照下面的顺序导入模块，这样可以清楚地知道模块来自哪里:

1.  标准库
2.  第三方软件包
3.  自写代码

## 导入垂直间距

在前面提到的部分之间放一个空行，在最后一部分之后留两个空行。

## 强调公共接口

有时一个模块的文档不足以理解它的工作方式或者它应该被利用的方式。模块的消费者只能访问它的公共接口。这些是标有出口符号的报关单。

当在一个模块中放置东西时，总是把重点放在导出的声明上。例如，导出的*进程*的前向声明应该在模块私有的*进程*之前。同样，导出的类型应该在私有类型之前，而且它们应该在不同的`type`部分声明。

## 编写您的模板/宏

不要害怕写模板或宏，而要写样板代码。虽然这在您的代码之上增加了一层间接层，但是它可以节省您的时间，如果编写正确，还可以增加代码的可读性。由于 Nim 中的元编程非常容易，任何人都可以对丑陋的问题提出干净的解决方案。

然而，编写有用和可读的模板/宏需要练习。用这些概念来解决问题，不要把问题交给它们。让它们看起来像一个直观的干净的语法，而不是像一些黑魔法，你可以满足你内心的计算机科学变态。

## 结果第一

隐式的`result`变量是一个非常方便的特性。大多数情况下，它可以与裸`return`一起用作回退返回值。在这种情况下，设置`result`的值应该是过程体的第一条语句。

## 返回选项[T]

对异常情况使用异常。有时不能产生一个结果是完全可以接受的。在这种情况下，使用`Option[T]`类型，它可以指示是否产生了结果。这种方法优于返回一个`(bool, T)`类型的元组或者抛出不必要的异常。

## 辜负他们的未来

异步代码也可能失败。有人可能会尝试使用`Future[Option[T]]`，但我认为这是一个糟糕的做法，因为未来本身可以表示失败。然而，为了使 Future 失败，必须向它传递某种类型的异常。我的建议是，如果失败值得使用描述性异常，或者当你对失败背后的原因不感兴趣，只对失败本身感兴趣时，使用一些通用的`NoResultAvailableError`。

## 让你能去的地方去，让你必须去的地方去

标题本身就说明了问题。使用一次性可赋值变量使得代码更容易推理，并且可以避免一些难以避免的通宵错误。理想情况下，你应该发现自己很少使用 var。Const 更好，但是它有不同的用例。

## 做 do 记号

将匿名进程传递给其他构造应该总是使用`do`符号来完成(如果可能的话)。它消除了不必要的语法干扰(proc 和括号),从而带来愉快的读写体验。

# 罗森克兰茨最佳实践

## 用->代替[ ]合成

Rosencrantz 为操作者提供了组合处理程序:`->`和`[]`。文档指出，当组合大量处理程序时，`[]`语法更好。我认为恰恰相反。

`->`更好地表达了组合，因为它看起来像它的效果:一个接一个地组合处理程序。它没有像`[`那样的闭合对，因此不会产生太多噪音，看起来更像是惯用的 Nim 代码。

## 分割路线:不要同时使用->和~

Rosencrantz 提供了另一个操作符`~`,可用于创建替代路径。一起使用`->`和`~`很好，但是会导致代码难以阅读，甚至更难维护。我们都知道，从长远来看，现在多输入一点将使我们免于更大的问题。有鉴于此，我提出以下建议。

在一个 let 语句中创建所有处理程序(全部详细描述)(仅使用`->`操作符),然后用`~`操作符将它们组合起来。不知何故像这样:

```
let
  getSingleUser =
    get ->
      pathChunk("/api/users") ->
        segment do (username: string) -> auto:
          ok(username) getUsers =
    get ->
      path("/api/users") ->
        ok("Users")let handler =
  getSingleUser ~
  getUsers
```

所有路线都是独立的，可以自由修改。此外，因为它们被分配给单独的变量，所以这些变量的名称可以作为一小段文档。这种风格可能有些冗长，但肯定会有所收获。

## 创建您自己的处理程序

Rosencrantz 肯定能做一些很酷的东西，但是大部分工作留给了开发者。创建 web API 时，最顶层应该负责输入验证、认证和授权、输入解析以及输出的正确表示。这些任务应该在应用程序的所有路径中完成，一遍又一遍的重写是麻烦且容易出错的。

幸运的是，Rosencrantz 很容易使用自定义处理程序进行扩展。使用该特性将上述任务提取到自定义处理程序中。这样，路由将只包括必要的和特定的逻辑。

# 坏零件

我还想指出一些目前不好的或缺失的部分，这些部分应该得到增强，以便提供更简化的开发人员体验。这只是一个快速和肮脏的列表，大多数事情可能已经在出血边缘分支修复。

## 唯一的模块名称

不能用相同的名称创建两个模块。所以禁止使用`model/user`和`service/user`，因为*用户*不是唯一的。这一限制应该取消。

## 导入失败

当导入的模块包含与该模块同名的声明时，编译会失败。从`article/handler`导入`handler`会导致编译器崩溃。

## 神秘的模板/宏错误消息

不像 C++那样糟糕，但是由错误的模板实例化或宏执行产生的错误消息应该更友好。

## 第三方软件包

这不是编译器或工具的问题，而是 Nim 生态系统的整体问题。对于一个特定的任务，只有一个或两个解决方案，或者根本没有第三方包！尽管可以使用 C 库，但这并不能弥补纯 Nim 甚至包装 C 库的不足。

# 结论

Nim 具有巨大的潜力，因为它快速、干净且易于使用。然而，编译器和工具仍然不稳定，第三方包的数量很少，其中大多数甚至不再维护。它还忽略了公认的最佳实践和商定的方法。这些是阻止尼姆变得更受欢迎的最大障碍。

现在关于现实世界…周末结束了，我的黑客马拉松也结束了。我已经建立了环境(框架、数据库)并开发了一个稳定的基础，我还在其上实现了`/api/users` routes。个人资料和文章的路线仍有待完成，但不幸的是，我不会有太多的时间。因此，我们热烈欢迎投稿人:)

从各方面考虑，我在这个项目上工作得非常愉快。在经历了那些 VM/managed/interpreted 语言之后，Nim 感觉像是呼吸了一口新鲜空气。有时它需要一些准备工作，但是总体上提供了一个愉快的开发体验。*强烈推荐！*

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 要了解更多信息，请[阅读我们的“关于”页面](https://goo.gl/4ofytp)、[在脸书上点赞/给我们发消息](http://bit.ly/HackernoonFB)，或者简单地说， [tweet/DM @HackerNoon。](https://goo.gl/k7XYbx)
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！