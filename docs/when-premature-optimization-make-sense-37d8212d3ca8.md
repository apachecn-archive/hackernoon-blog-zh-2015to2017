# 当过早优化有意义时

> 原文：<https://medium.com/hackernoon/when-premature-optimization-make-sense-37d8212d3ca8>

![](img/08aee251a40dd855c2f7b44db194aa81.png)

我们都被告知不要过早地优化我们的代码。无论您是为企业构建还是试图获得您的第一个 MVP，您都不应该花费太多时间来调整您的代码以获得边际效率收益。正如唐纳德·克努特(Donald Knuth)在他 1974 年的书《计算机编程作为一门艺术》(Computer [Programming](https://hackernoon.com/tagged/programming) ，*)中所描述的那样，“担心他们程序中非关键部分的速度，这些高效的尝试实际上有着强烈的负面影响……”。*但是，我们如何确定什么会对未来产生强烈的负面影响呢？在这篇文章中，我将详述我在最新的 [SaaS](https://hackernoon.com/tagged/saas) 项目“新奇”[中做出的一个小决定，这是一个面向 Etsy 卖家的社交媒体营销平台。](http://getnovelty.com/)对抗过早优化的决策。当我谈到优化时，我指的是将产品推向市场的商业环境，而不是算法性能的提高。

> 真正的问题是程序员在错误的地方和错误的时间花了太多的时间担心效率；过早的优化是编程中所有罪恶(或者至少是大部分罪恶)的根源。”

——作为艺术的计算机编程(1974)唐纳德·克努特

前几天，Product Hunt 的 Twitter 账户分享了这个迷因，让我忍俊不禁。

![](img/e4cca006338122a75783ea9ee1b1cccc.png)

我笑了，因为**的斗争是真实的！**很多时候，我们开始编码时并没有考虑我们将要构建什么。这通常是好的！在我们坐下来动手之前，我们希望花几个周期用线框、流程图之类的东西来记录和设计我们的产品。现在是实施的时候了。然而，开发人员经常需要考虑效率，并且经常为时已晚。

**开发人员需要优化某些事情，例如，如果您构建一个 web 应用程序，您应该尽早考虑优化服务器端缓存。**

假设你正在开发一个银行应用程序。当您向服务器请求帐户余额时，会进行数据库查询。然后，结果应该被序列化并存储在数据库缓存中，比如 [Redis](https://redis.io/) 。下次用户需要访问他们的帐户余额时，您可以快速“获取(id)”这些数据。只有发生存款或取款时，缓存才会无效。您甚至可以在存款或取款时预先填充这个缓存。他们称之为“加热”缓存。这里的想法是，这种类型的优化将极大地影响用户的体验，从而给人一种爽快的应用程序的外观。这才是用户需要的。这是你的应用程序需要的，所以尽快设置你的数据库缓存是有意义的。

**第二个不那么令人兴奋的例子是优化全球资源。**

当我为新奇的事物设计 MVP 时，我不得不走捷径以便快速进入市场。在第一版中，我遗漏了一些明显的东西，也有意遗漏了一些其他的东西。由于这是我用 ReactJS 编写的第一个 web 应用程序，所以对 React 处理全局资源的方式有些困惑，但是我将把它留给另一篇文章来讨论。我在应用程序中使用了脸书的 JavaScript API，客户端需要访问应用程序 ID。我从一个脸书 ID 开始，在我部署到产品并需要另一个“测试”ID 之后，这个 ID 很快变成了两个。脸书为你提供了一种创建[测试应用](https://developers.facebook.com/docs/apps/test-apps/)的方法，让这个过程变得更加简单。

我很快意识到，现在我必须记住在每次部署到生产服务器时用测试 ID 替换产品应用 ID。记住这一点非常重要！我对自己说，*我怎样才能让自己过得轻松些？*我们可以根据服务器环境变量构建一个 REST 端点来提供正确的应用 ID，这样我们就不必担心在部署之前更改应用 ID。优化还是不优化，tiz 这个问题…

我想了一会儿，决定不做了。我会继续在每次部署前切换 app ID，即使没有太大意义。我会把这个优化添加到我不断增长的列表中，当我需要的时候我会去做。关键是有更重要的事情要担心，比如获得客户和开发他们关心的功能。另一方面，当我的产品变得更好时，我可能会受到影响。

感谢阅读！我叫[亚历克斯](http://alexdaro.com/)，[新鲜感的创始人/开发者，这是一个为 Etsy 卖家提供的社交媒体营销平台](http://getnovelty.com/)。我写了我作为第一次创业者的旅程。随意伸手！

图片来源:【www.developers.facebook.com 

*原载于 2017 年 11 月 6 日*[*www.alexdaro.com*](https://www.alexdaro.com/writing/creating-a-test-facebook-app)*。*