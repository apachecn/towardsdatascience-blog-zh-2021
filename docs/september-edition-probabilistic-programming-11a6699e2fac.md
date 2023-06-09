# 九月版:概率编程

> 原文：<https://towardsdatascience.com/september-edition-probabilistic-programming-11a6699e2fac?source=collection_archive---------24----------------------->

## [月刊](https://towardsdatascience.com/tagged/monthly-edition)

## 模拟我们周围高度复杂的世界

![](img/3b9a36f2a22a5b6ef23266c29027c76d.png)

照片由来自[佩克斯](https://www.pexels.com/photo/close-up-photo-of-person-holding-lensball-2534493/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)的[麦克·穆林斯](https://www.pexels.com/@mac-mullins-1319876?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)拍摄

我们是一个不可思议的物种:我们对周围的世界非常好奇，喜欢学习，并经常找到新的方法和工具来做这件事。过去几十年中的一个进步就是计算。通过改进计算引擎的架构，我们在模拟复杂动态、列举大量潜在结果以及对大量可能性进行快速计算方面做得更好了。所有这些事件都推动了我们对周围世界的理解。特别是机器学习(ML)为我们提供了一套高度灵活和强大的工具来预测、理解和推理未来。虽然目前最先进的方法在第一个目标上表现出色，但在后两个目标上进展缓慢。其中一个原因是视角。世界本来就很复杂。

此外，事件或结果通常是众多因素之间非线性相互作用的结果。通常，我们并不掌握影响因素的完整列表的信息，也不知道它们如何相互作用以产生观察到的结果。这些属性使得预测现实世界的事件变得极其困难。ML 社区已经使用两种根本不同的模型构建范例来应对这一挑战。它们是:

1.  区别的
2.  生殖的

我们在学校学到的和在新闻中听到的大多数模特都属于歧视型。这个框架的主要焦点是预测的准确性。观察到的数据引导关系发现过程，而不是对因素如何相互作用强加严格的假设。在这种范式下训练的深度神经网络已经在各种各样的任务上取代了人类水平的表现，主要是因为强调预测的准确性。虽然这非常令人印象深刻，但这些模型有其局限性。特别是，高度精确的网络非常复杂，需要大量的训练数据才能达到人类水平的性能。通常，这些模型用可解释性来换取卓越的性能。这个方面有好有坏。

一方面，我们希望对未来有非常准确的预测。精确使我们在面对不确定的结果时能够做好计划并茁壮成长。然而，难以解释的模型招致了很多怀疑，并疏远了人们。这种信任的缺乏缩小了这些强大算法的使用范围。复杂性也让我们很难对未来进行推理。如果我选择路径 A 而不是路径 B 会发生什么？路径 B 比路径 A 短吗？统计学家已经开发了一个广泛的工具包来回答这些问题。在辨别范式下这样做是很棘手的，因为这种思维模式并不试图明确地模拟内在的不确定性。

生成范式正好解决了这一困境。这一学派主张对世界做出假设，而不是回避它。任何上过统计学入门课的人都知道，统计模型允许我们给不确定性一个函数形式。这些模型让我们对自己的预测充满信心。他们让我们假设潜在的结果。诸如此类的活动使我们能够思考未来，并根据新信息做出决策。每个 stats 101 的学生也知道，所有这些模型经常做出严格的假设。有时这些假设被违反，有时它们就是完全错误的。

更糟糕的是，这些模型中的一些并不能很好地近似真实世界的现象。这一缺点主要是由于这些模型不能适应可能影响感兴趣的结果的多个潜在变量。虽然你，读者，现在可能想认输，但我劝你不要。生成模型师也对构建糟糕的世界近似持谨慎态度。然而，与他们的歧视性同行不同，他们融合了计算机科学、统计学和软件工程的概念来解决上述问题。其结果是一类被称为概率图形模型(PGM)的模型。

这些图表允许我们使用尽可能多的变量来模拟我们周围高度复杂的世界。它们让我们将一些、许多或所有这些变量相互联系起来。它们还为我们提供了确定信息如何在网络中流动的灵活性。信息应该从节点 A 传到节点 B 还是从节点 B 传到节点 A？也许我们没有具体说明，因为我们对信号应该如何通过我们的近似世界流动没有强烈的信念。PGM 的强假设允许他们建立稀疏模型。这些假设也使这些网络能够用比判别模型少得多的数据点进行学习。这些特征类似于人类形成一个世界如何运转的心理图像，并对其进行查询以确定如何在不熟悉的环境中行为。

除了建立精确的模型，另一个阻碍 PGMs 广泛应用的挑战是计算。存储大量随机变量的分布并更新它们的分布在计算上是禁止的。这些限制往往是 PGM 如何使用当前的编程语言和数据结构编码的产物。因此，从业者开发了一种新的编程范式，称为概率编程，以规避这些问题。这些语言将随机变量和概率分布视为一等公民。由于这些发展和该领域中一系列相关的发展(例如变分贝叶斯)，越来越复杂的 PGM 变得更容易构建。这些创新还减少了查询这些模型和推理潜在行动过程的时间。

近来，生成模型还没有像判别模型那样受到关注。我希望这篇介绍能鼓励你们所有人看看这种不同的思维框架。如果你想更深入地了解这个话题，我强烈建议你去看看一些关于这个话题的精彩文章。

[Abdullah Farouk](https://medium.com/u/ea00177500c1?source=post_page-----11a6699e2fac--------------------------------) ，*TDS 的志愿编辑助理*

## [概率图形模型介绍](/introduction-to-probabilistic-graphical-models-b8e0bf459812)

有向图形模型和无向图形模型

到[布拉尼斯拉夫·霍兰德](https://medium.com/u/cb9a2fa1a025?source=post_page-----11a6699e2fac--------------------------------) — 11 分钟

## [让你的神经网络说“我不知道”——使用 Pyro 和 PyTorch 的贝叶斯神经网络](/making-your-neural-network-say-i-dont-know-bayesian-nns-using-pyro-and-pytorch-b1c24e6ab8cd)

当一个人不确定的时候，很大一部分智慧是不行动的

由 [Paras Chopra](https://medium.com/u/ce4d7f282c52?source=post_page-----11a6699e2fac--------------------------------) — 17 分钟

## [生成性与鉴别性概率图形模型](/generative-vs-2528de43a836)

朴素贝叶斯和逻辑回归的比较

由[四维引起维克](https://medium.com/u/301dc9114da0?source=post_page-----11a6699e2fac--------------------------------) — 5 分钟

## [变分贝叶斯:变分自动编码器(VAEs)背后的直觉](/variational-bayes-4abdd9eb5c12)

了解推动最先进模型的强大理念

到[安维斯·马尔韦德](https://medium.com/u/4bcb754eb66?source=post_page-----11a6699e2fac--------------------------------) — 7 分钟

## [概率编程简介](/intro-to-probabilistic-programming-b47c4e926ec5)

使用张量流概率(TFP)的用例

由[法比亚娜·克莱门特](https://medium.com/u/f957353899a?source=post_page-----11a6699e2fac--------------------------------) — 6 分钟

## [概率推理的基本问题](/fundamental-problems-of-probabilistic-inference-b46be1f96127)

如果你是机器学习从业者，为什么要关心采样？

作者:Marin Vlastelica pogan ii—6 分钟

我们也感谢最近加入我们的所有伟大的新作家:[奥辛·杜塔](https://medium.com/u/d6cc8b2f4d83?source=post_page-----11a6699e2fac--------------------------------)、[雷纳托·菲林尼奇](https://medium.com/u/45c682a44b92?source=post_page-----11a6699e2fac--------------------------------)、[奥姆里·卡杜里](https://medium.com/u/bdd98c8f5e5d?source=post_page-----11a6699e2fac--------------------------------)、[陈莉莉](https://medium.com/u/8c4ed724d89d?source=post_page-----11a6699e2fac--------------------------------)、[本·威廉姆斯](https://medium.com/u/348277337eba?source=post_page-----11a6699e2fac--------------------------------)、[伊恩·加贝尔](https://medium.com/u/c1f02b4cdd2b?source=post_page-----11a6699e2fac--------------------------------)、[乔纳森·拉塞尔森、博士](https://medium.com/u/56d1c8006910?source=post_page-----11a6699e2fac--------------------------------)、[乔安娜·伦丘克](https://medium.com/u/a1797fa50e3a?source=post_page-----11a6699e2fac--------------------------------)、[恰冲](https://medium.com/u/979f90d1d0cd?source=post_page-----11a6699e2fac--------------------------------)、[胡曼·阿布·阿尔拉贾](https://medium.com/u/ffb6117848cc?source=post_page-----11a6699e2fac--------------------------------) [佩德罗·布里托](https://medium.com/u/ab311ef28c08?source=post_page-----11a6699e2fac--------------------------------)，[丹尼斯·冯](https://medium.com/u/8f37637cb451?source=post_page-----11a6699e2fac--------------------------------)，[周扬](https://medium.com/u/ab8db76f5314?source=post_page-----11a6699e2fac--------------------------------)，[戴夫·德卡里欧](https://medium.com/u/96c0759c980?source=post_page-----11a6699e2fac--------------------------------)，[阿奇特·亚达夫](https://medium.com/u/c6d1f756f2d4?source=post_page-----11a6699e2fac--------------------------------)，[贾·一禅](https://medium.com/u/6136a4072f92?source=post_page-----11a6699e2fac--------------------------------)，[阿尔帕纳·梅塔](https://medium.com/u/c484705e735?source=post_page-----11a6699e2fac--------------------------------)，[拉胡尔·桑戈莱](https://medium.com/u/575baa0e041c?source=post_page-----11a6699e2fac--------------------------------)，[阿南亚·巴塔查里亚](https://medium.com/u/57cce684289b?source=post_page-----11a6699e2fac--------------------------------)，[罗汉·苏库马兰](https://medium.com/u/4e9f21318991?source=post_page-----11a6699e2fac--------------------------------)， <https://medium.com/u/4e9f21318991?source=post_page-----11a6699e2fac--------------------------------> [杰克·米切尔](https://medium.com/u/3d9ea428abd9?source=post_page-----11a6699e2fac--------------------------------)、[z·玛利亚·王博士](https://medium.com/u/9ae0925c6ef7?source=post_page-----11a6699e2fac--------------------------------)、[丹尼斯](https://medium.com/u/6e5946e53b95?source=post_page-----11a6699e2fac--------------------------------)、[南阮](https://medium.com/u/3db9e6680953?source=post_page-----11a6699e2fac--------------------------------)、[琪·市川](https://medium.com/u/8e797d0e0840?source=post_page-----11a6699e2fac--------------------------------)、[林赛·蒙塔纳里](https://medium.com/u/d186712ca417?source=post_page-----11a6699e2fac--------------------------------)、[戴维斯·特雷比格](https://medium.com/u/b2a36e2f3cc4?source=post_page-----11a6699e2fac--------------------------------)、[瓦妮莎·王](https://medium.com/u/27ce3ac93d70?source=post_page-----11a6699e2fac--------------------------------)、[普亚·阿米尼](https://medium.com/u/203a584aebef?source=post_page-----11a6699e2fac--------------------------------)、 [我们邀请你看看他们的简介，看看他们的工作。](https://medium.com/u/67ea5d79b73e?source=post_page-----11a6699e2fac--------------------------------)