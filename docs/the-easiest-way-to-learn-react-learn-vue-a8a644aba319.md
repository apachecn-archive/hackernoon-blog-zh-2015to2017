# 最简单的学习 React 的方法？学习 Vue。

> 原文：<https://medium.com/hackernoon/the-easiest-way-to-learn-react-learn-vue-a8a644aba319>

![](img/4668d9d518360910cd00b931d881c562.png)

Vue Logo

当我第一次开始学习 React 时，有一段时间我与相当频繁的“惊讶”作斗争。从好的方面来看，几个月前，我很幸运地偶然发现并学习了一个类似的框架 Vue。这是最好的一种库:你可以不看太多文档就随便修改，而且主要的重构操作也很容易，因为语法简单且一致。花一个月的时间来学习 React 是我做过的最好的事情。让我解释一下。

React API surface 是很多争论的话题——有些人说它很难理解(通常是想帮忙),我很聪明地反驳了他们。我认为 React 的基本问题有三个:

1.  JSX 很奇怪。这并不是说它不好——你可以让它做神奇的事情，但它不是模板语言，也不是 [Javascript](https://hackernoon.com/tagged/javascript) 。
2.  状态管理令人困惑:数据可能在`this`、`this.state`或`this.props`上。没有回调来通知你`this`的变化，但是有`state`和`props`的。`this.setState`是不设置状态。
3.  不断的反对:React 团队(上帝保佑他们)总是在前进，但是现在有这么多不同的做事方式，很难建立一个一致的、可学习的代码库来经受时间的考验。

因此，让我们来看看 Vue 如何处理一些核心问题，以及我们可以从他们那里了解到什么。

## 模板

模板以一种开发者容易理解的方式转换成渲染函数。您也许可以用一个以 react 为中心的模板包来复制这种行为。对于 React 和 Vue 来说，都有模板不够好的情况，然后你可以依靠渲染函数和 JSX。

## 真理的一个来源

在 Vue 中，只有一个地方可以存放数据，那就是对象本身。所有数据都在 JS 代码中的`this`、`this.something`和模板中的`{{something}}`上。它可以从模板、其他组件等中获得。你不能让 props 和某个状态变量同名——它们都在一个名称空间下。使用 React 很容易搬起石头砸自己的脚，因为在代码中有`this.props.value`、`this.state.value`，甚至可能还有`this.value`，所有这些都有重要而独特的功能。使用 React 最不容易混淆的方法是尽量减少状态来自的位置，并清楚地说明它是如何工作的。如果你有一个道具和一些内部状态(比如一个可编辑字段的值)，确保它们被命名为不同的东西，这样它们就不会在你的头脑中混淆。

## **状态队列**

在 React 中，调用`setState`不会立即变异`this.state`。这是因为，你知道，[原因](https://github.com/facebook/react/issues/122)。好吧，但这真的很难跟 T21 讲道理。我能够理解它的唯一方法是有一个严格的数据路径。从`this.props`或者事件到我自己的同步状态 hash(我一般叫它`this.syncState`)，然后从变异`this.syncState` ( `setSyncState`)的函数实际调用`setState`。所有逻辑只触及`syncState`，渲染功能只触及`this.state`。这避免了状态散列与应用程序逻辑不同步的混乱。我发现用`setState`调用不可能实现复杂的异步状态变化逻辑，而代码不会变成一堆互斥体、状态变量等等。依我拙见，最好是在 React 不关心的地方有一个完全相同、重复但同步的真实来源。

## 贬值

没有办法拐弯抹角——API 是会变的。Vue 从 1.0 到 2.0，有大量的突破性变化，切换前后的时间很尴尬。React 似乎从头到尾都有很大的变化。如果你想升级几个版本，祝你好运。我从 Vue 学到的最重要的事情就是组件中应该有什么，以及组件相对于其他组件应该如何表现。与 Vue 相比，React 提供了非常相似的核心功能。Vue 只是提供了更多的指南和最佳实践。构建几个 Vue 应用程序让我更清楚地知道什么属于哪里，当我回去做出反应时，我确切地知道事情应该去哪里，以及应该如何将它们放在一起。

我想我会说，如果你开始一个新的应用程序，给 Vue 一个尝试，即使你真的很喜欢 React。如果你深陷 React 应用程序，并且在结构、数据流或组件描述方面苦苦挣扎……花一周时间在 Vue 上闲逛，如果你像我一样，你从体验中获得的智慧将远远超过所花费的时间。