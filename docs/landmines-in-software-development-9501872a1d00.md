# 软件开发中的地雷

> 原文：<https://medium.com/hackernoon/landmines-in-software-development-9501872a1d00>

人们很容易低估[软件](https://hackernoon.com/tagged/software)开发的复杂性。开发人员和项目经理每天面临的挑战之一是[管理](https://hackernoon.com/tagged/managing)未知。未知是什么，管理它意味着什么？

未知并不新鲜。常识告诉我们，生活中没有什么是确定的。当灾难性事件导致计划失败时，人们自然会感同身受。然而，当计划因为不可理解的原因而失败时，就要由计划者*来管理*这些期望，并制定 b 计划。例如，预计会出现缺陷产品的制造商会制定退款政策，以便客户可以拿回他们的钱。

在软件开发中，未知是开发人员当前的工作知识和为了使一个特性工作所需的实际知识之间的差异。在一个知识无限的世界里，开发人员将能够精确地描述一个特性将如何实现，以及构建它需要多长时间。然而，现实情况是，有些特性比其他特性更难理解。

至少有三个因素决定了构建特征的速度:

*   输入代码需要多长时间？
*   解决问题和创建正确的算法需要多长时间？
*   找到满足方程中缺失变量所需的信息需要多长时间？

你可能认为当你的团队由摇滚明星开发者组成时，这些因素就不是问题了。但事实是，你不会仅仅因为把一个摇滚明星团队放到一个项目上就获得 10 倍的产出。即使是同一个团队，一个项目的开发也可能滞后于另一个项目，原因有很多:

*   完成一件事需要多少行代码？例如，开发人员用 C++而不是汇编来编写，因为更高层次的抽象允许他们用更少的代码行解决更复杂的问题。代码库的模块化程度如何？当模块越来越少时，重用代码的机会就越来越少，这意味着每次构建新功能时都必须重新键入代码。
*   框架有多容易理解？为了知道下一步要写什么，开发人员需要考虑多少层次的继承或嵌套函数调用，或者命令性代码行？有单元测试吗？当缺乏测试时，开发人员不得不在心里跟踪并重新测试他们接触到的每一行代码，这样他们就不会意外地出错。
*   项目文档有多完整？为了找到方法或 REST 端点的签名，开发人员需要扫描多少文件？产品规格有多清晰？UX 模型已经创建了吗？收集和处理信息需要时间。当然，在电子邮件的主题行中写连续句可能会更快，但是糟糕的写作会增加开发时间，因为开发人员必须更加努力地理解他们应该构建什么。

开发者对这些问题了如指掌。当他们不得不花费数小时试图找出正确的参数来连接到 REST 端点时，他们不会感到惊讶。这就是他们讨厌给出评估的原因。当有人问什么东西需要多长时间才能建成时，他们是根据过去的经验和当前对情况的了解做出直觉的猜测。

> 从根本上说，这种估计是直觉，因此不可靠。

重要的是要认识到这种估计是直觉。它们不是数据驱动的。没有确凿的事实支持他们。没有概率数字来定义这些估计的准确性。他们只是猜测。

不了解这些估计的本质的管理层自然会认为它们是具体的。直觉上，他们认为花更多的时间计算估计值会导致更高的准确性。在某种程度上，这是真的。然而，我们仍在应对未知。从根本上说，我们还不知道完整的答案，而且在这个过程中，我们可能会碰到一个未知的地雷。

这是典型的软件开发的样子:

![](img/c0ead51f58972cca6fb64576ffafc2e7.png)

在此图中，开发人员开始编写代码。一切似乎都在按计划进行。但是突然，他/她碰到了地雷，项目的其余部分被延迟了。

什么是地雷？以下是一些例子:

*   编写规范是为了允许用户上传文件进行数据处理。除了规范编写者没有意识到文件可能很大，因此需要一个更复杂的 UX 来报告用户等待操作完成时的进度更新。新的 UX 样机需要设计和额外的前端代码需要建立，以显示进度更新。
*   开发团队计划使用某个 API 来将事情挂钩在一起，但是在写代码的时候，他们意识到这个 API 是[漏洞](http://www.joelonsoftware.com/articles/LeakyAbstractions.html)并且不能做他们认为它可以做的事情。现在他们不得不寻找另一个可能存在也可能不存在的解决方案。如果没有简单的解决方法，他们将不得不自己构建解决方案。
*   编写规范是为了将特性 X 与特性 Y 集成在一起。除此之外，并非特性 X 的所有内容都与特性 Y 兼容，这是由于之前做出的实施决策，因为假设 X 永远不需要与特性 Y 集成。直到开发团队实际开始编写代码时，才会发现这些不兼容性。现在，团队不得不花费额外的时间寻找解决方法。如果问题足够严重，集成规范需要重写。
*   当开发一个新特性时，开发人员意识到该实现的一部分已经存在于由不同开发人员构建的另一个特性中。尽管复制和粘贴代码会更快，但这不是构建软件的可伸缩方式。最终，会有多个代码副本需要巩固和重新测试。此外，如果有任何错误，其他开发人员将不得不知道搜索其他副本，并做出相同的修复。因此，作为一名优秀的开发人员，他/她决定重用其他功能的代码。然而，要使现有代码可重用，首先需要进行一些重构。这比最初的估计增加了几个小时。除了每个人都这样做，现在这个项目的总体估计是完全关闭的。

从本质上说，地雷是一种未知因素，会导致未能满足的期望(通常是错过了最后期限)，必须加以管理。开发人员可以通过延长工作时间或在实现中走捷径来帮助吸收地雷(捷径会产生技术债务，以后需要更多时间来修复)。产品团队可以通过将优先级较低的功能推到以后的冲刺阶段来帮助防止地雷影响产品的推出。但是，当开发人员筋疲力尽，产品团队不能再推迟任何功能时，企业最终承诺的比它能够交付的要多。

地雷也不仅仅是需要在以后解决的问题。他们的伤害通常随着拖延时间的延长而成倍增长。他们基本上是定时炸弹，等着毁掉整个项目。忽视它们是不可取的。

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)，并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

[![](img/be0ca55ba73a573dce11effb2ee80d56.png)](https://goo.gl/Ahtev1)