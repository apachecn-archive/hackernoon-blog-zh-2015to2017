# 帮助 Opendoor 在住宅中买卖超过 100 美元 1B 的堆栈

> 原文：<https://medium.com/hackernoon/the-stack-that-helped-opendoor-buy-and-sell-over-1b-in-homes-4a2e59fbcea7>

## 最初发布于 [StackShare](https://stackshare.io/opendoor/the-stack-that-helped-opendoor-buy-and-sell-over-$1b-in-homes)

![](img/df3471c9e5749187d9bf76f3893ce6b5.png)

# 关于开门

除非你在旧金山或纽约，否则卖掉你的房子是一件非常头疼的事情，通常会持续三个月。 [**Opendoor**](https://www.opendoor.com/) 让你不再头疼——上网询价，回答几个问题，我们就会直接从你手里买下你的房子。我们会从那里接手，把房子卖给另一个买家，而你可以继续你的生活。

现在我们在凤凰城、达拉斯和拉斯维加斯开展业务。我们已经完成了 4800 多宗房地产交易——房屋价值超过 1B。对于一家即将成立 3 年的公司来说，我们已经走了这么远，这是相当疯狂的。

一笔房地产交易包含很多内容。首先，你可能会认为我们的核心工程挑战是:对每个家庭做出准确的报价。如果我们出价太高，我们会赔钱并倒闭；如果我们提供的太少，我们会显得像骗子，冒犯我们的顾客。

在我们买下房子后，我们会和承包商一起进行必要的维修和润色，然后把房子放到市场上，找到买家。由于我们拥有每一个家庭，我们可以做一些聪明的事情，比如在所有的门上安装智能锁，并提供全天开放的房屋。

我是一名前端工程师，主要从事面向消费者的网站工作。我目前正致力于改善首次购房者的体验。对于对房地产一无所知的人来说，这个过程真的很可怕。

# 工程组织

我们的团队分为产品工程和数据科学两部分:每个团队使用的工具都有很大的不同，以至于团队在不同的代码库中工作。当然，最终的产品必须是良好集成的，产品团队从数据科学 API 中提取大量数据。这种协调很难做好；数据科学团队的 Kevin Teh 在最近的一篇文章 中详细描述了这一点。

首先，我们将产品团队分成“面向客户”和“内部工具”组。让所有的前端工程师在同一个团队中是很好的，但是我们注意到一些项目没有明确的所有者。例如，我们的买家支持团队使用我们开发的一些内部工具。这些工具应该由“内部工具”团队开发，还是支持是客户体验的一部分？

现在，该团队被划分为基于部分业务的跨职能团队。卖家团队处理卖给我们的人；家园团队处理装修和库存；买家团队把我们的房子放到市场上，寻找买家。

随着我们的成长，团队之间的界限经常变得模糊，所以我们期望结构将会一直发展。工程师在团队之间流动很常见，包括在产品和数据科学团队之间。

# 产品架构

我们在 2014 年开始使用[**Ruby on Rails**](https://stackshare.io/rails)monolith 和 [**Angular**](https://stackshare.io/angularjs) frontend，这两者都是在我们非常小的时候快速移动的好方法。

![](img/efd6781017b6918be8b012479a12d671.png)

我们面向客户的产品的 MVP 是一个多页的表格，你可以输入关于你家的信息来获得报价，但这只是冰山一角。我们必须建立内部工具来帮助我们的团队正确地给房屋定价并管理交易过程。我们使用[](https://stackshare.io/angularjs)**和 [**引导**](https://stackshare.io/bootstrap) 来构建这些工具；主要目标是快速添加特性，不需要摆弄 CSS——事实上，根本不需要任何前端经验。**

**我们使用 [**Puma**](https://stackshare.io/puma) 作为我们的网络服务器，使用 [**Postgres**](https://stackshare.io/postgresql) 作为我们的数据库——一个很大的好处是用于位置数据的 [**PostGIS**](https://stackshare.io/postgis) 扩展。 [**Sidekiq**](https://stackshare.io/sidekiq) 在 [**Redis**](https://stackshare.io/redis) 的支持下运行我们的异步作业。[**elastic search**](https://stackshare.io/elasticsearch)在我们的内部工具中随处可见。我们使用 [**Webpack**](https://stackshare.io/webpack) 来构建我们的前端应用，并使用 Rails 资产管道来服务它们。**

**我们使用 [**Imgix**](https://stackshare.io/imgix) 来存储我们家的照片，以及我们网站周围的大多数图标和插图。我们主要使用 Imgix 的自动调整大小特性，所以我们不会丢失原始图像的轨迹，但是以后可以在前端为每个上下文加载适当大小的图像。**

## **整体到微服务**

**在适当的情况下，我们尝试将隔离的逻辑分解为微服务。例如，我们正在开发一项计算我们预计成本和费用的服务。我们的成本结构经常变化，我们想估计政策变化会如何影响我们的费用。这段代码不太适合 Rails 应用程序，因为我们希望分析师和数据科学家也能访问它。**

**我们现在已经将这个逻辑拆分成它自己的服务。它使用一个版本历史感知计算图来计算和回溯测试我们的内部成本，并且(很快！)将自带 [**React**](https://stackshare.io/react) 前端来可视化那些计算。**

**我们的数据科学堆栈也是一套完全独立的服务，因此有大量的应用程序间通信在进行。为了让这些服务相互认证，我们使用了一个名为 [**【圣骑士】**](https://github.com/opendoor-labs/paladin) 的 [**仙丹**](https://stackshare.io/elixir) 应用。Opendoor 工程师 Dan Neighman 编写并开源了 Paladin，并在这篇博文 中解释了为什么它很有帮助。认证基于 [**典狱长**](https://github.com/hassox/warden) 和 [**监护人**](https://github.com/ueberauth/guardian) 提供的 jwt。**

# **数据科学架构**

**我一直觉得 Opendoor 的数据科学很有趣，因为它不是我所熟悉的“尽可能多地获取数据，然后大规模处理它”的问题。**

**为了找到房子的价格，你查看附近最近出售的房子，然后通过与你对整个市场的了解进行比较，尽可能多地从这些数据中提取信息。 [**我们的联合创始人 Ian Wong 在这里有更深入的谈论**](https://www.youtube.com/watch?v=dR5N8cMkIGQ) 。**

**我们可以将大多数数据科学工作分为几个核心领域:**

1.  **从各种来源获取和组织数据**
2.  **训练机器学习模型来预测房屋价值和市场风险**
3.  **量化和减轻各种形式的风险，包括宏观经济和个人住房流动性**
4.  **在数据仓库中收集信息，为分析团队提供支持**

**对于数据摄取，我们从各种来源(如税务记录和评估员数据)中提取数据。我们将大部分数据转储到一个 [**RDS Postgres**](https://stackshare.io/amazon-rds-for-postgresql) 数据库中。在这一阶段，我们还会转换和规范化一切——我们从经常发生冲突的来源导入脏数据。 [**这篇博文**](https://labs.opendoor.com/2016/05/13/index-groups-postgres) 更详细地讲述了我们如何合并给定地址的数据。**

**![](img/06a0a7b327a52670319ef798c9682fa4.png)**

**对于我们的机器学习模型，我们使用 [**Python**](https://stackshare.io/python) 和来自 [**SqlAlchemy**](https://www.sqlalchemy.org/) 、 [**scikit-learn**](http://scikit-learn.org/) 和 [**熊猫**](https://stackshare.io/pandas) 的构建模块。我们使用 [**Flask**](https://stackshare.io/flask) 来路由/处理请求。我们使用 [**Docker**](https://stackshare.io/docker) 构建映像，使用 [**Kubernetes**](https://stackshare.io/kubernetes) 进行部署和扩展。我们的系统允许我们将模型描述为 JSON 配置，一旦部署，系统自动获取所需的特性，训练模型，并根据性能指标评估模型的表现。这种自动化让我们快速迭代。**

**我们开始使用 [**Dask**](http://dask.pydata.org/en/latest/) 进行特征提取和处理。其他公司经常为此使用 Spark 和 Hadoop，但我们需要支持更复杂的并行算法。Dask 的 [**与 PySpark post**](http://dask.pydata.org/en/latest/spark.html) 的对比完美地描述了这一点:**

> ***Dask 重量更轻，更容易集成到现有代码和硬件中。如果您的问题超出了典型的 ETL + SQL，并且您希望向现有解决方案添加灵活的并行性，那么 dask 可能是一个很好的选择，特别是如果您已经在使用 Python 和相关的库，如 NumPy 和 Pandas。***

**我们的数据科学架构的最后一部分是数据仓库，我们使用它从任何地方收集分析数据。在很长一段时间里，我们使用每晚`pg_dump`将 [**Postgres**](https://stackshare.io/postgresql) 数据从每个服务的数据库直接转移到一个自建的数据仓库中。我们最近改用 Google 的 [**BigQuery**](https://stackshare.io/google-bigquery) 了。BigQuery 速度更快，可以让我们在每个查询中放入更多的数据，但最大的特点是它是无服务器的。我们有很多人在“高峰时间”运行查询，不希望仅仅因为我们有预先分配的可用服务器数量而导致速度变慢。**

# **高科技开放日**

**由于 Opendoor 实际上拥有我们出售的所有房屋，我们可以在如何向潜在买家展示这些房屋方面有所创新。**

**通常情况下，如果你想看房出售，你必须给房屋中介打电话，安排时间。我们很早就意识到，我们可以通过在门上安装自动锁来使开放房屋更加方便，这样就可以随时进入房屋。对于该项目的 0 版本，我们在所有房子的门上贴上了产品副总裁的电话号码——买家会打电话进来，他会告诉他们解锁代码。**

**对于版本 1，我们增加了 [**Twilio**](https://stackshare.io/twilio) 这样我们就可以通过短信自动发送解锁码。对于版本 2，我们构建了一个移动应用程序。**

**![](img/67d30dcda9a7e5a569ff8a8e3ba37e44.png)**

**如今，客户期望获得良好的移动体验，但我们的全天开放功能使其变得更加重要。你可以在开车时使用该应用程序找到附近的房屋，并心血来潮地探索它们——这是对传统过程的巨大改进！**

**我们在 [**React Native**](https://stackshare.io/react-native) 中构建了我们的应用。这个选择的主要部分是务实的——我们的团队在 web 技术方面有很多经验，但在本地技术方面几乎没有经验。我们还希望从一开始就支持 iPhone 和 Android，React Native 让我们做到了这一点(我们首先发布了 iPhone 应用程序，添加 Android 只需要额外的几周时间)。**

**不是每个人都想安装应用程序，所以仍然可以通过短信访问我们的家庭。我们增加了一些安全机制——值得一提的是 [**Blockscore**](https://stackshare.io/blockscore) ，它让我们可以使用电话号码快速进行身份验证。对于风险较高的号码，我们会禁用自动输入系统，并让我们的支持团队致电客户收集他们的信息。**

# **工具和工作流程**

**我们管理我们的库，并在 GitHub[](https://stackshare.io/github)**上进行代码审查。所有的代码至少由另一个工程师审查，但是一旦它在`master`分支中，它就被假定为准备好部署。如果您想要部署代码，可以通过三个步骤来完成:****

1.  ****`./bin/deploy staging`****
2.  ****检查你在舞台上的工作****
3.  ****`./bin/deploy production`****

****这总共需要 10-15 分钟。我们努力实现流程自动化，这样我们就可以作为一个团队快速前进。我们使用 [**Heroku**](https://stackshare.io/heroku) 进行托管，并在 [**CircleCI**](https://stackshare.io/circleci/circleci) 上运行自动化测试。 [**懈怠**](https://stackshare.io/slack) 机器人程序报告正在部署什么。****

****我们非常依赖许多外部服务。简单浏览一下:帮助侦察邮件的[](https://stackshare.io/help-scout)**[**Dyn**](https://stackshare.io/dyn)； [**Talkdesk**](https://stackshare.io/talkdesk) 和 [**Twilio**](https://stackshare.io/twilio) 用于通话和客服； [**HelloSign**](https://stackshare.io/hellosign) 用于网上签约； [**新遗迹**](https://stackshare.io/new-relic) 和 [**纸质遗迹**](https://stackshare.io/papertrail) 进行系统监控； [**哨兵**](https://stackshare.io/sentry) 进行报错。******

****对于分析，我们使用了很多工具: [**Mixpanel**](https://stackshare.io/mixpanel) 用于 web， [**振幅**](https://stackshare.io/amplitude) 用于移动， [**堆**](https://stackshare.io/heap) 用于追溯事件跟踪。我们主要使用 [**Looker**](https://stackshare.io/looker) 来挖掘数据并制作仪表板。****

# ****加入门户开放工程****

****Opendoor 有一种非常创业、务实的文化:这里的工程师通常会与客户交谈，了解他们的需求，并在项目上采取主动。我们热衷于所有权和授权他人，并且积极地反对 snark。****

****![](img/7485694c2414c1d23bbd36b6e5d47f20.png)****

****我们正在寻找各种背景的工程师:不管你现在用什么语言工作，我们相信你会发展得很快。****

****在 [**StackShare**](https://stackshare.io/opendoor#jobs) 或我们的 [**职业网站**](https://www.opendoor.com/jobs) 上找到更多关于开放式职位的信息。****

****非常感谢 Kevin Teh、Mike Chen、Nelson Ray、Ian Wong 和 Alexey Komissarouk 帮助我们完成这篇文章。****

****[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)********[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)********[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)****

> ****[黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)，并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。****
> 
> ****如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！****

****![](img/be0ca55ba73a573dce11effb2ee80d56.png)****