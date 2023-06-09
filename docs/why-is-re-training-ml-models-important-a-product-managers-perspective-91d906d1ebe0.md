# 为什么重新训练 ML 模型很重要？

> 原文：<https://towardsdatascience.com/why-is-re-training-ml-models-important-a-product-managers-perspective-91d906d1ebe0?source=collection_archive---------30----------------------->

## 产品经理的视角

作为产品经理，你有责任衡量你的产品的*持续*成功。这可能包括启动前的验证、启动时测量 A/B 测试中的提升，以及跟踪核心 KPI。如果你正在管理一个机器学习产品，你的产品的长期成功将取决于保持你的模型是最新的。在这篇文章中，我将解释为什么这是一个重要的问题，以及如何通过模型再训练来确保持续的成功。

![](img/33bd42b232a6e24eeaf14df697967458.png)

如果你不训练你的 ML 模型，它会恶化到你再也不知道发生了什么的地步！(作者未命名的拼贴画，2020 年)

# 为什么您应该重新培训您的 ML 模型

ML 模型依赖于数据来“理解”特定的问题，并生成期望的输出。在大多数情况下，您的模型所依赖的数据会逐渐改变；例如，由于用户偏好的变化，也由于产品的性质而发生巨大变化；例如，由于黑色星期五这样的销售活动，或与 COVID 相关的旅行限制。由于系统中不可预见的变化，数据也可能发生变化，例如在没有预先通知的情况下，货币从美元兑换为美分的方式发生了变化。

在这篇文章中，我将使用两个你可能熟悉的例子。一个推荐歌曲的产品，一个从照片中检测植物种类的产品。我将解释这两个例子对于模型重新训练的不同之处。

# 你不知道你不知道什么

你应该知道你的模型是如何执行的，所以在投资模型再训练之前，确保你的 ML 系统(不仅仅是模型)有监控，使你能够看到性能是否随着时间的推移而下降。没有这些关键信息，你根本不知道你可能会遇到多大的问题——这应该是非常可怕的！👻

*   因为大多数模型依赖于这样一个前提，即他们在训练期间看到的数据的分布与他们将来会看到的数据相同，所以监控*特征漂移*对于何时重新训练是一个很好的指示。
*   监控*预测漂移*或*预测精度*可能是重新训练需求的一些最佳指标，因为这些指标衡量了模型的输出如何随着时间的推移而变化和执行。
*   ML 模型并不是孤立存在的，因此从用户体验的角度来衡量模型的输出非常重要——如果您想了解更多关于这个主题的信息，我强烈推荐来自 ACM RecSys'18 会议的 [Lina Weichbrot](https://twitter.com/rmminusrslash?lang=en) [“衡量建议的运营质量”](https://www.youtube.com/watch?v=UKa87yQr2es)的这个非常有趣的演讲。

# 决定多长时间重新培训一次您的 ML 模型

一些模型可以处理看不见的值并做出很好的预测，而一些模型在这方面有很大的麻烦。如果您的数据变化非常快，您可能希望构建一个能够很好地处理未知值的模型，并比数据变化缓慢时更频繁地重新训练。这对于推荐系统来说尤其重要。

从照片中检测植物物种的应用程序可能会使用颜色和形状检测器作为区分植物的特征。因为~ [每年有 2000 种新的植物物种被发现和命名](https://www.bbc.com/news/science-environment-46621092)你应该确保你的系统能够识别最新的植物物种，方法是用这些植物的图像重新训练 ML 模型，并在新物种进入市场时更新你的模型。然而，如果你的产品是为研究人员设计的，它应该总是与最新的发现保持同步，以支持他们的研究。

对于有人类互动的系统，一个非常有趣的问题是行为的改变，以及理解你的模型如何处理它。我们称之为“*漂移*”。如前所述，行为改变可以是缓慢的、稳定的、可预测的，也可以是急剧的、意想不到的。例如，音乐品味随着人们的成长而改变，每年都有新的流派出现和流行，但有时一首歌会像病毒一样传播开来，每个人都在听它，或者又到了圣诞节，人们在世界的一些地方听圣诞颂歌；推荐音乐时，应该考虑这两种情况。

如果模型很容易更新，甚至完全更新其参数，并且与重新训练模型相关的成本很低；你可能会决定定期安排再培训，然后忘记这篇文章的其余部分。然而，当问题是一个高风险的问题，或者重新培训一个模型的成本非常高( [GPT-3 重新培训](https://lambdalabs.com/blog/demystifying-gpt-3/)可能花费 460 万美元)，优化你应该重新培训的频率可以让你赚很多钱或者为你节省很多钱！

同样，您可能希望进行参数网格搜索来为您的机器学习模型找到最佳参数集，您应该对模型进行时间感知评估，以在离线评估设置中定义重新训练频率参数(我在之前的中帖的[中谈到了离线评估)](https://productcoalition.com/offline-experimentation-in-machine-learning-teams-a9c74643ff98)

*   模型需要多少数据样本才能达到最佳性能？众所周知，对于大多数算法来说，拥有更多训练样本的投资回报会在某个点达到峰值。其他人可能需要数据。
*   旧数据怎么处理？你可以忽略它，或者让算法给它“较低的重要性”
*   当然，当模型已经 N 天没有被重新训练时会发生什么。

# 如何让你的模型保持最新？

根据您的需要，有三种主要方法可以使您的模型保持最新。

*   轻度更新，模型被重新训练，看到新数据，可能忘记一些旧数据。
*   当问题发生很大变化时，需要进行大量更新，因此需要再次重新计算模型参数。
*   有时数据变化相当大，所以是时候完全重新考虑你的模型，甚至创建一个新的；想想新冠肺炎式的改变。

# 通过自动化来避免人为错误

当然，让某人查看监视器并手动决定何时重新训练模型会非常昂贵，并且也容易出现人为错误。您应该为您的模型投资一个自动化管道，根据一个事件(一个指标的恶化)或者定期地重新训练它。我将在以后的文章中更详细地讨论这个话题。

# 当再培训不够时

我们希望重新训练一个模型能够解决所有与模型性能损失相关的问题。然而，情况可能并非如此，有时事情会出错。很多时候事情会出错，并可能引发错误警报。例如，由于跟踪中断，数据的分布可能会改变。可能会出现新的特性值，因为另一个团队更改了价格格式，并且忘记告诉您。在这些情况下，重新培训可能不是解决问题的正确方法，但适当的监控将帮助您快速发现问题。

总之，在这篇博客中，我强调了一些问题，在决定如何在周围的世界发生变化时保持模型的性能之前，你应该回答这些问题，你应该监控哪些指标来自动化或标记模型重新训练的需求，以及你可以做些什么来跟上变化。

由您决定 ML 模型应如何适应变化，并考虑(1)这样做的技术复杂性，(2)与保持更新相关的成本，当然还有(3)投资回报。我强烈建议投资监控作为起点，不要去了解你的问题是否存在，而是了解问题有多大，然后继续跟进。哦，安全第一