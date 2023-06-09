# 深度学习可能还不是所有 NLP 任务的银弹

> 原文：<https://towardsdatascience.com/deep-learning-may-not-be-the-silver-bullet-for-all-nlp-tasks-just-yet-7e83405b8359?source=collection_archive---------38----------------------->

## [自然语言处理](https://towardsdatascience.com/tagged/nlpnotes)

## 为什么你仍然应该学习启发式和基于规则的方法

![](img/4168fba3d467d11bf5965e9fefc2807e.png)

由[蒂莫西·戴克斯](https://unsplash.com/@timothycdykes?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

## 介绍

深度学习；解决人类问题的方法。在过去的几年里，深度学习以新颖的方式推进了人类。这些受益者之一是整个自然语言处理领域(NLP)。但在我们进入如何之前，让我们探索一下深度学习领域。

我很确定我们都见过维恩图，它说明了人工智能(AI)与机器学习(ML)和深度学习的关系。如果不是，它只是证明了深度学习是机器学习的一个子领域，而机器学习是人工智能的一个子领域。

深度学习与机器学习的不同之处在于，它涉及基于人脑的结构和功能开发的算法——这些结构和功能被称为**人工神经网络**。

## 深度学习如何推进 NLP

软件行业的大部分正在转向机器智能或数据驱动的决策，但其他行业也注意到了它的影响，并对此感兴趣，如医疗保健行业。人工智能发展的一个很好的原因可以归结为机器学习和深度学习(当然还有其他使执行这些任务成为可能的因素)，然而，近年来深度学习越来越受欢迎，因为它在准确性等指标方面占据优势，并且当我们有大量数据来支持我们的深度学习算法时。

例如，在文本分类任务中，基于递归神经网络(RNN)的模型已经超过了标准机器学习技术的性能水平，这些技术曾经由革命性的机器学习模型解决，如[朴素贝叶斯分类器](/algorithms-from-scratch-naive-bayes-classifier-8006cc691493)和[支持向量机](/algorithms-from-scratch-support-vector-machine-6f5eb72fce10)。此外，LSTMs(它是 rnn 家族的一部分)在序列标记任务(如实体提取)中胜过条件随机场(CRF)模型。

最近，镇上有一个新的话题叫做变形金刚模型。Transformer 模型非常强大，已经成为大多数自然语言处理任务的最新模型。深入研究 transformer 模型的细节超出了本文的范围，但是如果您希望我在后面的教程中介绍它，请留下您的回复。

## 坠落

尽管深度学习取得了巨大的成功，但它仍然不是每个自然语言处理任务的灵丹妙药。因此，当面对 NLP 中的问题时，实践者不应该急于构建最大的 RNN 或转换器，原因如下:

***过拟合***

深度学习模型往往比传统的机器学习模型有更多的参数。因此，深度学习模型比传统模型具有更强的表达能力，这也是它们如此强大的原因。它如此强大的原因也是它最大弱点的来源。许多深度学习模型倾向于过度拟合小数据集，因此导致泛化能力差，这导致生产中的糟糕性能。

***缺乏少投学习技巧***

我通常不会比较，但在这种情况下，我们必须比较；看一看计算机视觉领域。深度学习在 CV 方面取得了很大的进步，因为一些技术，例如少量学习(例如，从很少的实例中学习)，这导致了更广泛地采用深度学习来解决现实世界的问题。在 NLP 中，我们只是没有看到类似的深度学习技术以与计算机视觉相同的方式被成功采用。

***域适配***

当我们没有大量训练数据时，迁移学习对于提高深度学习模型的性能来说是革命性的。然而，利用在公共领域训练的深度学习模型，例如报纸文章，然后将其应用到更近的领域，如社交媒体帖子，可能会导致我们的深度学习模型的整体性能不佳。更简单但仍然非常有效的解决方案可能涉及传统的机器学习模型或特定领域的基于规则的模型。

***可解释性***

可解释性是近年来变得突出的东西——它是有意义的。你难道不想知道为什么你会被拒绝贷款吗？虽然有一些技术正在开发中，试图解释深度学习模型，但在很大程度上，它们像黑盒一样工作。在这种情况下，使用像朴素贝叶斯模型这样的技术可能更有用，这种技术可以很容易地解释为什么进行某种分类。

***成本***

成本很重要；用深度学习构建解决方案可能在时间和金钱方面都非常昂贵。与 Kaggle 不同，真实世界中的数据集不会被标记，并且不要忘记，我们需要一个大的数据集来保证我们的模型不会过度拟合。收集和标注大型数据集可能非常耗时，然后继续部署模型并在生产中维护它，在硬件要求和工作量方面可能非常昂贵。

## 最后的想法

这绝不是为什么深度学习可能还不是 NLP 任务的银弹的详尽列表，但它提供了现实世界项目中可能出现的场景类型的真实感觉。这些症状经常导致项目周期比它需要的要长得多，更不用说项目上线和交付后维护的更高成本了。此外，相对于传统的机器学习模型，性能的提高通常不是非常显著(即，如果有的话，准确性没有很大的提高)。

感谢您的阅读！在 LinkedIn 和 T2 Twitter 上与我保持联系，了解我关于数据科学、人工智能和自由职业的最新消息。

## 相关文章

</combating-overfitting-in-deep-learning-efb0fdabfccc>  </4-data-related-books-ill-be-reading-in-april-efd06b367e35>  </5-ideas-for-your-next-nlp-project-c6bf5b86935c> 