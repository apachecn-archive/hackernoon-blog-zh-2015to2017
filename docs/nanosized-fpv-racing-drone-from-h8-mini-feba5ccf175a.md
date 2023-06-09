# H8 Mini 的纳米级 FPV 赛车

> 原文：<https://medium.com/hackernoon/nanosized-fpv-racing-drone-from-h8-mini-feba5ccf175a>

H8 Mini 是我第一次爱上的四轴飞行器。然而，尽管普遍认为，我敢认为这不是真正的室内或适合初学者，因为它的速度，敏捷性和疯狂的偏航率。人们应该把那个坏男孩带出去，所以很明显下一步将是给它增加 FPV 设备。

我在 YouTube 上看过很多视频，视频中人们简单地[把一个 AIO 相机](https://www.youtube.com/results?search_query=h8+mini+aio+camera)放在 H8 上，然后就飞来飞去；所以我给自己买了一台 [FX797T](http://www.banggood.com/FX797T-5_8G-25mW-40CH-AV-Transmitter-With-600TVL-Camera-p-1042994.html) 相机，试着做同样的事情。出于某种原因，这从来没有为我工作过。我不得不应用太多的油门，甚至起飞和四似乎并不挣扎与额外的重量，虽然，控制它并不容易。我甚至移除了道具保护和相机外壳，但控制问题依然存在。在这一点上我不得不提到，我使用我的 Devo 7E 发射机来控制 H8 Mini，我给它添加了一个 [3 合 1 射频模块](http://www.banggood.com/CC2500-NRF24L01-A7105-Multi-RF-3-IN-1-Wireless-Module-for-DEVO-Transmitter-p-1046304.html)，并用[偏差 TX](https://www.deviationtx.com/) 闪烁。

因此，事实证明，我需要升级电机，但股票框架不足以做到这一点。幸运的是，我碰到了 [H8CF101](https://droneflux.com/product/h8cf101/) 扩展套件，由[开箱创新](http://outoftheboxinnovations.com/)。

![](img/cb00f51775f51ee52c7135048c9be7a0.png)

Out of the Box Innovations H8CF101 frame kit

框架套件是专门为 H8 Mini 制作的，但我很确定它也可以适合许多其他玩具无人机的电路板。它支持 8520 电机尺寸(为此我推荐 [Spintech Motors](https://www.spintechmotors.com/) 的 [Sidewinder 8520](https://www.spintechmotors.com/products/spintech-sidewinder-8-5x20mm) ，因为这些电机提供巨大的功率)和高达 65 毫米的支柱，框架感觉像是设计巧妙。它非常容易组装，并且结果在美学上确实令人愉快。我特别喜欢马达保护帽，它是由某种橡胶材料制成的。你需要用双面胶之类的东西把 PCB 安装在框架上。H8CF101 的手册建议使用双面胶带将相机安装在框架上，但我发现一小块橡皮筋可以做得更好，因为它让你更容易调整相机的位置。中心杆下方有足够的空间，可以在相机周围缠绕一条带子。

![](img/7dd7496c827d0de03660c980265c642e.png)

H8CF101 assembled, camera mounted using rubber band

这款相机最初配有 Y 形电缆，可以将相机和 quad 连接到同一个电源。虽然这似乎是一个好主意，但很快发现多余的电线很容易在飞行中造成问题，因为它可能会被螺旋桨击中。电源通过非常小的焊点连接到相机，所以我想找到一种方法来消除多余的电线，而不必切断或更换它们。这是因为我不喜欢非常微小的焊接工作。幸运的是，我在 H8 迷你板上发现了两个标有 B+和 B-的焊盘，电源输入焊盘也标有 B+和 B-。

![](img/42302baff2de091dbe3c7ebd561ba633.png)

H8 blue board with extra battery out pads (B+ and B-)

我测试了这些焊盘，它们和我想的一样:电池电压输出。所以我用和相机电源线相同的连接器在上面焊了两根电线。然后，我只是把剩下的相机电线缠绕在相机上，这样我可以去掉大约 6 厘米不需要的电线。这是相机电源连接的样子:

![](img/8ac2d78cc1ad70a1dc660cdc6f110787.png)

Camera connector and wiring

到目前为止，我还不能解决的一个问题是 USB 编程连接。众所周知，H8 Mini(绿色和蓝色主板)可以刷新自定义固件(请查看 [Silverware Wiki](http://sirdomsen.diskstation.me/dokuwiki/doku.php?id=start) 了解更多信息)。闪烁是非常有用的，因为它给你提供了像 acro 模式这样的东西，除此之外，像 PID 调节和遥测。永久连接器是必要的，因为每次你需要改变一些软件设置，你需要刷新固件。所以我用来闪光的连接器阻止了我正确地组装框架，主要是因为我把它放在了相机支架应该在的一边。

![](img/8155aeb5499a76cbaa767e5b524055ac.png)

Servo connector soldered for USB programming

我还没有弄清楚我应该使用什么类型的连接器来代替伺服连接器，因为它显然太大了，不适合。我需要更小的东西，但我也需要一些适配器，因为 USB 编程器有引脚头，我仍然需要一个 USB 端的伺服连接器。

另一个问题是调平模式下的振动。一旦飞行器起飞升空，它就开始摇晃。在我看来这是 PID 失调的问题。然而，当我切换到 acro 模式时，这并没有发生。这也是我要检查的东西。这部分与另一个问题有关，因为更改设置意味着重新刷新，要重新刷新，我需要一个连接器，但使用当前类型的连接器，我无法组装框架。一旦我解决了这个问题，我会更新这篇文章。

我与本文中提到的任何产品的制造商都没有关系，也没有得到它们的赞助。我只是一个快乐的用户，所以我独立写了这个。

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)