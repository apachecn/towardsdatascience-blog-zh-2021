# 您的数据在云中安全吗？

> 原文：<https://towardsdatascience.com/is-your-data-secure-in-the-cloud-f074687b52c8?source=collection_archive---------27----------------------->

## 在云中工作时要记住的 4 个注意事项

![](img/18474b641c40c0ca47a4fd5d800a24df.png)

miosz klin owski 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

欢迎阅读关于云系列中的数据的新文章。如果您错过了之前的任何文章，我建议您快速阅读并赶上进度，因为在本文中，我们将继续讨论云，强烈建议结合上下文。在[云系列的第一篇文章](/how-the-cloud-will-help-or-not-your-business-42b72f4e51b3)中，我们讨论了云的优势和劣势，以及它如何帮助您的业务。在第二篇的[中，我们解释了不同的云服务模型是什么，以及您在每种模型中负责什么。](/the-6-things-you-are-responsible-for-in-the-cloud-c513ac07905e)

在本文中，我想与您分享一些关于安全性的想法，这个问题已经成为那些考虑使用云解决方案的人非常关心的问题。更具体地说，我们将讨论数据安全性。我相信您已经厌倦了听到有关数据中心安全漏洞将敏感数据暴露给公众的新闻。我也确信，人们会想到大公司如何利用数据来更好地了解他们的客户。当你听到云的时候，你可能会想到这一切，这通常会产生很多不信任，但事实是，你的想法是有偏见的，受到这个问题所造成的所有媒体的影响。

虽然安全是我热爱的领域，但我不是安全专家，我写这篇文章的目的不是列出必须考虑的一系列优点或缺点。我唯一的目的是提供一些你可能已经想到的考虑因素，并邀请你去思考它们。欢迎在评论中留下你的想法，我会尽力回答。

# 云提供商(大部分)是安全的

如果你不信任云，问自己一个问题:你是把钱存在银行里还是放在床底下？一般来说，人们把存款存在银行里。为什么？因为这样更安全。你的房子似乎很容易成为小偷的目标，但很少有人会去抢银行。为什么“大部分”是安全的？因为绝对安全是不存在的。

许多人认为抵制云迁移的原因之一是数据“转移”到云提供商。“我的公司数据会在第三方服务器上，为什么不能保存在我的服务器上？这样更有保障。”是的，你公司的数据会在不属于你的服务器上，那又怎样？你的云提供商会窃取你的数据吗？回到之前的例子，你的银行偷你的钱有意义吗？一般来说，将你的数据存储在云提供商那里并不会带来安全风险。

另一方面，您可能会怀疑云提供商是否能看到您存储在他们云中的内容。如有疑问，在开始任何云活动之前，我建议您阅读服务条款以及您选择的云提供商的隐私政策。实话实说，作为服务提供商，未经客户同意访问他们的数据是非法的。确保你没有同意。你的内容是你的，不是别人的。

# 你的数据在哪里？

另一个最常见的问题是您的数据在哪里。云是一个听起来如此抽象的术语，以至于你会认为你的数据可能在任何地方。

事实是，云提供商拥有庞大的基础设施，并且遍布全球。我接下来要说的内容可能会因不同的云提供商而异，但大多数都是这样组织的。

云提供商的基础设施分布在世界各地的不同地区。您可以随时选择要在哪个区域工作，因此您可以控制数据的存放位置。这样，你将能够遵守相应的法规。

当您选择一个地区时，除了选择最适合您的地区之外，您还必须记住，并非所有地区都有相同的服务目录，因此，根据您要使用的服务，您会稍微习惯于使用特定的地区。然而，大多数“共同”服务通常在所有地区都可以获得。

# 你是个风险

当我们谈论安全时，你应该永远记住，最薄弱的环节是你自己。一个不安全的密码、一个禁用的多因素身份验证、一台未锁定的计算机，都足以导致安全漏洞，带来可怕的后果。像贵公司这样的公司越来越意识到这一点，并投资培训员工以降低安全漏洞的风险。同样，作为云服务的客户，我们有责任确定谁可以访问我们的数据，谁不可以。

简单总结一下，我们作为客户，负责云中的安全**，而云提供商负责**云中的安全**。因此，您必须确保只有适当的人才能访问信息，并授予最低的访问权限，以便他们能够执行符合相应安全策略的任务。**

可以想象，根据您在云上使用的服务模型，配置工作会或多或少。你必须意识到，在每一种情况下，你要对什么负责。管理具有持久存储的虚拟机不同于管理 Google Drive 文件夹的权限。

# 数据加密

另一个重要的话题是数据加密。加密被定义为对信息进行编码的过程，该过程将信息转换成理想情况下只能由接收者解码的表示形式。我们不打算在本文中讨论密码学，因为这是一个太宽泛的话题。你必须明白的重要思想是，当你的数据被加密时，理想情况下，只有拥有解密密钥的人才能读取它。

当我们谈到数据加密时，有两种情况可以而且应该加密数据:

*   **静态**:当你的数据存储在云提供商那里，并且没有被使用时，它必须被加密。这样就算有人“抢银行”，也什么都不懂。
*   传输中:例如，当你在两台服务器之间传输数据时，它必须被加密。这样，如果有人拦截了通信，就像前面的情况一样，他们将什么都不明白。

正如我们所看到的，在开始在云中工作之前，我们必须考虑一些事情。有了正确的措施，在云中工作通常是安全的。云提供商将完成必要的任务来确保其基础设施和服务的安全，但请记住，最终是您必须通过应用严格的访问策略或数据加密来确保云中的数据安全。

感谢阅读“云中的数据”系列的第三篇文章🤗。