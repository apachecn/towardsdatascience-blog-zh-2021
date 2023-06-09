# 数据科学中更好的软件写作技巧:保持干燥

> 原文：<https://towardsdatascience.com/better-software-writing-skills-in-data-science-be-dry-efe6d3dc2e27?source=collection_archive---------38----------------------->

![](img/2954b760cdf83a8a05344656aa2a6e79.png)

*封面图片由*<https://pixabay.com/users/chillervirus-2033716/>**[*pix abay*](https://pixabay.com/)*组成。***

**首先，我想回到上周的帖子，问你一个问题。我收到了一位读过我博客的朋友的评论，他告诉我一些大致的内容:“显然，让你的学员读一本书是你的指导方式”。这让我想到……考虑到与不直接与我合作的学员进行准时的指导会议(连续数周，每周半小时),考虑到提高软件开发技能的总体目标，以及更具体的 Python 软件编写技能，有人能提出更好的方法吗？我真诚地接受建议。**

**现在，让我们继续使用当前的方法，并将本周的指导和帖子建立在“实用程序员:从熟练工到大师”的第二章:实用方法的基础上。在那一章中提出的观点之一就是所谓的干原理。不要重复自己。**

**不重复自己当然是软件开发的一个重要方面。在多段代码之间进行复制粘贴可能是最好的方法，而且速度很快。然而，当在那些多个副本中的一个中发现一个 bug 时，你会做额外的努力到处纠正它(包括其他人的工作)吗？你能找到所有这些拷贝吗？有时，复制粘贴的代码可能会有一些变化。更改变量名，到处添加条件，…**

**几年前，我领导了一个项目，开发了一个检测软件克隆的软件。即使我们能够识别出与原始版本不同的软件克隆，让软件开发人员基于这种洞察力重构代码也是非常困难的，甚至是不可能的。当一个克隆体被创造出来，就很难杀死它！所以最好的方法是不要创建它们，从头开始重构，根据需要创建函数或类，而不是复制粘贴。**

**希望我说服你在数据科学的软件开发中保持干爽。但这也适用于数据科学的其他方面。您是否曾经在这样一个地方工作过，那里的数据定义依赖于许多列，可能来自不同的表，这些表没有标准化，并且对于许多仪表板或查询是重复的。什么是你网站的访问者？网站的任何页面有点击率吗？你有没有安排一些会议，并且每次会议只数一次？你是否有一个登录名并且只计算用户数？假设会话跟踪或用户登录，你如何计算访问者的数量？是一段时间内的滚动平均值吗？那段时间是什么？它很容易成为确定谁是特定时间的活动用户的重要查询。你确定组织里的每个人都用最新最伟大的定义吗？查询是否从仪表板复制粘贴到仪表板？这个定义是根据一个人或一个团队的目的稍微修改的吗？你看，不要重复你自己也适用于数据定义。有多种方法可以解决这个问题，但没有一种方法是简单的，你允许代码、查询或定义复制粘贴的时间越长，就越难杀死那些克隆体。**

**在第二周的练习中，我建议找出一个你的团队中制造了大量克隆的区域或特定实例。找个人(最好是你团队里的)讨论一下。有没有什么方法可以提出一段代码、查询或定义，并开始重构相关的工件来消除这种克隆？这可能很难！什么是可接受的渐进方式？我们如何确保未来不会产生新的克隆体？这可能是您的团队将要采取的最初几个步骤，以限制和减少您的工件中的克隆。**

**至于上周，第二章还有更多内容。尽管如此，对于希望提高 Python 编程技能的初级数据科学家来说，我建议熟能生巧。在这种情况下，这个主题内的练习可能会被证明是有用的。**

**一旦你完成这个练习，问问你自己我上周练习中提出的所有问题。更具体地说，你应该确保自己不会重复。密码问题是对称操作的一个很好的例子，对称操作有很好的代码重用潜力。如果您没有定义在编码和解码之间多次使用的函数，我建议您重新考虑一下您的实现。另外，一定要思考上周的其他问题:你会早休息吗？你尊重合同吗？你记录你的程序吗？你有单元测试吗？**

**同样，如果你能接触到一个你觉得相处融洽并且你认为他写了很棒的代码的人，问问他对你的练习解决方案的意见。你可能会学到一两件事！或者，如果你解决了那个问题，你可以看看其他人的最佳解决方案。阅读他人的代码也是提高编程技能的好方法。**

**我知道我说的是每周一个话题，但是这一章还有一个方面值得一提。我不会增加更多的锻炼，只是一个潜在的终身追求！主题是评估。这本书会告诉你记录你的估计。我说:不要简单地记录这些，记录你做的每一件事以及花了多长时间。在你职业生涯的早期，记录下你做了什么，花了多长时间。随着时间的推移，尝试概括您收集的数据，例如，所有数据概念都定义良好的数据请求平均花费我 *x 小时*；使用现成的图表类型创建一个带有 *y 图表/数据点*的仪表板平均花费我 *x 小时*；…为自己建立一个评估库。**

**当你开始对你的个人估计有一个概括的心智模型时，用它做一个游戏。即使没有被要求做一个评估，也要做一个，然后检查它有多好。让游戏化成为你的优势，让你更好地预测未来！**

**如果或者当你毕业去领导团队时，你会发现你的评估也是一个很好的基础。然后，当您了解团队成员时，您可以对他们应用对等因素。甚至可能从那次练习中找出他们的长处和短处。**

**这是我对“实用程序员:从熟练工到大师”第二周/第二章的快速补充，作为提高数据科学中软件编写技能的媒介。下周见第 3 章:基本工具。**

**![](img/dc1ea9aa652b6182e81355e463ee319b.png)**

**在软件领域 20 多年了。目前在 Shopify 担任数据科学家。在深度学习、机器学习/分析、云计算、物联网、领域特定语言、遗传算法和编程、人工生命/智能以及所有技术领域的研究兴趣！[通过点击](https://thelonenutblog.wordpress.com/author/potvinpascal/)查看所有帖子**

***原载于 2021 年 3 月 30 日 http://thelonenutblog.wordpress.com**的* [*。*](https://thelonenutblog.wordpress.com/2021/03/30/better-software-writing-skills-in-data-science-be-dry/)**