# 系统设计基础——第 4 部分

> 原文：<https://medium.com/hackernoon/fundamentals-of-system-design-part-4-d6a62f3fa779>

你可以在这里阅读本系列[的上一篇帖子。在这篇文章中，我将介绍复制。](/@v_aparimit/fundamentals-of-system-design-part-3-8da61773a631)

现代应用程序每分钟可以处理成千上万的事务。为了实现可伸缩性，您肯定要做的事情之一是复制您的[数据库](https://hackernoon.com/tagged/database)。这样做有几个原因:

1.  您希望让数据在地理上靠近用户
2.  平衡多台机器的读/写，以防止单个数据库服务器的节流
3.  在你的系统中建立冗余

复制中有许多有趣的微妙之处，涉及到持久性保证和最终的一致性。作为产品人员或应用程序开发人员，打破术语的模糊性并理解复制实际上是如何工作的非常重要。

另一台机器或节点上的数据副本称为副本。有三种方法可以实现数据复制。

1.  单一主从复制:所有的写入都到一个节点，称为主节点。主节点中的更改被复制到其他节点，称为从节点。读取请求可以发送到主机或从机。
2.  多主机复制:写操作可以到多个主机，而不是到一个主机。然后，主节点可以将对其数据存储所做的更改复制到其他从节点。读取请求可以发送到主机或从机。
3.  没有主复制:在这个设置中没有主和从。写入和读取可以发送到任何节点。

在讨论其他配置之前，我将详细介绍单主从复制。

值得一提的一个重要细节是复制发生的方式。它可以是同步的，也可以是异步的。

同步复制意味着主设备将其写入发送给所有从设备，并等待来自“所有”从设备的写入确认。一旦主设备接收到写确认，它就向客户端返回成功的写消息。完成所有这些后，写入内容对其他客户端可见。这种模式提供了最高的耐用性保证。每次写入都会传播到所有节点，连接到任何从属节点的客户端都不会看到过时数据。如果这些保证对您的应用程序有意义，您应该选择同步复制。

同步复制的最大缺点是速度非常慢。如果到某些节点的网络连接不稳定，则一次成功写入可能需要很长时间。在实践中，人们总是不约而同地选择“异步”复制。在异步复制中，在主节点上成功写入后，主节点向客户端确认写入。它还将更改发送到其他从副本，但不等待来自其他从副本的成功写入确认。这实际上意味着耐久性保证被削弱，因为一些从节点稍后更新它们的数据存储，同时连接到一个从节点的客户机将被呈现旧数据。然而，使用异步复制通过提供显著的性能增益弥补了这一点。因此，异步复制是主要的复制策略。

大多数应用程序的读/写比率严重偏向于读取，即写入会减少。为了利用这一事实，读操作由从设备处理。在异步主从配置中，由于复制滞后，这带来了一个问题。让我来看几个由于复制滞后引起的问题的例子，以及解决这些问题的步骤。

1.  读取写入:用户在主机上提交写入，然后决定读取他/她的写入。读请求可以由任何从设备服务，并且由于复制延迟，服务读请求的从设备可能没有最近的写。这显然会让用户感到沮丧，看不到他/她最近的帖子。您可以通过确保所有读取在任何写入 1 分钟后到达主机来解决此问题。另一种方法是客户端记住写入的最后时间戳，然后使用此信息仅从那些时间戳比客户端时间戳更新的副本中读取
2.  在时间上向后移动:用户提交一个写操作，该操作在其中一个从设备 s1 上复制，但由于复制延迟而没有在其他从设备上复制。然后，用户从从机 s1 读取数据，并看到他/她之前的写操作。然而，他/她再次读取，并且这一次说读取是由不是 s1 的从机处理的。用户看到他/她的书写消失时可能会非常沮丧。可以通过仅从一个副本处理一个客户端的读取来解决此类问题。

可能还有其他微妙但操作上令人烦恼的问题，尤其是如果你在一个不稳定的互联网或满负荷运行的情况下。为复制的数据存储考虑整个系统的复制滞后[设计](https://hackernoon.com/tagged/design)是很重要的。

现在对很多高手配置。这种配置最常见的用例是当您有多个数据中心时。每个数据中心可以有一个主节点，其余的节点可以是从节点。

很多高手配置最大的优势就是性能。您的写入是分布式的，不再受单个主机容量的限制。然而，这个世界上没有免费的午餐。在并发写入的情况下，处理额外的复杂性弥补了您获得的性能。

在许多主配置的情况下，您可以将编辑他们自己的数据的用户绑定到一个主上。本质上，从用户的角度来看，配置变成了单一主配置。这真的很好，因为现在您可以避免由于在许多主机上并发写入而导致的所有合并冲突。但是，如果您无法做到这一点，那么您需要使用以下策略之一来解决冲突:

1.  使最近的写入成功
2.  编写关于在复制日志中检测冲突的自定义代码
3.  向用户提供一个值列表，让用户决定冲突时的合并和丢弃策略

显然，正确的策略取决于应用程序的性质和用户的期望。

最后我来介绍一下无主复制。在这种设置中，每个节点都可以接受读和写请求。您可以立即发现这种方法的问题。不仅您的读取可能因为复制滞后而过时，您的写入也可能不一致。

为了解决这个问题，读写被并行发送到许多节点。假设并行进行 r 次读取，并行进行 w 次写入，总共有 n 个节点。只要 r + w > n，就可以确保 r 节点中至少有一个必须是最新的，因此读取不会过时。

点击[这里](/@v_aparimit/fundamentals-of-system-design-part-5-c27b617cd532?source=linkShare-96c28ede917-1519499067)阅读本系列的下一篇文章。