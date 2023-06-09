# 什么是创造性对抗网络？

> 原文：<https://medium.com/hackernoon/what-are-creative-adversarial-networks-cans-bb81d09aa235>

![](img/fdc55b4cd38ef96219b9fe9df4e16e40.png)

Artwork generated by CAN

人类编程/教计算机做的最困难的事情之一是创造性思维。计算机非常擅长准确地做我们让它们做的事情，而且速度很快，但创造力是一个抽象的概念，向机器教授创造力已被证明是一个困难的机器学习挑战。

六月，罗格斯大学发表了一篇研究论文，向世界介绍了创造性对抗网络(CANs)的概念。正如你从上面的图片中所看到的，他们训练的罐子在创造一些看起来像是由真正的艺术家制作的东西和一些独特的而不是已经存在的艺术品的近镜方面做了出色的工作。

这些可能是机器创造性思维所获得的最好结果。

# 罐头是能创造性思考的甘

CANs 是基于几年前由 Ian Goodfellow 和他的一些同事创建的生成对抗网络(GANs)。为了理解易拉罐，你需要理解甘斯。

GANs 是一种神经网络，实际上由两个神经网络组成——一个生成器和一个鉴别器。

鉴别器的工作是将图像作为输入，并确定它们是真的还是假的(即由人类还是由生成者创建)。

生成器的工作是生成新的图像，让鉴别者误以为这些图像是真实的。

通过向鉴别器提供由生成器制作的假图像和真实图像的混合物，它学习识别模式，帮助它将每张图像分类为真实或虚假。与此同时，生成器会得到反馈，知道哪些图像最能骗过鉴别器，以及如何改变策略来骗过鉴别器。

鉴别器和发生器之间的竞争促使他们都在工作中变得更好，并且当 GANs 被正确训练时，发生器输出的结果看起来惊人地真实。

can 的设计方式与 GANs 几乎相同，但增加了一个关键点，即允许生成器创造性地“思考”……

鉴别器仍然试图学习如何将每个图像分类为真实或虚假，但它也学习如何将图像分类为 25 种艺术风格中的一种(即立体主义、抽象主义、文艺复兴、现实主义等。).

生成器仍然试图欺骗鉴别器，使其认为它生成的图像是真实的，但它也试图使鉴别器难以将其图像分类为 25 种艺术风格中的一种。

# 易拉罐为什么管用？

为了理解为什么在艺术风格中加入图像的分类可以让创作者进行创造性的思考，我们需要一个机器可以模仿的创造性的具体定义。

易拉罐的动机来自于这样一个理论，即当一件特定的艺术品是独一无二的，但又不太离谱时，观众会感受到创造力。我认为罗格斯大学的研究人员在他们的论文中很好地描述了这种动态。

> 唤醒潜力太小被认为是无聊的，太多会激活厌恶系统，导致负面反应。

让我们回头想想这与 CAN 架构有什么关系。通过奖励生成者生成鉴别者不容易归类到艺术风格之一的图像，它被迫生成独特的(创造性的)图像。与此同时，生成器仍然需要欺骗鉴别器，使其认为图像是真实的，因此它不能生成过于突出和明显不同的图像。

通过这种方式，罐模拟了我们如何看待艺术创造力的定义。

# 艺术观众几乎看不出区别

![](img/ab9ab0ec9ae85f8511d36dc26917ac4f.png)

上表比较了人类观众对四组作品的评价。DCGAN 图像由标准 GAN 创建(没有按照艺术风格进行图像分类，以使其能够进行创造性思考)。这些图像看起来像真正的艺术，但他们密切模仿定义的艺术风格。他们没有创造性思维。

“能集”显然是一个由创造性的对抗性网络生成的图像集。

抽象表现主义和巴塞尔艺术展 2016 数据集都是现代艺术作品的集合。抽象表现主义数据集由 1945 年至 2007 年间创作的图像组成；巴塞尔艺术展 2016 是在当代艺术旗舰展巴塞尔艺术展 2016 上发布的一系列图片。

令人印象深刻的是，来自 CAN 数据集的图像在新颖性、令人惊讶性、模糊性和复杂性方面排名最高。与甘的形象相比，他们也更善于欺骗观众，让他们认为自己是由人类创造的。

此外，易拉罐的创造者认为，易拉罐和抽象表现主义图像集之间的一些或大部分差异是易拉罐创造性思维的*结果。抽象表现主义数据集中的图像对艺术观众来说是熟悉的，因为它们年代更久，符合既定的艺术风格。相比之下，巴塞尔艺术博览会 2016 年的图像集，人类实际上发现最难正确标记真假。*

你可能会说，人类发现 2016 年巴塞尔艺术展的图像更难标记，因为按照我们的定义，它们*更有创意* *。推而广之，与熟悉的艺术风格的图像相比，易拉罐可能更理想地创造出人类更难区分真假的图像。*

不管怎样，对于创造性思维和参与艺术的机器来说，罐头是一个巨大的飞跃。

如果你想阅读罗格斯大学的 CAN 研究论文全文，你可以在这里找到。

# 行动呼吁

我目前正在探索如何创造 ***副业******产生被动收入*** 。如果你想及时了解我的写作、想法和项目，你可以在我的个人网站上找到更多信息和我所有社交渠道的链接:

[zackthoutt.com](https://zackthoutt.com)