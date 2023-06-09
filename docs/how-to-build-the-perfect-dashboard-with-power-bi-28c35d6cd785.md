# 如何使用 Power BI 构建完美的仪表盘

> 原文：<https://towardsdatascience.com/how-to-build-the-perfect-dashboard-with-power-bi-28c35d6cd785?source=collection_archive---------6----------------------->

## 在 Power BI 中构建杀手级仪表板的技巧

![](img/8e703b3e94bb9f4c2426451f7ed24233.png)

活动创建者的照片 [@campaign_creators](http://twitter.com/campaign_creators) 在 Unsplash

正如 Bernard Marr 在他为《福布斯》撰写的精彩文章 t [中所引用的那样，](https://www.forbes.com/sites/bernardmarr/2016/04/28/big-data-overload-most-companies-cant-deal-with-the-data-explosion/?sh=147dbd476b0d)我们正遭受着数据过载的困扰。数据以多种不同的格式随处可见，迫切需要将这些数据转换为信息。信息是决策的关键因素，因为它是数据中最有价值的部分。

信息的概念是客观的、可读的、易于理解的，我将在本文中介绍一些技巧，以提取数据的最佳部分，并将其转化为 PowerBI 仪表板中的有用信息。

![](img/e5d90ef87e0f86512e1b8e33851bd931.png)

作者图片:数据 vs 信息

在 Power BI 等数据可视化工具中，处理后的数据显示在报告或仪表板中。一个好的报告或小组的发展需要考虑许多领域，如编程、设计、UI/UX、神经科学、语言等等。为了保证信息的有效性，与用户建立联系是必不可少的，因此有了叙事的概念。

如果您是第一次接触 PowerBI，或者您没有这方面的经验，我建议您阅读下面这篇文章，它详细解释了什么是 PowerBI 以及如何启动它:

</powerbi-the-tool-that-is-beating-excel-8e88d2084213> [## power bi——击败 Excel 的工具

towardsdatascience.com](/powerbi-the-tool-that-is-beating-excel-8e88d2084213) 

# 讲故事

人类天生就有讲故事的能力，我们从小就一直在讲故事。讲故事是一种工具，用来与读者建立联系，并尽可能有效地传递信息。

为了创作好的故事，我们必须保证一些基本因素，例如:

*   **视觉化中的美和设计模式**——人类非常沉迷于模式和完美的形状。如果你使用一些设计模式的概念，如[黄金比例](https://www.invisionapp.com/inside-design/golden-ratio-designers/)和一些颜色模式，它会突然提高你的仪表板的美感。
*   **简洁** —有时少即是多，限制仪表盘中的图表数量，只展示最重要的图表，不要使用复杂的壁纸，白色背景可能是实现简洁的良好开端。
*   **易于阅读和理解**——“完美的图形是不需要进一步解释的图形”。对于每个关键用户来说，一个图表在第一眼看上去必须非常清晰易懂。如果你不得不花时间解释这个图表，那么它很有可能不是一个好的图表。
*   与目标受众使用相同的语言 —有时你在大学里向一群学生展示仪表板，有时你在为一家国际公司的首席执行官开发仪表板，他们使用的语言完全不同。因此，关注你的目标受众，并根据每个场景调整你的方法是非常重要的。
*   **数据可靠性** —仪表板中呈现的数据必须可靠。数据质量部分对每个面板都非常重要，检查每个数字、KPI、过滤器交互、随时间变化的图表，并尝试将数字与公司内的其他来源进行比较。一个错误的数字可能会导致决策过程中的巨大错误，并使您的仪表板失去信誉。

随着时间的推移和大量的研究，我们获得了以越来越自然的方式生成仪表板的经验，并有了良好的故事发展。

剩下的问题是，我怎样才能学会用更少的经验来构建一个好的仪表板并实现好的故事讲述呢？我如何在不花大量时间阅读内容的情况下发展我的数据可视化技能？
为了回答这些问题，我将给出几个小技巧，帮助你为各种场合打造完美的仪表盘。

# 如何选择你的图表

知道哪种类型的图表最适合每种洞察力是非常重要的。一个错误的选择会增加分析和理解洞察力的难度。图形可视化旨在以最简单、最直观的方式展示数据。

> "完美的图是不需要进一步解释的图."

Andrew Abela 博士发表了一个很好的图表，帮助我们决定哪个图表更适合每个场景。点击以下链接查看完整图表:

[https://apandre.wordpress.com/dataviews/choiceofchart/](https://apandre.wordpress.com/dataviews/choiceofchart/)

Andrew Abela 博士指出:

*   比较数据如果我们想比较不同项目之间的数据，我们应该使用条形图

![](img/0cf7f4a684d56bbce3f7d9062e6d81c5.png)

作者图片

或者使用折线图来比较一段时间内的数值

![](img/80ff1b853b3840749a3550f07773f811.png)

作者图片

*   为了显示数值之间的**关系**，我们应该使用两个变量的散点图和三个变量的不同点大小的散点图。

![](img/e7ce7532baf8f0887a1c5e1c7c985eb6.png)

作者图片

*   为了分析**数据分布**，我们应该主要使用单个变量的直方图或两个变量的散点图。

![](img/47624e493b45d5b2c46a3051d7683521.png)

作者图片

*   为了理解数据的**组成**,如果变量随时间变化，我们应该使用条形图或面积图

![](img/cd55ed709e573b30bf455b70f6661d6f.png)

作者图片

或者如果变量是静态的，则是比萨饼图或瀑布图。

![](img/b0c00ee6d3d2dbd725bd84932c67cf7e.png)

作者图片

# 调色板

在你的显示屏上，颜色也是至关重要的。糟糕的颜色选择会使你的仪表板难以阅读，或者在视觉上没有吸引力。避免在仪表盘中使用太多颜色，如果你要像 PowerPoint 演示一样从远处观看，选择对比度高的颜色以提高可视性，从远处和近处观看你的仪表盘，向其他人展示你的仪表盘，并查看她的反馈，想想你的观众中是否有色盲者。下面是如何使用色轮组合的基本说明。

![](img/027329b38ba795a53dc6d90e2617278b.png)

互补色—作者图片

![](img/cd7d4ee26c77223d42ae5a1d23225765.png)

相似的颜色-作者图片

![](img/79467a1267bf5df20482601f6ec3ca82.png)

三角形—作者提供的图像

![](img/3f7d71de86ad40854ecc3fef7fb104b0.png)

方形/矩形—作者提供的图像

Power BI 有几个带有预定义调色板的主题，但你也可以在互联网上找到一些，总之我在下面的链接中留下了一些不错的主题:

<https://colorhunt.co/>  ![](img/1ac72e841d5216681d7756c649c5378d.png)

米卡·鲍梅斯特在 Unsplash 的照片

# 如何展示你的见解

洞察力可以分为 3 个不同的组:*业务可见性、绩效改进和机会发现*。

这 3 种不同类型的见解有不同的观点，并针对每种情况进行了优化，以便更好地理解，我将在下面对它们进行更好的解释:

## 1.业务可见性

呈现业务可见性类型洞察力的最常见方式是通过**报告**。
报告是一次性报告，旨在显示有关业务的特定问题的答案。报告通常通过电子邮件共享或用 PowerPoint 演示。
报告是一个模板，旨在提供对业务中一段时间以来发生的事实的简单度量的洞察。一个更简单的视图，其中除了图表中显示的内容之外，它没有提出其他见解。

![](img/7e33e311d14b5c30d05f4cadc20949d0.png)

作者图片

## 2.性能改进

通常与绩效改进洞察相关的工具是**记分卡**。
在绩效改进类型洞察中，图表已经更加详细，包含一些指标，显示为目标受众带来价值的数据，如*目标、平均值、总计、最大值和最小值*，以便团队以更实际的方式提取最大值。这种图表使用大量 KPI(指标)、计算值和统计数据。

![](img/b5721dc43a0c5fdebd99bc0215f7fcaa.png)

按作者分类的图像—报告+记分卡

## 3.机会发现

通常与 Opportunity Discovery insight 相关联的设备是**仪表板**。
仪表板是以复杂但易于最终用户理解的方式以多种方式呈现的数据。仪表板显示已经处理的数据，包括各种 KPI、相关性、预测、数据随时间的演变、指标等。通常，这种类型的可视化经常被分析师、经理、投资者、协调员以及需要大量数据来做出决策的人使用。

![](img/52f0e4a773706c54783fb237180e81e3.png)

按作者分类的图像—仪表板

# 一般查看提示

构建完美仪表板或报表的一些通用可视化技巧。

1.  **移除边框** —尝试以自然的方式呈现您的图形，使其适合您报告的背景，并与其他图形形成互动，不要用边框删除它。
2.  **拥抱留白**——避免在你的仪表盘上留下太多杂乱的东西，通常一点留白有利于整体的和谐。
3.  **收缩文本** —尝试以标题或题目的形式将文本包裹在图形中。把几段话剪成简短易懂的句子。“一图胜千言，一图胜千图”

# 示范

最后，我演示了如何应用本文中给出的技巧来转换报表。
上述报告提供了巴西圣保罗市的啤酒消费信息。下面的第一份报告是一份很长的文本，有几个关于消费的图表和指标。颜色是标准的，文字太大，图形不在标准空间，很多数据难以理解。不管怎么说，要理解报告要经历的每一件事，都需要很多时间。

![](img/8f0281bf6f58496cf725f28c45a29bd7.png)

原始仪表板—按作者分类的图像

使用这些提示后，我们可以看到图形有了显著的改进。颜色更好，更个性化，对比度更好，重要数据突出显示且更大，数据位于标准化位置，文本大大减少，但没有丢失最重要的信息，最终我们可以更容易、更简洁地理解见解。

![](img/e7776523f3293b753bc5e7b083bac21f.png)

新仪表板—按作者分类的图像

非常感谢您的阅读！我希望这些技巧可以帮助您开发仪表板，并帮助您在数据世界中了解知识。

有任何问题或建议可以通过 LinkedIn 联系我:[https://www.linkedin.com/in/octavio-b-santiago/](https://www.linkedin.com/in/octavio-b-santiago/)