# 用 Unity3D 制作 Python 的 3D 界面

> 原文：<https://medium.com/hackernoon/user-interfaces-with-unity3d-and-python-eb2e7744518a>

## 使用 Sofi 和 WebSockets 命令游戏引擎

![](img/b44ff83a8fd8c3d46ddf696956910763.png)

不久前，我写了一篇关于使用游戏引擎作为前端接口的文章。我想在 Python 生态系统中启用丰富的接口，这些接口可用于虚拟和增强现实。从那以后，我能够在 [Sofi](https://www.github.com/tryexceptpass/sofi) 的基础上构建一些基本概念，我在这里分享它们。

## 后端

Sofi 作为一个 WebSocket 服务器工作，可以从客户端发出命令和处理事件。它旨在简化前端 web 技术作为 Python 后端接口的使用。你甚至可以[把它打包成一个桌面应用](http://tryexceptpass.org/how-to-turn-a-web-app-into-a-desktop-app)，拥有桌面的外观和感觉。

它的功能是将用户发送到一个网页，该网页提供了打开 WebSocket 客户端所需的基本信息。然后，这个客户机注册处理服务器命令的处理程序，告诉它如何改变 DOM 或响应事件。所有的逻辑都在 Python 中，网页是用户界面。

我用足够的模块化来编写它，以便命令和事件结构可以在任何技术中重用。因此，用游戏引擎取代网页部分并不是什么难事。只需要找到一个可以轻松访问 WebSocket 客户端的服务器。

## 游戏引擎

我看了 Unity3D，虚幻和 CryEngine。在这三者中，前两者拥有最广阔的社区，而在这些社区中，Unity 似乎拥有更大的生态系统。虽然这通常是一个品味问题，但我不是在这里争论哪个图形更好。在这一点上，我想要简单的概念证明，这是以 [WebSocketSharp](https://github.com/sta/websocket-sharp) 的形式出现的。

WebSocketSharp 是 Unity3D 的资产商店中提供的 C#库。它提供了可由项目场景中的任何脚本使用的客户端和服务器类。我运行了一些测试，它很好地满足了我的需求。映射回 Sofi，这部分执行运行在浏览器上的 JavaScript WebSocket 客户端库的功能。现在，让我们把它包装起来，这样它就能理解如何与 Sofi WebSocket 服务器对话，并做出相当于`sofi.js`的功能。

## 制作前端

如果你以前没有使用过 Unity3D，或者任何游戏引擎，进入“hello world”会很混乱。虽然不要求理解这个实现，但我将在这里介绍一些主要概念。请注意，Unity 有自己丰富的[文档](https://docs.unity3d.com/Manual/index.html)可用于了解更多细节。

制作“游戏”时要做的第一件事是创建一个项目，这也是我一直在做的事情。请将此视为一个包，其中包含渲染世界及其交互所需的所有资源。项目中的几乎所有东西都是资产:纹理、着色器、脚本、对象等。

在一个项目中有场景。把这些想象成游戏关卡，或者电影中的场景。它是一个对象、脚本和摄像机视图的集合，呈现出一个具有共同目标的体验。

一旦有了场景，我就可以添加 WebSocketSharp 库作为资产。这使得将它的`WebSocket`类导入到脚本中变魔术成为可能。您可以将脚本分配给场景中的对象，并通过引擎的事件循环触发执行。

每个场景都有一个默认的摄像机。相机，除了其他因素，决定了如何查看场景。这包括视角、距离、渲染设置、照明等。但是由于它们本身是对象，它们也可以保存脚本。这意味着我可以在相机上粘贴一个`WebSocketClient`脚本，它会立即加载场景。

Unity 脚本可以在主事件循环中调度处理程序。文档中详细描述了许多物理碰撞或用户输入的游戏事件。但是我感兴趣的是那些在初始化时定期运行的。在我们的例子中，我在寻找`Update`和`Start`。前者在渲染每一帧时运行，后者在加载后执行。我还为`OnDestroy`注册了一个处理程序，在退出时进行清理。

为了配置客户端，在引擎的启动事件中实例化一个`WebSocket`。这需要服务器的地址和端口，以及它自己的一组事件处理程序。当连接完成时，我使用`OnOpen`，当接收新数据时使用`OnMessage`，当连接断开时使用`OnClose`。

使用`Start`时，考虑事件循环很重要。这里不能进行消息处理，因为它会阻止场景加载。因此，我以客户端类中的`List`对象的形式创建了一个命令队列。这个想法是在每个`Update`事件上检查队列——每帧一次——然后处理命令。

除了消息处理之外，`Update`事件是检查连接的好地方。很容易触发重新连接，允许场景在需要时等待服务器启动。

该引擎收集用户输入并对其进行排队，就像早期的套接字消息一样。所以我在这里也添加了检查，使用`sendAsync()`方法将它们传送回服务器。

## 与 Sofi 通信

稍微说一下协议，Sofi 的通信机制是非常可扩展的。套接字服务器监听一个特定的端口，期待 JSON 数据。事件消息有一个名为`'event'`的键，服务器用它来检查回调。如果存在，执行传递给该函数，该函数又可以使用`dispatch()`方法发送命令。UI 命令有一个`'command'`键来标识它们和它们的其他参数。除了基本的，我不硬编码任何这些，所以它是非常容易的添加自定义事件和命令，不需要修改 Sofi 本身。

`WebSocketClient`可以处理生成新对象、更新对象属性、删除对象和订阅事件的命令。物体的类型是非常基本的形状:立方体、球体、圆柱体、胶囊、平面和文本。每个都有相当多的设置，包括颜色、大小、位置和旋转。

## 包装

另一个好的方面是 Unity3D 可以为所有主要平台生成二进制文件。这包括 Windows、Linux、MacOS、Android、iOS 和 otherx。因此，这不仅为 Python 添加了 3D 功能，还包括多平台支持。构建过程本身很简单，由游戏引擎本身来指导。将它与 PyInstaller 结合起来，就像我在[上一篇文章](https://medium.freecodecamp.com/the-python-desktop-application-3a66b4a128d3)中提到的那样，现在你只有一个可执行的发行版，Python 环境等等。

## 它看起来像什么？

要演示它能做什么，请看下面我的 PyCaribbean 演示。我在大约 20:09 跑它。

我已经在 GitHub 的 [sofi-unity3d](https://github.com/tryexceptpass/sofi-unity3d) repo 下发布了 Python 代码。`WebSocketClient`实现位于`engine/Assets`文件夹中。它还包括 Unity3D 项目。完整的代码将在我的 PyCaribbean 幻灯片中运行，并启动任何`#python`推文的监听器。

我还为 [Linux](https://s3.amazonaws.com/tryexceptpass/sofi3d.x86.zip) 、 [Windows](https://s3.amazonaws.com/tryexceptpass/sofi3d.exe) 和 [MacOS](https://s3.amazonaws.com/tryexceptpass/sofi3d.app.zip) 构建了二进制文件，所以你们可以自己下载并使用它们。当你运行引擎时，它将加载一个等待 WebSocket 服务器的空空的天空和绿草如茵的飞机场景。这可能是`server.py`中的 Sofi 实例或者您自己创建的监听端口 9000 的东西。

## 下一步是什么？

今天，我们探讨了创建基于游戏引擎的“小部件库”的可能性。展示了 Python 后端提供逻辑的可能性，同时将 UI 的重担留给了引擎。它也是可移植的跨平台的，并且不费吹灰之力就可以发布。

游戏引擎方面的下一步是提供实用的小部件和资产。有了这个框架，我们可以生成任何预先存在的游戏对象，网格和脚本。由我们来定义什么是好的可重用组件和交互，并用构建的二进制文件打包它们。

在 Python 方面，我想提供一个基于 HTTP 的资产服务器。这允许人们在类似于 [Blender](https://www.blender.org/) 的东西中创建自定义资产，并且将它们加载到任何场景中，其中 Blender 也支持 Python。不需要接触游戏引擎。

我还想建立一个在 Rift、Vibe、Hololens 等硬件上实现 VR 或 AR 的世界。我家里有一个 DK2，但是还没有用它做任何项目。

关于我如何制作 Sofi 的附加阅读，请看一下[一条蟒蛇吃掉了我的 GUI](/@tryexceptpass/a-python-ate-my-gui-971f2326ce59) 系列。

[![](img/4e728960fa1d1a8a3847021955abc3a4.png)](https://twitter.com/intent/follow?original_referer=https%3A%2F%2Fpublish.twitter.com%2F&ref_src=twsrc%5Etfw&region=follow_link&screen_name=tryexceptpass&tw_p=followbutton)

如果你喜欢这篇文章，并想了解我正在做的事情，请推荐它，访问[tryexecptpass.org](http://tryexceptpass.org)了解更多主题，以及[在 Twitter 上关注我](https://twitter.com/intent/follow?original_referer=https%3A%2F%2Fpublish.twitter.com%2F&ref_src=twsrc%5Etfw&region=follow_link&screen_name=tryexceptpass&tw_p=followbutton)。

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)