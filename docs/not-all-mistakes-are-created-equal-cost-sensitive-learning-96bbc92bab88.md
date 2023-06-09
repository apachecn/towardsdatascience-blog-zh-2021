# 并非所有的错误都是生来平等的:成本敏感的学习

> 原文：<https://towardsdatascience.com/not-all-mistakes-are-created-equal-cost-sensitive-learning-96bbc92bab88?source=collection_archive---------37----------------------->

## 成本敏感学习是解决许多问题的必要方法。请继续阅读，了解它是如何工作的。

![](img/8fb99c7194f8c33e7d80a152c9dbc0d2.png)

莎拉·基利安在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

在分类问题中，我们常常假设每一个误分类都是同样糟糕的。然而，有时这是不正确的。考虑尝试对是否存在恐怖主义威胁进行分类的例子。有两种类型的错误分类:要么我们预测有威胁，但实际上没有威胁(假阳性)，要么我们预测没有威胁，但实际上有威胁(假阴性)。显然，假阴性比假阳性危险得多——在假阳性的情况下，我们可能会浪费时间和金钱，但在假阴性的情况下，人们可能会死亡。我们称这样的分类问题为**成本敏感**。

那么，我们如何修改常规分类，将假阳性和假阴性同等对待，以考虑成本敏感性呢？有几种主要的方法。第一个称为**阈值**。在常规分类中，如果我们的输出概率大于 50%,我们预测正例，如果输出概率小于 50%,我们预测负例。阈值处理的作用是改变 50%的数值。回到恐怖分子的例子，假阴性的代价大于假阳性的代价。因此，我们希望算法对负面预测比对正面预测更有把握，因此我们将 50%的阈值移动到一个较小的数字，也许是 30%。如果我们有一个反过来的问题，假阳性的代价更高，我们会走另一个方向，将 50%的阈值提高到 70%。

当然，我们可能希望对我们的阈值有更具体的规定。我们可以更精确，而不是做一个大概的估计，说“是的，降到 30%听起来不错”。我们可以为每个假阳性(FP)和假阴性(FN)定义一个数字成本，例如恐怖事件中的 1 和 3。从最小化总成本敏感误差(数据集中所有假阳性和假阴性的总和，由我们刚刚定义的数字成本加权)的目标开始，可以推导出理想阈值应该是什么的表达式:FP/(FP + FN)。对于我们的例子，阈值应该是 1/(1 + 3) = 25%。直观上，我们可以看到这种表达是有道理的。假阴性越重要，分母就越大。那么阈值将会降低，这意味着我们对负面预测的标准更加严格，这正是我们想要的。

除了阈值处理，另一种解决成本敏感分类问题的方法是对数据进行重新采样。这个想法是因为我们更关心假阴性而不是假阳性，我们应该减少训练集中的阴性数量。这将导致算法更倾向于误报，这是我们更喜欢的。还有一个精确的数学公式——我们将训练集中的否定数乘以 FP/FN。我们看到，FN 越大，这个数字就越小，这是意料之中的。

我们应该提到，在成本敏感的分类问题中，我们也经常使用不平衡的数据集，这意味着正面和负面例子的比例要么非常高，要么非常低。例如，我们的恐怖袭击示例可能有一个不平衡的数据集，因为恐怖袭击并不常见。幸运的是，重采样也恰好有助于训练不平衡的数据集。

到目前为止，我们已经讨论了**元学习**成本敏感算法，这是被转换为成本敏感的常规分类算法。我们可以从一开始就把整个算法写成成本敏感的，而不是那样做。这些被称为**直接**方法。

例如，考虑均方误差函数。对于二元分类，如果预测是错误的，误差将是(1–0)= 1 或(0–1)= 1。换句话说，这个误差函数对于假阳性和假阴性给出了相同的值。我们可以修改这个误差函数，为假阳性和假阴性返回两个不同的值，然后在我们的算法中使用新的误差函数。我们不再需要进行阈值处理或重采样，因为成本敏感性现在已经内置。

对成本敏感的方法也不仅仅是区分假阳性和假阴性。有些情况下需要更精细的细节。考虑一个问题，我们在一组对象上近似一些函数，但是对象本身被分成 10 个子组。每个子组具有不同的重要性，这意味着每个子组在总误差函数中具有不同的权重。在最极端的情况下，训练集中的每个单独的例子都有可能具有唯一的权重。

在本文中，我们概述了成本敏感的学习方法。我们首先研究了元学习成本敏感的方法，如阈值和重采样。这些方法采用常规学习算法，并将其转换为成本敏感型。我们还引入了直接方法，例如直接修改成本函数以包括成本敏感性。请留下任何问题/评论，感谢阅读！