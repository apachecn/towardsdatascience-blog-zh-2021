# MLDrops —优化一个评估指标并满足所有其他指标

> 原文：<https://towardsdatascience.com/mldrops-optimize-one-evaluation-metric-and-satisfy-all-other-metrics-367457d3c32d?source=collection_archive---------38----------------------->

![](img/459dd0214ee3b8a0e44f34134eb45575.png)

照片由 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的[米切尔·布茨](https://unsplash.com/@valeon?utm_source=medium&utm_medium=referral)拍摄

## 常见场景

在项目中应用特定的技术来实现预期的目标，但是没有获得令人满意的结果。技术团队在收到某个需求后，进行分析，得出以下结论:这是一个机器学习项目的好案例。

项目批准后，考虑到必要的时间和投资，提出要求。这是一个非常常见，但绝不是积极的，可能发生的情况。该调查构成了一个类似于以下内容的列表:

*   该模型应该达到可能的最佳结果；
*   模型应该具有尽可能最短的推理执行时间；
*   该模型应该具有尽可能小的内存占用。

有了这些定义，团队开始工作。我问读者:无论工作组多么有经验，你认为在从事一个有这样需求的项目时能取得什么样的结果？

## 共同结果

一次又一次的迭代，需求似乎并没有达到。该模型是准确的，但是不考虑执行时间。当针对所允许的最大时间进行优化时，它最终会消耗比最优值更多的内存，或者具有明显更低的准确性。在极少数情况下，所有的需求都有一个“ok”的性能，团队将会分裂以优化各种度量，并且上述情况会一次又一次地发生。

> **注意**:一步一个脚印！

在定义我们的评估指标时，我们必须使用两个重要的概念:**优化指标和满意指标**。

优化度量在项目中必须是唯一的，并且模型改进的开发迭代必须将它作为改进的主要焦点。

> 令人满意的度量标准是我们应该用作指南的门槛，但是我们不会持续地工作来优化它们。我们使用这些指标作为不得超过的阈值。

在项目构思和每个迭代周期的开始，定义哪些度量是最佳的，哪些是令人满意的

非常重要的是，当开始项目或项目的新迭代以获得更好的结果时，团队有一个清晰的愿景，并且可以很容易地区分不同类型的度量标准。定义度量标准的工作与新项目的预期结果直接相关，或者类似地与先前生成的模型的结果分析中提出的问题相关。

有了这个定义，团队将会更加敏捷，将会实现更加符合期望的结果，并且也将会有一个清晰的路径来发展模型，并且，因此，相对于已建立的目标增加自信。

我希望你喜欢阅读这篇文章。

如果你喜欢这种快速、开门见山、机器学习的内容，*可以考虑关注我的* [*Twitter*](https://twitter.com/ogaihtcandido) *。*

谢谢你的时间。保重，继续编码！