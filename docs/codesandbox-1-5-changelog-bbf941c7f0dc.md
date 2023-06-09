# CodeSandbox 1.5 变更日志

> 原文：<https://medium.com/hackernoon/codesandbox-1-5-changelog-bbf941c7f0dc>

![](img/f40f780c3d7af6ef002070638de24b85.png)

这是 CodeSandbox 1.5！我不知道如何调用所有的更新了，所以我决定用任意的数字来版本化 CodeSandbox。

这是一个大的更新，我重写了编辑器，预览屏幕和打包程序。所有这些变化使部署相当令人兴奋，但它现在是在线的。我们开始吧！

# 编者ˌ编辑

编辑器已被改写，以使用[摩纳哥-编辑器](https://github.com/Microsoft/monaco-editor)。这个编辑器是 [vscode](https://github.com/Microsoft/vscode) 编辑器的摘录版本，因此*确实*强大。

## 查看定义，转到定义，查找所有引用

关于 monaco-editor 真正酷的事情是你得到了核心的编辑器特性(转到定义，查看定义，等等。)的 vscode。你唯一需要做的就是正确地连接所有的东西，我创建了一个单独的 Monaco 编辑器来更好地集成 CodeSandbox 中的交叉文件。

![](img/3758a48eb64028924c783d73085bfd46.png)

Peek Definition, Go to Definition, Find all References

## 自动类型获取

不仅导航变得更容易，monaco 编辑器还内置了用于 JavaScript 和 TypeScript 的 IntelliSense！这真的很酷，如果你有依赖性的类型，那就更好了。这就是为什么我添加了“自动类型获取”，这意味着对于每一个“已安装”的依赖项，我们都要在[https://unpkg.com](https://unpkg.com,)上搜索并下载类型定义。通过这种方式，您可以自动完成库。

![](img/805e51b740166c0cbb838cc8897820a3.png)

Autocompletions for many dependencies

## ESLint，更漂亮，Emmet.io

我移植了几乎所有现有的编辑器特性。这意味着你已经在编辑器中内置了 ESLint，Prettier 和 Emmet.io！不幸的是，我不得不放弃 VIM 模式，你仍然可以启用这个，但这将禁用摩纳哥和启用代码镜像。

![](img/84398f18397889facc1c41996b5a724f.png)

Emmet.io & ESLint & Prettier

我真的很高兴有了新的编辑器，并想声明，没有 monaco-editor、TypeScript、unpkg、emmet.io、ESLint 和 Prettier，这是不可能的。我想明确地感谢这些工具，我唯一要做的事情就是把所有东西连接起来，并修补一些集成。

# 反应-误差-叠加

我们有另一个工具使 CodeSandbox 变得更好，即[react-error-overlay](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-error-overlay)by[create-react-app](https://github.com/facebookincubator/create-react-app/)！CodeSandbox 中的错误处理已经被重做，感谢`react-error-overlay`我们现在支持异步错误和深度链接错误+有一个漂亮的错误覆盖。此外，我重写了预览的错误处理，所以错误现在显示在右边的文件中。

![](img/5faf6d9fcceebcf34a1a82483ae10ad5.png)

CodeSandbox 不仅显示错误，还提供已知错误的建议。在上面的例子中，`DeepComponent.js`正在导入`RawComponent`，注意没有扩展。这将抛出一个`Invalid Tag`错误。我们可以很容易地发现这一点，并给出重命名文件的建议。我在考虑写一个 API，允许库开发者为他们特定的库添加错误建议。

Error overlay (suggestions and error navigation don’t work here as you’re not in the editor)

# 外部框架

现在可以在外部 url 中打开沙盒。在开发过程中，您可以使用它在单独的窗口中查看预览，或者与朋友共享沙盒的全屏版本。请注意，这个外部框架离生产版本还很远，我正在与 ZEIT 合作集成“部署到现在”,这样您就可以自动部署生产版本的✨.

![](img/8aa3baeb10ef540d9785e15ea26fefd4.png)

External frames!

外部沙箱也可以脱机工作。这让我想到了下一点…

# 离线支持

CodeSandbox 现在由服务人员提供支持。这意味着您可以在离线时打开编辑器和预览，看到 CodeSandbox 而不是恐龙🙃。请注意，离线支持目前是有限的，你还不能保存你的沙盒离线(但你仍然可以下载)。为了做到这一点，我需要对服务器进行一些必要的更改。你可以编辑沙盒！这个特性确实是速度上的一个改进，它将节省网络往返时间，例如依赖关系。

![](img/79ab41026395d546122722b8555684b9.png)

No Dinosaur!

# 依赖性打包程序重写

依赖项的打包程序已被重写。它现在作为无服务器解决方案托管，这意味着它可以(实际上)无限扩展。我们还看到了速度上的很好的改进，我们看到了 40%-700%之间的改进。)在响应时间上。

新打包程序的一个新特性是，除了绝对版本之外，我们还支持版本范围。例如，你可以安装`react@next`，它会随着 React 的更新而自动更新。这项功能将于本周在某处部署，我需要先更改一些服务器逻辑。

在使用无服务器后，我不得不说，它在实践中的工作方式给我*留下了深刻的印象。我们的托管成本从每月约 50 美元下降到每月 0.03 美元的预计成本+我们现在速度更快、可扩展性更强，部署变得轻而易举。当我有时间的时候，我会写一篇关于这个的文章。*

*注意:打包程序现在已经回滚，由于磁盘空间限制，一些包组合无法加载，这是可以解决的。*

# 谢谢

你可以在这些功能中看到一个趋势，每个功能都大量使用了一些现有的技术。它为我节省了大量的时间，我想再次特别感谢让这一切成为可能的作者们。
感谢:

*   [vscode](https://code.visualstudio.com/) 团队，努力提取 [monaco-editor](https://github.com/Microsoft/monaco-editor) 并开源。这对在线编辑运动来说是真正有价值的**。**
*   [https://unpkg.com](https://unpkg.com)允许我们&方便地从 NPM 自动下载打字稿。
*   [ESLint](http://eslint.org/) 、[beautiful](https://prettier.io/)和 [Emmet.io](https://emmet.io/) 不仅制作了这些有价值的生产力提升工具，还保持了它们与浏览器的兼容性。
*   每个人都在[后面创建-反应-应用](https://github.com/facebookincubator/create-react-app)，具体来说就是反应-错误-覆盖。实现这个开始是一个笑话，但结果比我预期的要容易得多，并且实际上完成了。
*   他们让实现离线支持变得轻而易举。他们的配置是一流的。
*   [无服务器](https://serverless.com/)让无服务器开发和部署更容易&更容易接近。他们正在做一项非常重要的工作，而且做得非常好。