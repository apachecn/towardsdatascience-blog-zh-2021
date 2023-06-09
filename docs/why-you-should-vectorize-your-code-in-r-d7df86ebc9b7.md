# 为什么应该用 R 向量化你的代码

> 原文：<https://towardsdatascience.com/why-you-should-vectorize-your-code-in-r-d7df86ebc9b7?source=collection_archive---------21----------------------->

## *使用 R 中的微基准测试包比较矢量化运算和 for 循环的效率*

![](img/4485f6ab458cfce222763bd934d13e73.png)

由[维普·贾](https://unsplash.com/@lordarcadius?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

在本文中，我将通过比较使用向量化操作和使用 for 循环执行三个不同的任务所需的时间来说明使用向量化代码的好处。R 中的 microbenchmark 包提供了一个方便的工具来比较不同的 R 表达式执行需要多长时间。

本文中使用的代码可以在这个 [GitHub repo](https://github.com/TalkingDataScience/why_vectorize) 中找到。

# 乘法向量

我们先来看一个简单的两个向量相乘的例子。首先，我们编写了两个向量相乘的两个版本，并将它们包装在函数中，以便我们可以将它们传递给微基准函数。我们加载 microbenchmark 包，并将我们的两个版本传递给 microbenchmark 函数。通过设置 times = 100，我们将运行每个函数 100 次，结果将向我们显示汇总统计数据。

微基准测试返回测试的摘要，如果我们看一下平均值，我们可以看到使用 for 循环的乘法比矢量化乘法要多花 7 倍的时间。

![](img/3fd0f4e11f0ff82f76a1d8438fb4737b.png)

作者图片

那么，为什么矢量化运算会快得多呢？在这个例子中，我们将一个由 1 到 100 的整数组成的向量与它自身相乘。当使用 for 循环时，我们一次乘一对整数，就像每次迭代中的一次乘法一样。在这种情况下，for 循环有 100 次迭代，所以 R 做 100 次乘法。当进行矢量化乘法时，整个向量被传递到操作中，这意味着向量被乘以*一次*。在 for 循环中，我们也将乘积赋值给新的向量 100 次，而在矢量化版本中，我们只将结果赋值一次。因此运行时间更短。

# 生成随机数

你可能会发现自己经常做的另一项任务是生成随机数。下面的代码将从 0 和 1 之间的均匀分布中生成 1，000，000 个随机数。

在这个例子中，第一个函数调用随机数生成器函数 runif() *一次*，而第二个函数调用 runif() *一百万次*。毫不奇怪，for 循环花费的时间要长得多，在这个测试中几乎是 221 倍。

![](img/f5b538968e4c85a4512a6b45e4bf8df4.png)

作者图片

# 用蒙特卡罗模拟法估计圆周率

最后，我们将看一个例子，在这个例子中，我们都生成随机数，并对这些数进行一些计算。我们将比较两个使用随机抽样估算圆周率的函数，一个使用矢量化运算，一个使用 for 循环。

关于如何进行模拟的更多细节和指南可以在这篇关于蒙特卡罗模拟的文章中找到。

<https://medium.com/@andreagustafsen/estimating-pi-using-monte-carlo-simulation-in-r-91d1f32406af>  

基本上，这些函数的作用是为正方形中的点生成随机(x，y)坐标。它计算到圆原点的距离，以确定该点是否落在圆内，并最终估计圆周率。

在矢量化版本中，我们调用 runif()函数两次，每个 x 和 y 向量一次，分别调用 which()和 length()一次，做两次计算。在 for 循环中，我们调用 runif()函数 200 万次，计算距离 1，000，000 次，最后计算一次 pi。

微基准测试表明，for 循环版本的运行时间是矢量化版本的 117 倍！

![](img/3eaaa58f56c4f346f36eefd70b2ea8e8.png)

作者图片

希望这些例子能帮助你看到在 r 中使用向量化操作的好处，你不需要回到你的旧脚本，重新编写你的代码。在许多情况下，我们处理的数据量相对较小，操作可能只需要几秒钟，矢量化操作和 for 循环之间的差异可能并不明显。但是，您可能会发现自己在处理巨大的数据集，并编写耗时数小时的复杂操作，在这种情况下，您肯定希望让 R 尽可能高效地处理代码。理解矢量化操作中发生的事情可以帮助您编写更短、更简单、更快的代码。

如果你是 R 新手，想了解更多，可以在本文的[中找到如何在免费互动课程中练习编写 R 代码。](https://medium.com/@andreagustafsen/the-free-interactive-r-courses-most-people-dont-know-about-c49aff7e5d4c)

<https://medium.com/@andreagustafsen/the-free-interactive-r-courses-most-people-dont-know-about-c49aff7e5d4c>  

如果你喜欢阅读这样的故事，并想支持我成为一名作家，可以考虑报名成为一名媒体成员。每月 5 美元，你可以无限制地阅读媒体上的故事。如果你注册使用我的链接，我会赚一小笔佣金。

<https://medium.com/@andreagustafsen/membership> 