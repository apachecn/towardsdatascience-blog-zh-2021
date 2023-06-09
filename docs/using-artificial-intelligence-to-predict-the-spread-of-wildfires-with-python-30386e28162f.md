# 使用人工智能来预测野火的蔓延，用 Python

> 原文：<https://towardsdatascience.com/using-artificial-intelligence-to-predict-the-spread-of-wildfires-with-python-30386e28162f?source=collection_archive---------19----------------------->

![](img/7540df27a66b7f6ca25eb1ce22498b97.png)

Benjamin Lizardo 在 [Unsplash](https://unsplash.com/s/photos/wildfires?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

## 这是一个关于如何使用数据分析和机器学习来预测野火蔓延的分步指南

在过去的几天里，可怕的野火已经蔓延到撒丁岛、意大利和全世界。图像和视频令人心碎。当夏季开始时，这些事件往往会更频繁地出现，最终结果是灾难性的。

我决定学习人工智能(AI)的原因之一是能够直接帮助人们和解决现实世界问题的想法。我想这是其中之一。

在这篇文章中，我将指导你一步一步地使用人工智能来预测野火的蔓延。

让我们开始吧。

1图书馆:

您要做的第一件事是导入 **Python** 库。使用了很多不同的工具， **Pycaret** 用于开发机器学习部分， **Pandas** 和 **Numpy** 用于数据分析， **geopy** 用于获取距离等信息…

> 注意:这是一个通用的设置，我为这个笔记本做了一点改动。如果有什么东西在代码部分不会用到，我很抱歉。另外，我使用 plt.rcParams 来设置我最喜欢的绘图参数。你可以放心地跳过这一步。

2数据集

这是我用来下载数据集的[源](https://www.kaggle.com/ananthu017/california-wildfire-incidents-20132020)。这是一个加州野火的集合。让我们来看看。

可以看出，**纬度**和**经度**列不太可靠(例如 Ventura 是(0，0))。我们将在这方面努力。然后我们有了**市** ( **县**列)和野火发生的日期，即**开始。**名为 **AcresBurned** 的一栏是被野火烧毁的英亩数。

3数据可视化

让我们使用 geopy 通过使用**县**列来定位城市。让我们修复一些错误(例如，圣克鲁斯位于墨西哥，因此我们必须将其从数据集中删除)并绘制结果:

这是数据集的**世界地图**:

对于我们的分析，我们想要预测最终野火的城市在数据集中出现一定次数是很重要的。我们来策划一下吧！

随着**洛杉矶**出现足够高的次数，这个城市将被使用和研究。

我们需要的另一条信息是城市之间的距离。
让我们用这段代码得到它们，并绘制热图。

最后一步是绘制数据集的 4 个城市野火直方图:

4数据预处理

好了，现在我们对数据有了一个大致的概念，我们必须很好地定义我们需要什么。
我们想回答这些问题:

> “鉴于野火 X 发生在名为 Z 的城市的第 Y 天，从这里到 3 天，洛杉矶市会发生野火吗？3 天到 7 天会有野火吗？7 天到 10 天会不会有野火？”

为了做到这一点，我们希望有一个包含如下行的数据集:

**A .野火发生的日期
B .野火的距离
C .野火烧毁的英亩数
D .这场野火与洛杉矶另一场野火之间的天数**

特别是，d .列必须包含以下 4 个类中的一个:

**D.1 一到三天
D.2 三到七天
D.3 七到十天
D.4 十多天**(这意味着没有相关的野火)

这种数据集是通过使用以下代码行获得的:

1.  **划分 4 个等级**

**2。将它们全部归入单个数据集**

**3。创建最终数据集**

为分类准备的数据集如下:

5机器学习

你可能听说过，很多时候，机器学习部分是最快的一个。尤其是在 2k21 中用 **PyCaret 这样的工具。**已经测试了各种各样的机器学习模型。最好的一个在测试集上给了我们 87+%的准确率。

这是混淆矩阵，向我们展示了非常好的结果。

## 最终考虑

我们谈论的是人的生命，所以我们不能给虚假的希望。这篇文章只是野火预测挑战中一条看似有希望的道路的一个例子。必须使用大量研究和资源来验证这种方法。此外，各种不同的方法(例如，检查温度、湿度等)可以用来预测野火，当我写这篇文章时，研究人员正在开发新的方法。

如果你喜欢这篇文章，你想知道更多关于机器学习的知识，或者你只是想问我一些你可以问的问题:

A.在 [**Linkedin**](https://www.linkedin.com/in/pieropaialunga/) 上关注我，在那里我发布我所有的故事
B .订阅我的 [**简讯**](https://piero-paialunga.medium.com/subscribe) 。这会让你了解新的故事，并给你机会发短信给我，让我收到你所有的更正或疑问。
C .成为 [**推荐会员**](https://piero-paialunga.medium.com/membership) ，这样你就不会有任何“本月最大数量的故事”，你可以阅读我(以及成千上万其他机器学习和数据科学顶级作家)写的任何关于最新可用技术的文章。