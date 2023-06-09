# 反应本地有效模式

> 原文：<https://medium.com/hackernoon/react-native-effective-patterns-3e0c9db6c32c>

## 7 个简单的模式来提高你的反应能力

![](img/4d9ce4ae3e8f85d23180e660cbf76bdb.png)

我已经和 React Native 一起工作了一段时间，无论是从个人角度还是从职业角度，我都非常喜欢它；在这篇文章中，我将描述我使用的一些模式。请记住，对一个团队起作用的东西，不一定对另一个团队起作用，并且这些例子中的许多本身不会起作用(它们是代码中孤立的部分)。

## 1.让你的大部分组件保持愚蠢

对于任何 React 应用程序都是如此。你的**视图**和组件**应该依靠道具和回调**而**容器**(智能)组件**应该依靠状态**。我推荐使用 Redux，但是在一些应用程序中，您可以使用普通的旧 setState。MobX 也是一个很好的选择。

## 2.依靠回调

在学习如何在 Swift 中编写 iOS 应用程序时，我被教导使用委托模式将视图与其行为分离。在 React Native 中，同样的效果可以通过回调来实现。回调只是可以传递给组件的箭头函数。组件有责任执行它们，但不需要知道它实际在做什么。

大多数组件不应该有任何行为。暴露简单的**回调**，它们**就像你的组件**的公共 API。你应该通过读他们的名字来知道他们什么时候被处决。例如，如果你正在开发一个电子商务应用程序，像***onSelectProduct****或****onProductAddedToShoppingCart***这样的名字就非常具有说明性。

当决定是否公开回调时，每当组件有某种用户交互时，问自己这样一个问题:
这个交互只对这个特定的组件重要吗，或者它能触发应用程序另一部分的变化吗？如果你的答案是后者，那么你应该公开一个回调。

## 3.让你的导航栈远离你的视图

对于这个特定的应用程序，我们能够从 React Native 的默认[导航器](https://facebook.github.io/react-native/docs/navigation.html#navigator)，迁移到[导航实验](https://facebook.github.io/react-native/docs/navigation.html#navigationexperimental)，再迁移到 [React 导航](https://github.com/react-community/react-navigation)。这些变化只涉及几行代码。这个想法很简单:

屏幕和视图不一样。你的**视图不应该有任何关于导航栈**的知识，而**屏幕**(或者路线，取决于你喜欢什么名字)**必须知道如何导航**以及如何与导航栏/ TabBar 通信。使用这种方法，您的屏幕将简单地用导航感知的东西包装实际的视图。例如:

如您所见，FavoritesView 只是公开了一个“onSelectFavorite”回调，并不关心它实际做了什么。FavoritesScreen 使用该回调来告诉导航器导航到另一个屏幕。因此，这为您提供了替换导航栈工作方式的灵活性，并提供了良好的分离。

## 4.保持你的回调链接在一起

一个非常常见的模式是将行为注入到高阶组件内的回调中(Redux 的 mapStateToProps 实际上就是这么做的)，但许多人忘记了公共回调可能会在应用程序的另一部分中使用(例如，外部组件)。

每当您的一个视图公开一个可能在应用程序的另一部分使用的回调时(例如 mapStateToProps)，首先调用在 Props 上传递的实际回调。例如，这使您能够导航到一个屏幕，并获取一些信息以提供给下一个视图。

按照前面的例子，如果 FavoritesScreen 告诉 FavoritesView 在选择一个收藏夹时导航到 FavoriteScreen，Redux 会遵守这个命令，但也会调用一些 Redux 操作。

正如你可能看到的，每个领域都知道如何处理它的东西:屏幕知道如何导航，连接的视图知道如何处理 redux 动作，视图是哑的，无状态的，依赖于它们的道具。

## 5.保持你的归约器简单明了

任何开发人员都应该能够查看您的缩减器的代码，并理解它在做什么。在大多数情况下，每个动作类型有一个函数可以增加可读性。

用许多单行函数组成 reducer 函数可以给你更大的灵活性和代码重用。

## 6.保持商业逻辑远离你的减速器

**你的 Redux 商店**不是你商业模式的一部分，**它是一个视图模式**。像这样对待它。你的减压器应该只影响商店的变化，你需要对它们有高度的信心。你的下属对你的商业规则了解得越少，他们就会变得越简单。

这不是最好的方法，但是更好的方法是将业务逻辑放在动作创建器中，特别是当您使用像 Thunk 这样的中间件时。传奇和史诗也很棒。

## 7.尽量减少特定于平台的组件

不要误解我的意思，每个平台都有自己的设计/UX 语言，在许多情况下，你必须编写组件的不同版本。记住 React Native 的座右铭是 ***学一次，写任何地方*** ，但是首先尽量不要急着写平台特定的组件。

在许多情况下，简单的样式改变和条件操作符就足够了。我创建了一个简单的助手函数，叫做 platformSpecific，它允许我根据平台设置样式。

这是一个非常简单的函数，但是非常有用。后来有人提到，React 原生舰有一个 [**平台，选择**](https://facebook.github.io/react-native/docs/platform-specific-code.html#platform-module) 功能也是如此。

## 结论

用不用这些模式都没关系。我想说的最重要的一点是:保持事物的简单和分离。这将提高生产率，并允许更容易的测试。这些模式中的许多都实现了这一点。

> 保持事物的简单和独立