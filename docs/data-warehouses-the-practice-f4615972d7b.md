# 数据仓库:实践

> 原文：<https://towardsdatascience.com/data-warehouses-the-practice-f4615972d7b?source=collection_archive---------19----------------------->

## 真正的交易

![](img/97065b45960545f27b842e50879b3c41.png)

约翰·汤纳在 [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

在一个理想的世界里，理论和实践之间的差距并不大，或者至少对项目的生命周期影响不大。然而，在现实世界中，尤其是在处理数据时，人们知道事实并非如此。数据存储，尤其是长时间存储的数据，可能会变得混乱，并导致脏表，在某些时候需要处理和整理这些脏表，以便进行更好和更有效的分析，因此需要 ETL 管道。在这篇[文章](/data-warehouses-the-theory-2f0481eb5af8)中解释的理论经验法则，加上由于数据不一致而导致的较小(或较大)的调整，可以产生非常干净和有用的数据仓库，这对公司来说有很大的价值。数据的不一致性可能相当大，因为其中大多数是人为错误造成的；然而，尽管人们对他们所犯的错误很有创造力，但是在做 ETL 时所面临的问题类型是很常见的。

每个 ETL 管道都要经历三个主要步骤:

*   **数据分析**:彻底分析 AS IS，目的是理解需要应用的转换。
*   **模型定义**:定义好表格以及表格之间的关系。
*   **ETL 实现**:模型的实际实现，从数据源获取数据，产生设计的数据模型。

# 数据分析

这一步的重要性是双重的:

*   **业务需求**:在业务单元的指导下，了解正在实施的数据仓库需要从数据源的海洋中恢复的信息

数据仓库可以基于放在一起的许多不同的数据源，也可以只基于一个数据源，但只包含它所包含的表的子集。业务需求可能有两种情况:一种情况是他们确切地知道他们随后将使用数据仓库做什么样的分析，另一种情况是他们没有非常具体的想法。无论哪种方式，对于这一步，任务是理解哪些表将用于设计数据模型，更具体地说，这些表的哪些属性是有用的。黄金法则是设计一个满足必要条件的 DWH，如果它们存在的话，为这些必要条件将来可能的扩展留出空间。如果没有定义特定的必要条件，一个解决方案可以是确定对所讨论的数据进行分析的最流行的场景，然后为这些场景准备数据。不过，后一种情况非常罕见，因为一家公司几乎不会投资于不能带来中短期收入的项目。

*   **数据质量**:了解将要使用的数据源的当前状态

一旦确定了表，就该深入分析了:分析这些表及其属性。这实际上意味着考虑每个表的属性。可能有超过 150 个属性的表，但不是所有的属性都有用，也不是所有的属性都填充了值。首先要做的检查是寻找 ***缺失值*** 以及有多少缺失数据。一个 90–95%为空的属性很难用于分析或任何报表可视化，因此可以丢弃。对于多年的数据收集，表 中可能存在 ***不一致。数据不一致的另一个来源可能是来自不止一个数据源的同一个表(是的，这不是一个好的做法，但是现实世界是一个扭曲、复杂的地方)。对于这类问题，重要的是理解不一致背后的逻辑，看看是否可以修补。解决方案取决于分析:对于 DWH，如果旧数据不再相关，则可以丢弃旧数据，或者如果可能，可以应用变换来获得数据的一致性。数据质量需要考虑的另一个方面是如何让许多不同的来源相互交流，并在汇总时获得一致的结果。***

在这一步结束时，由于数据清理和业务需求，当您开始处理大量数据时，您最终会得到一个池。

# 模型定义

模型定义可以归结为划分维度和事实表中的表，以及设置这些表之间的关系。

*   **尺寸**:当谈到尺寸替代时，要考虑的是它们是否是 ***缓变尺寸(SCD)*** ，选择最适合自己需求的 SCD 类型。2 型 SCD 是最常见的。
*   **事实**:一个关键的方面是已经 ***实现了 KPI***用于进一步的分析，在最低的粒度级别，为任何种类的聚合留下了空间。可视化工具可能会限制您的数据转换可能性，或者使其变得非常困难，因此在 DWH 实施级别推动这种计算会使其变得更加容易，并且简化了未来可视化分析的实施。
*   **关系**:这两个类别的区别非常简单，但是设置 ***关系*** 可能会变得棘手，其中一个主要问题是当有更多的事实表出现时，这种情况会经常发生，并且这些事实表还需要与其他维度进行对话。基本规则是避免两个事实表之间的关系，始终坚持星型模式，这可能导致数据仓库中有多个星型模式。
*   **命名约定**:选择一个命名约定，并坚持下去。
*   **暂存区**:考虑为你的源数据表做一个复制层。
*   **索引和分区**:为了提高查询效率，根据正在构建的表的大小，如果必要的话，可以考虑并实现分区。此外，选择合适的索引也会对查询性能产生很大的影响。
*   **技术属性**:虽然添加和维护这些属性可能会很麻烦，但是跟踪诸如记录插入的时间戳、更新或导致更新的原因等信息在将来会很有帮助。
*   **更新频率**:根据分析的必要性，DWH 更新的时间安排可以从每天到一周几天不等。更新所需的时间会对此产生影响，因此在安排更新时需要考虑到这一点。
*   可扩展性:使模型易于扩展，适应变化。一直都是。

# ETL 实现

最后一块拼图:*实际实现*。如果前两步做得很彻底，这一步会很容易，你会面临一些在前面的分析步骤中可能错过的惊喜。

用于实现 ETL 的工具将对实现设计模型的工程师产生最大的影响，而不是最终产品。现在有很多工具可以完成这项工作，但是 ETL 实现软件的选择很大程度上取决于许多不同的因素，比如公司使用的其他软件、平台和编程语言，项目的预算等等。

不管使用什么工具来构建管道，最重要的步骤是测试。当一切都实现后，通过进行 ***测试*** 来检查整个过程的正确性。需要检查每个表，并注意每个表的所有属性，以便最终结果是正确的，并与初始要求一致。制定一个详尽的测试用例计划(插入、更新或记录取消是最基本的)可能看起来令人望而生畏，但这是确保模型有效性的最佳方式。

# 谨记在心

如果你仔细想想，数据仓库的设计和开发是一个相当机械的过程。业务人员的参与推动了分析，而分析推动了流程的其余部分。模型的设计和实现是需要评估和实现的事情的清单。一个设计良好的模型可以使未来的数据分析和仪表板开发变得非常简单。