# 找到正确的地方

> 原文：<https://medium.com/hackernoon/find-the-right-place-1e3c9f0496a2>

当阅读 Doug 的文章时，我想知道拉请求是否是记录变更的合适地方。我同意这些需要记录在案，但我不同意的地方。

**拉式请求不应该是你的团队讨论的地方！**当[拉动请求](https://hackernoon.com/tagged/pull-request)打开时，根本的改变就太晚了。在快速移动的团队中，拉取请求甚至在团队的大多数人看到它们之前就被合并了。如果您对拉取请求进行了长时间的讨论，这意味着您的拉取请求将保持开放状态太久。这违背了引用的[程序员誓言](http://blog.cleancoder.com/uncle-bob/2015/11/18/TheProgrammersOath.html) : #4:做增量小发布和#6 以高生产率工作。

所以如果你想要一个讨论的地方，那就换一种方式吧！

拉请求的想法是让其他人(1 到 x 个人)评审变更。这与在同一台计算机前的审查没有什么不同，事实上，我认为拉请求在结对编程的世界里已经过时了。您可能仍然希望保留它，例如在非常大的组织中，从不同的团队成员那里获得审核系统变更影响的批准。但是至少结对编程可以大大减少所需的评审员数量。

那么我们要记录的所有这些信息是什么呢？我们需要它们吗？
绝对！但不是为了团队讨论，而是为了你的代码的未来读者！他需要理解我们为什么以某种方式做事！这可以通过测试和良好命名的方法来记录，但有时需要更多。但是 pull requests 注释不是 Git 历史的一部分！因此，请将它们移至您的提交消息中！
这也是 Square 正在做的事情，看看这篇很棒的博客:
[https://medium . com/Square-corner-blog/how-Square-writes-commit-messages-8e 92 fcbf 77 c 9](/square-corner-blog/how-square-writes-commit-messages-8e92fcbf77c9)

它们使用相同类型的信息，但是对于提交而不是拉请求！