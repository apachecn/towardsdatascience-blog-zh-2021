# 如何将产品目标框定为机器学习问题

> 原文：<https://towardsdatascience.com/how-to-frame-a-product-goal-as-a-machine-learning-problem-a3c55aeb75b2?source=collection_archive---------27----------------------->

## 降低处理机器学习项目的风险

![](img/3d17673392525707cb6bc5f3afd12386.png)

由 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上[罗兰兹·齐尔文斯基](https://unsplash.com/@rolzay?utm_source=medium&utm_medium=referral)拍摄的照片

有些事情最好通过经验来教。机器学习中的许多任务就是如此。机器学习允许我们从大量数据中学习，并使用数学公式通过优化给定目标来解决问题。相比之下，传统编程期望程序员编写一步一步的指令来描述如何解决问题。

> “ML 对于构建我们无法定义启发式解决方案的系统特别有用”
> 
> — Emmanuel Ameisen，构建机器学习驱动的应用。第三页。

尽管它很强大，但机器学习的一个主要警告是它引入了一定程度的不确定性，这在基于规则的系统中是预料不到的。这是因为机器学习是基于模式识别的。因此，重要的是要认识到产品的哪些方面可以从 ML 中获益，然后考虑如何制定一个学习目标来降低用户体验不佳的风险。

## 确定产品的可行性

机器学习能够解决一系列问题，但区分哪些问题是可解决的是极其困难的。由于我们无法预先确定一个 ML 项目是否会成功，我们最好的办法是降低处理这样一个项目的风险，最重要的是，从产品目标开始。

一旦我们有了产品目标，下一个目标就是决定解决它的最佳方式。我以前出错的地方是，我会立即下定决心使用机器学习，因为我想建立有趣的方法。更好的方法是考虑解决问题的所有可用选项，不管是否需要 ML。

> 机器学习并不总是需要的！

如果我们决定使用 ML 方法，我们必须决定它们是否适合产品。《T4 构建机器学习驱动的应用》一书提出了两个步骤:

*   (1) **以 ML 范式**构建产品目标——对于一个目标，可能有多种表述。
*   (2) **评估 ML 可行性**——考虑所有潜在的框架，从最简单的开始。

这个过程要求我们检查问题的数据和模型方面。

## 设计产品框架

在这个场景中，我将假设我们想要构建一个写作助手。我们的写作助手要能接受作家写的中等文章，并加以改进，使之写得更好。考虑到这个公式，我们必须首先解决“更好”这个词的含义。我们可以通过问更多的问题来做到这一点，直到我们对我们的写作助手的产品目标有一个清晰的定义。

这里有一个更清晰的公式的例子:

> Medium 是一个社交媒体平台，供作家分享见解，读者向作家学习见解。然而，一些作家因为他们写的文章而疯狂传播，即使没有大量的追随者，其中一个原因是基于文章写得有多好。这对于那些有着非常有用的见解但不擅长通过写作表达自己的作家来说是不幸的。因此，我们的目标是建立一个写作助手，帮助作者写出更好的文章。

## 成为算法

在我们实现机器学习算法之前，尝试手动解决问题没有坏处。这样，我们可以了解你的学习算法必须成功解决什么样的问题。在我们的场景中，我们必须考虑如何提高文章的可读性，以及传播的几率。

一种方法可能涉及研究，以确定一些属性，可以用来帮助媒体博客写得更清楚。这些特征的例子有:

*   散文的简单性:散文意味着语言遵循日常语言的自然模式。因此，任何遵循基本语法结构的作品都被称为散文。我们可以利用这个特性来建立一个关于适当的句子和单词长度的标准，使我们能够在需要的地方提出修改建议。
*   **语气**:语气是指作者对读者的态度和信息的主题。通过评估语言，我们可以衡量文章的极性，并确定一篇文章是否触及读者的情感纽带，因为这些文章往往在某些上下文中表现良好。
*   **结构特征**:结构描述了文本在页面上是如何排列的，以及所有部分是如何组合在一起形成文章的。作家通常喜欢有意识地组织他们的文章，因为这对读者有影响。

> 注意:我们也想和病毒媒体的作者谈谈，了解一些他们用来让他们的作品病毒式传播的写作技巧。

通过识别和生成有用的特性，我们能够构建一个简单的解决方案，依靠这些特性向我们的读者提供推荐。报道这个过程可能会很无聊，因为它不涉及机器学习，但它对于提出一个快速基线来衡量其他实验是至关重要的。

## 基于我们所学到的

有了我们的初步特征，我们可以利用它们从一篇文章中学习一种风格模式。为了执行这一步，我们需要建立一个数据集，提取我们描述的特征，然后训练一个分类器来区分好的和坏的例子。

在建立分类器来分离文本之后，我们想要分析高度可预测的特征，因为这些是我们将用作对我们的系统的推荐改变的特征。

## 最后的想法

机器学习并不总是所有产品都需要的。在转向 ML 解决方案之前，建立简单的解决方案来测试产品的可行性并评估是否需要机器学习是很重要的。如果确实需要 ML，从一个简单的解决方案开始是一个好主意，可以为您提供一个基线和反馈，以便进一步发展。

感谢阅读！

如果你喜欢这篇文章，请通过订阅我的**[每周简讯](https://mailchi.mp/ef1f7700a873/sign-up)与我联系。不要错过我写的关于人工智能、数据科学和自由职业的帖子。**

## **相关文章**

**</the-moment-i-realized-data-science-certificates-wont-push-my-career-forward-efe2d404ab72>  </always-remember-data-comes-before-the-science-681389992082> **