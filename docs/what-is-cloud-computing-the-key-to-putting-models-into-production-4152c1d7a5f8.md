# 什么是云计算？将模型投入生产的关键

> 原文：<https://towardsdatascience.com/what-is-cloud-computing-the-key-to-putting-models-into-production-4152c1d7a5f8?source=collection_archive---------18----------------------->

## **AWS、Azure、Hadoop、PySpark 等顶级云计算平台的细分。**

![](img/2b3519889c2337095d88038e01065c04.png)

[天马](https://unsplash.com/@tma)上[下](https://unsplash.com/photos/WiONHd_zYI4)

任何数据科学家的一项关键技能是能够**编写生产质量的代码来创建模型**和**将它们部署到云环境中**。通常，使用云计算和数据架构属于数据工程师的工作。然而，每个数据专家都被期望成为通才，能够**适应和扩展他们的项目**。

下面是我在几十个职位描述中看到的热门平台介绍。这并不意味着我们必须在一夜之间成为专家，但这有助于了解现有的服务。入门总是学习新技能的第一步。

# **大数据&云计算**

尽管“大数据”最近已经成为一个时髦词，并引起了大企业的兴趣，但它通常很难定义。关于定义还没有明确的共识，但是**“大数据”通常指的是增长到无法使用传统数据库管理系统和分析方法管理的数据集。**这些数据集的大小超出了常用软件工具和存储系统在可容忍的运行时间内捕获、存储、管理和处理数据的能力。

当考虑大数据时，请记住 3 V:容量、多样性和速度。

*   **卷**:数据的大小
*   **多样性**:数据的不同格式和类型，以及数据的不同用途和分析方式
*   **速度**:数据变化的速度，或者说创建数据的频率

随着数据的发展，对更快、更高效地分析此类数据的需求也呈指数级增长。仅仅拥有大数据已经不足以做出高效的决策。因此，需要专门用于大数据分析的**新工具和方法**，以及存储和管理此类数据所需的**架构**。

# 我们应该从哪里开始？

每个公司都有一个独特的技术堆栈，其中包含他们更喜欢用于其专有数据的软件。堆栈中的每个类别都有许多不同的平台。这些类别包括可视化和分析、计算、存储和分发以及数据仓库。有太多的平台无法计数，但我会仔细阅读我在最近的招聘信息中看到的流行的云计算服务。

公司可以从云服务提供商那里租用从应用程序到存储的任何东西，而不是拥有自己的计算基础设施或数据中心。这允许公司在使用时为他们使用的东西付费。与其处理维护自己的 IT 基础设施的成本和复杂性。简单来说，

> **云计算**是按需交付计算服务——从应用程序到存储和处理能力——通常通过互联网，并以按需付费的方式进行。

虽然我不打算在这篇博客中深究细节，但重要的是要注意有三种云计算模式**。 **IaaS** (基础设施即服务) **PaaS** (平台即服务) **SaaS** (软件即服务)。在这三种模式中， **SaaS 是目前占主导地位且应用最广泛的**云计算模式。**

# ****亚马逊网络服务(AWS)****

**AWS 提供数据库存储选项、计算能力、内容交付和联网等功能，以帮助组织扩大规模。**您可以选择自己想要的解决方案，同时为自己消费的服务付费**。像 AWS 这样的服务允许我们每分钟在这些服务器上租用时间，使得任何人都可以进行分布式培训。此外，AWS 服务器允许公司跨服务器集群使用 Hadoop 或 Spark 等大数据框架。**

**亚马逊还将所有主要的数据科学服务集中在亚马逊 SageMaker 内部。SageMaker 提供了许多服务，如数据标签、基于云的笔记本、培训、模型调整和推理。我们可以建立自己的模型，或者使用 AWS 提供的现有模型。类似地，我们可以设置自己的推理端点，或者利用 AWS 创建的预先存在的端点。创建一个端点需要我们使用一个 **Docker** 实例。幸运的是，为我们自己的模型创建端点所需的大部分工作都是样板文件，我们可以在多个项目中反复使用它。**

**AWS 目前支持 2000 多个政府机构和 5000 个教育机构。此外，它还是全球四大公共云计算公司之一。好处包括**易用性、多样化的工具阵列、无限的服务器容量、可靠的加密和安全性、**加上**可负担性**。但是，一些缺点是 AWS 的一些资源受到地区的限制。它也受到许多其他云计算平台面临的问题的影响。有人担心**备份保护、数据泄露风险、隐私问题**和**有限控制。****

# ****微软 Azure****

**微软 Azure，通常被称为 **Azure** ，是由**微软**创建的云计算服务，用于通过微软管理的数据中心来构建、测试、部署和管理应用和服务。该平台**非常注重安全性，**确立了其在 **IaaS 安全性**方面的领先地位。此外，作为云计算服务，它是高度可扩展的，同时价格合理。**

**和任何事情一样，微软 Azure 也有一些潜在的缺点。与最终用户消费信息的 SaaS 平台不同，IaaS 平台，如 Azure，将企业的计算能力从数据中心或办公室转移到**云**。与大多数云服务提供商一样， **Azure 需要专业的管理和维护，包括补丁和服务器监控**。**

# ****谷歌云平台(GCP)****

**就像 AWS 和 Azure 一样，GCP 是由谷歌提供的一套公共云计算服务。该平台包括一系列在谷歌硬件上运行的计算、存储和应用开发托管服务。**

**GCP 与 AWS 强有力竞争的一些领域包括**实例和支付可配置性、隐私和流量安全、成本效益和机器学习能力**。GCP 还提供几个现成的与计算机视觉、自然语言处理和翻译相关的 API。机器学习工程师可以基于谷歌的云机器学习引擎开源的 TensorFlow 深度学习库来构建模型。**

**尽管这个竞争对手有优势，但也有一些不利因素。像 BigQuery、Spanner、Datastore 这样的核心 GCP 产品很棒，但是非常偏向于**有限的定制和可观察性**。此外，可用的**文档有限**，并且有传言称 GCP 的客户服务**总体上没有回应**。**

# ****Hadoop****

**Hadoop 是一个分布式计算系统和环境，适用于计算机集群上的超大型数据集。它为任何类型的数据提供大容量存储、巨大的处理能力以及处理几乎无限的并发任务或工作的能力。这个生态系统也利用了 MapReduce。**

****MapReduce** 是 Hadoop 框架内的一种编程模型或模式，用于访问存储在 Hadoop 文件系统(HDFS)中的大数据。MapReduce 作业通常**将输入数据集分割成独立的块**，由地图任务以完全**并行**的方式进行处理。该框架对映射的输出进行排序，然后输入到 reduce 任务中。通常，作业的输入和输出都存储在文件系统中。**

**Hadoop 和 MapReduce 允许任务被**划分**，而不是仅仅使用一个系统来执行任务。任务被分成许多子任务，它们被单独解决，然后**重新组合成最终结果**。**

**虽然 Hadoop 是开源的，并且使用了一种经济高效的可扩展模型，但它主要是为处理大型数据集而设计的。**处理少量数据时，平台效率下降**。此外，Hadoop 作业大多是用 Java 编写的，如果没有这种语言的专业知识，这可能会很麻烦，而且容易出错。**

# ****PySpark****

**PySpark 是在 **Python** 编程语言中用于 **Apache Spark** 的接口。它不仅允许您使用 Python APIs 编写 Spark 应用程序，还提供 PySpark shell，用于在**分布式环境**中交互分析您的数据。PySpark 支持 Spark 的大部分功能，如 Spark SQL、DataFrame、Streaming、MLlib(机器学习)和 Spark Core。**

**PySpark 的一些优点是，一些 Spark 作业在内存方面可以比传统的 MapReduce 快 100 倍。它还允许更高级别的查询语言在 MapReduce 之上实现类似 SQL 的语义。此外，PySpark APIs 类似于 Python 的 **Pandas** 和 **Scikit-Learn** 。**

**最初的 Apache Spark 服务是用 **Scala** 编写的，这是一种受大数据开发者欢迎的编程语言，因为它在 JVM (Java 虚拟机)上的**可伸缩性**。不幸的是，Python 总体上比 Scala 慢，效率也低。此外，与 Spark 相比，PySpark 还不成熟，无法在大多数项目中使用 Spark 的内部功能。**

# ****选择合适的服务****

**如果没有云计算，数据科学家和机器学习工程师将**不可能**训练当今存在的一些更大的深度学习模型。**

**有大量的云计算服务可供选择，但选择正确的服务取决于安全问题、软件依赖性、可管理性、客户服务支持等因素。**

**每个雇主最有可能有一个他们在公司范围内用于专有数据的首选技术堆栈。在那之前，网上有很多资源可以帮助你增加云计算知识。你也可以去每个供应商的网站，广泛阅读他们提供的服务。最后，需要注意的是，对于任何数据科学技能，没有比**亲自动手**实践个人项目更好的学习方法了。**