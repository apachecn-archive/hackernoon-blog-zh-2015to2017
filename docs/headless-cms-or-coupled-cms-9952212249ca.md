# 无头 CMS 或耦合 CMS

> 原文：<https://medium.com/hackernoon/headless-cms-or-coupled-cms-9952212249ca>

## 为什么不两者合二为一呢？

![](img/83036ff5486faa4453f1f372cb2ee586.png)

无头 [CMS](https://hackernoon.com/tagged/cms) 还是耦合(数据库驱动)CMS？你可能以前听说过这种混乱(互联网上有很多文章)，并希望澄清选择什么 CMS 软件，尤其是在什么情况下。最后一点是重点:你的选择完全取决于你的内容是为了什么。

# 无头 CMS

无头 CMS——内容[管理](https://hackernoon.com/tagged/management)系统，仅承担内容层，没有表示层。您创建和组织内容，以便稍后交付到您的网站、移动应用程序或其他任何东西。

因此，利弊显然会是这样的:

## 优点:

*   内容及其呈现的分离
*   独立于表示层:选择任何你喜欢的前端服务技术——静态网站生成器、普通 HTML 和 JS、web 框架
*   内容的单一位置:在任意数量的网站或移动应用程序上使用
*   开发人员喜欢 API——这不是一个明显的优势，但是有意义，因为不是每个开发人员都喜欢学习特殊的模板语言

## 缺点:

*   你需要多一层管理——表示层(所以你可能需要基础设施:版本控制、web 服务器等等)。)
*   孤立的成本:CMS 本身的付款，开发人员的工作付款，基础设施付款可能
*   更“昂贵”开发人员:很明显，开发人员应该更有资格，将花费更多的时间
*   可能需要时间:你需要学习 API，集成它，调试和测试

# 耦合 CMS

耦合 CMS——内容管理系统，处理两层:内容层和表示层。这些都是老派玩家，比如 Wordpress、Drupal 或者类似的。这个想法非常相似——你的网站应该完全由一个系统提供服务。

以下是这种类型的 CMS 的优点和缺点:

## 优点:

*   固体系统:内容和它的表现(HTML)耦合在一起
*   明确网站开发成本:一个系统—一个账户—一次付款
*   开发者准入门槛低
*   快速结果:“API”已经过测试和集成，您将立即看到变化

## 缺点:

*   依赖表示层:可能性有限
*   仅网站内容(在缺少 API 的情况下):你不能在其他地方的移动应用程序中使用相同的内容
*   开发人员的学习:比起特殊语言，他们更喜欢自己喜欢的语言

正如你可能注意到的，第一个的一些优点是第二个的缺点，反之亦然。根据您的业务任务和上面的列表，您可以决定选择哪一种 CMS 类型。所以这些系统看起来像是彼此的对应物。如果只是把两者的好处结合起来，顺便消除所有的缺点呢？听起来对我来说很有趣，这可能是在 [APIQ CMS](https://www.apiq.io) 进行研究和实施的一个很好的理由。

你怎么看待这种可能性，它对你有意义吗？

*这篇* [*文章*](https://www.apiq.io/2017/07/04/headless-cms-or-coupled-cms/) *原载于* [*APIQ CMS 博客*](https://www.apiq.io/blog) *。*