# 测试驱动的代码评审

> 原文：<https://medium.com/hackernoon/test-driven-code-review-3f05f6cee400>

![](img/f0c8611dc8bf52674c10c663ad38cac2.png)

source: [wikimedia](https://commons.wikimedia.org/wiki/File:Icon_stamp_under_Review_textured.svg)

一年前，我和我最好的朋友 Alex 就代码审查进行了一次有趣的讨论。他说当他做代码审查时，他总是从测试开始。他使用这种技术是为了理解代码真正做了什么，它是如何工作的，以及它覆盖了什么功能。

在检查完测试之后，他接着检查产品代码。生产代码应该是有意义的，并且遵循团队设定的[原则/指导方针和模式](https://hackernoon.com/the-importance-of-team-culture-af6fffead7b5)(团队所说的“干净代码”的一切)，这样每个人都可以遵循。

当您想要实现一个特性时，您将一个单一的需求转化为用例。您将单个用例转换为测试用例。您在生产代码中实现这些测试用例。

如果你正在练习 TDD，那么你正在遵循 TDD 的[三定律。这三个定律是:](http://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html)

*   在编写任何产品代码之前，您必须编写一个失败的测试。
*   您不能编写超过足以导致失败或编译失败的测试。
*   您不得编写超过足以使当前失败的测试通过的生产代码。

这里真正有趣的是第三条法则，因为它意味着如果你的测试通过了，你就不能添加更多的产品代码，如果你想添加更多的代码，你必须添加更多的测试用例。换句话说，您的产品代码仅仅是为了覆盖您的测试用例所描述的内容而编写的。仅仅通过查看需求并对照测试用例进行检查，您就可以很好地理解实现应该是什么样的，它涵盖了什么功能，以及开发人员是否忽略了任何用例并且需求没有得到满足。

# 代码的行为受到测试用例的约束

因为您的测试是 API 的第一个客户端，所以它们可以帮助您暴露设计问题，比如封装问题或者组件之间的紧密耦合。

如果测试模仿了许多组件，那么您需要检查封装是否被违反，以及这些组件中的一些是否可以被包保护或私有。封装是最重要的 OOP 概念之一，也是被开发人员滥用最多的概念。

如果测试花了太多时间模仿单个对象的方法调用链，那么你可以非常确定违反了 Demeter 的[法则。如果违反了 Demeter 定律，那么您可以非常确定代码存在封装问题。然而，我知道，甚至不用看代码，只要看一下测试的结构就知道了。](https://hackernoon.com/the-law-of-demeter-in-the-era-of-microservices-3186f4c399a1)

此外，您可以猜测开发人员没有实践 TDD，因为测试人员对实现的内部了解太多。只有在编写了产品代码之后再编写测试，这种情况才会发生。

如果您知道测试是在实现之后编写的，那么您需要检查产品代码是否包含隐藏的特性，并且没有描述这些特性的测试。这真的很糟糕，你不能让它发生，因为你会对你的测试套件失去信任。在提交代码几个月后的某一天，你会重构它，甚至可能在没有注意到的情况下删除整个特性，因为没有描述该特性的测试用例。这真的很糟糕！

# 顺便说一下，测试也是代码

测试是你拥有的消除对改变生产代码的恐惧的唯一工具。随着代码复杂性的增加(不管是不是偶然的)，您将重构代码，测试可以确保代码的行为是相同的。有一本*马丁·福勒*写的很棒的书叫[*《重构:改进现有代码的设计》，*](https://www.amazon.com/Refactoring-Improving-Design-Existing-Code/dp/0201485672) 你应该读一读！

所以花同样的时间，甚至更多的时间来确保你的测试总是处于良好状态。您需要代码审查和重构您的测试。测试应该遵循与生产代码相同的标准。

# 进一步阅读

1.  [TDD 的周期](http://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html)
2.  [微服务时代的德米特里定律](https://hackernoon.com/the-law-of-demeter-in-the-era-of-microservices-3186f4c399a1)
3.  [团队文化的重要性](https://hackernoon.com/the-importance-of-team-culture-af6fffead7b5)
4.  [重构:改进现有代码的设计](https://www.amazon.com/Refactoring-Improving-Design-Existing-Code/dp/0201485672)作者*马丁·福勒*和*肯特·贝克*