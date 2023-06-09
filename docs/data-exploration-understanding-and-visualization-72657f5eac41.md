# 数据探索、理解和可视化

> 原文：<https://towardsdatascience.com/data-exploration-understanding-and-visualization-72657f5eac41?source=collection_archive---------7----------------------->

## 生成可视化效果以快速理解您的数据

![](img/571f69d61f94ab5d36fa46dc1c26b161.png)

卢克·切瑟在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

D 数据探索、理解和可视化是数据科学问题的一个重要方面。在这里，我提供了几种方法来简化这个过程。

数据探索和可视化是数据科学问题的一个重要方面。最好的可视化总是与手头的问题相关，并利用领域知识。然而，作为一名数据科学家，你会发现自己经常重复许多相同的可视化。

**在这篇文章中，我生成了一系列可视化效果，您可以复制并粘贴这些效果来解决您的数据科学问题，从而简化您的工作并理解您的数据。**

## 部分

这些部分是根据用于探索的可视化类型来划分的:

*   相关热图
*   按特征分类分布
*   二维密度图。

所有的**可视化都是交互式的**，这是 Plotly 的标准。

本文的数据是 scikit-learn 乳腺癌数据集。但是，如果您创建一个数据框架，其中的目标变量被列为可视化的“目标”,则您可以将这些变量应用到您的数据中。

## 热图

第一种方法是简单的热图，描述特征和目标变量之间的相关性。

这些关联热图包含一条实线对角线，代表每个功能与其自身的关联。这些图旨在快速识别非对角线值中显示的高度相关的特征。

## 按类别的特征分布

第二种方法是按类分解特征分布。有了这些分布，您可以结合行业知识来识别异常和类别分离。

Plotly 还可以选择显示一维密度图，并将其添加到密度图中。这得益于显示每个单独的实例，而不是密度图中的汇总版本。

## 2D 密度图

最后展示的是一个二维密度图。这些图更复杂，因为它们需要选择和显示成对特征的组合。

在提供更多信息的同时，展示每一对都扩大了产生的图形的数量。这些类似于之前的密度图，但是它们更详细地揭示了类之间的分离。

根据二维图的性质，您的问题可能需要更复杂的模型来支持有效的分类。

# 特征相关热图

关联热图是快速识别与其他要素高度相关的要素的好方法。这些图揭示了那些与目标变量最相关的特征，这些特征可以作为特征选择过程来选择。

数据帧的关联热图(由作者编码)

然而，更重要的是**识别相关特征的极端情况。**

根据要素的布局，很难快速识别高度相关的要素。但是这些相关性在特征具有来自色标的相同极端颜色的区域中是可见的。

## 要找什么

高度相关的特征，无论是正相关还是负相关，都会影响您的模型。**这些高度依赖的特性会通过在特性集中添加冗余来影响模型有效建模**数据的能力。

简单地说，它们分散了你的模型学习它需要知道的东西的注意力，因为它必须不止一次地处理相同的信息。

此外，当特征与目标变量不相关时，这些特征有可能是噪声。这些噪声变量也可能对模型的整体性能有害。

**本质上，你的模型使用噪声变量没有任何好处。至少，你的模型需要学会忽略这些嘈杂的变量。当存在大量低相关性特征时，请认真考虑特征选择。**

因此，在第一次视觉化之后，你已经可以指导你的下一步了。识别并消除冗余和噪声变量。

数据框架的关联热图(由作者绘制)

# 按类别划分的特征分布

第二种方法是按类分解特征分布。在这里，您可以开始整合行业知识并**识别每个特征的异常。**

例如，如果年龄是一个特征，那么负年龄就不是一个准确的值。这些情况可以从特征分布中快速识别出来。同样，行业知识可以提供每个特性的更多细节。但是，这些将更多地视情况而定。

按类的特性分布(按作者的代码)

这些图还指示应该实现什么类型的缩放。根据您计划使用的模型，这是使模型有效的关键步骤。

顺便提一下，一些模型对不同的特征尺度更有弹性。例如，基于树的模型或多或少与规模无关。但是，在许多其他情况下，缩放数据可以将指数分布转换为均匀或正态分布，并更好地符合模型预期。

## 重新缩放问题

许多缩放方法需要知道特征分布中的临界值，并可能导致数据泄漏。例如，最小-最大缩放器应该只适合训练数据，而不是整个数据集。当最小值或最大值在测试集中时，您已经减少了一些数据泄漏到预测过程中。

## 直方图具有误导性

每个分布下方显示的一维频率图有助于理解数据。乍一看，这些信息似乎是多余的，但是这些信息直接解决了以直方图或分布形式表示数据时的问题。

例如，当数据被转换成直方图时，仓的数量被指定。仓太多很难破译任何模式，仓太少会丢失数据分布。

此外，将**数据表示为分布假设数据是连续的**。当数据不连续时，这可能表示数据中存在错误或关于要素的重要细节。一维频率图填补了直方图失效的空白。

按类别的特征分布(按作者绘制)

# 二维密度图

二维密度图结合了先前密度图的各个方面和第一次可视化中的相关热图。

但是这些可视化的代价是，当组合来自多个特征的信息时，有许多配置。

此外，当比较成对的特征时，可能性的复杂性急剧上升，因为特征的每种排列都是可能的。

二维密度图(作者代码)

Plotly 通过“figure_factory”模块为二维密度可视化提供内置功能。

该功能易于实施，分为两个系列，有标记颜色和尺寸选项。同时使用颜色和大小似乎有些问题，但是定义的函数实现了这两个选项。

可视化还利用相关性来限制特征对的大小。默认情况下，我只显示与目标变量最相关的 k 个特性。然后为可视化生成所有特征对的集合。

## 显示两个以上维度的信息

二维可视化无法显示我们的模型可能捕捉到的更高维度的关系。但是，当局限于二维空间时，人们可以创造性地用形状和颜色来显示数据的其他方面。

在这种情况下，我利用标记的形状来表示类别，用等高线来表示频率。以更高维度表示数据可以获得更多信息，但代价是很难快速理解这些模式。

二维是一个合理的限制，这样即使有大量的信息，可视化仍然容易理解。

二维密度图(作者绘制)

# 包裹

这篇文章展示了几种不同的可视化方法，用于理解数据中存在的要素。

开发模型时，一切都从数据开始。因此，有效的数据理解对于设计有效的模型至关重要。这些可视化为您的数据提供了大量的洞察力，并且易于重现。

这篇文章旨在展示一个预测建模项目的几个可视化功能以及目标模式。

您可以随意复制和粘贴这些函数，以供将来使用。

如果你有兴趣阅读关于新颖的数据科学工具和理解机器学习算法的文章，可以考虑在 medium 上关注我。

*如果你对我的写作感兴趣，想直接支持我，请通过以下链接订阅。这个链接确保我会收到你的会员费的一部分。*

<https://zjwarnes.medium.com/membership> 