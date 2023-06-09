# 前端开发环境作为一个包

> 原文：<https://medium.com/hackernoon/frontend-development-environment-as-a-package-7f74c3fe46d7>

## 或者何时构建自己的创建-反应-应用程序

![](img/51937a2a872022a8214c7b9519246e68.png)

[Photo by Ksenia Makagonova from unsplash.com](https://unsplash.com/search/photos/toolbox?photo=bngKirnA1EE)

近年来， [JavaScript](https://hackernoon.com/tagged/javascript) 工具生态系统的发展令人惊讶。可用工具的数量爆炸式增长，启动一个被认为是*现代*的项目所需的设置的复杂性直线上升*。*这一点，以及这些[工具](https://hackernoon.com/tagged/tools)的快速变动率在很大程度上导致了著名的 *JavaScript 疲劳。*这种挫败感催生了许多旨在抽象掉这种复杂性的项目，通常采用零配置开发设置的形式。最显著的例子是 [nwb](https://github.com/insin/nwb) 和 [create-react-app](https://github.com/facebookincubator/create-react-app) ，但是[列表正在增长](https://github.com/facebookincubator/create-react-app#alternatives)。

这些项目通常以两种方式帮助开发人员:

*   处理样板应用程序代码这可以采取简单地提供一个复制粘贴的应用程序*框架*的形式，但是使用 CLI 搭建工具如 [yeoman](http://yeoman.io/) 可以变得非常复杂。
*   **提供开发环境**这意味着捆绑一组组成前端开发环境的工具。这些包括开发服务器的实时重载，构建管道的代码捆绑和编译，测试设置，林挺，类型检查等。

最近对探索后者产生了兴趣，姑且称之为*开发环境作为一个包*(比较拗口，还是用吧💻🏞📦简称)。这个想法很简单。将应用程序代码周围的所有基础设施提取到一个项目所依赖的可安装包中。只需`yarn add my-dev-env -D`就大功告成了。虽然这看似合理，但让我们先来探究一下为什么这可能不是一个好主意。

# 为什么不应该使用💻🏞📦

每当您提取项目的一部分或它的依赖项并围绕它构建抽象时，您就引入了一个间接方式，将提取的代码放在一个黑盒中。一旦提取的代码[中的限制或错误开始泄漏](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)，这种间接性将不可避免地需要被拆箱。打破内心的抽象会变得混乱和令人沮丧。尤其是当流程涉及到复杂的工具和复杂的配置时，比如现代前端工具( [eslint](http://eslint.org/docs/user-guide/configuring) 、 [webpack](https://webpack.js.org/configuration/) 等)。).

> ***实际例子*** 您的单元测试套件出现了隐晦的测试运行错误。在传统的设置中，您可以通过在项目的根中使用测试运行器配置来进行调试，但是使用*💻🏞📦*你必须首先`*yarn link*`dev env 包，或者在`*node_modules*`目录中的某个地方进行修改。

围绕低级工具构建包装器会导致无法访问它们的某些特性。当工具引入新特性并且您的包装器阻止您轻松访问它们时，这变得特别受限。

> ***实用示例*** 新版本的 webpack 引入了对包大小的优化，前提是您在配置中添加了一个插件。使用传统的设置，你可以简单地升级 webpack 并将插件配置粘贴到你的`*webpack.config.js*`中，但是使用*💻🏞📦*您需要完成更新外部依赖关系(可能是第三方)的过程。

最后，大多数工具都是为直接在项目中使用而优化的，将它们提取到一个包中可能需要一些繁琐的工作。这给你的设置增加了新的复杂性，这是你原本不需要的。

虽然这些是不可否认的缺点💻🏞📦方法，他们并没有阻止`create-react-app`这样的项目变得非常受欢迎。

# 为什么您应该使用💻🏞📦

一些明显的优势包括启动新项目所需的时间和精力的显著减少，以及工具链的方便升级，尤其是跨多个项目的升级。当您不必花费数小时试图让不同的工具协同工作时，专注于创作为您的最终用户增加真正价值的代码也容易得多。外包开发环境设置对于那些发现*前端操作*任务具有挑战性、乏味或枯燥的开发人员来说是天赐之物。

> ***实际例子*** 一个由开发服务器、林挺、测试和构建管道组成的前端开发环境，可以轻松拥有 50 个开发依赖和 10 个配置文件。例如，通过使用`*create-react-app*`，你将得到一个开发依赖项，而没有配置文件。

但是使用的积极影响💻🏞📦超越了节省时间和更干净的目录列表。以我的经验来看，它可以鼓励大规模项目使用一个更加解耦的架构。通过允许轻松的引导和简化的更新，它有助于做出拆分代码库的决定。因此，它还鼓励通过试验新的工具和方法来持续改进，这些工具和方法可以很容易地移植到旧的项目或被丢弃。

> ***实际例子*** 当开始一个新项目时，一个团队选择不使用*💻🏞📦*用于 a 公司所有其他项目。他们这样做是为了尝试 Jest 作为单元测试运行器，而不是当前设置中使用的 Mocha。过了一会儿，他们决定完全迁移到 Jest——他们将 Jest 安装在他们的*中💻🏞📦*，发布一个新版本，在所有其他项目中升级它，并使用 [codemods](https://github.com/skovhus/jest-codemods) 来迁移测试。

从更全面的角度来看，选择💻🏞📦方法而不是为每个项目单独设置可以产生超出代码库的积极影响。在产品团队从事多个前端项目的公司中，引入💻🏞📦让开发人员更容易组成跨团队或切换团队，也让项目更容易改变所有权。它还减少了不同团队以稍微不同的方式解决相同问题所浪费的总时间。

> ***实战范例*** 在我工作的公司， [issuu](https://issuu.com) ，我们有 5 个产品团队，每个团队维护几个前端项目。不久前，这些项目中的每一个都有一个相似但略有不同的开发环境。我们开始迁移到*💻🏞📦*开始新产品时，首先在一个团队中尝试这种方法。今天，我们有大约 10 个项目跨 3 个团队使用它，并计划很快迁移更多。我们喜欢由一个团队实现的改进可以在所有这些项目中使用，而不需要额外的努力。

如前所述，开放源码有很多选择💻🏞📦解决方案就在那里。然而，我已经决定尝试编写自己的程序，这让我对这种方法的利弊有了一些了解。先说坏处。

# 为什么你不应该自己写💻🏞📦

如果你考虑建造一个克隆体的原因是 NIH 综合症，那么你和社区花时间为一个现有的项目做贡献可能会更有益。

通过坚持既定的和经过战斗考验的解决方案，你和你的团队将避免一系列其他开发人员已经遇到并花费数小时解决的问题。你也将能够轻松地跟上不断发展的社区最佳标准，而不会受到 FOMO 的影响。

> ***实际例子*** 前段时间的一些*原来是这样的💻🏞📦*像`*preach-cli*`一样用[不安全的方式](/@mikenorth/webpack-preact-cli-vulnerability-961572624c54)处理开发 SSL 证书。该漏洞很快被项目背后的社区修复。

当决定不使用社区支持的现有开发环境时，您还应该考虑团队的规模和涉及的项目数量。根据我的经验，这种方法在启动大量前端项目并需要维护的环境中最有意义。

还应该提到的是，编写一个健壮的💻🏞📦并不是一件容易的事情，尤其是如果你喜欢像弹出这样的高级特性(例如，一个将所有样板文件复制到项目中的选项)。

不考虑这几点，我发现内部解决方案对我的用例很有效。原因如下。

# 为什么你应该写你自己的💻🏞📦

构建自己的开发环境使您能够根据您和您的团队可能有的特定需求对其进行微调。你不必做出有时很难或根本无法接受的取舍。您可以只带您实际需要的工具，并按照您喜欢的方式配置它们。开发设置是一个非常固执己见的领域，所以遵从由现成的解决方案做出的所有决定可能是一个挑战。

> ***实际例子*** 很多开发者没有选择`*create-react-app*`，因为缺乏对 CSS 预处理程序如 Sass 以及标记的服务器渲染的支持。

此外，由于您是负责人，您可以快速迭代、修复问题和引入功能，而不需要社区批准。

在构建自己的工具时获得的经验和对工具生态系统的理解💻🏞📦是无价的。选择正确的工具并使它们作为一个可安装的包一起运行，需要对它们的特性、权衡和配置有深刻的理解。

> ***实际例子*** 为我的*选择 JavaScript bundler 时💻🏞📦*我了解到 [rollup](https://github.com/rollup/rollup) 非常适合库和小部件，因为它输出清晰，模块类型控制简单，而对于 web-apps [webpack](https://github.com/webpack/webpack) 之类的产品，它的工作非常出色，这要归功于强大的代码分割。

最后，当建立内部💻🏞📦比起一次性的开发设置，你通常更有能力关注 DX(开发者体验),让你的同事或你自己的生活更轻松。您可以优化最常见的任务和工作流程，并使用可读输出和自动完成等功能完善 CLI。

> ***实际例子*** 当在已经被另一个进程使用的端口上运行`*create-react-app*` dev server 时，这种对 DX 的关心就是一个例子——它会自动选择一个替代端口。太棒了。

# 简单的示例💻🏞📦

虽然像`create-react-app`这样的项目的代码库可能有点让人不知所措，但是构建一个简单的💻🏞📦不一定很难。不久前，我在哥本哈根的一次会议上做了一个关于这个主题的简短演讲，为了帮助这次演讲，我发表了一个简单的例子💻🏞📦使用 GitHub 上的[代码创作 JavaScript 库。您可以通过运行`yarn add cphjs-inst-dev-env -D`然后使用三个可用命令之一来尝试:`yarn cphjs-tdd` `yarn cphjs-test`和`yarn cphjs-build`。有了这个开发依赖项，你就可以用 Babel 编译捆绑 Rollup，用 SCSS 语法支持 Sass，从 JS 导入，用 ESLint 支持林挺，有更漂亮的自动修复，用 Jest 设置 TDD，在编译好的捆绑包上运行测试。](https://github.com/pekala/cphjs-inst-dev-env)

我已经使用开发环境作为我的副业项目(用`create-react-app`)以及工作(用内部解决方案)的打包方法有一段时间了。我对此相当满意，但我渴望听到你的意见。你怎么想呢?

*非常感谢* [*肯尼斯·斯科沃斯*](https://twitter.com/kenneth_skovhus) *和* [*麦兹·哈特曼*](https://twitter.com/Mads_Hartmann) *对这篇文章的评论。*