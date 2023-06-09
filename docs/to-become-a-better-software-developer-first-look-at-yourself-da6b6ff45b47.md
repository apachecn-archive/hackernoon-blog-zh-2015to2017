# 要成为一个更好的软件开发人员，先看看自己

> 原文：<https://medium.com/hackernoon/to-become-a-better-software-developer-first-look-at-yourself-da6b6ff45b47>

![](img/4572d7fe60105db87eeb7ea915e321be.png)

The road ahead or the road behind?

你曾经收到过对你的代码的不好的反馈吗？你有没有想过“为什么是我？”你有没有努力接受这种反馈？

在这篇文章中，我将描述成为一名更好的开发人员的部分方法。

我现在是 2017 年。2008 年，我开始了我的[职业生涯](https://hackernoon.com/tagged/professional)，成为一名[软件开发人员](https://hackernoon.com/tagged/software-developer)，尽管早在 90 年代，我 11 岁时就写下了第一行代码。那在工作中不算，但对我来说很重要。鉴于我从未上过大学，也没有做过信息学学徒——我完全是自学的。我所学到的都是艰苦的工作。

今天我看了看我在 2012 年写的一些代码，那是 5 年前，也是我工作的第 4 年。那时我正在开发一款 3D MMO 射击游戏。在检查我所编写的程序时，我回到了过去，与过去的自己交谈。我所发现的，让我屏息…

当你反思自己时，当你质疑自己的过去时，你可以学到很多东西。就像你过去几年走过的路。

今天我学到的是，我对我当时的技能有一种奇怪的印象。如果有人说*“丹尼尔，你的代码一团糟”*，我会强烈反对他们。我可能会生气，因为我付出了这么多努力。事实上，我今天发现的代码一团糟！虽然不是全部——至少我的命名是正确的——但是有很多问题是我当时没有意识到的。

我所说的软件是一个文本文件解析器。它应该解析的文件是**光波场景** (LWS)文件，其中保存了关于 3D 场景的信息，如相机和物体位置、灯光等等。说真的，这个任务并不太琐碎。它不仅包括阅读文档并将其转化为代码，还包括理解文件结构和光波本身背后的概念。顺便说一下，LightWave 是一个 3D 建模和渲染软件，在许多伟大的游戏和电影中使用。

当我在 2012 年写这个代码的时候，我觉得还可以。我知道这不是我做过的最好的代码。但当时对我来说已经足够好了，考虑到我当时所拥有的知识。今天，你可以想象，我对它的感觉是不同的。

2012 年我还不知道[固](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)) 甚至[单一责任原则](https://en.wikipedia.org/wiki/Single_responsibility_principle) (SRP)。我写类是为了完成某项工作。如果我为这个解析器类写了一个工作描述，应该是这样的:

解析器将读取文本文件。

*和*构建一个**对象树**。
*和*加载**对象**。
*和*将它们放入一个**场景**。
*和*设定它们的**位置**。
*最后，我会有一个 ***完整的场景*** 。*

> *不严格或者不知道固体、干燥、YAGNI 等原则会导致你的软件陷入灾难性的状态。*

*你可能会猜到，这个任务描述中的每一个“和”都是打破 [SRP](https://en.wikipedia.org/wiki/Single_responsibility_principle) 的指标，开发糟糕的架构，是下一个开发者的噩梦，还有很多我不想点名的东西。不严格或者不知道像[实](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design))、[干](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)、 [YAGNI](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it) 等原理，更会导致你的软件出现**的灾难性状态。在这种状态下，几乎不可能让代码摆脱技术债务或轻松添加新功能。当然，你总是可以添加新的特性，给一个项目添加更多的代码。但是随着项目变得越来越复杂，添加的功能越来越多，难度也越来越大。添加新功能将需要越来越多的时间，这一规模只会越来越大，不会越来越小。***

> *如果您更改了未测试代码中的一条指令，您可能会破坏您没有意识到的东西。*

*最重要的是，如果需求没有通过测试验证，那么从长远来看，您将会失败。如果您更改了未测试代码中的一条指令，您可能会破坏您没有意识到的东西。无论是在编译时(如果你的技术中有这样的东西)，无论是错误报告还是愤怒的客户打来的电话，你都会得到反馈。*

*我的 LWSParser 类没有经过单元测试。它包含大约**1800**行代码(LOC)，而最长的方法有大约 **500** 行 LOC 和超过 **10** 的嵌套级别(意思是 if-if-while-if-while 等等)。它包括逻辑、计算，甚至文件的异步加载。一旦我不得不改变某些东西，我会花相当长的时间来找出实施改变的正确方法。*

*今天，我是一个不同类型的开发人员。在过去的几年里，我学到了很多东西，我把它们铭记于心。如果我今天必须完成这项任务，我会把它分成几个班。我会非常严格地要求每个类应该做什么——确切地说是一个简单、独特的任务。一旦嵌套达到 3 级，我会重新考虑我的程序。我会尽量让每堂课都尽可能的小。为什么？因为它不仅让你的代码保持干净——拥有小的类和方法让你的大脑保持干净！*

*你知道吗，我以此为荣！我真的很抱歉，因为我知道当时靠我自己做这些有多困难。我很自豪，因为我知道我已经取得了什么，后面还有什么路要走。我很自豪，因为今天我可以看到我当时是错的。有一天，我意识到我并不像我想象的那样是一个高年级学生。永远不要放弃，独自完成工作不会让你成功。我做得很好，没有更多。我很自豪——也很高兴——因为今天我可以和你们分享这一经历。*

*我犯了很多错误，我承认它们。只有接受我并不总是对的，并试图从不同的角度看待自己，我才给了自己改进的机会。我不仅提高了我的编程技能。此外，接受和处理关键的反馈，以及向他人提供反馈，以便他们能够成长和变得更好。*

> *永远虚心接受反馈。不要认为自己是工作中的最佳人选。要谦虚。承认是错的。*

*如果我能给你一个重要的建议，那就是:永远虚心接受反馈。不要认为自己是工作中的最佳人选。要谦虚。承认是错的。*

*当人们收到对他们工作的反馈时，他们往往会把它当成是针对个人的。资深开发者不给反馈是为了指责你或者让你难受！他们是为你做的，所以你可以从他们的错误中学习，利用他们的知识，一步步变得更好。*

*你从这篇文章中学到了什么？请在评论里告诉我！*

*我的下一篇文章将更加关注技术，因为我想写如何清理如此复杂的代码。我喜欢重构，我会与你分享我的技巧和诀窍，成为一名更好的开发人员，并交付干净的代码(并保持你的大脑干净)。*