# 你应该知道的数据科学课程中遗漏的 3 个方面

> 原文：<https://towardsdatascience.com/3-areas-missing-from-data-science-courses-you-should-know-55d4209e7db2?source=collection_archive---------36----------------------->

![](img/c480a9e00a659b754deb153fbe31720e.png)

理查德·弗里曼博士

凭借机器学习博士学位和 18 年的应用经验，有抱负的数据科学家问我，他们可以做些什么来提升技能。鉴于我担任导师/顾问、首席技术官以及大数据和机器学习工程、AWS 云计算和自然语言处理(NLP)方面的知识，我希望与更广泛的受众分享我的学习和见解。

我看到的第一件事是，他们只会专注于 ML / NLP / Deep Learning (DL)模型的玩具数据问题的课程或教程，这是一个好的开始。但是这还不够，因为有三个重要的领域是你在数据科学课程或某些大学学位中通常找不到的。原因可能是他们更难教，需要行业经验。在这里，我不是在谈论干净的数据科学教程或研究问题，而是大多数组织都有的典型的现实世界业务数据科学问题。

# 数据准备

你会经常听说数据科学是 21 世纪最性感的工作，但你很少听说数据科学家 80%的时间花在数据准备上，这是很容易被遗忘的一面，因为很难营销和宣传它，但它是一个必须做的重要基础。

什么是数据准备，它可以是刮擦、清理、标准化、连接、填充缺失数据、向量化、旋转、标记等等。数据集。这一点很重要，因为使用 ML 而不是基于规则的算法的全部意义在于，你要基于数据来训练/测试它。没有干净的数据，即使最先进的 DL 模型也无法运行。

一个问题是，那里的数据集通常已经是干净的，并且有一个训练/测试集，所以给人一种错觉，你可以简单地用最少的准备直接应用你的 ML/NLP/DL 模型。在现实世界中，数据非常脏，需要连接、丰富或创建复合要素。

## 你能做什么？

成为用熊猫做数据准备的专家，如果你想规模化就用 pySpark。为什么要把修理的权力和依赖交给别人呢？

如果您也看看数据分析师做什么，他们清理 Excel、SQL 或 ETL 工具中的数据以创建分析仪表板，这是一个类似的任务，但理想情况下是以代码和规模进行。例如，有时您可以使用基于规则的方法或 NLP 来清理姓名、地址或日期。无论您是想为客户做分析报告，还是在数据科学模型中使用 is 培训/测试/验证集，都需要这样做。

> 不要低估 SQL 在您的工具包中的威力，您可以轻松地连接表，而不需要依赖其他人来查询和提取数据。我发现很多时候，使用 SQL 直接查询 Amazon Redshift 比编写一些 Python 代码要快。

# 领域知识

尽管数据科学家的许多技能可以移植到任何行业，但你仍然需要获得行业特定的知识才能有效。

例如，想象一下，你希望有人创建一个预测股票市场价格的数据科学模型，并且你投入一年的工资作为投资，以便模型决定购买/出售/做空哪些股票。现在想象一下，你让一名初级数据科学家做这件事，而他们在投资银行或金融服务方面没有任何经验，在你的年薪面临风险的情况下，你对该模型预测最佳股票的信心有多大？

这就是为什么没有领域知识，你的模型很可能不准确或没有意义。您将如何验证/衡量它？你真的知道你的客户/用户想要什么吗？有时，他们会有基于规则的算法，可以执行得更好，更容易解释，可以作为你在推理中做什么的基线。

> 你还会看到，除非你是一个研究机构，否则企业关注的主要问题是投资回报率(ROI):在我看来，这基本上是为了节省时间、省钱或赚钱。然后将这些映射回您正在进行的基于数据科学的推理。我解释了一些这方面的内容，以及根据我的经验什么时候你应该不使用人工智能而使用它。

技术和数据科学是实现这些投资回报指标的新手段之一。除非你有研究重点，否则大多数公司不会介意你使用最新的深度学习或强化学习，并且会优先考虑预训练或更简单的模型，这些模型可以更快地上市并产生 ROI，特别是当你使用大规模 GPU 服务器和云计算进行训练时，成本可能会很高。

## 我能怎么做呢？

在我看来，你应该**对你工作的领域/领域**充满热情，这将有助于你成为专家。当您选择一个行业时，深入了解领域知识，这适用于 FinTech、IsureTech、AdTech、AgroTech、MedTech、PropTech。查看现有的数据模型、客户需求、术语以及分析/数据科学的应用。

> 我的是医疗保健，因为我认为它对人类有巨大的积极影响，并且用例非常开放，具有挑战性。

获得技能的方法是与领域专家一起工作，阅读大量特定领域的内容，并获得处理特定行业数据的经验。

# 软件工程

现在你已经有了数据准备和领域知识，最后一个支柱是软件工程。

做得好，您可以在 Jupyter 笔记本中的玩具数据上本地执行样本 scikit-learn 和 Keras 代码！这对于洞察、探索性数据分析和演示很有用，但真正的投资回报是当你将你的**模型转移到客户或用户直接使用的管道、产品或服务中**。例如，假设一个用户访问你的网站，你将实时推荐最相关的内容，这将导致更高的用户保留率，更高的点击率或购买量。要正确地做到这一点，你需要像优秀的开发人员一样编写、测试和部署你的代码和模型。您的代码必须具有伸缩性。

> 例如，当我在 JustGiving 领导数据科学团队时，我们有对 2600 万用户进行实时预测的模型，代码作为服务部署在具有超低延迟的高度可用和可扩展的架构上。

当您操作 ML 模型时，有许多元素开始发挥作用，如 API、模型版本、模型准确性监控、特征存储、数据流入/流出等。此外，如果您在追求最小可行产品(MVP ),您很可能会使用预先训练的模型和/或现有的推理 API，这将需要开发技能。

## 我能怎么做呢？

特别是如果你不是计算机科学背景，如果你只直接学过数据科学课程，那么你接触开发或软件工程的机会将是有限的。与优秀的开发人员一起工作，提升自己的开发技能，包括测试、设计模式、Docker、AWS 等云平台和 CI/CD。许多核心技能都与数据和机器学习工程有关——对我来说，这些是紧缺人才，而不是数据科学家。我认为原因是，对于非开发人员或计算机科学背景的人来说，进入门槛会很高。不管怎样，你的代码越好，你就能越快地准备数据或者解决实际的用例。

# 摘要

在我看来，数据科学领域如此受欢迎，因为它似乎向所有人开放，而且很性感，但当你深入挖掘并在现实世界中工作时，你会发现你需要大量的**数据准备技能**、**领域知识**和**软件工程技能**，这些技能经常被遗忘，但却是必需的。致力于这三大支柱将使你成为一名更好的数据科学家，特别是随着领域的成熟，用例变得更加复杂，并且你在团队中工作。要了解更多我的观点，请阅读我的另一篇文章，如[根据我的个人经验对从事数据科学、人工智能和大数据工作的建议](https://medium.com/@rfreeman/recommendations-for-working-in-data-science-ai-and-big-data-based-on-my-personal-experience-8dbc24be368c)。祝你好运，如果你有问题或意见，请给我发消息。