# 天气预报与机器学习，使用 Python

> 原文：<https://towardsdatascience.com/weather-forecasting-with-machine-learning-using-python-55e90c346647?source=collection_archive---------1----------------------->

![](img/2108841571dd222cc666826ee4e083cc.png)

由 [Unsplash](https://unsplash.com/s/photos/climate?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的[卡斯滕·沃思](https://unsplash.com/@karsten_wuerth?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)拍摄的照片

## 简单而强大的天气预报机器学习应用

物理学家将气候定义为一个**【复杂系统】**。虽然有很多关于它的解释，但在这个具体的例子中，我们可以认为**【复杂】**是**【无法以分析的方式解决】**。

这可能看起来令人沮丧，但它实际上为旨在解决气候挑战的广泛的数字算法铺平了道路。随着过去几年的计算发展，机器学习算法肯定是其中的一部分。

我想讨论的挑战是基于使用传统机器学习算法预测平均温度:**自回归综合移动平均模型(ARIMA)** 。

虽然这篇文章不想详细介绍理论背景，**但它确实想一步一步地指导如何在 Python 中使用这些模型，并将其应用于现实世界的数据。**

**所以让我们从描述 Python 框架开始。**

## 0.图书馆

用过的库都是最著名的数据分析，绘图，数学运算 **(pandas，matplotlib，numpy)** 。还有一些是用于高级数据可视化的(比如**叶子**，还有一些是用于 ARIMA 模型的特定库(比如 **statsmodels** )。以下是导入的代码:

## 1.数据集/数据集探索

数据集是开源的，可以在这里找到。

如果您想知道数据集中的城市，请使用这条熊猫线选择它们:

如果我们想在世界地图上标出这些城市，我们需要稍微改变一下纬度和经度。为了做到这一点，让我们使用这几行代码:

并显示城市:

## 2.预处理、高级可视化、稳定性

我选择隔离芝加哥，并将该城市的数据视为我的数据集。没有什么特别的原因要那么做…我就是喜欢芝加哥:)。当然，您可以使用自己的城市，并使用自己的数据集执行后续步骤。

> 目标是 **AverageTemperature 列**，即该特定月份的平均温度。我们有 1743 年到 2013 年的数据。

通过这条线，我们确定了 **NaN 值**，并用饼图显示它们:

由于它们不是数据集的一致部分，**我决定用以前的值来填充缺失的值。**我对平均温度的不确定性做了同样的处理。

“dt”列是标识年和月的列。对于接下来的操作，**更方便的方法是将该列转换成 datetime 对象，并在两个不同的列中显式标识年份和月份**。我们可以通过使用以下代码行来实现这一点:

使用该数据集，可以获得如下散点图:

但是读起来并不容易，所以我们应该做得更好。

现在让我们来描述我创建的三个超级基本函数:

*   **get_timeseries(start_year，end_year)** 提取两年之间的数据集部分
*   **plot_timeseries(start_year，end_year)** 以可读的方式绘制 get_timeseries 中提取的时间序列
*   **plot _ from _ data**(**data，time，display_options)** 以可读的方式绘制时间(dt)的数据(AverageTemperature)。显示选项允许显示记号，改变颜色，设置标签…

完成后，我们可以画出这样的图:

当我们使用 ARIMA 模型时，我们应该考虑平稳的时间序列。为了检查我们考虑的时间序列是否是平稳的，我们可以检查相关和自相关图:

这表明时间序列不是静止的。尽管如此，如果我们对整个数据集执行 [AD Fuller 测试](https://en.wikipedia.org/wiki/Augmented_Dickey%E2%80%93Fuller_test)，它会告诉我们数据集是稳定的。

但这是真的，因为我们在看整个数据集。事实上，如果我们分析一个单一的十年，很明显数据集在十年时间内绝对不是静止的。

**为了考虑这种非平稳性，将在 ARIMA 模型中考虑微分项。**

## 3.机器学习算法

让我们考虑 1992 年至 2013 年这十年，并绘制图表:

**执行训练/测试分割:**

**绘制拆分:**

机器学习算法是 [**ARIMA 模型。**](https://en.wikipedia.org/wiki/Autoregressive_integrated_moving_average) 这些都是基于采用最大似然函数的优化程序。

使用 [AIC](https://en.wikipedia.org/wiki/Akaike_information_criterion) 来考虑和评估零微分 ARIMA 模型。

而**一阶微分**模型用这些线考虑:

使用此功能突出显示总摘要，并显示(2，1，5)模型和(2，1，6)模型是最好的模型。

可以看到**的统计汇总值几乎相同**

同样的事情也发生在统计图表之间:

*   **模型(2，1，5)**

*   **模型(2，1，6)**

尽管如此，最好使用低指数模型，以避免过度拟合并减少计算机的计算压力。为此，**考虑了(2，1，5)模型。**

## 4.预测

让我们绘制预测操作的结果:

现在让我们考虑具有相应不确定性(由数据集给出)和置信区间(由算法给出)的特定预测区域:

**最后，让我们考虑一个可读性更强的版本的剧情:**

## 5.结论

这些方法非常容易采用，因为它们不需要像深度学习方法(RNN，CNN……)那样的任何特定计算能力。

尽管如此，**预测完全符合数据集本身设计的误差范围**。考虑到我们只检查了月平均值，这一点很重要，同时考虑日值并进行日预测可能也很有趣。

如果你喜欢这篇文章，你想知道更多关于机器学习的知识，或者你只是想问我一些你可以问的问题:

A.在 [**Linkedin**](https://www.linkedin.com/in/pieropaialunga/) 上关注我，在那里我发布我所有的故事
B .订阅我的 [**简讯**](https://piero-paialunga.medium.com/subscribe) 。这会让你了解新的故事，并给你机会发短信给我，让我收到你所有的更正或疑问。
C .成为 [**推荐会员**](https://piero-paialunga.medium.com/membership) ，这样你就不会有任何“本月最大故事数”，你可以阅读我(以及数千名其他机器学习和数据科学顶级作家)写的任何关于最新可用技术的文章。

再见。:)