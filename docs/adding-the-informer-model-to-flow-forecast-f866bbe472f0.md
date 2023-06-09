# 在流量预测中加入信息员模型

> 原文：<https://towardsdatascience.com/adding-the-informer-model-to-flow-forecast-f866bbe472f0?source=collection_archive---------22----------------------->

## Informer 是一个用于长序列时间序列预测的新转换模型，在 AAAI 会议上获得了最佳论文奖。

## 介绍

![](img/d995c10898bcfe25c575af3ed10ecadd.png)

[图片来自文章](https://arxiv.org/abs/2012.07436)

变形金刚彻底改变了自然语言处理，并推动了神经机器翻译、分类和命名实体识别等领域的重大进步。最初，变形金刚在时间序列领域发展缓慢。然而，在过去的一年半时间里，出现了许多用于时间序列分类和预测的转换变量。我们已经看到了像时间融合转换器、卷积转换器、双阶段注意力和更多尝试进入时间序列的模型。最新的模型 Informer 建立在这一趋势的基础上，同时融入了几个新颖的组件。

[Flow Forecast](https://github.com/AIStream-Peelout/flow-forecast/issues) ，PyTorch 内置的时间序列预测和分类库深度学习，已经支持 transformer 的几个变体，但我们决定特别添加 Informer，因为它改善了内存使用，预测长期序列的能力，以及整体更快的推理速度。

Informer(作者、周、张上航、、彭、、、张万才)旨在改善自我注意机制，减少内存使用，加快推理速度。Informer 同时利用了变压器编码器和(屏蔽的)变压器解码器层。解码器可以在单次前向传递中有效地预测长序列。这个特性有助于在预测长序列时加快推理速度。告密者模型采用概率注意机制来预测长序列。Informer 还包括相关时间特征的学习嵌入。这允许模型生成有效的基于任务的时间表示。最后，Informer 同样可以根据任务的复杂性堆叠 n 层编码器和解码器。

## 概率与完全注意力

作者引入了一种概率性注意来降低自我注意的时间复杂度。与传统的 O(L)相比，这种概率注意力机制实现了 O(L log L)复杂度。传统的自我注意存在这样的问题，即只有几个关键值对对注意分数起主要作用。这意味着大多数计算出来的点积实际上毫无价值。prob 稀疏注意允许每个键只关注主要的查询而不是所有的查询。这允许模型只计算一小部分查询/值张量的昂贵运算。具体来说，ProbSparse 机制还有一个可以指定温预测的因素。该因子控制你减少多少注意力的计算。

## 基准数据集

作者对几个主要与电力预测相关的时间序列数据集进行了基准测试:具体来说就是电力变压器和用电负荷。他们测试预测几个不同时间间隔的数据的模型，包括他们还在天气预测数据集上测试模型。他们使用 MSE 和 MAE 作为他们的评估指标，并将 Informer 的性能与其他几个 transformer 变体以及流行的 LSTM 模型进行比较。

![](img/1786ba1646d833b2a1279e50cbd4eba4.png)

论文的结果。ETT(电力变压器温度)和 ECL 用电负荷。

## 将模型移植到流量预测中

尽管与我们的完整 transformer 模型和 Informer 有相似之处，但是出于几个原因，将模型移动到我们的框架中是具有挑战性的。最大的问题与我们的训练循环和数据加载器如何将数据传递给模型有关。因此，重构核心功能花费了相当多的时间

我们总共做了以下调整

*   添加了解释核心组件的详细文档字符串
*   重构了几个函数来提高代码的整洁度和架构
*   像其他流量预测模型一样，允许多目标交换

我们仍在努力验证该模型使用我们的格式再现了原始论文的结果。然而，我们希望尽快完成这项工作。

## 流量预报中线人的使用

我们现在有几个关于如何在流量预测中使用 Informer 进行时间序列预测的教程。你可以访问这个 [Kaggle 笔记本](https://www.kaggle.com/isaacmg/pytorch-time-series-forecasting-with-the-informer)获得使用 Informer 的快速教程(有和没有 Wandb 都可以)。或者，您可以通过 Informer 查看该笔记本，进行全面的超参数扫描。如果您喜欢使用自己的训练循环和函数，也可以使用 Python API 直接使用 Informer。

一如既往，请留下任何意见或其他问题！