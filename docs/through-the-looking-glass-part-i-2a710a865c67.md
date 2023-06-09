# 透过镜子(第一部分)

> 原文：<https://medium.com/hackernoon/through-the-looking-glass-part-i-2a710a865c67>

## 进入 YCombinator

对于我们在 YCombinator 项目下的团队工作经历来说，这原本是一个更大的部分，但已经被精简了。原文仍然是一个参考点，但一些重要的方面和个人元素，现在不再是这三篇文章的一部分。第二部分可以在这里找到[](/@siilime/through-the-looking-glass-part-ii-db18c35aeca4)**。**

*![](img/f0e00de889fa1e4bd8a459845c3e0d50.png)*

*In April I received a call from an old friend, which we’ll refer to as Pete for the sake of privacy. I knew him from my time working in Manchester, United Kingdom. We’d previously worked on three separate projects together, mostly focused on hardware development, including a scalable gaming & artificial intelligence development platform, a fashion-based wearable, (launched in 2017), and a portable storage solution. Our relationship mostly consisted of him reading a wealth of material on what he felt he wanted to build, and then testing his ideas against me. I would then feedback with in-depth technical reviews and routes to delivery. What persisted was a partnership with great respect, communication, and an appreciation for great design, oriented around Japanese aesthetics, including Wabi-sabi (侘寂), and Ensō (円相).*

*当电话铃响的时候，我们立即开始互相更新我们在哪里；我们在做什么项目；我们面临的困难。我知道他想从我这里得到什么，我非常愿意支持他。话题不可避免地转到了我是否有时间接手另一个项目。那时，我完全被锁定在一个我已经研究了 5 年多的机器学习项目上。我即将发布一个新的更新，并希望保持专注。然而，当他提到高度可扩展的分布式数据、安全性和密码学——我自己的项目中不可或缺的主要元素——我觉得这将是一个很好的机会来测试这个新项目中我现有工作的一部分。我仍然犹豫不决，特别是因为这个项目是围绕金融科技展开的。特别是保险——很容易赚钱，但我自己没什么兴趣——所以我说我很乐意继续这个话题，并尽我所能给予支持，只要这个项目对我目前的工作来说是一个补充。*

*在这一点上，他承认他有另一个技术负责人的选择，这个人由于他自己的分布式账本项目而不可用，但他将作为一个全新的可重复使用的[区块链](https://hackernoon.com/tagged/blockchain)解决方案提供这个项目的核心骨干。我没有因为不是他的首选而生气；我很高兴他向我征求意见，而不觉得需要获得一个特定的角色，或者以任何实质性的方式参与进来。我表达了我对帮助一个已经有第三方平台的解决方案的担忧。我需要对项目的所有元素进行尽职调查，这将是一个重要的部分，作为堆栈的核心基础。*

# *这个概念*

*最初的想法是围绕一个基于表单的保险行业 Web 应用程序。大多数功能似乎不需要区块链的解决方案，或者任何形式的分布式账本技术。一个核心特征是“无信任”模式，该系统可以验证通过各方输入的数据生成的合同上的数字签名，然后自动与银行执行这些协议和支付条款。这个不可信的要求是决定研究区块链/DLT 的关键，加密签名对我来说很有意义。然而，在项目的这个阶段，区块链似乎仍然是一个额外的、不必要的跳跃。最近，我将自己项目的很大一部分从以太坊迁移到了 Hyperledger Fabric，因为很明显，Hyperledger Fabric 将促进必要的智能合约功能，而没有区块链的性能开销，我觉得这个新项目可能不会有实质性的不同。*

*我和他的区块链专家谈过了；“德韦恩”，正如我们所同意的，我们进行了一次相当有礼貌的谈话。我不同意他的技术选择，(主要是在 Java 虚拟机上构建 DLT)，但他坚持认为这项技术可以在以后改变，尽管他投入了 5 年的时间和 300，000 行代码来构建它。我也觉得他的背景似乎很混乱，没有重点，但我的背景也是如此，所以我没有理由进行这样的争论。*

*我说我需要在使用他的技术之前验证它，并且我仍然会将系统设计成与任何第三方平台松散耦合，包括他的平台。Dwayne 希望将该平台作为自己的知识产权保留在一个独立的公司实体下，这敲响了警钟，因此保护我的朋友并确保解决方案始终使用最合适的组件对我来说非常重要。我在通话后明确了这一点，我们同意进行代码审查，我们会有一份代码副本以降低风险，并且最终将由我决定我们是否利用这个第三方平台。*

# *应用于 YCombinator*

*皮特在结束这些初步对话时表示，他正在申请 2017 年夏季 YCombinator 加速器计划，需要我同意担任联合创始人兼首席技术官(CTO)，以便进一步发展。他觉得如果他不能在申请书上附上我的名字，他就不会成功。在我任职期间，我需要把工作室现有的薪水减半，并且完全专注于他的项目。我花了几天时间做决定，出于尊重和热心帮助，我勉强同意了，规定我们将专注于在项目结束时准备好演示产品，也许在 6 周内得到一个功能原型。我们的目标是在最初几周内有 4 到 6 名开发人员参与这个项目，并有大量的预算来实现这一目标。*

*我觉得 YCombinator 有经验的人会在这个阶段看到任何产品的缺乏，无论如何都会拒绝申请，可能会给我们机会再次尝试更合理的 2018 年冬季计划。我有丰富的与创业公司和加速器项目合作的经验，我很少看到任何仍处于孵化阶段的想法成为加速器，尤其是 YCombinator，我建议 Pete，几个月的开发将使他的项目进入一个更健康的状态。*

*几天后，我收到一条短信，询问我能否在 5 月 1 日飞往山景城参加 YCombinator 的演讲。我已经有计划了，所以我不情愿地拒绝了，并试图安排另一个会议日期。在收到提议的时间表和回复之间的几个小时里，所有的时间都被占用了，所以我问皮特是否可以不带我去。*

*YCombinator 上的演示没有我参加，我对它没什么期待。紧接着，我收到了一条短信，告诉我收拾行李，因为我们已经被 2017 年夏季项目录取，从 6 月初开始。我既失望又兴奋；从内部观察 YCombinator 如何运作的想法很吸引人，但我想在赫尔辛基为我自己的项目专注于优先事项，并且觉得这个想法太不成熟，不适合参加这个项目。我决定不让皮特失望，并把我的另一个项目推到一边，通知我现有的客户和合作伙伴，因为我把所有需要的东西拉到一起，建立一个团队，设计和制造一个新产品。*

# *在山景城着陆*

*招聘过程立即开始，在社交媒体、 [StackOverflow](https://stackoverflow.com) 、 [LinkedIn](https://linkedin.com) 上登广告，最后是[科技女孩](https://girlsintech.org/)(令人失望的是，我们没有收到科技女孩的申请)。我选择用 [Go](https://golang.org) 、 [Rust](https://www.rust-lang.org) 、 [Swift](https://swift.org/) 来开发产品的核心，分别专注于基础设施、数据 IO、应用逻辑。我在赫尔辛基的工作室使用了这三款软件，感觉它们涵盖了所有的内容，达到了很好的标准。我研究的大多数有趣的新 DLT 技术都使用了类似的技术，我觉得它会给我们提供一个强大的前进平台。事实上，我们将有 3 个月的时间来交付项目，这解决了我对他们的新性的担忧，并且这三个社区在加密货币和 DLT 市场以及云计算提供商方面的实力都在快速增长。我还可以重复使用我工作室的许多技术来扩大我们的地位，并更快地行动。*

*在我们搬家之前，我已经在赫尔辛基对世界各地的候选人进行了几次远程面试。Rust 社区非常支持我，一旦他们明白 Rust 将是我们产品成功的核心。他们在社交媒体上发布了我关于需要优秀开发人员的帖子，Mozilla 团队的一些人把我和印度一位年轻的 Rust 开发人员 Ravi 联系了起来。我们聊了聊，他完成了我给所有候选人的任务，然后我们又聊了聊。尽管他缺乏作为社区成员开发 Firefox 之外的经验，但他的才能和对挑战的兴奋使这一决定变得很容易。我给皮特打了电话，提出了一个薪水提议，让他们两个人来安排。*

*Our original tweet, supported by the Rust community*

*我们需要有人专注于不分心的设计工作，以便其他的技术工作可以迅速发展。我在工作室的合作伙伴，一个图形、网页和移动设计师(Gabi)是可用的，所以我建议我们利用她作为一个自由职业者，只要我们需要设计。决定权在我，所以我们俩都收拾好行李，飞往山景城，德韦恩和皮特已经搬进去安顿好了。这栋房子——每月 6800 美元的平房——有一个附属的后扩建部分。加比和我搬进了隔离区，我们开始确定我们需要建造什么。*

*我已经开始转换我自己项目的一些核心元素来支持这个智能保险解决方案；我将一些部分移动到位，并开始收集构建一个简单的基于 web 的应用程序所需的服务。没过多久，来自印度的新员工 Ravi 就来到了山景城。我到这里已经一个星期了，但是这里已经挤满了无聊的管理和安装工作。*

*我已经为未来的项目工件创建了一组基本的代码库，设计了一个初步的开发路线图，为整个项目应用了一个敏捷的工作流程，并且我们已经就产品需要如何向前发展进行了大量的计划会议/讨论。我们准备好开始编码了。*

*这是三部曲中的第一部。第二部分可以在这里找到[](/@siilime/through-the-looking-glass-part-ii-db18c35aeca4)**。***