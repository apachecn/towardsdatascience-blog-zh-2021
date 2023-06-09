# 变压器的自定义回调函数

> 原文：<https://towardsdatascience.com/custom-callback-functions-for-transformers-ae65e30c094f?source=collection_archive---------24----------------------->

## 在为 NLP 任务微调预训练的变形金刚时，如何量化 F1-Score？

![](img/095c0c0558640c517da5175e001a37b1.png)

图片由 [Samule 孙](https://unsplash.com/@samule)在 [Unsplash](https://unsplash.com/)

## 介绍

自从 Vaswani 等人(2017)发表了[“注意力是你所需要的全部”](https://arxiv.org/abs/1706.03762)论文以来，变形金刚一直主导着自然语言处理(NLP)领域的最新进展，其中针对下游 NLP 任务微调预训练语言模型已经变得相当流行。如果你不熟悉变形金刚，这篇[文章](https://medium.com/inside-machine-learning/what-is-a-transformer-d07dd1fbec04)和这篇[文章](https://medium.com/geekculture/deep-learning-for-nlp-transformers-explained-caa7b43c822e)是很好的起点。Jay Alammar 的[图解示例](https://jalammar.github.io/illustrated-transformer/)也是一个很好的资源。

《变形金刚》库[由 Huggingface】🤗提供几个预先训练好的模型，以便于执行下游任务，如文本分类、文本生成、摘要、问答等。变形金刚库与最流行的深度学习平台 *Jax* 、 *PyTorch* 和 *TensorFlow* 兼容，并提供 API 来下载和微调预训练模型，并提供各种 NLP 任务的可用数据。](https://github.com/huggingface/transformers)

在为分类任务微调预训练模型时，我们通常使用诸如*损失* ( *二元交叉熵*或*分类交叉熵*等)和*准确度*等指标。然而，当数据不平衡时，我们通常会对模型训练期间和验证数据上的监控指标感兴趣，例如*精度*、*召回*和*F1-分数*。TensorFlow 的 *Keras* API 不会在每个时期结束时直接访问这些指标。简而言之，TensorFlow 2.0 中删除了这些指标，因为对每批进行评估会产生误导。然而，我们可以开发并利用一个定制的*回调函数*来量化每个时期结束时整个验证数据集的这些指标，这将在本文后面讨论。

## 什么是精度、召回率和 F1-score，如何量化？

在任何分类或信息检索任务中，当数据不平衡时，准确性可能不是性能评估的可靠度量。这就是精确度、召回率和 F1 分数被认为是模型性能评估的良好替代指标的地方。在分类的情况下，精度与 I 类误差或对目标类别的高估有关。回忆与第二类错误和低估目标类别有关。换句话说，高精度说明没有太多的误报，高召回说明没有太多的漏报。F1 分数是两者的调和平均值，因此非常有用，因为它很好地平衡了低高估和低低估。这篇 [TDS 文章](/accuracy-precision-recall-or-f1-331fb37c5cb9)提供了包括公式在内的进一步见解。

在 NLP 任务中，这些度量变得非常有用，例如当我们处理文本分类任务(以及其他任务)时，其中类别的比例严重不平衡，我们希望确保我们评估模型的方式能够指示所有类别的性能，而不仅仅是具有较高频率/比例的类别(与准确性不同！).

Python 的 [Scikit-Learn 库](https://scikit-learn.org/stable/modules/model_evaluation.html#classification-metrics)提供了计算这些指标的 API，包括多标签场景的选项。如下所示，当使用 F1_score 时，参数*‘average’*默认为’*binary*，它只报告由参数*‘pos _ label’*指定的类的结果。或者，参数*‘平均’*可以设置为*‘微观’*、*‘宏观’*、*‘加权’*或*‘样本’*。

根据 Scikit-Learn 关于 F1-score 的[官方文档，option *【微】*通过计算总的真阳性、假阴性和假阳性来计算全局指标。选项*‘宏’*计算每个类的度量，并找到它们的未加权平均值，其中它平等地对待所有类。选项*‘weighted’*计算每个类的指标，并根据每个类的实例数计算它们的加权平均值。这将改变*“宏”*以说明标签不平衡，并可能导致*F1-分数*不在精确度和召回率之间。最后，*‘samples’*计算每个实例的度量，并求出它们的平均值。Scikit-Learn 的 *precision_score* 和 *recall_score* 具有类似的平均选项。](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.f1_score.html)

在本文中，我们将*sk learn . metrics . f1 _ score*传递给一个 Keras 自定义回调函数，这样我们就可以维护所有平均选项的可选性。

## 微调变压器时计算 F1 分数的自定义回调

Keras 是用 Python 编写的深度学习 API，运行在 ML 平台 TensorFlow 之上。在 Keras 中，[回调](https://keras.io/api/callbacks/)是一个可以在训练的不同阶段执行动作的对象(例如，在每批训练后写 TensorBoard 日志，或者定期保存模型)。回调被传递给各种 Keras 方法(例如，fit、evaluate、predict ),因为它们与模型训练、测试和预测生命周期的各个阶段挂钩。

如上所述，对于精度、召回率和 F1 分数等指标，我们需要对整个数据集进行评估，而不是对任何一个批次进行评估，否则会产生误导。因此，我们可以使用历元级方法' *on_epoch_end(self，epoch，logs=None)'* ，其中 *logs* 字典包含丢失值，以及一个历元末尾的所有其他度量。此外，' *self.model'* 属性用于访问与当前一轮训练相关联的模型，该模型可用于对验证数据进行评估。下面是一个示例代码，使用全部验证数据，在每个时期结束时量化并打印出 F1 分数:

在上面的示例中，' __ *init__'* 方法在传递验证数据的同时实例化对象。接下来，' *on_epoch_end'* 方法在每个 epoch 结束时量化 F1 分数值，并填充 *logs* 对象。需要注意的是*。predict* 方法返回所有类的*逻辑值*(而不是类概率或类标签)。因此，我们需要应用 *Softmax* 函数将它们转换成概率。随后，我们应用 numpy 的 *argmax* 来指定具有最高概率的类作为预测标签。

[GitHub](https://github.com/amirhossini/Medium/blob/main/2021-11-Transformers_Custom_Callback_F1_Score/Example_Transformers_f1_score_Custom_Callback.ipynb) 上提供了一个工作示例，用于微调变压器(本例中为 DistilBERT ),同时在每个时期结束时计算整个验证数据集的 F1 分数。在这个工作示例中使用了一个[公共数据集](https://github.com/huggingface/datasets/tree/master/datasets/banking77)，其中训练集的一个子集用于微调，整个测试集被传递给*。将*方法作为验证集。然后，回调函数量化并报告验证集的 F1 分数以及每个时期结束时的损失和准确性:

![](img/285be377bca1a428e413f05e7bc1daf5.png)

作者图片

感谢阅读！请在 [GitHub](https://github.com/amirhossini) 上关注我，在 [LinkedIn](https://www.linkedin.com/in/amir-hossini-04086a53/) 上联系我，或者在 [Twitter](https://twitter.com/amirhs2000?lang=en) 上关注我，我会在那里发布我正在进行的工作和其他与数据科学相关的有趣文章！