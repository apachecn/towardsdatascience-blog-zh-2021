# 什么是特征工程？

> 原文：<https://towardsdatascience.com/what-is-feature-engineering-bfd25b2b26b2?source=collection_archive---------32----------------------->

## 一个非常宽泛的机器学习概念的简要介绍

对于“特征工程”具体指的是什么，很难找到任何一种共识。我这篇文章的目标是为新的和有抱负的数据科学家提供一个关于构建成功的机器学习(ML)模型的非常广泛而基本的方面的介绍。我们将讨论变量和特性之间的区别，为什么特性工程是重要的，以及什么时候你可能想要设计特性。在以后的文章中，我将介绍一些如何使用 Python、Pandas 和 NumPy 来设计特性的基本示例。

![](img/f38edb1eeefde644cf4faab960b558ca.png)

凯文·Ku 通过 [Unsplash](https://unsplash.com/) 拍摄的图片

# 那么什么是特征工程呢？

有些人认为特征工程包括数据清理，将数据转换成机器学习(ML)算法可用的格式。这包括处理缺失值或空值、处理异常值、删除重复条目、编码非数字数据以及转换和缩放变量。我倾向于认为这些事情是重要的预处理步骤，但是大部分是与特征工程分开的。我说“大部分”是因为(像数据科学中的大多数其他事情一样)探索、清理和工程特性应该被视为迭代过程的一部分。这些步骤中的每一步都会通知其他步骤。

对我来说，特征工程专注于使用你已经拥有的变量来创建额外的特征，这些特征(*希望是*)更好地表示你的数据的底层结构。特征工程是一个创造性的过程，非常依赖于领域知识和对数据的彻底探索。但是在我们继续深入之前，我们需要后退一步，回答一个重要的问题。

# 什么是特性？

要素不仅仅是数据集中的任何变量。特征是一个变量，对于预测您的特定目标和解决您的特定问题非常重要。例如，在许多数据集中常见的变量是某种形式的唯一标识符。该标识符可以代表唯一的个人、建筑物、交易等。唯一标识符非常有用，因为它们允许您过滤掉重复的条目或合并数据表，但是唯一 id 不是有用的预测器。我们不会在我们的模型中包含这样的变量，因为它会立即过度拟合训练数据，而不会为预测未来的观察提供任何有用的信息。因此，唯一 ID 是一个变量，而不是一个特征。

所以一个特征可以被认为是一个潜在有用的预测因子。

# 特征工程的目的是什么？

当你拿到一个数据集时，你很少会觉得你已经得到了解决问题可能需要的所有信息。那么，如果你不能收集更多的数据或测量额外的变量，你能做什么呢？你可以设计特征。

这实际上意味着应用领域知识来弄清楚如何以新的方式使用您所拥有的信息来提高模型性能。直到你开始探索你的数据，你才会完全理解你所拥有的信息。这就是为什么很难找到涵盖特性工程主题的非常具体的资源。它是如此依赖于

*   你工作的领域，
*   您在该领域中的具体问题或任务，
*   你已经拥有的变量，
*   以及你产生额外信息的能力。

没有人能给你一步一步的指导，告诉你应该设计哪些功能以及如何设计。抱歉。

创建能够更好地强调数据趋势的附加要素有可能提高模型性能。毕竟，任何模型的质量都受到输入数据质量的限制。仅仅因为这些信息在技术上已经存在于你的数据集中，并不意味着机器学习算法能够识别它们。在大的特征空间中，重要的信息可能在噪声和竞争信号中丢失。因此，在某些方面，特征工程就像试图告诉模型数据的哪些方面值得关注。这是您作为数据科学家的领域知识和创造力真正发挥作用的地方！

# 什么时候应该设计功能？

当您浏览已有数据时，请记住以下几个问题:

1.  用不同的方式表示同一个变量，有可能获得信息或减少噪音信号吗？
2.  是否有任何变量具有重要的阈值，而这些阈值没有明确地反映在变量当前的表示方式中？
3.  可以将任何变量分解成两个或更多的变量来提供有用的信息吗？
4.  有没有任何一个变量可以以某种方式组合起来，变得比它们各部分的总和更能提供信息？
5.  您是否有信息可以让您收集或以其他方式获得有用的外部数据？

如果你对这些问题中的任何一个回答“是”，花一些时间来设计功能可能是一个有益的尝试。

# 最后

与数据科学中的许多事情一样，特征工程是一个迭代过程。调查、试验和返回进行调整是至关重要的。您将获得的对数据结构的洞察以及对模型性能的潜在改进通常非常值得付出努力。此外，如果您对这一切还比较陌生，那么特征工程是练习使用和操作数据框架的好方法！因此，请继续关注未来的帖子，这些帖子涵盖了如何做到这一点的具体示例(*，代码为*)。

关于特征工程的更多信息:

[特征工程示例:宁滨分类特征](/feature-engineering-examples-binning-categorical-features-9f8d582455da)

[特征工程实例:宁滨数字特征](/feature-engineering-examples-binning-numerical-features-7627149093d)