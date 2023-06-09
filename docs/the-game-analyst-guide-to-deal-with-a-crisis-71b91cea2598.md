# 游戏分析师应对危机指南

> 原文：<https://towardsdatascience.com/the-game-analyst-guide-to-deal-with-a-crisis-71b91cea2598?source=collection_archive---------41----------------------->

## 尽管所有的努力都是为了提高软件质量，但有时还是会发生意想不到的事情，作为一名游戏分析师，你必须处理危机情况。

当你是一名游戏/产品/商业分析师时，你很可能以一杯你最喜欢的含咖啡因的饮料和一个监控会议开始你的一天。你检查了你的主要 KPI，你最喜欢的仪表板，然后，在危机的一天，你会注意到有些不对劲。理想情况下，一些警报系统已经提示你房间里有烟，或者可能是其他人首先注意到这种情况。

根据危机的严重程度，(即对底线的潜在影响)，你的心脏会跳动，你的大脑会释放多巴胺，奖励你发现有什么不对劲，在“战斗或逃跑”的反应中，你会感到肾上腺素突然激增。你需要所有这些化学物质来度过这一天。是时候戴上侦探帽了。

![](img/a321cab201d08344f96764e8c3de8f19.png)

夏洛克·福尔摩斯侦探和约翰·华生医生在火车上一起破解一个谜。西德尼·佩吉特的插图

# 从为什么开始

除了作为一本令人惊奇的书的标题之外，西蒙·西内克的《从为什么开始》是你注意到你的产品/游戏发生了一些事情之后的第一个任务。

你的任务是帮助你的团队理解某些 KPI 过低的原因。如果你能找出原因，团队就能更快地解决问题。或者至少，会有应对后果的策略。

![](img/082ea201de08201a8661cf56ad6d8712.png)

由[马库斯·温克勒](https://unsplash.com/@markuswinkler?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](/s/photos/crisis?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄

因此，您的首要任务是为可能对您的产品造成负面影响的任何因素制定假设。为了提出更好的假设，你应该试着理解:

*   是否报告了任何可能影响 KPI 的错误？
*   谁受到影响/有多少玩家受到影响？
*   负面影响是否与更新/修补程序相关？
*   有没有可能在以前的更新中引入了一些东西，以前的 AB 测试开始了雪球效应？
*   是否有任何不可预见的季节性/黑天鹅事件可以解释这场危机？

# 客户支持/社区是您的得力助手

我明白了，同情和接触玩家/用户是获得玩家体验核心的关键。在团队中，没有人比客户支持(CS)和社区经理更了解玩家/客户。

询问 CS 某一类型的票证是否有所增加，是否报告了任何值得注意的错误，可以加快了解是否存在错误的时间。你将能够利用这一信息来源开始制定假设，或者为你正在考虑的现有假设提供支持。

# 沟通和可见性

大多数公司都有一定的程序来处理即将到来的产品危机。不管过程如何，你都应该是团队和利益相关者的持续信息来源。

![](img/fb7cfdfe5ba43e67384e11ec45eec8a6.png)

掌握事实，让每个人都了解情况。西德尼·佩吉特的插图

你应该让团队参与你的假设和整个调查过程。让他们了解任何可能帮助他们解决/解决问题的新信息。

您还应该让所有利益相关者参与当前的调查。让每个人都了解最新情况有助于在问题解决后报告长期影响。

# 分步解决

细分、细分、细分、细分……所有你能想到的细分用户的潜在方法都应该考虑到你的跑步假设。这里有一些典型的例子，如果你感到恐慌，并且在这个需要的时刻你的创造力让你失望了，这里有一个你可以参考的列表(专业提示:创建你自己的“飞行前检查”/“正常清单”部分，你可以浏览一下以确保你覆盖了所有的基础):

*   按设备。不同平台的用户受到的影响是一样的吗？这意味着检查看到负面影响的主要 KPI 是否表现不同，无论用户是在桌面上玩还是在移动上玩，iOS 还是 Android，iPhone 9 还是 iPhone 12。
*   WiFi 与 4G。WiFi 上的玩家和 4G 上的玩家受到的影响有区别吗？
*   按国家/地区。不言自明，但在处理涉及季节性、游戏服务器位置等假设时会很有帮助…
*   按用户获取来源。如果问题只影响新用户，那么了解我们在有机活动与付费活动、代销商活动与营销活动之间的 KPI 行为是否有任何差异至关重要…在过去几天中，交易量是否有显著变化(考虑至少 30 天的时间来检测这些变化)
*   AB 测试。如果你正在进行多变量测试/实验，不要忘记检查一个特定的变量是否导致了即将到来的危机。

# 关联并消除

细分有助于了解和找到哪些球员受到影响的证据，从而有助于缩小搜索范围。但是，我们不应该忘记良好的旧技术图表分析，以了解什么可能导致手头的问题。在这里，我们使用与[单受试者设计](https://en.wikipedia.org/wiki/Single-subject_design)实验相同的原则，并使用视觉分析来快速了解是否存在与可能影响游戏状态的事件的相关性([在单案例设计研究中系统地使用视觉分析来评估结果](https://www.cambridge.org/core/journals/brain-impairment/article/systematic-use-of-visual-analysis-for-assessing-outcomes-in-single-case-design-studies/57014928F0BDC5D2E26F331627D94341))。

为了实现这一点，我们希望绘制一段时间内的相关 KPI，并将基线移动与某些事件相关联。

专业提示:让团队的所有成员都参与绘制/记录可能影响基线的特定事件。当你不得不回顾和关联基线运动和特定事件时，这是非常有用的。如果你需要灵感，这里列出了一些常见的东西:

*   营销计划和特色。我们想检查一些营销活动是何时发生的，或者是否有病毒/特色活动。这些事件通常会导致新玩家的大量涌入，而这些新玩家可能并不最适合该产品。在这些事件期间和之后，一些早期 KPI 会受到影响，这是正常的。
*   AB 测试。除了对当前的 ab 测试进行细分之外，回到过去并理解推出一个变体是否会产生不可预测的负面长期影响通常也是相关的。
*   游戏更新，补丁。更多的时候，游戏更新或补丁引入的错误会成为危机的根源。当涉及到先前更新的不可预见的长期影响时，要特别好奇。当你觉得你的产品知识不是最好的时候，仔细检查所有引入的变化并询问团队成员他们是否认为某些东西对游戏有负面影响是很重要的。
*   已知的错误。有时还有众所周知的“宠物”虫子。这些曾经被标记为低优先级，并被归入 bug backlog 的遗忘区。当团队发现与新内容的新协同作用，或者环境发生变化，并且它们的相关性增加时，其中一些 bug 会回来困扰他们。
*   直播行动。现场修改或游戏内事件。

![](img/e7d2019dacb7e12af0bacd38d9835f32.png)

无害的“宠物”细菌有时会演变成超级细菌，对游戏 KPI 产生负面影响。Joshua Hoehne 在 [Unsplash](https://unsplash.com/s/photos/ladybug?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

根据危机的性质，你的游戏分析师工作和优先事项可能会在一段时间内发生变化，从几天到几周。因此，我在这个系列中又增加了两篇文章，重点介绍预防措施以及如何处理后果。

我喜欢在工作中遵循一个著名的“5-P”咒语:适当的准备可以防止糟糕的表现。在[游戏分析师工具上了解更多关于如何为危机做准备，以防止和解决危机](https://danielafontes.com/2021/03/10/the-game-analyst-guide-to-deal-with-a-crisis-part-2/)。

如果你已经准备好处理产品危机避免后的事情，请阅读本系列的第三部分，也是最后一部分:[游戏分析师处理危机后果指南](https://danielafontes.com/2021/03/10/the-game-analyst-guide-to-deal-with-a-crisis-part-3/)。

*原载于 2021 年 3 月 8 日 https://danielafontes.com**的* [*。*](https://danielafontes.com/2021/03/08/the-game-analyst-guide-to-deal-with-a-crisis/)