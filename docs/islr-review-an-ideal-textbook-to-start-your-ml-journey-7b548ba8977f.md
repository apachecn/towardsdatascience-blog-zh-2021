# 《ISLR 评论》:开始你的 ML 之旅的理想教材

> 原文：<https://towardsdatascience.com/islr-review-an-ideal-textbook-to-start-your-ml-journey-7b548ba8977f?source=collection_archive---------27----------------------->

## 你是不是也一直在想接下来要学什么？让 **ISLR** 成为你阅读的下一本教科书——复习和学习技巧。

几个月前，我觉得我的机器学习基础有点不牢固。我*想开始 Kaggle，但是我被所有可用的技术吓倒了。我想尽可能高效地改变这一点，我已经找到了一个好的解决方案。我很兴奋现在就和你分享！*

在这篇文章中，我将告诉你我在 R (缩写为 **ISLR** )的**统计学习导论教材中的工作经验。我希望这能帮助你弄清楚*你是否也应该捡起来*，我也会分享一些让你学习更有效率的小技巧。**

![](img/7a013c54410f31e69374f1f1e764e4dd.png)

这么多书要读，时间却这么少——一定要挑一本好书！|照片由 [Alfons Morales](https://unsplash.com/@alfonsmc10?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 为什么我选择了 ISLR

大约一年前，我开始了我的机器学习之旅——当我开始厌倦时，我在 Coursera 上完成了*吴恩达著名的* [*机器学习课程。虽然我喜欢这门课程，它给了我一个工作的基础，但我觉得我需要更多的帮助和指导来用实际的方式使用 T21 新学到的知识。我想学习更多的技术，比如随机森林，更多地了解何时使用哪种算法，以及如何在 Python 中实际实现它们。我想创办 Kaggle，所以我决定参加 Kaggle 的*](https://www.coursera.org/learn/machine-learning)*[和*课程。当第一批 Kaggle Learn 教程中有一个是关于*实现*决策树，但是*没有解释*是什么或者它是如何工作的时候，我很快就泄气了。在半个小时的疯狂搜索和阅读了许多没有真正解释任何东西的博客帖子后，我决定**我需要一些知识更详细和更有条理的东西——一本教科书。***](https://www.kaggle.com/learn)*

挑选教材时，我在寻找以下内容:

*   入门/本科水平，容易理解，不适合博士生
*   深入数学的细节，但也解释了直觉
*   介绍了 Ng 的课程中没有涉及的许多不同的 ML 技术
*   实用，有编码练习来实现我所学到的东西
*   可在 2-3 个月内完成

经过一番 Reddit 深潜(*go join*[*r/learn machine learning*](https://www.reddit.com/r/learnmachinelearning/))发现**最值得推荐的入门水平书**好像是 **ISLR** 。它也满足了我想要的所有要求，所以我试了一下。

# 关于 ISLR 的一切

这本书的好处在于它可以从作者的网站上免费下载。你可以先看一眼，然后决定你是否喜欢这本昂贵的教科书。然而，我确实建议获得一个物理副本来浏览它。

如题所示，ISLR 在 R. *中用例子和练习介绍了统计学习技术，但是什么是静态学习呢？这本书将它定义为“理解数据*的一套庞大工具”。一般来说，统计学和 ML 之间正在进行一场战斗，你可以在[这篇非常有趣的帖子](http://brenocon.com/blog/2008/12/statistics-vs-machine-learning-fight/)中读到它。关于这本书，与通常的 ML 资源有轻微的文化差异，有时是不同的术语(例如，“Lasso/Ridge”而不是“L1/L2”)，有些侧重于经典的统计概念(如 p 值和假设检验)，但它主要解释了通常可以归类为 **ML 算法**的方法，如回归、支持向量机、基于树的方法和无监督学习概念。

这本书是为不同行业和背景的人设计的，这些人需要在他们的专业领域处理数据，而不一定需要大学水平的数学教育。这本书并没有比一本入门数学课程**，**更多的数学背景，也没有使用矩阵或向量符号来简化事情。它也**不假设任何以前的 R 经验**，认真讲解每一行代码，包括写函数和制作剧情。

ISLR 分为 **10 章**，从介绍性章节开始解释符号、偏差/方差权衡，并介绍 r。在第一章之后，**所有后续章节都围绕选定的技术**，从线性回归慢慢构建到更复杂的概念，如随机森林和层次聚类。**每一章的结尾都有实验**，指导你实现本章所教的方法，并进一步**概念和编码练习**来加深你的理解。

在每一章中，重点是对概念的**高层次理解**和**良好的直觉**。我发现对于我所需要的这本书来说，这些细节已经足够了，可以自信地在我自己的项目中使用一个方法的实现。它通过列出优缺点来比较类似的方法，并给出一种方法优于另一种方法的例子。作者用简单的数据集和真实的例子来说明每一种方法，这进一步有助于直觉。我特别喜欢几乎每一页上丰富多彩的图表——每当解释新的东西时，都会有一个图表来说明数据上的概念。

![](img/ae83fdcb09361626dfc5bd229de1dbc3.png)

可访问所有数学背景*和*漂亮图片|照片由 [Ben White](https://unsplash.com/@benwhitephotography?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# ISLR 被推荐给谁？

我认为你肯定会从阅读这本书中获得很多价值，如果以下任何一条适用的话:

*   你想要一个单一的信息来源来解释最流行的 ML 方法的基础，而不是花费大量的时间来搜索不同质量的相关文章和教程
*   您想做 Kaggle，但是对所有可用于数据的 ML 方法感到害怕
*   你知道算法在理论上是如何工作的，但不知道如何开始实现它们
*   你需要一本解释直觉的预备教材，然后才开始阅读数学厚重的研究生教材
*   在数据科学面试之前，你要提醒自己算法背后的数学。据我的一些朋友说，这本书里的材料对一些数据科学家毕业生的在线面试非常有帮助(也足够了)。

# 一些提示

## 将 ISLR 移植到 Python

这本书是 R 语言的，很多人(包括我)在他们的数据科学项目中不使用 R 语言。不过，如果你和我一样是团队 Python，这本书还是很惊艳的。你可以阅读它并接受一个挑战:**用 Python 而不是 r 解决实验室问题。**

这给了你一个框架，让你通过练习来实践理论概念，但是更少的手动操作:你不能只是重新键入 R 代码来完成实验，你必须首先弄清楚如何去做。这将意味着深入研究 Numpy、scikit-learn 和 StatsModels 库文档，并理解每个函数中的参数，以获得与 r 中相同的行为。老实说，这样做给我带来的益处**至少与阅读这本书给我带来的益处**一样多。

好的一面是，如果你被卡住了，你总是可以查找其他人的解决方案，因为许多人已经这样做了。(这里有 [*我的 GitHub 回购与 Python labs*](https://github.com/alexandrasouly/ISLR-but-python) *，*但你总是可以谷歌“Python 中的 ISLR”并找到十几个其他回购。)

## 认证在线课程+视频

比起视频，我更喜欢书，但我们都不一样。如果你从视频中学得更好，你不必担心——作者已经根据这本书录制了一门课程，以补充你的阅读。 **15 小时 Youtube 播放列表**从 [**链接至此**](https://www.dataschool.io/15-hours-of-expert-machine-learning-videos/) 。
如果你通过努力获得一张**证书**而变得更有动力，你可以购买这张证书来展示你的简历，这个选择也是存在的。斯坦福大学在 edX **，**网站上提供课程 [**，如果你决定购买证书，还会有额外的练习和反馈。**](https://www.edx.org/course/statistical-learning)

## 时间范围

如果你想让自己负起责任，这里有一个估计，你可以如何为自己设定目标来完成这本书:

*   我估计这本书可以在 **10 周**，**内完成，每周工作大约 5-6 小时**(如果你是自己移植到 Python 的话，8-10 小时)
*   如果你做笔记的话，通读一章的文本大约需要 2 个小时，半个小时用于概念练习，一个小时用于 R 语言的实验(或者对我来说用 Python 最多 4 个小时)，1-2 个小时用于编码练习。当然有更短和更长的章节，但这是我对平均值的粗略估计。

单独阅读一本教科书可能会有点让人泄气——没有像在线课程那样的提醒和红色弹出窗口。我建议你**给自己设定一个目标**，在某个特定的日期前完成每一章，让自己保持动力。这是一本非常受欢迎的书，你可能也能在 Reddit 上找到一些负责任的伙伴。

![](img/6f565b4a410830d5bd13aaba79133c05.png)

独自完成一本教科书是一项艰巨的工作……|照片由 [Siora 摄影](https://unsplash.com/@siora18?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 下一步做什么？

如果你已经读完了这本书，你应该会对应用机器学习方法来解决你选择的问题感到更舒服一些。如果您感兴趣，您可能已经准备好开始使用数据集进行实验，并在 Kaggle 上进行实践。如果你正在寻找一种温和的比赛体验，我推荐从 [**表格游乐场系列**](https://www.kaggle.com/c/tabular-playground-series-apr-2021) 开始。这些数据集易于使用，不占用大量计算资源，非常适合尝试各种简单的模型。如果你想了解更多，我可以全力推荐 Rohan Rao 的文章[逐步接近 Kaggle。](/progressively-approaching-kaggle-f58db71a42a9)

如果你对在 ISLR 学的数学还不过瘾，并且有扎实的线性代数和微积分基础，我推荐你去看看 [**《统计学习要素》**](https://web.stanford.edu/~hastie/ElemStatLearn/) **(ESL)** 。从技术上来说，《ISLR》是 ESL 的入门书，它更多地涉及了数学内容，更像是博士生和研究人员的参考书，而不仅仅是你通读的东西。

*无论你决定下一步做什么，我希望这篇评论对你有用，并祝你在机器学习之旅中好运！*

*原载于 2021 年 4 月 25 日*[*https://Alexandra souly . github . io*](https://alexandrasouly.github.io/ISLR_review)*。*