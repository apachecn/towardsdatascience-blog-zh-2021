# 我们签了统计数据了吗？🤔

> 原文：<https://towardsdatascience.com/are-we-stats-sig-yet-c78686392b26?source=collection_archive---------22----------------------->

## 先决条件:这个故事是为有运行实验经验的技术人员和业务人员编写的。

![](img/0d46ea614e679c951310e8cc73d882bb.png)

卡洛斯·穆扎在 Unsplash 上的照片

> TL；DR——实验的目标是做出决定，而不是追求特定的显著性水平。

这是在你的业务部门进行最关键实验的第 14 天。你的领导在工作聊天中向你发出 pings 命令，并问:“我们开始了吗？”

您快速运行 t-test 并报告，“嗯，我们在 90%的显著性水平上几乎是 stats sig。”

"好吧，但是我们什么时候能达到 95%的统计签名？"，领导回复。

你指回方差图来解释为什么有些实验即使设计得很好也达不到 95%的统计 sig。不太符合数学，领导回答，“但我们需要做些什么才能得到统计签名？”

好吧…

我们都经历过，对吧？

首先，让我们提醒商界人士“统计签名”是什么意思。

> 统计显著性(stats sig)是什么意思？

根据维基百科:

> 在统计假设检验中，当给定零假设的情况下一个结果不太可能发生时，该结果具有统计意义。更准确地说，一项研究的定义的显著性水平，用α表示，是假设零假设为真，该研究拒绝零假设的概率；一个结果的 p 值，p，是在假设零假设为真的情况下，获得至少是极端结果的概率。根据研究标准，当 p≤α时，结果具有统计学意义。研究的显著性水平在数据收集之前选择，通常设置为 5%或更低——取决于研究领域。

大多数数据科学家认为:

> 统计显著性意味着我们的实验结果不是由于随机的机会。这让我们对我们的决策充满信心，行业标准是使用 95%的统计显著性水平(p ≤ 0.05)。

根据大多数线索:

> 我们获得影响力、人数或晋升的防弹证据。

Stats sig 很重要，但它可能不是我们应该关注的事情。追逐像 95%显著性这样的技术阈值通常会减缓组织学习和迭代的机会。最终，决策从来都不是完美的。

> **杰夫·贝索斯说,“大多数决策可能需要你希望拥有的大约 70%的信息。**如果你等了 90%，在大多数情况下，你可能很慢。”

简而言之，比相关性更好的事情就是学会采取行动。我们是否需要达到 95%显著性水平的高严谨性，这一切都取决于。应该问的问题是，我们能否在当前显著性水平上根据观察到的影响做出决策。

此时，您的利益相关者可能会问“我们没有进行统计签名的原因是什么？”这是一个公平的问题。以下是一些最常见的:

*   **样本量太小** —大多数情况下，这种情况可以在您设置实验之前通过运行功效分析来估计某个效应量(预期影响)所需的样本来回答。我说“大部分时间”是因为不是所有我们测试的产品都有历史数据来计算方差和估计影响大小。经验法则是，效应大小越小，方差越高，所需样本越大。
*   **影响太小**——不是一切都好看。大多数实验失败是因为撞击不存在。延长实验时间不是解决办法。如果在估计的时间内没有看到预期的效果，最好继续前进。
*   **主要指标糟糕** —您的指标不代表您的假设，您可能使用了更难检测的滞后指标，您没有护栏指标来了解任何其他潜在的不利因素，或者您可能有太多或太少的指标。外面有很多文章，有时它更像是一门艺术(煞费苦心地与你的利益相关者保持一致，并不断完善它)而不是科学。

总之，实验的目标是做出决定，而不是追求特定的显著性水平。不要误解我，“统计信号”很重要——它验证你的假设是否有力，它给你一个信号，告诉你你的产品是否有效，它让每个人都高兴，但过分强调无助于决策。正如贝佐斯所推断的——价值在于决策的速度！下一次，如果有人问你，“我们开始签约了吗？”深呼吸，冷静下来，让我们帮助他们理解为什么这可能不是最重要的问题。给他们发这篇文章，祈祷吧🤞，并希望他们喜欢它。

…

这是我的第一篇文章，非常感谢你能说到这一步！如果你觉得它有趣，请鼓掌并分享它！如果你想联系，在 LinkedIn 上联系。

✌·莉莉