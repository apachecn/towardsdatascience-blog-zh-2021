# 使用机器学习预测文本的难度并获得单词的视觉表示

> 原文：<https://towardsdatascience.com/predicting-the-difficulty-of-texts-using-machine-learning-and-getting-a-visual-representation-of-75f5a96b92e5?source=collection_archive---------13----------------------->

![](img/967573892f7c2b1e2a5391c5f3c1f1e7.png)

乔恩·泰森在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

## 借助 WordCloud 和预处理步骤，发现文本数据中隐藏的见解和模式，并预测难度

我们看到文本数据在自然界中无处不在。有很多文本以不同的形式呈现，比如帖子、书籍、文章和博客。更有趣的是，有一个名为**自然语言处理(NLP)** 的人工智能子集，可以将文本转换成可用于机器学习的形式。我知道这听起来很多，但了解细节和机器学习算法的正确实现可以确保人们在这个过程中学习到重要的工具。

![](img/064d63ef86cce6f34f50bb9aeb954319.png)

照片由[杰米街](https://unsplash.com/@jamie452?utm_source=medium&utm_medium=referral)上的 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

因为有更新更好的库被创建用于机器学习目的，所以学习一些可以用于预测的**最先进的工具**是有意义的。我最近在 Kaggle 上遇到一个关于预测文章难度的挑战。

输出变量**文本的难度**被转换成本质上连续的形式。这使得目标变量连续。因此，各种回归技术必须用于预测文本的难度。由于文本在自然界中无处不在，应用正确的处理机制和预测将非常有价值，特别是对于以文本形式接收反馈和评论的公司。

现在让我们检查代码，并分别理解关键的可视化和结果。

**注:**数据集取自[https://www.kaggle.com/c/commonlitreadabilityprize/data](https://www.kaggle.com/c/commonlitreadabilityprize/data)

**阅读图书馆**

我知道当使用各种库进行机器学习时，这看起来很复杂。然而，如果我们试图理解这些库，事情就会变得简单。让我们利用上面提到的库来预测课文的难度。我们导入用于科学计算的 numpy。我们使用 **seaborn** 和 **matplotlib** 来绘制图形和数字。**熊猫**用来读文件。WordCloud 将帮助我们分别标出最常出现的单词。

我们使用一个**自然语言处理工具包**来执行句子到不同记号和单词的转换，以便它们可以用于机器学习目的。我们还将使用 **TFIDF 矢量器**和**计数矢量器**将一组给定的单词和句子转换成数学矢量。库**‘tqdm’**只是用来计算执行各种计算所需的时间。最后，我们使用 **train_test_split** 将数据分别分为训练和测试部分。**缺失号**用来给我们提供机器学习缺失值的图。我们也将**地**互动可视化。这些是我们将分别用于我们的自然语言处理项目的一些库。

## 预处理功能

在将数据交给机器学习模型进行预测之前，**对数据进行预处理**是非常重要的。使用像代表正则表达式的库可能会很方便。此外，应完成**文本标记化**，以便将文本简化为标记。**文本中的停用词**不会增加很多意思，但大多像填充词。因此，从我们的**语料库**中移除那些单词降低了训练我们的模型的计算成本。从代码中可以看出，停用词被删除了。最后，转换后的文本由函数返回，以便在我们的机器学习管道中进一步处理。

## 读取数据

上面将注册一个训练和测试路径，并将这些值加载到。csv 文件。有一个名为“low_memory”的属性被设置为“False ”,以便于读取数据。

现在是时候从本地文件中读取数据了。在代码的前面，指定了文件的路径。现在是存储那些**的时候了。csv'** 文件中的变量如上图所示。

## WordCloud 功能

从上面的代码中可以看出，我们已经定义了一个函数来生成 **WordCloud** ，它给出了数据中出现频率最高的单词的图表。这真的很方便，特别是如果我们想知道基于文本输出难度的单词的出现。

## 文本预处理

在常规回归的帮助下，现在是时候让我们的文本清晰易懂了。为了做到这一点，各种单词被替换为它们的长形式，以便提高文本的可读性。例如，在上面的代码块中，“t”被替换为“not ”,以提高对文本的理解。类似地，所有其他表达式都被替换，这有助于我们分别删除这些停用词。

## TFIDF 矢量器

现在让我们使用 **tfidf 矢量器**，它可以将单词编码成**数学矢量**，供我们的机器学习模型处理。 **Tfidf 矢量器**会计算所有文本中常见的单词以及单词的频率。例如，**‘the’**可能出现在我们的某篇文章中。但是由于**‘the’**也出现在大多数其他文本中，所以它的 **tfidf** 值将会很低。让我们也用另一个词来理解。如果我们在我们的语料库中找到一个单词**‘感恩’**，这个单词可能在我们的某篇文章中很常见。但同一个词可能不会出现在所有其他文本中。因此，它的 **tfidf** 值会很大。同样，我们对所有的单词进行同样的步骤，以确保它们被转换成数学向量进行处理。

## 训练深度神经网络

定义一个**神经网络**对于训练我们的数据很重要。我们已经定义了一个**神经网络**以及几个密集层。我们首先从第一层的 **500 个隐藏单元**开始，慢慢减小尺寸，直到我们只达到 **1 个输出单元**。由于**‘可读性’**变量是一个连续变量，输出单位应该是线性的。我们是否也要显示验证分数是根据设置为**真**或**假**的 **validation_data** 决定的。值得注意的是，我们目前正在使用**‘Adam’**优化器来完成深度学习任务。

## 评估模型

神经网络模型训练成功后，就到了评估其性能的时候了。我们现在可以使用模型的历史属性来评估性能。我们将考虑每个历元值的均方误差和验证均方误差。在绘制之后，您可以得到关于历元的增加如何导致训练均方误差减少的曲线。有时交叉验证均方误差会在某一点后增加。这意味着我们的模型过度拟合了数据。因此，应该分别采取措施来减少模型的过拟合。

完整的代码和详细的描述，你可以点击下面的链接。

suhasmaddali/Predicting-Readability-of-Texts-Using-Machine-Learning:这个项目的目标是分别使用各种机器学习技术来预测文本的难度水平。(github.com)

## **结论**

总的来说，我们学会了如何阅读数据，预处理数据，理解经常出现的单词。看完这篇文章后，希望你了解了如何使用机器学习和深度学习来预测文本的可读性。欢迎分享您的想法和反馈。谢了。