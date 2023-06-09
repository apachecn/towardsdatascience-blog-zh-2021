# 缺失的值将消失

> 原文：<https://towardsdatascience.com/missing-values-be-gone-a135c31f87c1?source=collection_archive---------37----------------------->

## 处理数据集中缺失值的策略。

![](img/1042157319a93d380c8011b7ff174469.png)

照片由[在](https://unsplash.com/@thecreative_exchange?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) [Unsplash](https://unsplash.com/s/photos/clean?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的创意交流

清理数据是几乎所有数据项目的必要组成部分。数据清理的一个常见主题是处理不完整的样本。插补有多种选择，每一种都有其好处和风险。我将介绍几个我喜欢使用的标准选项，然后讨论选择插补策略时的重要考虑因素。

**策略 1 —丢弃脏样品**

这是最直接的方法，也是我遇到的最常见的方法之一。删除包含缺失值的行。事实上，作为我最初的 EDA 步骤的一部分，我经常选择这样做来获得一些关于我的数据看起来像什么的基线图。然而，这牺牲了你的一些宝贵的数据！在大多数情况下，这不是一个很好的策略，因为您正在减少用于得出结论或训练模型的信息总量。

**策略#2 —用 0 替换缺失值**

这是我看到人们采取的另一个简单策略；然而，我认为这几乎不合适。用常数替换缺失值是一个不错的选择，但是，这个常数不应该总是 0。这里的问题是，在大多数情况下，0 是一个任意的选择，并不反映数据集试图描述的实际情况。这里有一个警告，如果你已经将你的数据归一化到平均值为 0，那么 0 是一个很好的选择。(看下一个策略！)

**策略# 3——用平均值替换缺失值**

这比用 0 这样的任意值替换丢失的值要好得多。这是因为样本都分布在该值周围，如果缺失值没有缺失，它很可能位于平均值附近。在我看来，这是最简单的方法。此外，请记住，这里有不同的可能的平均值。通常，插补的一个好选择是该列的总体平均值。但是，在处理时间序列数据时，您可以使用该特征的个体平均值。

**策略 4——用线性模型代替缺失值**

这种策略适用于时间序列数据。有时，当您的数据有趋势时，每个个体的平均值通常不适合插补。这是因为它没有考虑那个变量随时间的变化！但是，用简单的线性回归模型拟合数据将会估算(和外推)时间序列的数据点。不幸的是，当您的数据集显然没有描述线性趋势时，这就没什么用了。

**策略# 5——用多项式模型代替数值**

同样，这也是时序数据集的一个选项。在前面的策略中，我们讨论了使用线性模型进行插补和外推，我们可以通过使用多项式模型来进一步扩展这一概念。这允许我们估算非线性趋势的值！

**策略 6 —使用聚类替换值**

输入值时的另一个有效选项是使用无监督学习技术(如聚类)来识别个人属于数据集的哪个子组，从而对要输入的值做出明智的决定。我已经在 K-means 聚类中成功地使用了这种策略，最近又在相似性传播中使用了这种策略。相似性传播是识别代表每个聚类中心的样本的聚类技术。使用这个中心样本会给你一些平均值的概念，用于该组其他成员的插补。

**策略# 7——用其他机器学习模型代替价值观**

我想你可以开始看到一个熟悉的模式。有无数其他有效的机器学习(ML)模型可以用于此目的。我不会把它们一一列出来，我会把这个策略作为一个总括。请记住，在为此目的选择机器学习模型时，您必须仔细了解该模型的工作原理，以及它可能通过插补向您的数据集引入什么样的偏差。

![](img/47b5743a260550c9a2a137a7176965ea.png)

缺失值消失！| GIF from: [Giphy](https://giphy.com/gifs/hero0fwar-iasip-glenn-howerton-dennis-reynolds-pGfeUvh4hnoKnJ9JkW)

在处理插补时，还有其他重要的考虑因素。一个大问题是稀疏性，以及您处理的实际缺失数据有多少。在有大量缺失数据的情况下，像均值插补这样的方法通常不是一个好的选择。它极大地改变了数据集的方差，并导致分布不再代表数据集编码的基础概念。我觉得线性/多项式/ML 建模在这些情况下是更好的选择，因为它们估算了一系列值。虽然它们很少与基础数据集的实际方差相匹配，但它们将大大减少在稀疏数据集上使用均值插补等方法获得的巨大峰度。

当你希望将多项式模型用于插补和外推时，它有一个明显的缺点。高阶多项式倾向于在你适合它们的区域之外向无穷远处发射。这意味着您的推断值很有可能不代表实际趋势。当然，这是你可以想象的，所以不要完全排除这个选项，只要记住在你想要推断的整个领域检查这个模型发生了什么是很重要的，而不仅仅是你适合的领域。

有时，如果您清理这些数据的目的是构建一个机器学习模型，您可能根本不需要清理这些值！现代的 ML 模型有时可以把缺失的信息当作一个独立的特征。例如，LightGBM 在内部使用缺失值作为模型信息的一部分！

缺失值是我们数据科学家永远不得不面对的问题。我希望这篇文章有助于阐明这个问题的复杂性，并为您了解如何管理它们的旅程提供一个起点。祝你好运，编码愉快！

<https://pandas.pydata.org/>  <https://scikit-learn.org/stable/>   