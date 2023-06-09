# 构建伟大数据文化的 6 个基本步骤

> 原文：<https://towardsdatascience.com/6-essential-steps-to-building-a-great-data-culture-e529d4dcad7e?source=collection_archive---------13----------------------->

![](img/d386a12690ea363c7e4b1b25eeb0996a.png)

卢克·切瑟在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

## 因此，像“我们去年的收入是多少”这样的问题不再被当作“数据请求”来提出

在我担任数据科学顾问的这些年里，我与数据能力各不相同的客户共事过。在此期间，我得出了一个关键的观察结果:成功利用大数据时代的公司在整个组织中建立并维护良好的数据文化，而不仅仅是在他们的“数据组”中。

那些只投入资金和精力雇佣优秀数据人才，而不注意在组织的其他部门建立数据文化的公司，通常很难留住这些优秀的数据人才。他们最终会精疲力尽，因为他们大部分时间都在充当“数据 Siri”:“嘿，XXX，我们去年的收入是多少？”“嘿，XXX，你能调出我们过去三个月的销售数据吗？"

在整个组织中建立数据文化将使运营、产品、营销、人力资源和许多其他部门的员工能够以自助方式完成大多数简单的数据查询和数据可视化。除了使这些团队更加自给自足和灵活之外，它还允许数据分析师和数据科学家将他们的时间重新分配到他们的核心职责上，即构建和改进数据系统和模型，以及提供复杂、有意义的分析，而不仅仅是简单的数据提取。

如果你是你公司数据组织的一员，或者是一名数据倡导者，请继续阅读。本文将为您提供一些关于如何构建良好的数据文化的有价值的提示。

GIF 由 [GIPHY](https://media.giphy.com/media/l4RKhOL0xiBdbgglFi/giphy.gif)

## 1.从无代码选项开始(比如 Looker 或 Tableau)

由于大多数从事高要求工作的人没有时间在短时间内掌握像 SQL 这样的新的硬技能，所以无代码选项是让您组织中的人舒适地使用数据的一个不那么令人生畏的起点。

有越来越多的选择可以帮助这一步，Looker 和 Tableau 是大多数公司追求的两个首选。为了给你的公司选择一个合适的，了解两者之间的区别和它们的局限性是很重要的。

Looker 有一些很棒的内置分析功能，可以让没有深入分析知识的人更容易采用。我想到的一个限制是，Looker 主要可以连接到不同的数据仓库，如 **PostgreSQL、Google BigQuery** 等。但是目前没有接收 CSV 数据的好选择。唯一的解决方法是将 CSV 文件上传到这些数据库中，并建立一个与 Looker 的连接。但是，如果您所有的数据目前都在 Excel 中，并且没有数据仓库，该怎么办呢？

GIF 由 [GIPHY](https://media.giphy.com/media/QvFl5Ym0Ug9EpyeV4o/giphy.gif)

如果你所有的数据都保存在电子表格中，Tableau 可能是一个更好的选择。Tableau 可以处理到数据仓库的连接和本地 excel 表的接收。然而，它在可定制的分析和对分析知识和背景较少的人的易用性方面有所欠缺。

尽管当前的无代码选项有其缺点，但它们仍然降低了进入数据世界的门槛，并作为在您的组织内建立伟大的数据文化的良好起点。

## 2.为应该学习更高级选项(SQL)的团队提供在职学习机会

尽管无代码选项很棒，但是当它们用于执行复杂的分析时，它们不可避免地会遇到限制，并且需要更高级的 SQL 知识。此外，许可证可能会很贵，因此许多公司选择限制特定团队的访问权限。

对于像运营和营销这样经常进行复杂的大量数据分析或进行 AB 测试和其他实验的团队，员工最终会意识到他们需要足够的 SQL 知识来构建 Looker 中的“派生表”,或者至少知道足够的伪代码来有效地将他们的数据需求传达给数据团队。学习 SQL 还可以让您的员工完全抛弃 Looker 等工具，直接查询数据库，消除工具限制或依赖数据团队的瓶颈。

您可以通过提供在职学习机会，例如通过第三方提供商(如[verta bello](https://academy.vertabelo.com/))、免费替代方案(如 [W3Schools](https://www.w3schools.com/sql/) )和/或由您的数据组织开发的内部 SQL 培训，来支持这些群体中的员工。

GIF 来自 [GIPHY](https://media.giphy.com/media/W08NhmRkBg6OKMFYv5/giphy.gif)

## 3.确保每个人都能访问数据库

这个听起来很简单，对吧？你会惊讶地发现，有多少公司的数据库只有数据组中的少数人可以访问。因此，毫无疑问，来自整个公司的全部数据拉取请求都落在了十几名员工的肩上。

无论您限制访问的原因是什么，通常都有一个简单的解决方法；如果实现了限制以避免意外删除或篡改数据，那么写和编辑的权限可以限制到特定的数据组，而查询和读取数据库的权限应该授予每个人。如果可访问性的限制是出于对敏感数据(例如 PII——个人身份信息)的考虑，通常很容易实现一个变通办法，比如构建一个没有 PII 的辅助表**，每个人都可以访问它。**

引入分析和建立数据文化已经让很多人走出了他们的舒适区；不要让他们为权限而战，这是不必要的。

## 4.将所有数据放在一个地方，研究数据仓库解决方案

把你的数据放在不同的地方，对每个使用数据的人来说都是一种痛苦；例如，无代码选项通常不能连接来自不同连接(不同数据库)的表。这就是像雪花和 BigQuery 这样的数据仓库的用武之地。它们作为数据的一站式商店，避免了多种真实信息来源分布在不同地方的情况，这种情况很容易造成混乱。

![](img/1cb7f5a7040762372a5eadd43a4c77ae.png)

[娜娜·斯米尔诺娃](https://unsplash.com/@nananadolgo?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

如果您的数据目前居住在不同的地方，不要担心；随着数据仓库解决方案的发展，只需要很少的工程资源就可以将所有数据迁移到数据仓库中。

## 5.为数据库和表格准备好文档，并有一个专门的小组(Slack 或其他渠道)来回答与数据相关的问题

考虑到大多数公司数据的复杂程度，没有人完全了解数据库中的一切也就不足为奇了。让每个数据用户了解每个表中的每一列实际上是不可能的。

因此，对于每个表的所有者/创建者来说，在创建时正确地记录表是很重要的，这样将来的表用户就不必绞尽脑汁试图弄清楚表的“重量”列的单位是“磅”还是“千克”。当表格中的某些内容没有被很好地记录或难以理解时，有一个专门的小组来回答类似上面的问题也是有帮助的；假设有一个客户服务部门负责您的数据源。

## 6.开始将查询(或无代码选项源)链接到数字

假设您已经在两份不同的报告中看到了去年的销售数字；一个说销售额是 1000 万，另一个是 900 万。是什么导致了这里的差异？是因为其中一个是含税销售额而另一个不是吗？还是因为一个是用公司的财年，另一个是日历年？对于这种差异，你可以提出各种不同的假设，但是如果你不知道这些数字是如何得出的，检查它们将是一个巨大的痛苦。

这就是为什么在报告和演示文稿中链接所有数字和图表的来源如此重要。无论您使用的是 SQL 查询还是 Looker/Tableau 仪表板链接，这些链接的源都将使那些希望重现报告或只是好奇如何找到数字的人的生活变得更加轻松。

链接源的另一个好处是利用了查询/仪表板的可重用性。想象一下，另一个部门的某人正在试图找出过去 10 年的销售数字；他们可以简单地使用您的链接查询并更改一些参数，而不是与您安排一次会议来询问您是如何得出这些数字的。现在你有 15 分钟的时间可以用来喝杯咖啡。

GIF 来自 [GIPHY](https://media.giphy.com/media/l2QEilXOdTp3kKdeU/giphy.gif)

有了上面提到的所有步骤，希望可以问这样的问题:“我们去年的收入是多少？”将不再显示在任何人的收件箱中。