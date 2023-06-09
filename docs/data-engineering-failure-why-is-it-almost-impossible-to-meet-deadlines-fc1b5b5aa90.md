# 数据工程失败—为什么几乎不可能在截止日期前完成？

> 原文：<https://towardsdatascience.com/data-engineering-failure-why-is-it-almost-impossible-to-meet-deadlines-fc1b5b5aa90?source=collection_archive---------16----------------------->

## [思想和理论](https://towardsdatascience.com/tagged/thoughts-and-theory)

## “我喜欢截止日期。我喜欢它们经过时发出的嗖嗖声。”

![](img/d04a088713be0bcf2a25f5ae53cbbd13.png)

工程是一门艺术(鸣谢:我)。

失败。我想写关于失败的东西。为什么数据工程师很难评估项目的持续时间，也很难满足截止日期？

在我过去 7 年的工作经历中，我有机会与多个数据工程团队合作。我注意到一个项目接一个项目的一个常见模式是，工程师很难定义和满足里程碑。

为了创建路线图和里程碑，我们一个团队接一个团队尝试了所有流行的方法。从 Scrum 跳到 Lean，尝试使用扑克计划或同行评估来确定任务的大小。这并没有阻止我们失败。但是，这很正常。

在这篇文章中，我将分享我们作为数据工程师失败的 3 个主要原因，并提出解决方案，以开启与社区的讨论。

# 数据工程师不擅长区分优先级

我们不擅长优先排序，这意味着大量的中断和不切实际的时间表。你说打扰？是的，数据工程深受上下文切换之苦。我们每天经常在不同的任务间穿梭。

这里是夸张的(是真的吗？)数据工程师的日常计划:

*   早上——修复夜间破裂的管道
*   noon —回答#data-public 上关于仓库列的公共松弛问题
*   下午——帮助一位分析师解决一个你在早上喝咖啡休息时聊到的棘手问题
*   下班后——你开始你的日常工作

因为数据工程师在历史上被视为一个支持团队，他们需要(或者他们想要)尽可能快地回答问题，这显然与项目期限相冲突。很难拒绝。我知道。但是为了保持你的心理健康，你需要学习。

另一方面，我们也有太多反复出现的管道问题。编写无错误的管道是一项艰巨的任务。但是为什么呢？因为我们经常处于数据提供者和消费者之间(参见数据网格)，面对太多的移动部分。我们将数据从数据库转移到存储或第三方平台。数据库模式、存储、第三方 API 或业务需求可能会发生变化。然后产生新的问题。

但是，我们不要只责怪其他团队，我们有时也会因为没有足够的时间或因为我们只是拙劣地建造蹩脚的管道。很难区分计划好的项目、计划外的项目和日常的 bugs &问题。

**解决方案**

为了解决这个优先化的问题，我给你提供了 4 条探索的途径。你会看到前三个是组织性的，最后一个更多的是关于消除技术债务以避免每天支付。

1 —开始成为产品团队的旅程。让人们明白你和他们一起开发工具，而不仅仅是提供服务。然后，开一个产品管理岗位，才能开始像考虑产品一样考虑数据。这颗子弹是目前数据网格及其周围一切的行业大趋势。警告:不要雇佣项目经理来管理积压的任务。

2 —如果你管理一个数据团队，创造一个信任的氛围，让工程师在必要时说不。**当来自高层的压力很大时，说不并不是一件容易的事。**

3-创建图腾持有者角色。团队中应该有人每周负责回答所有可能的外部干扰。创建每周轮换和角色很容易，但不要忘记检查角色是否真的有效。这会减少干扰吗？如果没有，找到原因并改进。

3 —将[软件工程最佳实践应用到您的管道](https://maximebeauchemin.medium.com/functional-data-engineering-a-modern-paradigm-for-batch-data-processing-2327ec32c42a)或应用程序开发中。像幂等性、可再现性、读/写模式等概念。是必须做的。当你开发一个管道时，它很可能有一天会失败。所以，为了未来，让调试和重启变得容易些。并且记住:*造复杂是简单，造简单是复杂。*

![](img/887c2a03264c025df6ce0296ee9cee05.png)

每天都有新的十字路口

# 数据工程项目在另一个时间表上

与其他数据任务相比，数据工程任务很少是小任务。您可能已经遇到过这种情况，分析师要求用一个表来回答一个业务问题，而当您添加该表时，分析师已经找到了获取数据的解决方案。

前一种情况说明了人们所处的不同时间表数据，也描述了同步它们的复杂性。

*   数据分析师每天都有时间表，因为他们主要回答问题(业务或直觉)。
*   数据科学家每周都有时间表，由于特征工程，他们将问题转化为模型。
*   数据工程师按月安排工作，他们构建平台以支持过去、当前和未来的使用案例和增长。

我们按月工作的主要原因是，到今天为止，工具仍然很难操作(你还记得 Hadoop 吗？)，对于同一项任务，我们有太多的工具和可行的解决方案，而不考虑这样一个事实，即每次我们在做一些事情时，都会发现一些计划外的东西。

如果我们增加工具的复杂性，数据平台得到的低质量输入。它带来了很多边缘案例:*正常案例正在成为边缘案例，不良输入成为常态。*说实话，许多数据平台尚未涵盖数据质量路径，数据工程师每天仍面临边缘情况。

工具复杂性和输入质量之间的这种混合会给我们工作的每个任务带来延迟。我们终于明白为什么我们需要这么长时间才能前进。

![](img/2bede10f0bd40f397a8c881fc13ec6f2.png)

一名数据工程师因为洪水而推迟了他的项目

**解决方案**

1 —循序渐进。第一次评估项目？不要试图确定一年项目的规模。将它分割成 3 周或 3 个月的小项目，并创建小的可理解的任务。第一次你会错，但是经过几次尝试后，你肯定会变得更好。*不练习，成不了大师*。

2 —我们都在同一条船上。在数据团队中，我们的北极星应该是为同事提供数据。让我们成为队友，理解彼此的限制。工程师在这里为公司创造最好的平台，分析师和科学家在这里创造数据的可见性、用途和界面。

3-关注技术创新，拥抱它们。许多新产品(Airbyte、Meltano、Singer 等)都加入了云数据存储(BigQuery、Snowflake、Databricks)。他们旨在简化数据工程的复杂性。使用它们。更重要的是:*让它们适应您的堆栈。*

# 数据工程学科仍然年轻

这一学科如此年轻的事实突出了前面两点。每一个选择或小错误都可能很容易导致技术债务。

这个行业错了好几年，随着数据科学的大肆宣传，许多公司雇佣了数据科学家，让他们做数据工程工作。**这导致了两个主要问题:我们有沮丧的数据科学家和糟糕的工程平台。**

不要误解我的意思，我认为数据科学家可以建立很好的平台，但是当你在做一项你不应该做的工作时，结果可能是欺骗性的。

数据工程团队通常被整合到“传统的”产品团队中，但是因为这个学科是新的，所以其他团队无法弄清楚数据工程师的能力。这是一个问题。有时，数据工程师可以带来更适合的解决方案，以避免不必要的工作。

我们也缺乏数据产品经理或者对数据平台有了解的产品经理。经常发生的情况是，产品经理在他们的范围界定中完全忘记了数据生态系统，后来给数据团队增加了计划外的工作。

此外，由于他年轻的数据工程技能相当广泛，除了大公司有足够的资源专门团队，小公司需要雇用 5 条腿的绵羊数据工程师。数据工程师被要求从 DevOps 技术跳到生产级代码编写，然后再跳到 SQL 调试。

![](img/5d0b8e354bb4848760c3c5df31c99108.png)

一名数据工程师正在阅读“数据工程杂志”([鸣谢](https://unsplash.com/photos/0qmXPnZKeLU))

没有多少工程师有构建数据平台的丰富经验。对于一个新项目的团队来说，如果团队中没有人做过，那么很难评估这个项目会持续多久。如果我们再加上每两年变化一次的工具和趋势，我们如何才能更好地进行评估呢？

**解决方案**

1 —寻求帮助。你可能没有机会在你的团队中有一个前辈，但我认为如果你要求的话，会有人愿意帮助或挑战你。例如，询问其他规模相同或市场相同的公司，要有创意。我过去做过，我遇到了很棒的人。

通过在公共会议和/或聚会上展示来挑战你的选择和愿景。从这里你会得到问题和反馈，这将有助于你评价你的平台。

2——阅读别人写的东西，获得灵感。但不要忘记，你可能不是网飞、优步或 Airbnb。您可能不需要创建新的开源数据库技术来计算您的度量。

3 —雇佣拥有不同技能的团队。如果适合您的使用情形，最好雇用 2 名多面手和 2 名专业人员(例如开发操作系统和流)，而不是 4 名多面手。但是要小心，过早地专门化你的团队也会产生问题。你不希望只有一个人负责流媒体。否则假期对他来说会很难熬。

# 结论

如果你是数据工程师，请善待自己。成为一名伟大的数据工程师需要时间。如果这是你第一次独自创建一个平台，挣扎是正常的。

如果你和数据工程师一起工作，请善待他们。在他们的日常职业生活中，工程师喜欢看到人们使用他们制造的工具。

但是不要忘记给你的项目设定(具有挑战性的)截止日期。只有这样，你才会进步，并开始与同事建立信任。还要记住，每个解决方案都有自己的文章，我们有许多可操作的杠杆来改善这种情况。

这篇文章也可以更普遍地应用于软件工程。数据工程真的如此讲究，有特定的需求吗？**难道我们不应该把数据工程师当成另一个工程团队吗？**

*特别感谢 Augustin、Charlotte、Emmanuel 和 Pierre 的评论。*

*副标题由道格拉斯·亚当斯引用。*

*这篇文章最初发表在* [*blef.fr*](https://www.blef.fr/data-engineering-failure-why-is-it-almost-impossible-to-meet-deadlines/) *上，我在那里发表了一份关于数据的每周策划简讯。工程、筹款、分析、组织一切都是。*