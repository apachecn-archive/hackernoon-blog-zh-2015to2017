# 围棋中的死循环

> 原文：<https://medium.com/hackernoon/the-sleepy-for-loop-in-go-4e6fee88c5ad>

**虚构的例子:**假设您有一个 JSON 文件，其中包含一组 IP 地址字符串，您希望每 3 秒钟重新加载一次这个文件，然后对每个新的 IP 地址做一些事情。如果文件不存在，或者包含无效的 JSON，您也需要在 3 秒钟内重试:

上面的代码应该可以完成这项工作，但是有点烦人的是，我们需要到处重复睡眠语句。

这是我最近开始在这种情况下使用的一种模式，我称之为“*”循环睡眠:*

*我可能不是第一个(ab)像这样使用 for 循环的 post 语句的人，但我以前没有见过这种模式被使用得多，所以我分享它，希望它对你们中的一些人来说是有趣和有用的。*

*稍加修改，它也可以用于有限循环。例如，如果我们只想加载一次 IPs，出错时重试 2 次:*

*无论如何，尽管我对循环的*sleep 很满意，但是同样的代码显然也可以不用它来编写。事实上，今天早上我的同事并不喜欢它，所以我们最终满足于这样的事情:**

*我肯定更喜欢*sleep for loop*，但我对它的感觉还不够强烈，不建议强迫那些认为它很奇怪的人:)。*

*不管怎样，你觉得怎么样？请分享您的反馈和替代想法。*

> *[黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是阿妹家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。*
> 
> *要了解更多信息，请阅读我们的“关于”页面、[在脸书](http://bit.ly/HackernoonFB)上给我们点赞/发消息，或者简单地发送 [tweet/DM @HackerNoon。](https://goo.gl/k7XYbx)*
> 
> *如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！*