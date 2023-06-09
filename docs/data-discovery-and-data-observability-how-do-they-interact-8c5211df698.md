# 理解数据发现和数据可观察性之间的关系

> 原文：<https://towardsdatascience.com/data-discovery-and-data-observability-how-do-they-interact-8c5211df698?source=collection_archive---------28----------------------->

## 数据可观测性是后端，数据发现是前端

![](img/74069f19b615bbdf3cebc8355e8bfb67.png)

图片来自 [Castor](https://www.castordoc.com/blog/data-discovery-and-data-observability-how-do-they-interact) 的博客

合著者:[凯尔·柯文](https://www.linkedin.com/in/kylejameskirwan/)——big eye 的联合创始人兼首席执行官

数据可观察性工具和数据目录已经成为现代数据堆栈的重要组成部分。这不足为奇。数据量呈爆炸式增长，移动和操作这些数据的工具正以惊人的速度增长。数据越多，工具越多，就越难**找到、理解和信任**你拥有的数据。最近，有两个关键问题使数据可观察性和数据发现解决方案成为焦点:

1.  负责将数据从一个系统转移到另一个系统的数据管道已经变得极其复杂。随着数据操作工具的增多，数据管道中相互连接的部分越来越多。数据更有可能在整个管道中被破坏，并且定位故障发生的位置或了解如何解决问题变得更加困难。因此，数据工程师需要花费数天时间来寻找数据问题，整个组织对数据的信任度直线下降。
2.  随着组织中数据集的数量呈指数级增长，文档编制成为一项极其艰巨的任务。手工记录数千个表和数百万个列是不可能的。因此，数据用户花更多的时间去寻找和理解数据，而不是进行有价值的数据分析。

而是新的问题，新的解决方案。数据**可观察性**解决第一个问题，而**数据发现**解决第二个问题。本文致力于解释这些工具是什么，以及它们如何协同工作来为您公司的数据带来可信度。

# 数据可观察性和数据发现:它们是什么？

数据可观察性指的是组织完全了解其系统中数据的**健康状况的能力。可观察性实现了对数据管道中数据行为(如数据量、分布、新鲜度)的持续**监控**。基于这些见解，它创建了对系统、其健康和性能的整体理解。拥有对数据管道的“可观察性”意味着你的数据团队可以**快速**和**准确**识别和防止数据中的问题。数据可观察性工具结合了工具、监控、异常检测、警报、根本原因分析和工作流自动化等功能。这有助于数据团队发现、修复和防止问题搞乱他们的分析和 ML 模型。**

数据发现工具使任何使用数据的人能够快速**和准确**地**找到并理解他们需要的数据。以发现为中心的目录(与企业中常见的以控制为中心的目录相反，这些目录需要仔细管理谁可以在多长时间内访问哪些数据)将搜索、受欢迎程度排名、查询历史、世系、标记、Q & A 历史等功能与公司仓库中的所有数据相结合。这有助于数据团队更快地移动，减少混乱和误用风险。**

# 但是为什么“快速”和“准确”如此重要呢？

**快速**很重要，因为许多从事数据工作的人很难找到，雇佣起来很贵，而且每周都超负荷工作。减去 10 分钟的空闲时间，找到并通读过时的文档，或者运行一系列重复的 SELECT *查询。尤其是当每个人都在静静地每周做 5-10-20 次的时候。如果您有一个 10 人的数据团队，平均每年花费 900，00 0 美元，那么您很容易每年损失 70，0 00 美元，而且随着您的团队规模的扩大，损失还会增加。

**准确地说**很重要，因为当团队成员为企业做实际工作时，工作的正确性取决于他们是否正确地使用了数据。做分析以告知当年支出增长的人可能不得不猜测使用 3 个时间戳列中的哪一个:事件记录在用户移动设备上的时间、事件到达公司网关的时间、记录写入数据库的时间。除了它们可能被命名为对记录它们的工程师有意义但对其他人来说难以理解的事物:ts、created_at 和 local_time。最终的分析通常以数据用户的纯粹猜测而告终。

# 需要一个全面的解决办法

速度和准确性是复杂的问题。完全解决这些问题的团队可能仍然会获得手工文档或者基本管道测试覆盖的一些好处，但是他们错过了由于知道这两个问题正在被全面解决而带来的生产率提高。事实上，速度和准确性作为投资的函数有一个凸值，这意味着**你要么全押，要么根本不做**。半心半意的努力不会让你有任何进展。这促使优步、Airbnb、Lyft 和 LinkedIn 等公司的一些世界上资金最充足的数据团队不仅建立了俗气的局部解决方案，还为这两个问题领域建立了成熟的内部产品。

当团队全面解决了这两个挑战**时，他们会得到一个神奇的奖励特性:**信任。****

**信任是一种模糊的东西，很难量化，但每个组织都非常想要。没有人喜欢质疑他们用来决定是否继续每月花费 5 万美元进行广告宣传的数据，或者新产品功能是否真的提高了 11%的参与度，或者用户看到的模型预测是否会出问题。**

> ***💡但是要获得信任，组织需要知道两件事:我们是否以正确的方式使用数据，以及数据是否真的按照预期的方式工作。***

**像 Castor 这样的发现产品解决的是前者，Bigeye 这样的可观测性产品解决的是后者。但是当你两者都有的时候会发生什么呢？**

**在像优步、Airbnb、网飞和 LinkedIn 这样已经在内部构建了这些产品的全球规模的公司中，它们通常是深度集成的——看看他们关于 Databook、Metacat 和 Datahub 的博客帖子就知道了。这为数据团队提供了他们需要的所有元数据，让他们知道他们正在以正确的方式使用数据，数据正在按预期工作，并且在不增加工作流摩擦的情况下完成所有这些工作。**

**现在，数据科学家知道使用三个时间戳列中的哪一个。他们知道，在过去的 90 天里，没有任何 nulls、dupes 或 future 值隐藏在其中，会扰乱他们的分析。由于耦合良好的工作流程，他们在大约 10 秒钟内就知道了所有这一切。**

# **为什么需要独立的数据目录和数据可观测性平台？**

**您现在可能已经理解了，以一种全面的方式解决速度和准确性问题将使您在数据策略方面达到您想要的位置。但是一个问题仍然存在:全面解决这些挑战是否意味着使用一个单一的、一体化的工具来实现数据可观察性和数据编目，还是应该投资购买两个独立的工具来无缝集成？出于显而易见的原因，我们个人建议使用两种不同的工具。**

**发现和可观察性问题是特殊的，因为数据发现解决方案的主要用户不同于可观察性平台的主要用户。**数据分析师、产品科学家**和其他数据消费者关心数据发现，因为他们需要找到、理解和使用数据来完成工作。**另一方面，数据工程师**更关心可观察性，因为他们负责修复和预防数据管道中的问题，以确保数据的可靠性。**

**这两个配置文件具有完全不同的工作流程。数据工程师希望在他们自己的内部系统中的工具(如 PagerDuty)中捕获数据质量信息，而数据分析师希望看到这些信息显示在数据目录中。即使在 UI 方面，数据工程师和数据分析师也有不同的期望。独立的数据可观察性平台可以满足数据工程师的工作流，而独立的数据目录可以满足分析师和业务用户的工作流，而不会影响他们。**

**数据发现和数据可观测性是两个复杂的问题，需要大量的专业知识才能有效解决。由于这个原因，只要两个解决方案无缝集成，许多数据团队将会更好地结合每个问题的最佳解决方案。**

# **最后的想法**

**如果没有**数据发现**和**数据可观察性**，利用您的数据是极其困难的。随着组织收集越来越多的数据，以及数据管道过程变得越来越复杂，这种情况会变得更加严重。同时解决**速度和**准确性将建立对您所拥有的数据资产的根深蒂固的信任。全面解决这些问题的最佳方式是将最佳发现和数据可观察性解决方案结合在一起。如果您需要任何选择帮助，我们已经将[可观察性](https://notion.castordoc.com/catalog-of-data-quality)和[发现](https://notion.castordoc.com/catalog-of-catalogs)解决方案的基准放在一起。**

***原载于*[*https://www.castordoc.com*](https://www.castordoc.com/blog/data-discovery-and-data-observability-how-do-they-interact)*。***