# ngrx/存储重用缩减器逻辑

> 原文：<https://medium.com/hackernoon/ngrx-store-reuse-reducer-logic-b6c0449e695d>

![](img/ea1ea8090e7dc7a01fc622bea0f1651f.png)

当您的应用程序增长时，您可能会发现您的存储的几个部分为不同类型的[数据](https://hackernoon.com/tagged/data)做着相同的工作，理想情况下，我们希望通过为每种数据类型重用相同的公共[逻辑](https://hackernoon.com/tagged/logic)来减少重复。还可能发生这样的情况，您希望拥有同一类型数据的多个“实例”。

假设我们正在创建一个有两个页面的应用程序，每个页面显示一个用户列表。每个列表显示一组不同的用户，例如:管理员或编辑。每个列表都可以排序，我们可以选择一个用户。页面的缩减器可能看起来像这样:

首先是管理员减压器。

然后编辑缩减器:

之后，我们可以使用`combineReducers`来设置我们的状态

对于每个减速器，我们都做了一些事情:

1.  因为我们使用 typescript，所以我们首先为我们的状态设置一个接口。
2.  然后我们定义我们的初始状态
3.  之后，我们用它的动作类型来定义我们的缩减器

虽然每个单独的缩减器都没有问题，但这段代码并不枯燥。因为每个缩减器的结构完全相同，所以我们可以抽象代码，创建一个管理员和编辑状态都可以使用的缩减器。

## 抽象您的 reducer 代码

我们可以通过在状态的键中使用`user`，而不是`editor`或`administrator`，使我们的 reducer 更加抽象。我们的减速器可能看起来像这样:

然后可以像这样设置我们的状态

然而，这种设置有一个问题。因为`combineReducers`会调用每个具有相同动作的减速器。如果我们分派一个动作`{"type": "sort"}`，它实际上会对管理员和编辑状态进行排序，而不仅仅是你想要排序的状态。为了实现期望的行为，我们需要某种方法来包装 reducer 逻辑，这样我们就可以确保只有我们关心的 reducer 被更新。这可以通过使用高阶减速器函数来实现。

## 使用高阶减速器

高阶 reducer 是一个函数，它将一个名称作为参数，并返回一个新的 reducer 函数作为结果。我们可以使用这个模式来创建一个 reducer 的新实例。这个高阶减速器可能看起来像这样:

我们现在可以在我们的`combineReducers`函数中使用这个函数来生成 reducer 的多个实例:

现在给你的动作名称加上后缀，这样它们就和你的减速器中的新名称相对应了。

# 结论

使用高阶缩减器模式，我们能够调度只影响我们所关心的那部分状态的动作，并且我们能够以 DRY 方式创建我们的数据的多个实例。我们防止了减少器逻辑的重复，这导致了更易维护的代码库。

谢谢你的阅读。在我的下一篇文章中，我将写关于重用效果逻辑。这是我的第一篇帖子，有什么反馈吗？让我知道。

*跟我上* [中](/@luukgruijs)*中*让我们连线上* [*领英*](https://www.linkedin.com/in/luukgruijs/)*

*[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)**[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)**[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)*

> *[黑客午间](http://bit.ly/Hackernoon)是黑客们下午的开始。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家族的一员。我们现在[接受提交](http://bit.ly/hackernoonsubmission)并很高兴[讨论广告&赞助](mailto:partners@amipublications.com)的机会。*
> 
> *如果您喜欢这个故事，我们建议您阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实视为理所当然！*

*![](img/be0ca55ba73a573dce11effb2ee80d56.png)*