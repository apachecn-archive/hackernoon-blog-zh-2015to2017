# 创造理解:ClearFactr 背后的前提

> 原文：<https://medium.com/hackernoon/creating-understanding-the-premise-behind-clearfactr-3a8be7e5a3af>

![](img/35fa086b72ad0d55598abab1c474f84f.png)

在[创业](https://hackernoon.com/tagged/startup)的情感过山车上，你的核心论点得到客户反馈的肯定总是很棒的。最近，我有机会问一个用户，在试用 [ClearFactr](http://www.clearfactr.com) 之前，他在用什么来进行金融建模。他告诉我:

> *“我用的是 Google Sheets，没问题。但是随着模型的增长，跟踪发生的事情会变得更加混乱。有时候，我的老板叫我去解释一个单元，我可能不记得了，所以我必须站在那里，在他面前弄清楚，这很尴尬。现在我只是用通俗易懂的语言来读公式。我宁愿使用一个工具来了解我的模型，也不愿浪费时间尝试自己创建工具。”*

有人曾经向我描述一类电子表格用户为“神职人员”这些人对他们的电子表格印章感到自豪，有一些真正令人惊讶的牧师在那里，产生一些真正令人惊讶的东西。他们是“制造者”。他们通常是内部创业者。在上面的情况下，牧师会说*“是的，这就是为什么我们使用命名范围。”*(我会问他们，*“你会给每个细胞命名吗？”这就是圣职的特点——对于一个下午或深夜坐在网格、函数调用和键盘快捷键的诱人组合前来说，几乎没有什么挑战是太大的。*

我其实很了解神职。在我职业生涯的大部分时间里，我拿着大量的钱用定制软件取代他们的工作，因为通常情况下，大量的协作工作流问题和企业风险取代了最初史诗般的生产率增长。为什么？通常，这样的专家使用电子表格作为软件开发环境。通过它传递的信息。xls 文件与其说是“电子表格”，不如说是“应用程序”但是如果缺乏最罕见的纪律，他们最终会得到一个脆弱的解决方案和一场维护噩梦(也许还有一些临时的工作保障)。事实上，识别和管理由此产生的“[电子表格风险](http://www.eusprig.org/)”是一个成熟的行业。[一项研究描述了近 90%的电子表格包含某种错误](http://www.marketwatch.com/story/88-of-spreadsheets-have-errors-2013-04-17)，在最坏的情况下，你会发现像 [Tibco 的 1 亿美元崩溃](http://blogs.wsj.com/moneybeat/2014/10/16/spreadsheet-mistake-costs-tibco-shareholders-100-million/)这样的事情。

与神职人员相反，绝大多数电子表格用户会说*“什么是命名范围？”*

当考虑到对社会的影响时，电子表格的发明可能应该与汽车或空调一样:改变景观的转换工具，然后实际上成为景观。据说，没有电子表格，许多现代金融就不会存在。

在 ClearFactr，我们说:[我们热爱 Excel，但不是对一切都热爱](http://www.clearfactr.com/blog/we-love-excel-and-google-spreadsheet-and-the-others-just-not-for-everything)。

更详细地说，这是这样的:即使你是一名牧师，在某个点上，将“2016 年 7 月的净支出”翻译成“15 美元”，来来回回，一遍又一遍，一遍又一遍，这样的精神负担会削弱你的生产力。这只是为了表示数据的机制，以及将数据转换成信息的数据中的重要关系。我们还没有触及如何分析它。也许你为自己能制造出好的工具而自豪。但是，也许制造这些工具并不是对你时间的最好利用。

也许更重要的是，如果你的观众不能理解你的作品，你取得了什么成就？你的效率被削弱了，生产力问题被提了出来。如果你不知道自己是否有观众呢？他们有没有看一下你熬了一整夜的附件中最酷的部分，但现在也过时了，你宁愿回忆起来？但是*他们*已经在*你*都不知道的情况下把它发给别人了吗？

有人问我，是什么让你创建了 ClearFactr？这很简单。它看着一群痛苦，超过 25 年，并想知道:

*   如果我们可以用英语取代传统的公式语法——所有人都知道的“$ G $ 15”——但以无缝的方式保留熟悉的网格表示，会怎么样？
*   如果我们随后添加一堆可视化工具来识别、放大(必要时，调试)数据片段之间的关系，从而形成一个高度动态且非常有趣的模型，会怎么样？
*   如果我们随后构建了 power modelers 倾向于自己编码的分析工具，甚至是一个全功能的蒙特卡罗模拟器，会怎么样？
*   如果我们让一切都变得非常容易分享和监控，并让模型的观众能够参与其中，因为他们最终能够理解他们在看什么，会怎么样？
*   最后，如果我们将它托管在云中，以消除所有版本化的噩梦——包括应用程序和模型——并且可以毫不费力地将其部署到整个世界，会怎么样？

就像程序员进入了一个全新的领域，他们用类似于 IntelliJ 或 Eclipse 这样的工具取代了简单的文本编辑器一样，有多少电子表格用户可以用更好的工具成为他们的听众的牧师呢？

![](img/b580545a59c92cb07234256961ae8138.png)

从规划自己的未来到管理企业再到治理国家，对金融的理解在经济的各个层面都是至关重要的。然而，对上述任何一个方面有清晰的财务理解都是例外，而非常态。我们认为这是因为现有的工具太差了。我们构建了 ClearFactr 来解决这个问题。

![](img/ec4d1ff5e097067a9693882b1fec2bcc.png)[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是阿妹家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

[![](img/be0ca55ba73a573dce11effb2ee80d56.png)](https://goo.gl/Ahtev1)