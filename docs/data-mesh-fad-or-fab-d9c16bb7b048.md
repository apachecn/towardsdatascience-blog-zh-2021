# 数据网格——时尚还是流行？

> 原文：<https://towardsdatascience.com/data-mesh-fad-or-fab-d9c16bb7b048?source=collection_archive---------19----------------------->

## 爱它或恨它——它就在这里。因此，我们向其中一位专家请教了一些关于数据领域最热门话题的难题。

![](img/f97475076c6598f645fe50dbcf826aaa.png)

图片由[参孙](https://unsplash.com/@samsonyyc)在 [Unsplash](http://www.unsplash.com) 上提供。

在过去的一年里， [**数据网格**](https://martinfowler.com/articles/data-monolith-to-mesh.html) 席卷了数据社区。有些[人喜欢它](https://www.youtube.com/watch?v=31BTUYaVSqw)，有些[人不太理解它](https://www.montecarlodata.com/decoding-the-data-mesh/)，许多人已经[向一个](https://medium.com/yotpoengineering/our-journey-towards-an-open-data-platform-8cfac98ef9f5?source=rss----afbe60b11b62---4)迁移，即使他们还不知道。不管你在哪里跌倒，都很难忽视这种嗡嗡声。

对于那些不熟悉的人来说，[数据网格](/what-is-a-data-mesh-and-how-not-to-mesh-it-up-210710bb41e0)是一个文化和技术概念，它将数据所有权分布在产品领域团队中，具有集中的数据基础设施和分散的数据产品。随着分析变得越来越分散，以满足现代洞察力驱动的组织的需求，这种范式变得越来越普遍。虽然我不能代表这个概念的创造者 Zhamak Dehghani，但我发现 data mesh 特别引人注目，因为它雄心勃勃地描绘了当数据工程团队[不是分析的瓶颈](https://maximebeauchemin.medium.com/the-downfall-of-the-data-engineer-5bfb701e5d6b)时，数据民主化和自助工具可以实现什么，因为它们经常是这样。

> 自从 Zhamak 的文章第一次发表，以及我写了第一篇关于这个主题的文章之后，客户问我他们应该如何实现数据网格架构。很明显，水里有东西。

在过去的几个月里，经过数百次交谈，我发现了关于数据网的四件事:

1.  像任何组织转变一样，数据网格需要自上而下的支持才能成功。
2.  数据网格是由多种技术组成的，作为现代数据平台的一部分，这些技术层层叠加，您无法仅使用计算、存储和 BI 工具来构建数据网格。
3.  对于大多数数据领导者来说，结果(而不是过程)才是最重要的。数据网格作为一个概念仍处于萌芽状态，只要数据网格的基本原则保持不变，就没有正确或错误的“构建”方法。结果呢？大规模的数据民主化。
4.  数据网格反映了数据分析去中心化的更大趋势——这让我无比兴奋。

也许没有人像马马德·扎德那样对数据网格充满热情，他是 T2 Intuit T3 数据平台团队的前工程副总裁。Mammad 于 2000 年加入雅虎，担任高级架构师和开发人员，开始涉足数据基础设施领域。在[雅虎](https://www.yahoo.com/)的时候，他建立了一个分布式云商店和一个完整的端到端分布式监控框架。2009 年，他加入网飞，在云中建立他们新的身份和会员平台。2012 年，他加入 LinkedIn，担任分布式数据系统的负责人，帮助塑造所有实时数据基础设施需求的愿景。在因纽特工作期间，Mammad 负责领导[公司数据平台](https://medium.com/intuit-engineering/the-intuit-data-journey-d50e644ed279)背后的团队，在那里他们实现了 Intuit 数据基础设施的现代化，并开始实施其[数据网格](https://medium.com/intuit-engineering/tagged/data-mesh)战略。

**但是什么是数据网格，我们为什么要关心它？**

我最近和 Mammad 坐下来聊了聊数据网格。以下是 Mammad 对此感到兴奋的五个原因——他认为你也应该如此。

# 数据网格上的玛马德·扎德

## 数据网格分散了责任——这是一件好事

作为一个多年来一直与数据打交道并处理扩展数据解决方案的方法的人，我很清楚，当围绕数据的所有责任都由一个中央数据团队承担时，您能做的事情就只有这么多了。当需要专业技能和专业知识时，我们通常喜欢将新的复杂问题隔离到一个中心团队。这往往在垂直领域内工作得很好，在早期，数据分析有点像这样。但今天，数据分析、机器学习和获取优质数据是我们所做一切的核心，并以指数速度增长。我们需要一种新的组织方式，以及一种新的思考架构和基础设施的方式，以满足组织内数据生产者和消费者的需求。这意味着重组中央数据团队，并在工程领域中分配数据责任。

> 我认为，在某些方面，我们可以看到与移动技术之旅的相似之处。十年前，常见的是一个中央“移动团队”，所有的移动应用程序开发都将在这里进行。

然而今天，移动开发是每个产品开发团队不可或缺的一部分。这种将责任从专门的中心团队“转移”到领域开发团队的情况也可以在运营和质量工程中看到。

这是一件好事，因为它帮助我们更好地扩展，更重要的是，它将责任放到了正确的位置；产生数据的地方。领域团队是他们自己数据的专家，他们有责任确保高质量的数据能够提供给这些数据的消费者，通常是分析师和数据科学家。作为中央数据团队的一员，我们应该确保数据生产者和消费者都可以使用正确的自助式基础设施和工具，以便他们能够轻松完成工作。给他们配备合适的工具，让他们直接互动，不碍事。

这一切都很好，但我们还没有完全实现。到目前为止，工程领导者一直不愿意改变他们围绕数据、数据工程和数据科学的传统组织结构。部分原因是这仍然是一个相对较新的概念，成功的故事并不多。另一个主要问题是，我们还远远没有达到将这一责任推给领域团队所需的自助式、易于使用的基础架构即服务的水平。

Data mesh 正试图正面解决这些问题，这给了我很大的希望。数据网格的主要原则是域所有权、数据作为产品、自助式数据平台和联合治理，所有这些对于帮助我们在未来十年扩展数据分析和机器学习都是绝对必要的。

## 数据网格让数据成为一等公民

分散化的结果是数据成为开发团队的一等公民。数据网格引入了“数据产品”的概念，像产品的其他功能一样，它由领域工程团队拥有和操作。网格上的节点是这些分散的数据产品。

重要的是要记住，大多数组织仍然处于制定数据网格策略和数据产品的早期阶段。当我们重新思考我们的数据分析方法时，我们不可避免地需要重温一些妨碍我们的旧习惯。例如，从事务性数据库的内部收集分析数据是一条捷径，但却引入了很多复杂性。正如我之前所说的，工具也不太到位，这意味着开发和操作这些数据产品仍然需要专业技能。

> 随着时间的推移，两件事将会改变:1)新加入工作队伍的工程师将会更加熟悉数据技术，2)数据基础设施本身将会变得更好、更容易使用，并且完全自助。在这种情况下，拥有和运营一个数据产品类似于拥有和运营一个功能性的微服务。

需要明确的是，当我谈到将数据的责任交给领域团队时，我并不是说要指定一个单一的联系点，让领域中的一个人了解他们数据的一切。我说的是数据的极端所有权和完全责任，以确保他们的数据是相关的、可消费的、可访问的和可信的。换句话说，将数据视为一种产品。如果没有发生这种情况，网格就不能起飞。

## 数据网格将改善体验的责任推给了供应商

很多人都在问，数据网格是否只适合那些数据的复杂性和规模是个大问题的大型组织。我认为遵循数据网格的原则是好的架构，并且将是正确的事情，无论你是一个小的创业公司还是一个在一个巨大的数据湖中拥有大量遗留数据的大公司。

话虽如此，一旦您更深入地研究了网格的设计和实现，您会注意到工具的当前状态在很大程度上假设了一个中心数据块，并且没有很好地与标准开发实践集成，这使得现有的产品开发人员很难构建和操作他们的数据产品。对于数据平台提供商来说，这是一个围绕这种新体验重新思考其产品的机会。工程领导者可以在推动供应商优先考虑这一点方面发挥重要作用。

> 我还希望我们能在基础设施层面上看到更多的开放标准，以鼓励供应商远离他们封闭的花园，构建能够与其他供应商的其他组件进行互操作的工具。我认为拥有这种可互操作的解决方案市场对我们的行业至关重要。

在我看来，这种同类最佳的方法将允许工程领导者以最适合他们的方式设计和组合他们的基础架构，而不是局限于一家供应商。随着时间的推移，基础设施将变得更加智能，允许多面手开发人员自主轻松地构建和操作他们的数据产品。谁知道呢，也许在某些时候我们不会区分功能微服务和数据微服务(即数据产品)！

## 数据网格优先考虑整个组织的数据治理

作为其主要原则之一，数据网格提出了对联合治理设计的需求。这允许每个域为组织范围的数据策略实现适当的解决方案，以确保数据的可用性、质量、可信度和合规性。

你和你在蒙特卡洛的团队正在解决这个框架的一个关键组成部分，因为[数据可观察性](https://www.montecarlodata.com/what-is-data-observability/)在确保整个网格的[数据质量](https://www.montecarlodata.com/the-new-rules-of-data-quality/)中起着基础作用。我认为可观察性需要做好几件事:

*   它应该能够检测到网格中出现的任何异常
*   它应该是智能的、自动化的、有弹性的、非常可靠的
*   并且它应该有实时开放的 API 来以编程方式与之交互

尽管这听起来很简单，但这些问题很难解决。有一点我怎么强调都不为过，那就是对开放实时界面的需求。作为一名从业者，我希望能够消费由可观察性层生成的事件，并在检测到异常时立即构建自动化、自我恢复和通知。拥有强大的开放 API 允许工程师以前所未有的方式将东西缝合在一起，并在问题出现时解决问题，而不是等待供应商来填补空白。

## 数据网格使数据更接近产品工程

不考虑数据网格，数据和机器学习将成为每个人工作的一部分；它将成为产品工程团队的 DNA。这种转变正在顺利进行，非常令人兴奋，但同时也令人不安。

一方面，在未来十年，我们将看到由数据推动的指数级技术进步。另一方面，我们还不知道消费者会如何使用这些数据。这就是为什么我们需要确保我们有正确的范式，可以给我们规模和灵活性来改变。Data mesh 正试图解决这个问题。

数据网格将数据与产品开发作为一个整体更加一致，而不是作为一个专门的孤立的活动。过去，您拥有“独一无二”的数据库，它归应用工程师所有。分析师将不得不乞求和借用时间来运行他们的查询，通常是在下班后，因为这不是一个优先事项，它更多地被视为后台活动。随着数据重要性的增长，我们将自己划分为事务和分析领域，创建了集中式数据团队，并将所有的复杂性和责任委托给他们。虽然它在一段时间内有效，但我们现在正处于这种模式无法进一步扩展的阶段。这就是为什么我对数据网格的前景感到兴奋。

**对数据网格好奇？**

*联系* [***马马德·扎德***](https://www.linkedin.com/in/mammadz) *和* [***巴尔·摩西***](https://www.linkedin.com/in/barrmoses) *或* [***蒙特卡洛团队的其他成员***](https://www.montecarlodata.com/) *，了解像 Intuit 这样的公司如何以可观察性为目标大规模实施数据网格架构。*

*报名参加 Zhamak Dehghani 在* [***IMPACT:今年 11 月的数据可观察性峰会***](https://events.montecarlodata.com/impact-data-summit-2021?utm_source=blog&utm_medium=kolibri+data+mesh&utm_id=impact) *了解更多关于数据网格的信息！*