# 谁说单片应用已经死了？

> 原文：<https://towardsdatascience.com/who-said-that-monolithic-applications-are-dead-2a4b9e3ac56d?source=collection_archive---------29----------------------->

## 整体服务与微服务:没有放之四海而皆准的方法

![](img/c43eab4ee2a9ee866cb34733ef20de85.png)

图片来自 [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=1590047)

就软件设计而言，微服务和单片应用是设计、构建和部署软件的两种截然不同的方法。那么，微服务和单片应用有什么区别呢？

首先，微服务是业务逻辑的小部分，旨在彼此独立地开发、部署和扩展。相比之下，整体式应用程序被设计为作为一个整体来开发、部署和扩展。

然而，不同的组织有不同的资源，并且没有一个放之四海而皆准的方法来构建一个成功的产品。开发人员花费大量时间和精力来设计、构建和部署应用程序，结果却发现代码库不可维护、伸缩性不好，或者团队没有足够的资源或知识来维持项目，这种情况很常见。

因此，从一开始就确定项目结构和理解权衡是很重要的。本文将解释每种方法的优缺点，并帮助您决定哪种方法适合您。

> [学习率](https://www.dimpo.me/newsletter?utm_source=medium&utm_medium=article&utm_campaign=cloud_native)是我每周给那些对 AI 和 MLOps 世界好奇的人发的简讯。你会在每周五收到我关于最新人工智能新闻、研究、回购和书籍的更新和想法。订阅[这里](https://www.dimpo.me/newsletter?utm_source=medium&utm_medium=article&utm_campaign=cloud_native)！

# 设计考虑

设计应用程序时，通过列出所有的功能和业务需求来设置环境是很重要的。在一张纸上写下申请的范围将有助于你确定实现目标所需的资源。这个阶段奠定了基础，我们都知道如果你在一个错误的基础上开始构建会发生什么。

因此，第一步是描述应用程序将交付给用户的服务。考虑所有的功能需求，把自己想象成客户。然后，你应该列出所有可以帮助你完成项目的资源。

为什么要破解这个练习？简单的回答是，它将帮助您确定您应该遵循的架构模型；这将使在单片和基于微服务的架构之间进行选择变得更加容易。

## 收集功能需求

最初，收集和理解项目的业务需求是非常重要的。一种简单的方法是提供以下问题的答案:

*   你的应用程序的最终用户是谁？
*   你的产品将提供什么服务？
*   应用程序的输入和输出是什么？
*   输入和输出的格式是什么？

## 列举可用的资源

确定了业务和功能需求之后，下一步是列出所有可以帮助我们完成这个项目的资源。同样，让我们做同样的练习，并回答一系列重要问题:

*   我们可以支配的工程资源有哪些？开发人员使用什么工具，哪种编程语言是他们工作中的常用语言？
*   你愿意花多少钱来实现它？换句话说，预算是多少？
*   截止日期是什么时候？你有时间吗，或者有到达市场的紧迫性吗？

# 单片与微服务

既然您已经收集并列出了应用程序的所有业务需求以及实现这些需求的可用资源，那么是时候决定最合适的应用程序架构了。

没有两个系统是完全相同的。然而，在大多数情况下，您可以在基于单片的架构或基于微服务的架构之间进行选择。无论您采用哪种系统，主要目标都是设计一个能够为客户提供价值并且易于维护和扩展的应用程序。

每个体系结构分为 3 个主要层:

*   UI(用户界面):UI 通常响应 HTTP 请求并提供图形界面，这有助于用户体验
*   业务逻辑:业务逻辑层包含控制一切并向用户提供服务的代码
*   数据层:数据层提供对应用程序所需信息的访问，并存储应用程序的状态

## 巨石

在整体架构中，我们之前看到的应用层是同一个单元的一部分。它们在一个存储库中管理，共享所有资源，并且用一种编程语言开发。最后，它们被打包并作为一个二进制文件分发。

## 微服务

在微服务架构中，应用层是独立管理的。通常，每个单元都保存在一个单独的存储库中。它在运行时消耗自己的资源，有一个定义良好的 API 用于与其他微服务建立通信，它的实现栈独立于其余部分。最后，它作为一个单独的单元发布，通常作为一个容器化的服务。

# 在微服务和单芯片之间选择

我们如何在这些方法中做出选择？毕竟，微服务是新的趋势，如果我们选择这种方式，似乎我们总是会赢？还记得我们在*“设计考虑”*部分做的练习吗？让我们来测试一下。

那么，你什么时候会选择建造一个整体呢？假设您有严格的预算，并且您的工程团队由几个熟悉特定框架(例如 Java Spring 框架)的开发人员组成。此外，时间紧迫，你必须在一个紧张的期限内建立一些东西。

在这种情况下，我认为开发一个单一的、集成的系统是你最好的选择。单一应用程序具有较低的启动成本，较低的开发复杂性(一种编程语言，一个存储库)，以及更快的上市时间(一个部署整个堆栈的交付管道)。

然而，基于微服务的架构的优势是如此巨大，随着时间的推移和业务的增长，您应该制定一个计划，将您的代码库迁移到河的对岸。这种转变的好处是更大的可伸缩性、更低的规模运营成本、更高的可靠性和更高效的软件开发过程。

# 结论

自从引入 web 应用程序以来，微服务范式慢慢地在其他组织中获得了牵引力。微服务是业务逻辑的小部分，旨在彼此独立地开发、部署和扩展。相比之下，整体式应用程序被设计为作为一个整体来开发、部署和扩展。

然而，没有放之四海而皆准的方法，单一的应用程序设计肯定不会消亡。你必须做好功课，决定什么最适合你所在的职位，然后开始建设！

# 关于作者

我叫[迪米特里斯·波罗普洛斯](https://www.dimpo.me/?utm_source=medium&utm_medium=article&utm_campaign=monoliths_microservices)，我是一名为[阿里克托](https://www.arrikto.com/)工作的机器学习工程师。我曾为欧洲委员会、欧盟统计局、国际货币基金组织、欧洲央行、经合组织和宜家等主要客户设计和实施过人工智能和软件解决方案。

如果你有兴趣阅读更多关于机器学习、深度学习、数据科学和数据运算的帖子，请在 Twitter 上关注我的 [Medium](https://towardsdatascience.com/medium.com/@dpoulopoulos/follow) 、 [LinkedIn](https://www.linkedin.com/in/dpoulopoulos/) 或 [@james2pl](https://twitter.com/james2pl) 。

所表达的观点仅代表我个人，并不代表我的雇主的观点或意见。