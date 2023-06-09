# 虫子是你最好的朋友

> 原文：<https://medium.com/hackernoon/bugs-are-your-best-friends-b1dc226edecd>

你打开电子邮件，浏览一些工作信息，注意到一封关于 bug 的经典邮件。

```
RuntimeError: Your app is terrible  
app/controller/page:17 - what is  
config/route/blah:24 - this I  
bin/app:4 - can't even
```

看起来…很奇怪。错误消息和堆栈跟踪看起来有点熟悉。还有一丝评判的味道。

你会被原谅在那一刻感到恼火，甚至焦虑。

但是那只虫子和它的兄弟姐妹实际上是你最好的伙伴。这不仅仅是一种“总是看到生活光明的一面”的强有力的精神体操方式——有内在的理由相信这一点。

"然而，有太多的理由拒绝这种说法了！"是的，有，让我们探索其中的一些。

一个简单的例子是 bug 的干扰性。他们自己来的，就像一个粗鲁的派对客人。他们往潘趣酒碗里吐唾沫，打碎你的灯，然后没好气地在舞池中央坐下。你不得不放下你正在做的事情去处理他们的一般情况。

当然，如果你有一两个星期的工作计划，是新的工作，需要你认真关注，你最不希望的就是一个 bug。

还是你不想要的那个*中断*，而不是 bug 本身？当然，[的中断有很多隐性成本](https://www.ics.uci.edu/~gmark/chi08-mark.pdf)。但是，如果您将您的[工具](https://hackernoon.com/tagged/tools)和流程设置为不中断，而是缓冲通知，以便您按照可预测的时间表处理它们，那么拒绝索赔的理由还成立吗？

但是，嘿，还有一个拒绝索赔的理由，对吗？即使你缓冲了 bug，它们还是太多了！而这仅仅是我们能注意到的。我们没有提前发现的经验中的紧急需求怎么办？

当然，如果你有一大堆看起来只会越来越多的臭虫，那么臭虫是你最不应该庆祝的事情。

或者是资源限制让你沮丧？我不认为我们中的许多人喜欢做只会增长的列表，它们令人沮丧。由于所有权的变更，需求的变更，或者仅仅是没有预测到每一个边缘情况的代码/测试，我们可能经常会有比我们实际能够完成的更多的工作。

然而，关于处理繁忙的工作队列，我们学到了很多有用的东西。比如选择一个受限的和更可用的媒介，如果-那么计划，和每日优先化技术。

有很多方法可以解决需求不确定性。它并不完美，但随着更多的迭代、更好的工具和更清晰的交流，我们可以走得相当远。

但是，嘿，这还不是最糟糕的部分。它们会让我们的客户和我们自己付出高昂的代价！最坏的情况下，他们可以摧毁生命！

当然，当虫子能造成如此大的破坏时，我们不会珍惜它们。

或者是——不，事实上，这是一个有效的关注，哈哈。臭虫*会让你付出代价，它们会伤害你和其他人。*

但是，这个世界不是一次性游戏。你不是只有一手牌。在许多情况下，集体“我们”从过去的错误中吸取教训。就个人而言，大规模的失败会给人很大的教育和回报。在元文明的层面上，它可以消除机构的脆弱性。战斗伤痕等等。哎，不完美，但也不全是负面的！

此外，没有什么能阻止你在宇宙发现它们之前*找到它们*！例如，看看开源数据库项目的模拟和[测试，可以成为测试人员羡慕的一个很好的来源——你可以提前模拟问题，或者通过使用](https://www.sqlite.org/testing.html)[正式方法](/espark-engineering-blog/formal-methods-in-practice-8f20d72bce4f)系统地根除问题，这是令人惊讶的。

~

虫子不仅仅是“不全是坏事”，它们还是友好的。

第一，bug 是谜题。真的是这样。他们有关于根本原因的模糊线索，以及由信息痕迹和对周围世界的因果影响组成的踪迹。他们甚至奖励纯粹的发现，更不用说掌握修复！

想象一下你最后一次发现错误的确切时间。当我想起上周的几个例子时，我记得我笑得很开心，说“哦！”挺满足的。

是的，不是所有人都喜欢谜题。思考这些问题的成本很高，需要时间和注意力。但我仍然认为，我们中的大部分人能够欣赏困难的事情，最终给我们带来情感上的回报。延迟满足。

虫子的另一个好处是它们锻炼了我们大脑中如此多有趣的部分。为了找出 bug，你需要开发和练习代码考古、模拟和调试技能，等等。像`git blame`、`git bisect`，使用 web 调试代理，或者查询访问日志。

但除此之外，臭虫锻炼了我们的概率决策技能。例如，如果您的 web 应用程序中只有一个区域处理用户上传的 CSV 文件，则表明一个新的 bug 与导入相关，这增加了您应该对 web 应用程序的该区域进行指责的可能性(甚至在完全确定 bug 的来源之前)。你也可以通过快速剔除可能的原因来寻找根本原因，最好每次将假设空间减半。有时查询一些事件计数直方图会有所帮助，以便了解什么函数调用发生得最频繁，以及在什么上下文中发生。

当您注意到一个 bug 时，您通常会有一个关于各种情况的背景概念，在这些情况下它可能会发生，也可能不会发生。如果你还没有一个，在解决了一些错误之后，你还会对应用程序的哪些部分更有风险有一个概念。有一个增加对系统的内在熟悉度的反馈循环，这种熟悉度帮助您挑选出如何编写更好的测试，如何构建更好的元工具，以及如何减少发现和开发时间。

只是…有太多的开放领域来完善这种调查艺术！通过运用这种艺术，你基本上是在积累知识财富。这种财富让你对构建未来功能和更好地完成整个项目有更深刻的见解。

除此之外，他们迫使我们行使健康的怀疑。bug 让我们承担了一定程度的责任，这是知识界其他人*渴望得到的反馈。你能想象作为当今世界的学术科学家，*喘息着*从宇宙中得到一点一滴的反馈吗？我们有幸得到了我们甚至不知道正在进行的实验的带注释的结果。*

我认为臭虫甚至对登机有用。有什么比找出为什么代码没有正常运行更好的方法来真正了解代码库呢？你不仅要引导项目并理解它的行为，你还必须理解它应该如何行为，然后如何控制它，这样你就可以解包或模拟问题来真正理解它。这比一个小的(不太有意义的)功能更难，并且把*减轻他人的痛苦*作为你的首要任务更令人满意。

人们想帮助别人，就让他们去吧！

持怀疑态度的一个原因是，如果你没有选择正确的 bug 级别，你只是让人们转几天(希望不是几周！)但是通过对更熟悉的人进行一些 bug 管理，bug 队列可以成为方便的入门工具。

无论如何，朋友不希望你停滞不前，他们想培养你，看着你成长。虫子不是人，但我会邀请它们参加我的派对。也许我会把潘趣酒碗盖上，让他们不要惹其他人生气。但我会听听他们要说什么。

*原载于*[*kilotau.com*](https://kilotau.com/)