# 现代 JavaScript 开发路线图(2017)

> 原文：<https://medium.com/hackernoon/a-map-to-modern-javascript-development-2017-16d9eb86309c>

所以你在过去的 5 年里一直在做 REST APIs。或者，你可能一直在优化公司庞大数据库的搜索。也许是为微波炉编写嵌入式软件？您已经有一段时间没有使用 Prototype.js 在浏览器中进行适当的 OOP 了。现在你决定是时候提高你的前端技能了。你看一看风景，它看起来像这个。

你当然不是在找沃尔多。你随便找了 25 个人，却不知道他们的名字。这种不知所措的感觉在 [JavaScript](https://hackernoon.com/tagged/javascript) 社区非常普遍，以至于“JavaScript 疲劳”这个术语实际上是存在的。当你有时间看一些关于这个主题的喜剧时，[这篇文章](https://hackernoon.com/how-it-feels-to-learn-javascript-in-2016-d3a717dd577f#.1ubvm0x0u)出色地反映了这一现象。

但是你现在没有时间了。你在一个巨大的迷宫里，你需要一张地图。所以我做了一张地图。

首先声明一点:这是一个帮助你快速启动并运行的备忘单，你不必自己做太多的决定。基本上，我将设计一套工具，这些工具可以一起用于通用前端开发。这将使你对环境感到舒适，并为你省去一些麻烦。一旦您完成了这些主题，您将有足够的信心根据您的需要调整堆栈。

## 地图的结构

我会把地图分成你需要解决的问题。对于每个问题，我将:

*   描述问题或对工具的需求
*   决定你将使用哪个工具来解决这个问题
*   解释我为什么选择这个工具
*   给出几个备选方案

## 包装管理

*   **问题:**需要组织你的项目和你的依赖项。
*   **解决方案:** NPM 和纱线
*   **原因:** NPM 几乎是事实上的包装经理。Yarn 运行在 NPM 之上，但优化了依赖关系解析，并保留了一个库的精确版本的锁文件(与 NPM 的语义版本化一起使用，它们不是排他的，而是互补的)。
*   替代品:据我所知没有。

## **JavaScript 风格**

*   **问题:** ECMAScript 5(又名老派 JavaScript)烂透了。
*   **解决方案:** ES6
*   原因:这是未来的 JavaScript，但你现在就可以使用。合并了许多其他编程语言已经使用了很长时间的有用特性。有趣的新特性:箭头函数、模块导入/导出功能、解结构、模板字符串、let 和 const、生成器、承诺。如果你是一个 Python 程序员，你会有宾至如归的感觉。
*   **替代品:** TypeScript，CoffeeScript，PureScript，Elm

## 运输文件

*   **问题:**很多仍在大量使用的浏览器并没有实现 ES6。你需要一个程序将你的现代 ES6 翻译(转换)成同等的、支持良好的 ES5。
*   **解决方案:**通天塔
*   **理由:**运行完美，几乎是事实上的标准。传输文件服务器端。
*   **替代品:** Traceur
*   **注意:**您将使用 babel-loader，一个 Webpack 加载器(稍后会详细介绍)。如果您打算使用任何其他类型的 JavaScript，您将需要 transpiling。

## **林挺**

*   问题:编写 JavaScript 有无数种方式，一致性很难实现。有些虫子可以用棉绒来防止。
*   **解决方案:** ESLint
*   **理由:**出色的代码洞察力和可配置性。airbnb 预置是你启动和运行所需要的一切。真的可以帮助你习惯新的语法。
*   **替代品:** JSLint

## 集束

*   问题:您不再使用平面文件或文件序列。需要正确解析和加载依赖关系。
*   **解决方案:** Webpack
*   **原因:**高度可配置。可以加载各种依赖项和资产。它是可插拔的。它几乎是 React 项目事实上的捆绑器。
*   **备选方案:**浏览确认
*   **缺点:**刚开始可能有点难配置。
*   你会想花些时间真正了解这个家伙是如何工作的。你也应该学习巴别塔加载器，风格加载器，css 加载器，文件加载器，网址加载器。

## 测试

*   **问题:**你的 app 很脆弱。它会分崩离析。你需要测试。
*   **解决方法:** Jest。
*   **理由:**包含电池，[快照测试](https://facebook.github.io/jest/docs/en/snapshot-testing.html)，可以检测受你的更改影响的测试，并只运行那些测试，与 monorepos 配合良好，默认与 CRA 一起提供，由脸书支持。
*   **替代品:**茉莉、摩卡、胶带。

## UI 框架/状态管理

*   **问题:**这是其中一个大问题。水疗变得越来越复杂。易变状态特别麻烦。
*   **解决:**反应并还原
*   使用 React 的理由:令人兴奋的范式转变，打破了许多和网络一样古老的教条，并且做得令人惊讶。比传统方法更好的关注点分离:不是通过技术(HTML/CSS/JavaScript)来分离，而是通过功能(内聚组件)来分解。你的 UI 是你的状态的一个纯粹的函数。
*   **使用 Redux 的理由:**如果你的应用程序很重要，你需要一个工具来管理状态(否则你就要为你的组件相互对话做体操，先学习普通的组件间通信来体验它的局限性)。网上的每一个教程都将带你穿过令人困惑的、抽象的通量模式和所有曾经有过的实现。为自己节省大量的时间，直接去 Redux。它以非常简单的方式实现了这个模式。甚至脸书也用这个。额外的精彩:重新加载和保持应用程序状态，时间旅行，可测试性。
*   **替代品:** Angular2，Vue.js。
*   **警告:**第一次看《JSX 电码》的时候，你可能会有一种想用生锈的勺子把自己的眼睛挖出来的冲动。抵制诱惑，找到一个论坛，愤怒地大喊大叫。这只是多年灌输造成的认知失调。原来在一个文件中混合 HTML、JavaScript 和 CSS 是超级棒的。相信我！—成就因在一个项目符号中使用两个蹩脚的引用而解锁。

## DOM 操作和动画

*   **问题:**猜猜看？在必须针对选择器并直接在 DOM 节点上执行操作的情况下，您仍然需要偶尔的快速修复。
*   **解决方案:**普通 ES6 或者 jQuery。
*   **原因:**是的，jQuery 还活得好好的。React 和 jQuery 并不相互排斥。但是，请注意，您应该能够使用 vanilla React(和`querySelector`)完成您需要的大部分工作。添加 jQuery 也会稍微增加您的包的占用空间。我要说的是，在 React 上使用 jQuery 是一种怪味，你应该尽可能避免它。如果您遇到了某个仅靠 React + ES6 特性无法解决的难题，或者您正在处理一些令人讨厌的跨浏览器问题，jQuery 可能会扭转局面。
*   道场(那还存在吗？).

## 式样

*   **问题:**现在你有了合适的模块，你希望它们是独立的、可重用的软件，你可以到处移动。组件风格应该和组件本身一样具有可移植性。
*   **解决方案:** CSS 模块。
*   **理由:**尽管我很喜欢内嵌样式(并广泛使用)，但我必须承认它们相当有限。是的，在 React 中使用内联样式是完全可以的，但是你不能用它们来针对伪类选择器(比如`:hover`)，这在很多情况下是一个障碍。
*   **替代品:**内联风格。我特别喜欢 React 中的内联样式的一点是，它们允许您将样式视为常规的 JavaScript 对象，这使您能够以编程方式处理它们。此外，它们与您的组件位于同一个文件中，这使得它们非常容易维护。有些人仍然主张萨斯/SCSS/少。这些语言意味着一个额外的构建步骤，不像 CSS 模块/内联样式那样可移植，但是和以前一样强大。

## 关于样板文件

像 [Create React App](https://github.com/facebookincubator/create-react-app) 这样的样板项目可以减轻上述问题的负担。当使用样板文件时，您仍然需要了解幕后发生了什么——否则，您将永远不会真正拥有您的构建。

## 就是这样！

你现在有一大堆东西要研究，但至少你不需要花这么多时间做研究。你觉得我错过了什么吗？我把球掉在什么地方了吗？发表评论或在 twitter 上联系我 [@bug_factory](http://twitter.com/bug_factory) 。

**编辑 1:** 修正了关于 JavaScript 疲劳的帖子的链接(谢谢，[克里斯·伍兹](https://medium.com/u/41ed62efbc0?source=post_page-----16d9eb86309c--------------------------------)！).添加了关于其他语言也需要翻译的注释(谢谢， [Ignacio Rossi](https://medium.com/u/c219a686a2eb?source=post_page-----16d9eb86309c--------------------------------) ！).将 Jest 添加到替代测试工具列表中(谢谢， [Tiago Pina](https://medium.com/u/dc21ca37053a?source=post_page-----16d9eb86309c--------------------------------) 和 [Chris Khoo](https://medium.com/u/6b6cbb72e6ef?source=post_page-----16d9eb86309c--------------------------------) ！).增加了关于造型的部分(谢谢，[补锅匠](https://medium.com/u/eba2f00f98b9?source=post_page-----16d9eb86309c--------------------------------)！).感谢大家分享和发送反馈！

**编辑 2:** 关于 jQuery 的改进章节(谢谢， [Eldar Shamukhamedov](https://medium.com/u/74fb6839f7f4?source=post_page-----16d9eb86309c--------------------------------) ！)

**编辑 3:** 在测试部分用 Jest 替换了 Mocha。

**编辑 4:** 添加了关于样板的注释。

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 要了解更多信息，请[阅读我们的“关于”页面](https://goo.gl/4ofytp)、[在脸书上给我们点赞/发消息](http://bit.ly/HackernoonFB)，或者简单地说， [tweet/DM @HackerNoon。](https://goo.gl/k7XYbx)
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！