# 狗屎创业做:第 1 集

> 原文：<https://medium.com/hackernoon/shit-startups-do-episode-1-cbfa73f9c25f>

## 在主机上花费太多的钱

想象一下这个场景——你是一个炙手可热的开发人员，为某个没有灵魂的财富 500 强邪恶巨头工作。你已经厌倦了技术债务。低劣的源代码控制。可怕的基础设施。官僚机构。

![](img/604769ded357277c43006ea68664cd74.png)

Dark Cloud Photo credit: [Michael Ico / Unsplash](https://unsplash.com/search/dark-cloud?photo=Dc9r3VMU1Mo)

要是我有自己的 [*创业*](https://hackernoon.com/tagged/startup) 就好了，你做梦吧。我会让单元测试从我的眼球里出来。我的反应式影子 DOM 组件将会非常灵活，我可以将它们连接到一个超级*高性能*无服务器微服务架构，然后等待资金滚滚而来。

可伸缩性问题将成为过去。你可以将 400 种不同的 [AWS](https://hackernoon.com/tagged/aws) 产品放在一起实现高可用性，跨越多个地区的多个可用性区域，并自动故障转移到谷歌云平台，以防 S3 再次崩溃。忘记把所有东西都放在一台机器上的日子吧，你的初创公司将会采用负载平衡的多 Web 服务器配置，这意味着你可以通过简单的`git push`把你的新 ninja 代码部署给客户。

在 Web 服务器上运行长时间运行的任务？在你的初创公司中没有——你像老板一样提供一群工人来处理图像和转码视频，多个队列和负载平衡器确保你的异步作业在纳秒内完成。你使用连接到 web socket 实现的 Amazon SNS，通过向用户实时发送他们的猫视频更新，向他们显示你有多他妈的棒，因为它转换成十几种格式，并带有十种不同语言的自动字幕。谁他妈的在乎喵是不是全球通用的——如果猫能把它们的屎集中起来，开始在不同的市场本地化，你就准备好了。

当然，现在您正在构建一个多 web 服务器环境，基于文件的会话将不再适用。有什么比 Redis 或 Memcached 实例更好的方法来存储会话数据呢？一个他妈的高可用性 Redis 或 Memcached 集群——这就是！当您可以拥有三个集群时，为什么要有一个昂贵的缓存实例呢？

所以你决定把你所有的文件放在 S3。你太棒了，你实现了直接从客户端到 S3 的上传和流媒体，完全绕过了你的服务器。您庞大的视频内容库像老板一样以惊人的速度流下。但现在你的基础设施处于 beast 模式，你不会被看到死摇一个设置，你的应用资产直接从一个 S3 地区提供。你不是一个真正的摇滚明星，除非你有一个 CDN 坐在那狗屎前面，这样一些在廷巴克图的 GPRS 连接上的家伙就可以从 1000 英里半径内的某个服务器上获得你的 12 兆字节的 JavaScript 包。如果你没有把你的东西分散到 35 个不同的边缘区域，你就不是一个真正的开发者。

头几个月一帆风顺。你去的那个创业加速器为你提供了 6 周的陈词滥调的建议，你公司的 10%都有 1 万美元的 AWS 信用，所以你是黄金。你注册了一些客户，他们被你的应用程序的速度和可靠性惊呆了。他们不知道，这与你庞大的云基础设施有着千丝万缕的关系，更多的是因为你现在只有极少数的客户在使用它。

一天，你的负责管理资金的合伙人带着担忧的表情走进来。“我以为 AWS 是免费的？”她说。你拿着账单晕倒了。原来你的六个客户中的一个上传了一个猫视频，并在网上疯传，你在 S3 的数据传输上个月花费了 6k 美元。你每月 3000 美元的可扩展基础设施已经榨干了你的信用，比你说 *Amazon Web Services 简单存储服务*还要快。你的脸色变得苍白，你意识到你已经浪费了大部分天使投资，而你所需要的只是一个月 5 美元的 Linode 或 DigitalOcean 盒子。

# 收场白

读到这里，你可能会认为我试图引发一场关于 AWS 和类似的云托管与更传统的专用和 VPS 选项的辩论。其实我爱 AWS。如果你正处于成长阶段，在 AWS 上运行可能会为你节省多份工资的成本，使额外的支出物有所值。

然而，当您开始时，关键是要知道何时使用各种 AWS 服务，何时不使用。在 S3 存储数据非常便宜，每千兆字节不到 3 美分。但是 9 美分一千兆字节的数据传输会让你很不爽。有效地利用 Lambda、Elastic Transcoder 和 SES 等服务可以为您节省大量时间、金钱和麻烦——但配置不当的自动缩放 EC2 设置也会无缘无故地让您损失一大笔钱。

成长往往需要时间。在最开始，你的精力最好放在弄清楚你的产品需要做什么才能卖给真正的客户。对于几乎所有成功的科技公司来说，技术债务和可扩展性问题都是一个现实——因为为了赚钱，他们在必要时会拼命干。你的超级优化设置只会榨干你的银行存款，除非你有真正的客户来利用它。作为一名工程师，很难不想以正确的方式做事，并按照你梦想中完美的世界观构建一切。但残酷的现实是，通常情况下，这可能完全是浪费时间和精力。

从积极的一面来看，最终你会非常精通 AWS，你应该会毫无问题地找到一份工作，摆脱隔壁初创公司在成立时制造的混乱和可扩展性噩梦。也就是说，如果你能克服由他们的公司仍然存在而你的公司不存在这一简单事实引起的黑暗沮丧。

# 关于这个系列

这是一系列半开玩笑的帖子，讲的是创业公司在他们典型的短暂存在期间所犯的一些常见的错误。它的灵感来自于我自己的经历和不朽的失败，以及我在其他创业公司看到的失败。

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)，并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)