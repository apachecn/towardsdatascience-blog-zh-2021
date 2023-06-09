# 方法是你所需要的:数据科学中要避免的 7 个错误

> 原文：<https://towardsdatascience.com/method-is-all-you-need-7-mistakes-to-avoid-in-data-science-a18bec2c5e99?source=collection_archive---------36----------------------->

## [行业笔记](https://towardsdatascience.com/tagged/notes-from-industry)

## 来自我们经验的精选收藏

![](img/0004fa5bcaf8a44fcdfd130c6f2e7e18.png)

由[汉斯·雷尼尔斯](https://unsplash.com/@hansreniers?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄的照片

曾几何时，数据科学只对少数大型科技公司有价值。那些日子已经过去了。数据科学正在彻底改变许多“传统”行业:从汽车到金融，从房地产到能源。

普华永道的研究估计，到 2030 年，人工智能将为全球 GDP 贡献超过 15.7 万亿美元——作为参考，2018 年欧元区的 GDP 价值 16 万亿美元[1]。

现在，所有企业都将其数据视为资产，并将获得的洞察力视为竞争优势。

> 然而，超过 80%的数据科学项目失败了[2]。

为什么？

每个失败的项目都有其独特的原因，但是，根据三年的经验，我们注意到了一些模式。所以，这些就是:你在下一个数据科学项目中应该避免的七个错误。

# **1。假装数据科学不是软件开发**

*model.ipynb* ， *model_new.ipynb* ， *model_final.ipynb* …我们多少次看到笔记本和脚本不受控制的泛滥？几个星期后，你就不可能记得它们包含了什么，也不可能记得它们最初是为什么被创造出来的。混乱导致重复，重复导致错误，错误导致缓慢。缓慢的实验导致糟糕的结果。

通常，数据科学家没有软件工程背景:尽管如此，这也不是接受代码质量妥协的借口。

> 生产代码的质量是没有商量余地的。

不要搞错:我们正在谈论*生产代码*。为了快速了解实验的真相，走捷径是可以的。实际上，这是一个很好的实践:快速自由的实验是找到越来越好的解决方案的关键。然而，实验和生产是两个不同的世界:正如我们在[上一篇文章](/lessons-from-a-real-machine-learning-project-part-1-from-jupyter-to-luigi-bdfd0b050ca5)中所讨论的，一旦一个解决方案开始工作，它就应该从笔记本中拿出来，进行重构，设计成适当的软件模块，进行自动化测试，并集成到生产代码库中。

# **2。假装数据科学只是软件开发**

不，这里没有滥用复制粘贴——这一点与前一点相反。数据科学不是软件工程的子领域:它是一个复杂的学科，包含了数学、软件工程和领域知识的元素。

因此，最适合软件开发的实践可能不适合数据科学。这种差异在项目工作流程、部署后维护和测试中尤为明显。

敏捷方法，如 Scrum 和看板，广泛应用于软件开发中。不幸的是，他们没有考虑数据科学项目中涉及的不同步骤:

1.  定义问题陈述，
2.  检索有用的数据，
3.  执行探索性分析，
4.  开发模型并评估结果。

因此，至少需要一个更高层次的框架，比如微软团队数据科学流程[3]。更常见的是，采用特定的工作流:全面的讨论超出了本文的范围，但可能会出现在未来的帖子中——如果您感兴趣，请告诉我！

我们列表中的第 7 点解决了第一次部署后模型的维护和发展:这留给我们测试。

在软件开发中，测试金字塔是一个公认的隐喻[4]。您可以通过单元测试来测试每个功能或方法的正确执行，通过集成测试来测试各个组件的正确集成，通过端到端测试来测试您的应用程序的某个特性的良好行为。所有的检查都是自动进行的，并且可以在每次引入更新时重复进行。

现在，这很好，应该尽可能地应用到数据科学项目中，但是……如何检查模型或探索性分析的“正确性”?

需要一种不同的方法。首先，在建模阶段开始之前，应定义建立模型性能的适当指标，以避免任何偏差。然后，数据也应该被版本化，因为它们是每个实验可重复性的关键。最后，应该对每个更新的建模管道的性能进行自动检查，以评估它是否带来任何额外的好处。对于“建模管道”，我们在这里指的是从原始数据到训练模型的一系列转换。这一流程是提升 MLOps 范式的核心，并通过 [MLFlow](https://mlflow.org/) 等新工具得以简化。

# **3。隔离您的数据科学家**

一个数据科学项目需要很多不同的技能，而这些技能在个人身上很难找到。数据科学项目通常涉及至少三个群体:IT 团队、业务利益相关者和数据科学家。

假装一群有能力的数据科学家可以独自解决数据科学项目是毫无意义的。首先，因为数据科学是一种工具，应该被用来产生商业价值。业务价值所在的知识，提出正确问题的能力，都在业务涉众之中。同样，如果没有 IT 团队的帮助，将经过验证的解决方案投入生产也是极其困难的。

因此，这三个小组必须一起工作，能够相互理解，并恰当地融合他们的专业知识。为此，建立一个共享的术语表和一个像 Slack 或 MS Teams 这样的交流平台是很有用的。此外，接受并充分利用失败也很重要。即使在客户-顾问环境中，没有性能改进的实验仍然必须被展示和讨论，因为它们有助于为将来的迭代指明方向。

笔记本是促进有效协作的强大工具:对于数据科学家来说，它们是快速实验的完美平台，对于 IT 和业务人员来说，它们是易于理解的报告。

# **4。忽略数据**

探索性数据分析(EDA)是任何数据科学项目的关键阶段。如果总运行时间的 80%用于检索、清理和分析数据，那么也可以说项目的成功很大程度上取决于提供给模型的数据的质量。

正如我们在[的上一篇文章](/lessons-from-a-real-machine-learning-project-part-2-the-traps-of-data-exploration-e0061ace84aa)中所讨论的，从 EDA 中收集的洞察可以带来内在价值。另一个来自我们项目的例子来自食品和饮料行业。该项目旨在评估广告和折扣对销售额和利润的影响，以便自动计算出最佳策略。在 EDA 过程中，我们注意到我们客户的竞争对手能够同时提升他们产品的大部分销售，而我们的客户却不能。这一事实让他们的营销部门感到惊讶，并引发了对这一现象的详细调查。

然而，EDA 的主要目的是了解如何在建模之前清理数据，以及将哪个假设嵌入到模型本身中。在这样一个阶段偷工减料会极大地损害整个项目的结果。

# **5。跳过文档**

在文档上投入时间和资源是一种浪费。代码是不言自明的，不是吗？

不对。

> *高绩效的组织发现前期的文档记录可以避免以后的痛苦[5]。*

生产代码可能会告诉你*你正在做什么*，但是它不会向你提供关于*为什么*你正在做这件事的提示。那么所有产生次优性能的实验呢？导致最终解决方案的所有小见解、发现和挑战呢？这类问题的答案和解决方案本身一样有价值。

是的，但是如何记录数据科学项目的发展呢？

我们发现背页[和出口的 Jupyter 笔记本上的乳胶极其有效。如果它们被适当的可再现性补充，用 git 实现代码版本化，用](https://www.overleaf.com/) [DVC](https://dvc.org/) 实现数据版本化，用 [MLFlow](https://mlflow.org/) 或一些类似的工具实现实验版本化，就更是如此。

# 6.试图让第一个模型正确

数据科学项目本质上是迭代的。第一次尝试就获得最优解是不可能的，而且通常也是没有用的。

在对解决方案进行过度设计之前，有必要研究一下经过试验和测试的方法的文献。对于计算机视觉任务，很少有人会开发自己的神经网络架构:依赖现成的模型和迁移学习要容易得多，也更有效。

在不同的环境中，例如处理时间序列或表格数据，从简单的模型开始通常是明智的，更容易调整和解释。对于时间序列预测来说，优秀的老 ARIMA 预测器肯定不是最先进的，但它们可以告诉我们很多关于序列结构的信息，并指导更复杂方法的开发。

此外，最重要的指标不是关于准确性或错误，而是关于业务价值。用一个足够好的模型快速投放市场会带来有意义的反馈，并有助于引导随后的迭代产生最大的价值，而不仅仅是最好的模型。

> 最好的组织从简单开始，并将结果融入业务。在用更复杂的方法更新模型之前学习和测量[5]。

# 7.认为模型是永恒的

没有一种模式是永恒的。即使一个预测器今天在生产中有效，它也可能在几个星期后失效。这是因为一个模型的有效性通常取决于模型现象发生的背景。

当 COVID 在 2020 年初引发 lockdowns 中风时，我们开发的一些预测电能需求的模型经历了性能的急剧下降。这是可以的:没有一个模型被训练来应对全国性的关闭，因为(I)这以前从未发生过，以及(ii)考虑到这种遥远的可能性没有经济意义。

这是一个极端的例子，但模型运行的环境或数据中不太显著的变化会对它们的性能产生深刻的影响。因此，建立适当的监控基础设施并尽快将新的解决方案投入生产，同时避免危险的错误是至关重要的。

5 岁时，*你的 ML 测试分数是多少？Google 的 ML 生产系统标题仍然是这个主题的主要参考之一。这篇论文解决的许多问题现在都是 MLOps 的核心，它有望给数据科学带来像 DevOps 给软件开发带来的一样大的推动。*

*谢谢你，我的读者，来到这里！*

*我们永远欢迎每一个评论、问题或总体反馈。如果你对* [*me*](https://www.linkedin.com/in/emanuelefabbiani/) *或者*[*XT ream*](https://xtreamers.io)*很好奇，可以上 LinkedIn 看看我们！*

*如果你喜欢这篇文章，你可能会感兴趣:*

</stop-copy-pasting-notebooks-embrace-jupyter-templates-6bd7b6c00b94>  </lessons-from-a-real-machine-learning-project-part-1-from-jupyter-to-luigi-bdfd0b050ca5>  </lessons-from-a-real-machine-learning-project-part-2-the-traps-of-data-exploration-e0061ace84aa>  

# **参考文献**

[1]普华永道研究小组，[确定奖项:人工智能对你的业务有什么真正的价值，你如何才能利用它？](https://www.pwc.com/gx/en/issues/analytics/assets/pwc-ai-analysis-sizing-the-prize-report.pdf)，2017

[2] Brian T. O'Neill，[分析、人工智能和大数据项目的失败率= 85% —哎呀！](https://designingforanalytics.com/resources/failure-rates-for-analytics-bi-iot-and-big-data-projects-85-yikes/)，2019

[3]微软，[什么是团队数据科学流程？](https://docs.microsoft.com/en-us/azure/architecture/data-science-process/overview)，2021 年

[4]汉姆·沃克，[实用测试皮拉姆](https://martinfowler.com/articles/practical-test-pyramid.html)，2018

[5] Domino，[大规模数据科学管理实用指南](https://www.dominodatalab.com/resources/managing-data-science/)，2021 年

[6]埃里克·布雷克，·蔡，埃里克·尼尔森，迈克尔·萨利布，d·斯卡利，[你的 ML 测试成绩是多少？大规模生产系统规则](https://research.google/pubs/pub45742/)，2016 年

# **鸣谢**

*本帖的大部分内容和原稿由* [*马可·帕鲁西奥*](https://medium.com/u/aee113c92618?source=post_page-----a18bec2c5e99--------------------------------) *创作。xtream 的整个数据科学团队在审阅本文时提供了有效的支持。*