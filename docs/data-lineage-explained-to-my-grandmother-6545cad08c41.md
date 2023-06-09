# 向一个五岁的孩子解释数据血统

> 原文：<https://towardsdatascience.com/data-lineage-explained-to-my-grandmother-6545cad08c41?source=collection_archive---------11----------------------->

## 以及为什么所有的数据团队都在家谱上花费$$$的原因

![](img/5b1ce86ad06a3e613bd1adfddc5a6851.png)

“数据谱系就像数据的家谱”。图片由 [Castor](http://www.castordoc.com) 提供

> *“如果我改变这个字段，我怎么知道我不会破坏下游的任何表？”*
> 
> *“财务仪表板似乎出错了。我可以在哪里查看哪些数据支持它？”*
> 
> *“如果我用另一个优化更好的表替换这个表，我需要用新的数据表更新哪些仪表板？”*

这些问题我都不知道问过自己多少次了。或者当我与数据工程师、分析工程师或数据主管交谈时，我听到过多少次这些话。在大多数公司，如果你问这些问题，人们会回答类似“检查源代码”或“问约翰，他知道”。问题是约翰通常是最好的工程师之一。他如此优秀的原因是他不会把时间花在回答 Slack 上无情的 pings 上。

这就是数据血统发挥作用的时候了。让我向您介绍一下数据血统。我将从解释什么是数据血统开始，然后解释最常见的用例，最后为精通技术的读者进行更深入的技术探讨。‍

重要提示:你在文章中走得越远，它就变得越专业。不要惊讶。

# 什么是数据血统？

数据血统就像一个家谱，但对 data'‍来说

![](img/af8318b4b5d69be035ec5417b01d0a28.png)

辛普森家族树。图片由 Xavier de Boisredon 提供。

‍Data 血统是一种追溯数据资产之间关系的技术。在数据世界中，您首先从各种来源收集原始数据(来自您网站的日志、支付等)，然后通过应用连续的转换来提炼这些数据。为了构建一个数据表(我们称之为“子表”)，您必须使用一个或多个其他数据表(我们称之为“父表”)。数据谱系有助于您重建数据的家族树。如果您有坏数据，您可以在数据系谱树中寻找“坏分支”,并从根本上解决它。‍

# 现实中的数据血统是什么样的？

数据血统可以势不可挡，如果你不知道你在看什么 at‍

数据沿袭的新接口往往更简单，每个可视化处理一个用例，以便业务专家更容易理解。‍Here's 是 Castor 中数据血统的一个例子。

![](img/192507cc97e34ade13a690387a6bd8be.png)

数据表 SUPPORT_METRICS 的数据沿袭。图片来自 [Castor](http://www.castordoc.com) app 经许可。

# 为什么我们需要数据血统？

数据沿袭用例

首先，数据血统与其说是产品，不如说是技术。它是许多数据产品(数据目录、数据质量、数据管理等)背后的底层技术之一。

数据谱系如此流行的原因是有许多新的用例，无论是对于业务、工程、领导还是法律部门。让我试着解释一下最常见的用例。总的来说，数据沿袭有助于获得数据系统的鸟瞰图。

这里列出了所有的用例，我打算解释一下:

*   数据故障排除
*   影响分析
*   发现和信任
*   定义 Propagation‍
*   数据隐私法规(GDPR 和 PII 地图)
*   数据资产清理或技术迁移

‍

## 数据故障排除

“找到问题的根源”

![](img/c6a6512fd5a5020fa35fc562f1323696.png)

端到端数据沿袭对于解决数据问题非常有效。形象灵感来自[彼得·扬达](https://petrjanda.substack.com/p/why-the-data-analyst-role-has-never)

‍Data 用户有时会在仪表盘或数据表中发现奇怪的行为。他们希望进行调查，以了解这是由于数据管道中的技术问题还是需要立即关注的业务问题。所有数据人员的梦想是，当真正出现问题的是数据管道时，避免对业务问题拉响警报(例如，“活跃用户”部分的收入下降)。

在上面的例子中，仪表板中的数据急剧下降。业务用户想知道为什么会发生这种情况。潜在的问题是:“我有业务问题还是数据管道问题？”。他可以检查所有上游数据的状态。在这种情况下，问题来自改变其 API 的数据源(app store)。这一变化打破了数据源的 ETL 工作。在几分钟内，用户就可以了解整个数据系统。

‍

## 影响分析

"我会弄坏首席执行官最喜欢的仪表板吗？"

![](img/28dcedfbfd0d8be526fd56a421c802cb.png)

数据沿袭有助于您可视化变更的影响。图片由 [Xavier de Boisredon](https://www.linkedin.com/in/xavier-de-boisredon/) 提供。

数据用户想要知道他们想要进行的更改对数据流和下游数据资源的影响。在大多数组织中，数据报告和仪表板由数据湖中的数据表提供支持。如果工程师做出改变，这可能会破坏数据管道和流程。因此，组织内的整体数据质量和信任度将大幅下降。

由于这种传承，工程师可以识别所有受影响的资源，并精心编写代码以最大限度地减少负面影响。如果有影响，他们可以识别受影响的数据资源，并向这些资源的活跃用户发送警告。

‍

## 发现和信任

“垃圾进来，垃圾出去。但是我怎么检查什么是进去的呢？”

![](img/5339ef1747b040c02b854a23640753e2.png)

数据沿袭通过了解数据的来源来帮助您信任数据。图片由[泽维尔·德·布瓦雷东](https://www.linkedin.com/in/xavier-de-boisredon/)提供。

用户想要识别、理解和信任他们想要消费的数据资源(表、报告和仪表板)。当用户查看数据资源时，知道它来自哪里有助于信任它。俗话说“垃圾进来，垃圾出去”。了解“活跃用户”控制面板上的数据将为您提供如何阅读这些数据以及是否可以信任这些数据的信息。Lineage 会让您知道它被插入到一个“BI 批准”的表中，具有黄金评级，并帮助您更快地信任它。

‍

## 定义 Propagation‍

“我懒。要是我能写一次文档并传播它就好了”

![](img/fd72731e274701c5e95bca76e7b2340d.png)

通过识别相同的数据点，数据沿袭可以帮助您在整个数据仓库中传播定义。图片由 Xavier de Boisredon 提供。

从治理的角度来看，数据沿袭被证明对于传播元数据非常强大。用户可以轻松地跨数据系统传播定义。

如果一个列在另一个表中使用，而没有进行任何转换，那么可以合理地假设在 99%的情况下定义是相同的。现在，假设您的数据目录连接到列级沿袭元数据，通过只记录源，您可以将定义治理的效率提高 10 倍。如果在数百个表中使用一个流行的列而不进行任何转换，您可以通过单击安全地传播定义和属性。

数据沿袭帮助来自大数据或企业公司的数据治理团队以可扩展的方式部署元数据管理工作。事实上，在一个拥有大数据资源和众多数据库的环境中，理解数据流及其来源是一项挑战。有许多重复的任务。

‍

## 数据隐私法规(GDPR 和 PII 地图)

“我无法保护我不知道自己拥有的东西”

![](img/203299144626b3cea1877c00214c70f7.png)

数据沿袭可以帮助您标记个人信息和跟踪访问权限。图片由 [Xavier de Boisredon](https://www.linkedin.com/in/xavier-de-boisredon/) 提供。

逻辑真的和上面的逻辑差不多。标记个人或敏感信息可能是一件非常痛苦的事情。今天，这是一项耗时的任务。由于沿袭，您可以了解和跟踪访问权限以及依赖性。通常你会意识到，你的角色策略中有一些弱点。您无权访问子表或父表，但可以访问中间表。这可能是正确的，但也可能是危险的，因为您可以重建/追溯敏感数据。

数据沿袭对于改善数据治理、访问权限管理和遵守 GDPR 法规来说非常强大。

‍

## 数据资产清理或技术迁移

“请告诉我！我该保留什么？”

![](img/83d7927dade6002b98a1238685930a8e.png)

数据沿袭有助于识别为最有价值的数据资源提供动力所需的资源。图片由 Xavier de Boisredon 提供。

数据团队有时希望转换技术。例如，一家企业公司从旧的本地 Oracle 数据库迁移到像雪花或 BigQuery 这样的云数据仓库。这些大规模迁移的成本非常高，因为一切都是相互关联的。甚至在开始这样一个项目之前，追溯依赖是一个业务关键的过程。

作为此过程的一部分，您需要确定可以删除的数据资源和要迁移的数据资源。这种鸟瞰图有助于引导建筑思维。‍

# 数据沿袭提供了数据流的鸟瞰图

它有助于追溯跨数据系统的关系

![](img/43389cf3be367a30d0d7f96b6b09ed49.png)

从数据源到 BI 工具的端到端数据沿袭系统。图片由 Xavier de Boisredon 提供。

‍A 几年前，沿袭主要是关于在数据湖或数据仓库中追踪关系。这意味着系统跟踪数据表之间的关系。现在数据血统是跨系统的。

这些表通常支持 BI 工具，如 Looker、Tableau、Mode、Metabase、PowerBI 等。对业务用户和工程师来说，绘制这个流程证明是非常强大的。事实上，业务用户可以轻松地检查数据的来源和流向，而工程师可以检查变化对业务的影响。‍

现在，从数据源(ETL)到业务报告的端到端沿袭是可能的，因为大多数 BI 工具都有 API，并且 BI 工具以标准化的方式在数据仓库上执行 SQL 查询。当数据目录提供商必须为每个新工具、语言和集成构建尽可能多版本的沿袭解析器时，他们现在可以构建沿袭引擎并等待定制最后一英里连接器。‍

# 数据血统何时以及为何变得如此流行？

数据沿袭最近获得了关注。这有几个原因。第一个是企业拥有更多数据，比 10 年前更快。对元数据管理工具的需求越来越大。第二，数据行业用工具和流程来构建自己。这使得云技术和公司的计算血统更加容易和可靠。最后一个原因是各大洲(GDPR、HIPAA 等)出现了苛刻的数据法规，这使得沿袭成为一种必须。

这三种结构性变化是复合趋势。它们将随着时间的推移急剧增长。公司将继续收集更多的数据，并招募更多的人来分析这些数据。数据行业将继续构建自身，并带来标准流程。如今，遵从数据法规对企业公司来说是一个更大的问题，但对中端市场和中小型企业来说很快就会成为问题，因为工具将使评估数据法规变得更容易。

出于所有这些原因，数据血统正在进入这个领域，您可能希望尽早开始投资这样一个工具。‍

# 深入研究数据谱系的技术方面

请注意——仅限数据血统专家。

## 表级血统和列级血统有什么区别？

数据沿袭流可以以不同的格式存在。您可以跟踪数据表或特定表中的列之间的父子关系。事实上，每个列都是用其他表中的其他列创建的，有时甚至是来自同一个表。

列沿袭是表沿袭的子集。如果不同表中的两列之间存在链接，则这两个表之间存在链接。相反的情况并不总是正确的。列沿袭在列级别提供父子关系，而不考虑下面的表。这是一种非常强大的血统，但随着连接数量的增加，很快就会变得非常难以想象。列级沿袭系统也特别难以计算。处理列沿袭的开销更大，耗时更长，并且需要更好的解析算法版本来理解这些变化。

![](img/dd3a430d529917980dd2eac0b8601ba3.png)

列沿袭的示例。图片来自 [Castor](http://www.castordoc.com) app 经许可。

‍ **表级方法**

在下面的 SELECT SQL 语句中，我们正在使用另外两个表 *parent_table_1* (FROM 子句)和 *parent_table_2* (JOIN 子句)构建一个表 *child_table_1* 。这意味着，如果两个“父表”中的一个发生了变化或出现了问题，子表可能会受到变化或错误的影响。‍

![](img/723f053b7f45b8350352e078f0330c97.png)

可以被解析以查找父级和列级沿袭链接的 SQL 查询示例。图片由 [Xavier de Boisredon](https://www.linkedin.com/in/xavier-de-boisredon/) 提供

**列级方法**

在上面的 SELECT SQL 语句中，我们在 *child_table_1* 中构建了三列 *child_1* 、 *child_2* 和 *child_3* 。前两个“子列”与来自 *parent_table_1* 和 *parent_table_2* 的“父列”相同。有直接的血统依赖。

*child_3* 列是*parent _ table _ 1 . parent _ column 1*和*parent _ table _ 1 . parent _ column 1*的和。这里也有血统依赖。‍

# 更现代的数据堆栈分析？

![](img/c706fbedbabeed353f227726521f1fc8.png)

点击此处，了解更多关于现代数据堆栈[的性能指标评测和分析。](https://notion.castordoc.com/)

我们写了利用数据资产时涉及的所有过程:从现代数据堆栈到数据团队的组成，再到数据治理。我们的博客涵盖了从数据中创造有形价值的技术和非技术方面。

如果您是一名数据领导者，并希望更深入地讨论这些主题，请加入我们为此创建的[社区](https://notion.castordoc.com/unsupervised-leaders)！

*最初发表于*[T5【https://www.castordoc.com】](https://www.castordoc.com/blog/what-is-data-lineage)*。*