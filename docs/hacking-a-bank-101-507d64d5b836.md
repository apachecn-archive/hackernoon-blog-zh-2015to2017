# 入侵银行:101

> 原文：<https://medium.com/hackernoon/hacking-a-bank-101-507d64d5b836>

![](img/f3fdd276c997862a69acdb3724734a2b.png)

# 高级银行业务逻辑漏洞

银行是经济的核心。如今，网络攻击每天都在发生，全球的银行都受到了影响。

在过去的一年里，我们观察了各家银行在移动应用安全方面的[安全](https://hackernoon.com/tagged/security)。所描述的安全缺陷是由于糟糕的编程实践造成的。

缺陷可以解释如下—

1.  重放攻击
2.  绕过对恶意受益人的付款
3.  2FA 中的旁路质询响应

为了描述这些攻击，考虑一个虚构的银行“SPDL 银行”。银行的客户是爱丽丝和鲍勃，黑客是伊夫。我们希望反映逻辑中的缺陷，我们使用 Charles Proxy 来嗅探移动银行和银行服务器之间的 SSL 流量。

移动[银行](https://hackernoon.com/tagged/banking)应用程序应该允许用户执行他们可以在银行执行的操作的子集。因此，我们提出了我们对移动银行应用程序实际上应该如何运行的假设。付款时，付款请求只应有效一次。同样，转让应该只可能给批准的和信任的受益人。继续讨论质询响应，作为附加的安全层，银行可能会要求密码的某些数字(如第 2、第 3 和第 7 位数字)，或类似形式的二次身份验证。只有在响应了所请求的内容后，交易才会被处理。

# 1).重放攻击

假设 Alice 正在通过移动银行应用程序向 Bob 转账。付款申请只应有效一次。任何向银行提供相同信息的企图都应被视为无效。在实际场景中，假设 Alice 合法地向 Bob 转账 10 美元。Bob 可以与黑客 Eve 配对，并且可以将请求重放 10 次。因此，在未经授权的情况下，90 美元从爱丽丝的账户中被取走。

对重放攻击的防御是一个随机数，或作为时间函数的客户机和服务器之间的秘密。

# 2.绕过支付攻击

作为日常业务的一部分，Alice 向 Bob 转账 100 美元。这是一个有效的交易，因为 Bob 存在于批准的受益人列表中。

完成交易的步骤如下-

> 爱丽丝->服务器:转账 100 美元给鲍勃
> 
> 服务器->爱丽丝:好的；给我认证号码:1，5，8
> 
> 爱丽丝->服务器:转账 100$给鲍勃；认证 1:22 5:45 8:12
> 
> 传输成功

认证字符可以被认为是密钥值对，其中有 16 个密钥 1…16。这些都有认证数字

绕过支付攻击发生在步骤 3。Eve，对手可以篡改请求

> 3.爱丽丝->服务器:转账 10000$给 Eve 认证 1:22 5:45 8:12

服务器接受它，并且传输成功。问题是

1.  如果收件人是受益人，第 3 步中缺少检查
2.  步骤 1 和 3 之间未保持状态。

因此，金钱可能被转移到恶意实体。

# 3.双因素身份验证旁路

如交易步骤中所述，需要提供认证值。服务器要求从 16 个值中随机选择 3 个值，作为双因素验证。

一次攻击改变了挑战应答问题。

在步骤 2 中，当银行要求 2FA 时

> 2.服务器->爱丽丝:好的；给我认证号码:1，5，8

Eve 可以篡改请求响应，并提供她知道的 3 个有效的键值对。因此，不管服务器要求什么，Eve 都可以提供她知道的键值对，交易仍然可以进行。因此，她有效地绕过了安全机制，因为她可以欺骗每个交易。

> 爱丽丝->服务器:转账 100$给鲍勃；认证 1:22 2:99 3:10

这是一种高级攻击，需要 Eve 拥有会话密钥。然而，一旦她通过嗅探一个实时交易，结合漏洞 2 和 3，她可以创建恶意交易。

这些缺陷与逻辑相关，可能不属于银行的威胁模型，因为它们假设应用程序位于可信计算基础中。然而，这种假设可能不成立，因为通过具有误导性权限的应用程序来毒害电话证书存储是多么容易。

公钥锁定将解决嗅探中的问题，但是在首次安装和运行银行应用程序时，可能会有对手嗅探流量。此外，这些逻辑漏洞甚至会存在于网络银行应用程序中。

在球形防御(neural.ai)，我们正在为银行开发技术，通过学习语法和可信通信的语义，使用深度学习来实时检测入侵企图。

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)，并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)