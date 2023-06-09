# IDVector 的开始

> 原文：<https://medium.com/hackernoon/inception-of-idvector-33194d1e3bca>

![](img/7fafe05fe5efc31f13cd0103fb19dfb3.png)

## **设置舞台**

事实证明，2013 年末和 2014 年初是公众对数字隐私和安全理解的分水岭。我们了解了很多美国和外国情报组织在国内和国际监视方面所做的事情。我假设很多人。大多数？—信息安全专业人士认为，斯诺登泄密事件证明了情报收集能力的水平……但没有人证实这一点。很明显，没人应该证实任何事，但是…事情就是这样。由于塔吉特、家得宝、冰雪皇后、艾伯森、联合包裹、摩根大通、史泰博和凯马特的[事件，我们的商业和通信系统的安全性一再受到质疑。服务提供商](http://www.forbes.com/sites/moneybuilder/2015/01/13/the-big-data-breaches-of-2014/)[窥探我们的生活，把我们变成商品的事实已经成为众所周知的事实。这些关于政府和企业获取我们的个人数据和通信的披露将互联网隐私和安全推到了我们集体意识的最前沿。以前属于老 UNIX 老手和 IT 书呆子的话题，现在成了晚间新闻和国会听证会的热门话题。](http://www.wired.com/2015/10/verizon-curbs-zombie-cookies-theyll-still-stalk/)

在这些事件的背景下，我工作的公司 [Kyrus Tech](http://www.kyrus-tech.com/) 宣布，它正在寻找一种新技术来孵化和推出。我花了相当多的时间为政府建立归属管理和在线匿名领域的系统。我在政府部门工作的经历让我得出结论，互联网隐私存在三个基本问题:

1.  无处不在的免费互联网和服务正在成为常态。在这种模式中，用户用隐私和安全来换取免费和方便的访问。
2.  最适合制定适当的隐私控制措施的组织是最没有动力这样做的组织。当人们期望企业免费提供服务时，他们会找到其他赚钱的方法。
3.  在我们当前这个“永远在线”和“永远连接”的世界里，[每个人都是旅行者](http://www.networkworld.com/article/2904439/wi-fi/is-it-safe-to-use-public-wi-fi-networks.html)，周边环境在很大程度上已经成为过去。

换句话说，我看到了一系列问题或伤害，这些问题或伤害永远不会被那些应该由*解决的人解决。这样做会破坏他们的真正目标:以我们的隐私为代价赚钱。我决定做点什么，Kyrus 支持我的想法。我们的目标是:创建一个可扩展的云平台，为所有互联网用户提供隐私、安全和匿名服务。强大的安全性，交付简单。*

## 【IDVector 如何帮助解决这些问题？

[IDVector](https://www.idvector.net/) 通过提供简单、可扩展的解决方案来加密传输中的数据，并在需要时提供多样化的互联网访问路径来确保隐私、安全和匿名，从而解决关键的数据保护和隐私问题。

为此，我们设计了几种核心技术，分为两个基本类别:

1.  客户端设备和/或软件
2.  短暂、按需、基于云的网络重定向和出口节点

目前[有两个客户端](https://www.idvector.net/products.html):id vector Pro USB 客户端和 IDVector Mobile 客户端。Pro client 是一款小型 USB 供电设备，其核心是 Atmel 片上系统和 WiFi 芯片组。它运行一个定制的 Linux 实现，并使用专有(正在申请专利)客户端软件和商用开源 VPN 软件。一个硬件设备可以让我们解决一些软件解决方案无法单独解决的问题。

首先，也是最简单的，我们提供了一个额外的安全层—良好的传统纵深防御。通过使用非车载 WiFi 设备，我们将面向外部的表面区域从用户的笔记本电脑硬件和软件上移开。换句话说，我们让您的笔记本电脑的硬件和操作系统与未知和可能不安全的 WiFi 隔离，同时仍然允许您通过这些免费连接访问互联网。

其次，我们引入一些新概念和新特性。我们创建了一个预协商或强制网络门户保护代理，确保您的计算机在协商连接时不会受到攻击。该功能的灵感来自一系列针对商务旅行者的攻击，昵称为“ [Darkhotel](https://blog.kaspersky.com/darkhotel-apt/6613/) ”。在这些攻击中，酒店的强制门户系统遭到破坏，并安装了恶意软件，这些恶意软件会根据特定旅客的个人信息将 [*作为目标*](https://securelist.com/blog/research/66779/the-darkhotel-apt/) 。该恶意软件在用户协商酒店强制网络门户(输入房间号、姓氏等)时出现。最重要的是，恶意软件以合法软件更新的形式呈现给旅行者，带有有效的([但较弱的](https://securelist.com/files/2014/11/darkhotel_kl_07.11.pdf))加密签名，因此目标系统下载并安装它，就好像它是有效的更新一样。我们的强制网络门户保护代理技术通过在 IDVector Pro 客户端层阻止二进制代码到达客户端计算机。我们还允许用户自动随机更改其 IDVector Pro 客户端的 WiFi MAC 地址。这有助于防止“免费 WiFi”提供商根据之前收集的 MAC 地址来分析用户或锁定他们。

最后，IDVector 客户端允许用户选择通过 IDVector 共享路径或自定义专用路径访问互联网。共享路径很便宜，所有 IDVector 用户都可以使用。共享路径有一个有限的生命周期，并使用新的服务器实例、新的加密密钥和新的 IP 地址定期自动创建和销毁。IDVector 私有路径是完全私有的——它们托管在专用的云服务器上，只需点击一个按钮，就可以*字面上的*创建和销毁这些服务器。有了共享和私有路径，你可以选择你想出现在互联网上的什么地方。保护 Pro 客户端到这两种路径的连接的加密材料从不用于多个连接，而是在 IDVector Pro 客户端上生成。IDVector 服务器从不拥有客户端的加密密钥。

在移动方面，我们提供了一个 iOS 应用程序，它可以在苹果 iOS 平台内做许多与 Pro 客户端相同的事情。因为苹果和 iOS 有些限制，所以有一些局限性。例如，我们不能实现强制网络门户保护代理，因为苹果有自己的 iOS 设备强制网络门户协商机制。IDVector 技术的其余大部分直接传递给 iOS 客户端。您可以使用共享路径或专用路径，您的所有数据都将通过安全和专用的 VPN 技术，通过该路径到达全球任何您想要的地方。我们面向 Android 的 IDVector 移动客户端将于 2016 年第四季度初推出。

在云中，我们使用各种提供商来实现全球覆盖。我们利用 Apache LibCloud 来控制我们的云实例。随着特定地区需求的增加，LibCloud 允许我们快速轻松地添加更多提供商。我们的云基础设施具有难以置信的可扩展性；我们很想测试它能长到什么程度。如上所述，因为 Pro Client VPN 连接的加密材料是在客户端设备上生成的，所以我们(作为服务提供商)*不能*窥探我们客户的流量。默认情况下，所有 VPN 路径都使用具有完美转发保密性的 IKEv2。我们从一开始就设计了这个系统，把我们自己排除在外。

你所有的重要数据应该已经在你的网络浏览器和服务器之间加密了，但是使用 IDVector，我们和大数据收集平台都无法知道你是谁，你的数据来自哪里，在许多情况下，它最终会到达哪里。即使您使用公司或个人 VPN 来加密从您的系统到您的远程工作环境和/或互联网的流量，您的系统仍然直接连接到不安全的 WiFi，因此容易受到本地攻击以及可以看到您的加密数据流的来源和目的地的数据收集方案的攻击。IDVector 会阻止这些攻击，并屏蔽所有网络流量的端点。在我们的网页上有一个[图，展示了(在高层次上)它是如何工作的。](https://idvector.net/how-it-works.html)

因为我们确实认为隐私、安全和匿名很重要，所以我们允许用户通过匿名机制为 IDVector 服务付费。为此，我们选择 Stripe 作为我们的支付处理合作伙伴，部分原因是他们接受比特币。如果你对加密货币领域不感兴趣，最好的“老式”匿名支付机制是预付卡 Stripe 也支持预付卡。

## **那么，谁需要 IDVector 呢？**

我们认为每个人都需要 id vector——我们都是无边界世界中的旅行者。首先，我们关注 5 个核心群体:

1.  企业高管——成为目标的原因既在于他们能够访问信息，也在于他们可能会在各种不安全的地方开展业务。
2.  信息安全专业人员—事件响应人员、取证分析师、逆向工程师以及其他进行开源情报收集并且不希望在服务器日志中记录公司或私有 IP 地址的人员。
3.  律师、医疗组织、媒体和内容创作者——负责保护他人隐私、匿名、权利、内容和知识产权的人。
4.  记者——所有人。无论他们是为敏感消息来源工作的调查记者，还是在限制性制度下在禁区外活动的记者。记者可以用 IDVector 保护自己和他们的消息来源。
5.  政府旅行者——国防部、国务院或任何联邦雇员，他们可能身在国外，却无法安全地与总部联系。

我们的长期路线图包括企业产品，以及探索将 IDVector 技术整合到小型办公室和家庭办公室(SoHo)路由器中。我们相信地理上分散的团队应该能够创建动态、安全、私密的共享工作空间。我们相信每个人都应该能够在家上网，而不用担心他们的服务提供商窥探他们的流量。IDVector 技术的企业版和 SoHo 版将实现这些场景。

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)，并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

[![](img/be0ca55ba73a573dce11effb2ee80d56.png)](https://goo.gl/Ahtev1)