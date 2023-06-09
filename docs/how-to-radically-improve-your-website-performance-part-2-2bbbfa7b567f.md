# 如何从根本上提高你的网站性能(第二部分)

> 原文：<https://medium.com/hackernoon/how-to-radically-improve-your-website-performance-part-2-2bbbfa7b567f>

![](img/9b13dab8693199add0a73bebd68d0ac5.png)

是时候升级游戏，在你最喜欢做的事情上变得伟大了！我们已经在本文的第 1 部分(见下文)看到了一些重大改进。我们看到了如何让网站变得更轻便以及如何提高后端性能的创新方法。现在，我们将看看如何有效地调整和实现服务器端的改进。

[](https://hackernoon.com/how-to-radically-improve-your-website-performance-part-1-c728f4e5b08f) [## 如何从根本上提高你的网站性能(第一部分)

### 等待网站加载并不是一件愉快的经历。性能是 web 开发的支柱之一

hackernoon.com](https://hackernoon.com/how-to-radically-improve-your-website-performance-part-1-c728f4e5b08f) 

…所以，废话不多说:

# 服务器端改进

![](img/74d242f02d567e9351503b45b8884251.png)

**服务器请求**

要编写高性能的网站和应用程序，你需要了解浏览器如何处理 HTML、JavaScript 和 CSS，并确保你编写的代码(以及你包含的第三方代码)尽可能高效地运行。这可以通过以下方式实现:

*   **尽量减少要求。**每次你访问一个网站，浏览器都要发送一个新的请求来获取所有的外部文件和资源。每个请求需要几毫秒的时间(取决于文件大小)，减少请求的数量也会对站点性能产生积极的影响。如果您有多个可以组合在一起的样式表，那么就这样做。我们没有理由为生产留下多个 CSS 文件。在开发过程中，使用像 [SASS](http://sass-lang.com/) 这样的预处理程序来组织你的文件。同样的道理也适用于 JavaScript 文件，你会明白，请求的文件越少，你的站点加载的速度就越快。
*   **按需加载脚本和样式。虽然将 CSS 和脚本文件结合起来减少请求是很好的，但有时如果一个特定的页面只需要请求，将它们分开会更好。例如，不需要在展示产品的登录页面上加载主库和样式。使第一页尽可能地浅，以便给用户留下更好印象。稍后加载其余的库。**
*   **将你的图标堆叠在一个精灵表中。对于拥有多个图标或小图片文件来说，这是另一个需要知道的好技巧。sprite sheet 是放在一起成为一个图像文件的一组堆叠的图标。这样，我们现在只向服务器请求一个文件，大大减少了获取多个图标文件的时间。 [Stitches](https://draeton.github.io/stitches/) 是一个伟大的工具，它为你完成繁重的工作，同时也为生成的 sprite 工作表提供 HTML 和 CSS 代码。**
*   内容交付网络。我们的浏览器一次只能从一个特定的服务器请求多个文件。为您的网站提供来自不同交付网络的资源，可以在大部分文件被缓存到浏览器之前，缩短首次“新鲜”获取网站的加载时间(下面将详细介绍)。

**实现缓存**

浏览器能够缓存大多数文件类型，包括样式、脚本和图像。这意味着这些文件将保存在您的本地计算机上。第二次访问时，浏览器将调用从本地存储缓存的文件，而不是从服务器获取新文件。在使用时要小心，我们不需要缓存一个用户可能只访问过一次的站点(比如一个活动页面)。记住这一点也很好，如果您在缓存到期之前对文件进行了任何更改，您应该为它们指定一个新的名称(例如-1.0.1.css)。这将确保*新的*文件将被请求。

**不使用重定向**

尽量避免重定向，除非它被用作后备，例如发生错误时。你能对你的访问者做的最令人沮丧的事情就是把他们从一个网站送到另一个网站。有时，这可能快到看似不被注意到，但想想那些碰巧有糟糕的互联网连接的人会如何体验这一点。

**托管服务和服务器速度**

如果你的主机服务性能差，处理速度慢，你在这里读到的所有方法都是徒劳的。你的网站性能很大程度上取决于你的主机服务的硬件性能和网络速度。在给自己买一个新的之前，一定要比较多个主机服务提供的规格。处理器速度、内存和网络带宽等因素都会影响网站的性能。我已经用了 [Bluehost](https://www.bluehost.com/) 很长一段时间了，支持非常好，他们的云服务价格也足够了。强烈建议您在选择首选服务之前进行彻底的研究。请记住，你不希望每年改变你的主机，因为这是一个巨大的头痛转移域名和证书从一个主机服务到另一个。好好看看规格，而不仅仅是价格！

**HTTP/2**

这是最新的网络协议，用于通过 web 进行低延迟的内容传输。您的编码方式没有任何变化。神奇之处在于如何获取文件。虽然[浏览器支持](http://caniuse.com/#feat=http2)很棒，但这项技术非常新，许多主机服务肯定会花时间从 http1.1 升级到 http2。需要知道的另一件好事是，当前大多数浏览器都需要 TLS (https)连接才能让 HTTP/2 正常工作。

**使用网络分布式图书馆**

[谷歌的 CDN](https://developers.google.com/speed/libraries/) 有一份最受欢迎图书馆的优秀列表。使用托管库的主要优势在于，普通用户很有可能已经访问过另一个使用相同库的网站(例如:jQuery)。这意味着库可能已经被缓存，浏览器不需要再次下载相同的数据文件。

# 结束语

![](img/1d131815c0ea5256cc8a6e385b3c12fc.png)

**感知时间背后的心理**

有时候，没有其他方法可以让网站更快，尤其是如果它包含大量媒体，如图像(用于文件夹)或视频文件。在这一点上，有一个加载机制是非常重要的。gif 图标或进度条)。这篇[文章](https://www.smashingmagazine.com/2015/12/performance-matters-part-3-tolerance-management/)很好地解释了一个进度加载栏如何对用户感知时间的流逝产生巨大的影响。在加载过程中有所关注——特别是估计完成时间——似乎可以使过程进行得更快。你自己有没有注意到这一点？当某些东西似乎被卡住了，而屏幕上没有任何东西在移动时，我们突然会有这种挫败感。但是当我们看到一个移动的图标时，我们倾向于确信背景中正在发生一些事情。

你真的需要使用网络字体吗？

网络字体是为你的网站创造独特外观的好方法。选择自定义字体是个不错的主意，但是请记住，这也会增加网站的权重和加载时间。有时候——在打开一个新网站时——你可能会在页面加载后看到字体风格的突然变化。发生这种情况是因为浏览器已经用默认(备用)字体绘制了文档，然后一旦下载了所需的 web 字体，就必须重新绘制 DOM(文档对象模型)。不要害怕使用通用的字体系列(Arial 就是一个很好的例子)。添加网页字体不会神奇地让你的网站看起来更好。你的内容质量要重要得多。当考虑使用网络字体时，我的建议是考虑使用这种字体是否值得牺牲性能。

**PWA(渐进式网络应用)**

我想提到 PWA，因为它最终将成为 web 开发未来的“事实”。尽管这项技术是最近才出现的，仍处于开发的早期阶段，但一些浏览器(如 Google Chrome)已经在利用这种设计模式了。简而言之，PWA 达到了与网站实际上是一个本地移动应用程序相同的性能水平。这是最有可能的，通过使用服务人员，将允许网站离线工作。反过来，与服务人员一起缓存将允许浏览器在本地保存网站，从而从根本上提高性能，就好像它是应用程序商店的本地安装一样。如果你有兴趣了解更多这方面的内容，这里有一个很棒的[PWA 文章集](https://dev.opera.com/articles/pwa-resources/)。

*提示:PWA 第一次让网络开发者可以直接在用户的主屏幕上发送移动通知*

# 结论

拥有优秀的编码知识会让你成为一名优秀的 web 开发人员，但是对互联网如何工作有更广泛的理解会让你成为一名专业人员。对新的进步保持好奇，并了解浏览器如何与服务器协同工作来显示网页。从零开始创建一个网站一开始似乎很可怕，但是一旦你开始理解质量有多重要，你就再也不会回头使用那些旧的库或框架了。

我一直在急切地寻找改善 web 性能和用户体验的最佳策略。如果你刚刚入门，想要快速入门，想要征服 web 开发的学习曲线，你也可以看看我即将出版的书— [成为专业的 web 开发人员](https://masteringwebdev.com/)。

感谢您的阅读！如果你想继续学习 web 开发的关键秘密，请关注我或者加入我的时事通讯。

# 更从[欧文远](http://owenfar.com/professional-web-developer/?ref=medium):

[](https://hackernoon.com/the-advantages-of-building-your-website-from-scratch-da5748a1baaf) [## 从头开始建立网站的优势

### 大多数和我谈论我正在开发的产品或网站的人，倾向于问我是否在使用任何…

hackernoon.com](https://hackernoon.com/the-advantages-of-building-your-website-from-scratch-da5748a1baaf) [](https://hackernoon.com/frameworks-libraries-both-or-none-my-honest-opinion-3a21ddf75323) [## 框架？图书馆？两个都有，还是都没有？—我的真实想法

### 哦，我被红迪网封杀了。

hackernoon.com](https://hackernoon.com/frameworks-libraries-both-or-none-my-honest-opinion-3a21ddf75323) [![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)