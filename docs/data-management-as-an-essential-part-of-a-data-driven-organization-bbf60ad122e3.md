# 数据管理是数据驱动型组织的重要组成部分

> 原文：<https://towardsdatascience.com/data-management-as-an-essential-part-of-a-data-driven-organization-bbf60ad122e3?source=collection_archive---------33----------------------->

![](img/19b4eb023f82b0bd3ba07ae1b0eff771.png)

[https://unsplash.com/photos/ZOHa76txKfo](https://unsplash.com/photos/ZOHa76txKfo)

*数据科学领域至少在 10 年内快速发展，尽管时间很短，但数据文化已经开始成为主流。即使是石油和天然气或采矿等传统领域的企业公司，也已经将他们的思维模式从作为会计需求商品的数据提升到数据优先，甚至政府也宣布了国家数字战略。也许今天没有一家公司没有宣布他们是数据驱动的，每一个决策都是基于数据的。尤瓦尔·诺亚·哈拉里在他的书《德乌斯之家》中反思了数据宗教的兴起*

当一种数据文化正在兴起时，各种各样的专业出现了，今天我们不再怀疑何时会遇到首席数据官、数据分析师、计算机视觉工程师、数据工程师、商业智能专家、数据产品经理、数据管家等。与此同时，MLOps、DataOps 或 Data Governance 等整个方向似乎就在昨天兴起。一切都取决于数据，没有任何迹象表明数据发展有所放缓。

然而，在这次反思中，我会找出基本的定义:什么是数据管理，以及创建一个数据驱动的公司需要怎样的核心数据团队。

# 什么是数据管理

数据管理协会(DAMA)提供的官方定义将数据管理解释为在数据和信息资产的整个生命周期中交付、控制、保护和提高其价值的计划、策略、程序和实践的开发、执行和监督活动。

与此同时，Gartner 词汇表提供了一个实用的定义:数据管理由实践、体系结构技术和工具组成，用于在企业的各种数据主题领域和数据结构类型中实现一致的数据访问和交付，以满足所有应用程序和业务流程的数据消费需求。

换句话说，一般来说，数据管理是一个专注于为最终用户提供数据证明、安全性及其质量的领域。该领域的主要课题可分为:

*   **数据库管理** —关系数据库和 NoSQL 数据库的设计和维护是必不可少的，但同时对任何组织的用户都是隐藏的，当出现问题时，普通用户会知道。在开始从数据使用中获得收获之前，应该推出数据仓库或/和数据湖。随着数据文化的兴起，这个领域也在不断发展。然而，只有在关键业务流程中使用数据之后，业务用户才明白投资核心数据基础设施的重要性。
*   **数据整合** —从不同来源收集数据是任何分析的起点。这包括提取、加载和转换(ELT)，它是 ETL 的一种变体，在将数据加载到目标平台时，它会保持数据的原始形式。
*   **数据治理、数据质量** — GIGO(垃圾输入，垃圾输出)是一个众所周知的概念，每个分析师都至少曾经面临过数据质量问题。清理和保持数据有序是数据驱动型组织的一个主要概念。如果你不确定所用数据的质量，你如何保证决策的质量。数据治理定义了应该做什么，数据一致性和完整性是该过程的关键指标。

因此，数据管理是发展数据驱动型组织的基础或起点。与此同时，最终用户或首席执行官可能会在进入数据分析和重新设计数据驱动的现有业务流程后感到努力。

# **数据分析 vs 数据管理**

记住这一点，让我们定义什么是数据分析。
Garner 词汇表解释了分析特定领域信息的过程，或/和将广泛的 BI 功能应用于特定内容领域(例如，销售、服务、供应链)的过程。

因此，正如我们在定义中看到的，数据分析至少是数据生命周期中产生商业价值的最后阶段，但不是最后阶段。数据字段之间有很大程度的重叠，但在我看来，主要的区别是数据管理更侧重于数据获取和准备，而不是数据分析流程对业务价值提取的响应。

尽管数据管理是任何分析项目的重要组成部分，但只有在核心业务流程中开始实施分析活动后，它才开始对整个组织变得重要。

# 安**数据团队的组织架构和演变**

当许多组织刚刚迈出数据驱动文化的第一步时，他们面临的主要问题是，他们应该将约会团队分成两个专门的团队，还是只有一个团队。

在我遇到的大多数情况下，这高度取决于两个要点:

*   提供业务连续性所需的数据量
*   您的企业客户有多渴

假设第一点非常清楚，但是第二点需要解释。业务需求的数量与公司的数据文化水平相关。这意味着当您的客户缺乏数据素养，不熟悉数据的力量，不了解他们可以如何以及用什么来改进他们的流程时，他们的需求不会有任何大的变化。

我只是强调，数据团队的发展包括与您的整个组织相同的流程部分，而不是一个结论。从一个由全栈分析师组成的小团队开始，他们能够独立创建数据管道、调查数据管道、创建仪表板、发现洞察力并为最终用户翻译。当商业用户在开发时，他们的需求也在增加，你必须拥有先进的技术和对其工作原理有深刻理解的人。在这个阶段，evolution 保持维护，对于一个小团队来说，成为整个企业分析堆栈的专家是非常困难的。出于这个原因，你将不得不对新人敞开团队的大门，并且可能会考虑离婚来分配深度锻炼。