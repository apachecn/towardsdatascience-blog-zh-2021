# 架构完善的框架—在云上实现可靠性

> 原文：<https://towardsdatascience.com/well-architected-framework-achieve-reliability-on-cloud-260572f27cd0?source=collection_archive---------55----------------------->

## 通过整合应用解决方案架构的可靠性框架来克服业务损失

# 介绍

企业依靠对数据和应用程序的可靠访问来满足客户的需求。如果最终用户无法使用关键系统，最终会导致企业收入损失。因此，云架构的 ***可靠性*** 方面使您能够结合架构考虑和设计来克服这些业务挑战。

> *这是一系列帖子，将涵盖云架构良好的框架，其他帖子的参考网址是:
> 【1】*[架构良好的框架—云上的性能效率](/well-architect-framework-performance-efficiency-on-the-cloud-15cf87c10297) *【2】*[架构良好的框架—云的安全方面](/well-architected-framework-security-aspects-of-the-cloud-1119417f7cb8)

![](img/f006fc451e00b5d1f360cc8fff9ea8a9.png)

[马克·柯尼希](https://unsplash.com/@markkoenig?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

# 高可用性架构

高可用性(HA)服务意味着在不影响业务的情况下吸收波动、故障、负载和临时故障。这意味着根据业务需求和目标以及 SLA，服务始终是可用的和在线的。

建议仔细考虑解决方案架构，并确定由于其他一些原因而变得不可用的潜在组件。这些组件可以是虚拟机、数据库和网络组件，如 LBs 或网关。由于计划维护、故障或某些云区域/数据中心脱离电网，这些组件可能变得不可用。因此，您必须确定您的故障点在哪里以及如何出现，并确定如何在您的架构中解决这些故障点。

根据以下参数评估解决方案架构:

1.  **SLA &应用程序的 SLO**

SLA 是服务提供者和服务消费者之间的服务级别协议，服务提供者承诺并受法律约束遵守该协议。吞吐量、可用性和容量等指标用于衡量 SLA。违反 SLA 会给服务提供商带来严重的财务后果和处罚。

SLO，即服务级别目标，是用于衡量性能、可靠性或可用性的目标度量值。这些是为支持服务的团队和消费这些服务的客户设定的目标和期望。因此，SLO 确定是否满足总体 SLA。

**2。应用程序的 HA**

要从故障分析的角度评估应用程序焦点的 HA，请考虑单点故障，以及关键组件，如果这些组件不可达、配置错误或出现故障，将会产生重大影响。

为了处理这种情况，评估应用程序的每个组件，用提供 HA 的组件(例如 LBs)包括或替换它们，或者使组件冗余以克服由它们引起的单点故障。

**3。依赖应用的 HA**

如果您向客户承诺 99.9%的正常运行时间，但您的应用程序所依赖的服务只有 99%的正常运行时间，这可能会使您面临无法满足客户 SLA 的风险。因此，如果依赖关系离线，解决方案架构应该处理替代解决方案。一种替代方法是使用缓存或加载工作队列。

因此，在为高可用性进行架构设计时，您将希望了解您向客户承诺的 SLA。然后评估您的应用程序所具有的 HA 功能以及相关系统的 HA 功能和 SLA。

# 灾难恢复策略

*灾难*是一种高影响事件，持续时间比高可用性部署应用程序预期的要长，此类事件无法缓解，最终可能导致停机或数据丢失。此类事件可能是自然发生的—地震、洪水，也可能是黑客从外部造成的。

## 灾难恢复计划

*灾难恢复计划*是一个单独的文档，详细说明了从灾难导致的数据丢失和停机中恢复所需的程序。该计划还确定了谁负责指导这些程序。这是一个全面的用户指南，用于在灾难发生后恢复应用程序连接和数据。

灾难恢复计划应包括以下指导原则:—

*   执行风险分析，检查不同种类的灾难对应用程序的影响。你甚至可以考虑分析任何假设的场景。风险评估还应考虑无法承受*无限制*停机的应用程序组件。重要的是，计划负责人可以使用该计划对需要注意的事项以及如何对每个项目进行优先排序进行全面盘点。
*   考虑恢复目标 RPO 和 RTO，R *恢复点目标(RPO)* 是可接受的数据丢失的最大持续时间，而 RTO 是可接受的停机时间的最大持续时间。指定 RPO 和 RTO 不应该只是简单地选择任意值，该决策会影响工作负载和成本效益权衡的灾难恢复设计。
*   恢复步骤的详细信息构成了灾难恢复计划的核心，它是在发生灾难时要执行的行动手册，应该包括有关管理的信息—备份、数据副本、部署、依赖关系和配置。

## 将灾难恢复纳入解决方案设计

发生灾难时，灾难恢复计划的执行不是一个自动过程，需要手动执行这些步骤。任何灾难恢复计划都应该考虑两个主要问题

*   如何恢复数据？
*   如何恢复应用程序及其进程？

***数据恢复*** 由*备份*以及与业务 SLO/SLA 相关的复制策略、工具和技术组成。备份策略应该包括允许返回多少时间来获取数据的只读快照。*复制*计划使系统能够在发生灾难时近乎实时地进行故障转移。因此，这是维护高可用性和灾难恢复设计的关键组件。相对于业务 SLA 和应用程序 RPO 的成本效益分析& RTO 对于决定备份和复制策略非常重要。这些可能是—仅备份、主动-被动复制或主动-主动复制策略。

***应用恢复*** 侧重于灾难事件后应用恢复的方法、流程和路径选择。目标是设计您的应用程序需求，使您能够将其恢复到工作状态。这包括— *故障转移*到辅助区域。同样，这些策略是由业务或应用程序的 RTO 和 SLOs 需求驱动的。

## 测试灾难恢复计划

测试灾难恢复计划是灾难恢复的一个重要方面，以确保方向、说明和责任是清晰的和最新的。验证恢复结果、确定差距并迭代地改进以克服新的挑战是至关重要的。确保在你的测试中也包括你的监控系统。

# 备份策略

您的应用程序跨文件系统或数据库管理不同类型的不同重要性的数据。应用程序的备份要求应反映基于不同数据源的备份需求、外部要求，如数据保留法律和业务合规性。

*   企业能够承受多少数据丢失？
*   实现完全数据恢复需要多长时间？
*   企业希望数据备份保持可用多长时间？

同样，基于定义的 RPO 和 RTO 的成本效益分析对于制定备份和恢复策略至关重要。该战略由框架、工具、流程、程序和利益相关方组成，以应对所有可能的灾难恢复情形。

最后，与灾难恢复策略的验证和确认不同，备份策略应该经过彻底的测试，并反复改进以纠正潜在的差距。

备份和恢复策略是确保您的体系结构能够从数据丢失或损坏中恢复的重要部分。

# 结论

在这篇文章中，我们讨论了云架构良好的框架的*可靠性*支柱的一些关键原则。我们已经了解了如何考虑在应用程序的整个解决方案架构的核心中整合高可用性的需求。

我们讨论了灾难恢复，以及如何为您的应用程序定义 RPO 和 RTO。还了解测试您的恢复计划以确保它们符合业务要求的重要性。

最后，在您的恢复策略中涉及备份和恢复，以防止典型的数据丢失情况。

在本系列的后续文章中，我将重点介绍云架构良好的框架的其他支柱。

> 在 [**LinkedIn**](https://www.linkedin.com/in/p-jainani/) 上和我联系进一步讨论

# 参考

[1] [微软 Azure 架构良好的框架—可靠性](https://docs.microsoft.com/en-us/azure/architecture/framework/resiliency/overview)
【2】[AWS 架构良好—可靠性](https://docs.aws.amazon.com/wellarchitected/latest/framework/reliability.html)
【3】[谷歌云的架构框架—可靠性](https://cloud.google.com/architecture/framework/reliability)