# 给分析师(和他们的经理)的 5 个建议

> 原文：<https://towardsdatascience.com/5-tips-for-analysts-and-their-managers-4327ef6e9e13?source=collection_archive---------20----------------------->

## [办公时间](https://towardsdatascience.com/tagged/office-hours)

我在大型零售机构做了两年多的专业分析师。根据你工作的公司的不同，分析师要么被视为一种资产，要么只是一个数字咕噜，在我的经验中，这种鸽子洞是由一些经理的不安全感驱动的，当涉及到更多的数据驱动而不是基于直觉的决策时，也就是所谓的河马(**嗨**最大**P**aid**P**person 的 **O** 小齿轮)。

![](img/e88d678af5f8ff08e1ce8929eca22926.png)

照片由 [Isaac Smith](https://unsplash.com/@isaacmsmith?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

这篇文章的灵感来源于每周一次的会议，在会上，不同的团队展示了他们上周的职能 KPI 指标。你知道那种会议，经理们用他们团队中的分析师准备的电子表格解释他们的数字，用 KPI 框，或者更糟的未格式化的表格。有人关注吗？我们如何才能做得更好？在这里，我为分析师提供了 5 个技巧，以增加他们给团队带来的价值，并为经理提供了一些建议，以更好地与您的分析师打交道。

**分析师提示 1—了解您的最终用户**

分析师的生活很艰难。我们需要成为强有力的沟通者、极具逻辑性的思考者和创意者。在深入研究您的数据仓库(或数据湖)之前，花一些时间考虑您的最终用户需求。这甚至可能意味着留出时间从他们那里获取一份摘要，并询问有意义的问题，因为最终这将使编写查询更加容易。无论他们要求什么，都要增加 50%的范围。浏览可能为您的分析增加更多价值的相邻数据集。我总是有“如果”这个问题为新的分析编写查询时在我的脑海中盘旋。

经理提示:非常具体地说明你要求你的分析师做什么，当他们试图充实你的想法时，要有耐心。设定明确的期望，并给出合理的交付时间表。将此视为协作，而不是自上而下的管理练习。

**分析师提示# 2——通过可视化分析产生影响**

数据可视化是一种艺术形式。大多数人都是视觉化的，分析师的努力是通过使用设计良好的视觉化，让他们的目标受众很容易察觉到洞察力。我见过很多次，人们在一个表格里有四个星期的数据，而你的观众会更容易、更好地察觉到时间序列图的变化。观想应该在头脑中设计一个他们想要回答的特定问题。理解一段时间内的趋势对管理者来说非常重要，而理解趋势如何变化或保持不变的原因更为重要。报告汇总数字往往会隐藏简单 KPI 报告无法反映的潜在变化，通过一系列精心设计的可视化来讲述故事。

经理提示:勇敢一点，在你的下一次演讲中展示一些形象化的东西，这些形象化的东西以更好的细节报告了同样的数字，提高了你与听众的互动。这可能会引发一场讨论，带来更好的业务成果。

**分析师提示 3——开发灵活、动态的仪表盘**

以上的延伸，是仪表板设计过程。谁不喜欢好的仪表盘呢？仪表板是度量和可视化的集合，目的是能够提供更深层次的分析，并使 KPI 无法立即看到的潜在趋势能够被感知。我曾与 Tableau、Microstrategy、PowerBI 和 Quicksight 合作过，总的来说，它们都是同一主题的变体。当你开始开发交互手段时，它们会变得更加强大。这通常是以可控过滤器和参数的形式。

参数是我最喜欢的，尤其是在处理时间序列数据时，能够改变 group by 子句使用的维度，或者改变度量的计算方式是如此强大。我最近开发了一个仪表板，可以让你改变时间序列，从一周到一周的数字，今年到目前为止的累计，每周的百分比变化和 4 周的移动平均值。仪表板应该易于使用且直观，并使您的客户能够使用您收集的数据回答一系列问题。设计是一个令人难以置信的深思熟虑和创造性的过程，不应该匆忙。不时回顾一下你的工作，考虑改进的方法

经理提示:花时间和你的分析师在一起，让他们解释新仪表板的特点，以及你如何最有效地使用它。确保理解它可以回答的问题的范围，并提供有意义的反馈。这是一种合作。

**分析师提示 4——不要访问原始数据**

这是我最讨厌的事情，当经理不信任你提供的数据，所以他们坚持要看数据或者在仪表板上显示原始数据。这到底有什么意义？事实上，关键是你没有做好你的工作。如果你被要求提供大型数据集，一定要问“你想了解什么？”。你最不希望的事情就是经理或同事浪费时间玩电子表格，试图找到一些不存在的东西，或者更糟的是，有一些东西你却没有发现。为了透明起见，如果有人想了解数据集是如何生成的，请解释(在合理的情况下)表逻辑。这又回到了我们的第一个技巧，在理解了最终用户的需求之后，正确理解你所收集的数据。

经理提示:不要要求看原始数据，把这作为一个反馈的机会，和你的分析师一起探索你想要回答的问题。10 次中有 9 次可能需要生成进一步的查询。

**分析师提示 5——重视自己**

有时分析师没有得到我们应得的赞扬或认可。我们苦于复杂的查询，与数据工程师和架构师合作，这样我们就可以访问额外的数据源，开发可视化和仪表板。在付出所有努力后，你最不希望的就是不被你的团队和管理层重视。我们所做的需要时间，但当分析可重复地完成时，会为我们各自的业务增加巨大的价值。现在是做分析师的最佳时机，随着新冠肺炎的影响遍及全球，下一波技术提升正在加速，企业正在转向更好地利用他们最宝贵的资产——数据。所以，珍惜你自己，你的技能，如果你觉得自己没有被重视，(谨慎地)找另一份工作。你没什么可失去的。

经理提示:让你的分析师从事有意义的工作，并促进他们的持续发展。给他们找一个内部导师，或者如果你的组织有能力的话，让他们接受进一步的培训。就业市场正在经历一场代际转变，随着企业寻求提高内部分析能力，竞争越来越激烈。员工流失通常是糟糕的管理和组织文化的结果。

**结束语**

我曾在对分析师的角色有不同看法的环境中工作过。分析师是天生的商业伙伴；我们的业务线和数据之间的接口。您在贵组织的未来发展方向中扮演着越来越重要的角色。您可以通过数据驱动决策来传达您的发现，并实现自助服务分析。你对业务系统有独特的理解，并能看到别人可能看不到的链接。你将跨职能领域合作，并在组织内部和外部建立专业网络。想一想你可以增加价值的方法，以及如何更聪明地工作。最后，要引人注目，并为自己的工作邀功。

对于阅读本文的经理们，我建议建立一个定期的一对一会议，以保持与你的分析师的沟通渠道畅通。与他们进行建设性的协作，他们将为您提供推动业务成果所需的数据火力。

今天的分析师是明天的商业领袖，通过数据和独特的商业理解获得信息，我们代表着新一代的管理者，他们将做出更好更快的决策。