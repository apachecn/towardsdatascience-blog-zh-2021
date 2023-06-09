# 数据集成的未来

> 原文：<https://towardsdatascience.com/the-future-of-data-integration-7694ebacfe92?source=collection_archive---------19----------------------->

## 云计算、Python 堆栈、数据仓库和 SaaS 平台的发展将如何改变数据集成的面貌。

云计算、大数据、机器学习、数据湖、数据仓库——毫无疑问，如果你一直关注科技世界，你一定听过这些时髦词汇。这些趋势和由此产生的技术已经改变了世界，并继续挖掘新的创新机会。

如果你看看 15 年前 Talend(现在是该领域的巨头)推出 Talend Open Studio 时数据集成的面貌，脑海中出现的词汇是“拖放”界面、基于 SQL、内部部署和 Windows 原生。从那以后，事情发生了巨大的变化。

> “我们已经观察到行业向云技术的过渡，以及内部大数据应用采用的减少……我们未来的成功取决于此类市场的增长和扩张，以及我们适应和有效应对[it]的能力。”— [塔伦德](https://investor.talend.com/sec-filings/sec-filing/10-q/0001668105-20-000072)，2020 年

![](img/fa2e0c712b112de29f7c3e605e96b3fc.png)

来源: [unDraw](https://undraw.co/)

# 新时代

破坏 Talend 和 Informatica 等公司遗留集成解决方案的工具非常不同。首先，它们是基于云的而不是本地的，是 web 应用而不是桌面软件，受益于强大的转换工具，如 [dbt](https://www.getdbt.com/) ，并利用数据仓库和数据湖的容量，如 [Snowflake](https://www.snowflake.com/) 来整合比以往更多的数据。

这些新工具如此吸引人的原因很大程度上是因为数据变得越来越分散。帮助企业管理线索、销售、发票、账单、广告、投资、用户分析等的新 SaaS 平台正在快速发展。现代业务分析师的任务是有效整合这些数据，并得出影响业务决策的有用见解，而这些工具正是如此。

# 简要概述

为了让您了解一些背景知识，我们来讨论一下数据集成领域的一些现代参与者。

![](img/7bd43673e90e1a03ad65b09d7ecd83c6.png)

来源: [unDraw](https://undraw.co/illustrations)

## StitchData

[StitchData](https://www.stitchdata.com/) 创建了一个平台，专注于将数据从这些 SaaS 平台转移到数据仓库。该公司最终在 2018 年被 Talend 收购，这是 Talend 渗透新的基于云的市场的更大努力的一部分。

Stitch 的天才吸引了分析师和开发者。他们开始了一项名为[歌手](https://www.singer.io/)的开源计划，该计划引入了在 Python 中构建 **taps** (不同平台的连接器，如 CRMs、ERP 等)和 **targets** 的标准规范。近年来，Python 堆栈因其与机器学习和数据清理(例如，Pandas、PySpark、Dask 和 [more](/python-data-transformation-tools-for-etl-2cb20d76fcd0) 等包)一起使用而闻名，因此为获取数据而设计的 tap 使用相同的堆栈并吸引相同的开发人员是有道理的。

这个想法是，每个人都可以从所有这些平台的良好维护中受益。毕竟，当 API 和模式发生变化时，哪个组织愿意投入人力来维护数百个这样的 tap 呢？

对于他们的企业产品，Stitch 提供了一个很好的 web 界面和 API，使业务分析师和开发人员能够通过 Stitch 的基础设施利用这些 tap。

## Fivetran 和 Xplenty

像 [Fivetran](https://fivetran.com/) 和 [Xplenty](https://www.xplenty.com/) 这样的工具采取了一种稍微不同的方法，并专注于业务分析师市场。这两个平台都拥有数百个由他们的团队维护的预构建的专有连接器、一个健壮的转换层和高度可伸缩的基础设施，以便将数据从这些连接器同步到您的数据仓库。

这些平台吸引了需要整合数据和获得洞察力的技术业务分析师。Fivetran 强调预先规范化的数据，并通过 dbt 提供基于 SQL 的仓库内转换。虽然 Xplenty 提供了一个基于 UI 的转换系统，让人想起了 Talend Data Studio，但是具有云计算可能带来的可伸缩性。

## 梅尔塔诺

不幸的是，在 Talend 收购 Stitch 之后，Singer 项目失去了方向，许多 tap 不再维护。幸运的是， [GitLab 资助了](https://about.gitlab.com/blog/2020/05/18/why-gitlab-is-building-meltano-an-open-source-platform-for-elt-pipelines/)[Meltano](https://meltano.com/)开源项目，该项目旨在继续辛格的工作。该项目旨在为分析师提供他们自己托管、创建和运行数据集成管道所必需的工具。他们同意 Singer 的最初使命，并且[正在开发 SDK](https://gitlab.com/meltano/singer-sdk)以使创作高质量的歌手抽头更容易。

与 Stitch 不同，他们希望完全实现分散的开源维护 taps 的想法，每个组织都可以利用它并为之做出贡献。他们的目标是在 Meltano 员工之外找到开源维护者，这些人使用他们的 Singer taps，并有动机维护它们。他们已经有了几家咨询公司和开发商，他们已经开始让这些水龙头为整个社区服务。

## 空气字节

Airbyte 正在构建另一个快速增长的开源平台，以解决数据集成中的问题。与 Meltano 非常相似，他们的目标是将数据集成商品化，并为 Fivetran 等工具提供一个自托管的替代方案。该公司专注于扩展他们的开源平台和社区，并致力于成为市场的新标准。

# 一个不同的视角:SaaS 平台怎么样？

有趣的是，这些业务分析师在试图整合来自所有 CRM、ERP 和计费平台的业务数据时面临的问题，也是这些 SaaS 平台背后的开发人员所面临的问题。

![](img/7501085a6ffc9f8778b766c839c9d7f1.png)

来源: [unDraw](https://undraw.co/)

事实上，这些 SaaS 平台已经开始通过它们支持的集成将自己的产品与竞争对手区分开来。例如，支持直接从 Quickbooks 导入发票的会计报告平台比需要手动将发票上传为 CSV 文件的平台更有可能赢得客户。

坚持住！我们刚刚讨论了所有这些不同的工具，这些工具帮助分析师利用所有这些新奇的新技术趋势为他们的数据创建管道。这些难道不能帮助这些开发者吗？

在某种程度上，是的。事实上，像 Stitch 和 [Airbyte](https://airbyte.io/) 这样的产品背后的 API 是作为解决方案提供给这些开发者的。问题是开发人员通常比分析人员需要更多的对集成的控制，所以他们通常会自己构建和维护这些集成管道。

对我们来说，这似乎是对已经在帮助业务分析师的所有新基础设施和工具的浪费。为什么不利用同样的软件来帮助这些开发人员呢？这就是我们开始 [hotglue](https://hotglue.xyz) 的原因——这是一个轻量级工具，专注于帮助开发人员为他们的 SaaS 平台构建集成，利用这些新趋势。

# 结论

数据集成空间是巨大的。整合您的业务数据有许多不同的原因，还有更多工具可以帮助您做到这一点。不过有一点是明确的——最好的工具正在利用最新的数据工程趋势，并吸引越来越多的技术受众。

数据集成的未来似乎是一个有更多利基参与者的市场，并重新依赖开源社区来扩展所有新的 SaaS 平台和用例。

感谢阅读！欢迎在下面留下评论或问题。