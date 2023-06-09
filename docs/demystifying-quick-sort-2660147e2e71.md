# 揭秘快速排序

> 原文：<https://towardsdatascience.com/demystifying-quick-sort-2660147e2e71?source=collection_archive---------50----------------------->

## 排序算法指南

## 升级你的排序游戏！

在前 3 篇文章中，我们讨论了冒泡排序、选择排序和插入排序。在一般情况下，所有这些算法的时间复杂度都是 O(n)。剧透警报！这是第一个在一般情况下运行得比 O(n)更好的排序算法。

![](img/21f88f4e3043db18362d69808cf2435a.png)

图片由[UX](https://unsplash.com/@uxindo)在 [Unsplash](https://unsplash.com/) 上拍摄

我们走吧！当我们开始深入研究更高级的算法时，我激动不已。这些概念一开始可能不会被理解，即使如此，继续尝试，我保证你会在几次尝试后理解它。

# 什么是快速排序

快速排序，也称为分区交换排序，是现有的最快的排序算法之一，也是大多数排序库中常用的方法。这种排序方法在其他方法中表现最好，因此被命名为快速排序。该算法基于分治策略。

在快速排序中，从称为轴心的数组中选择一个元素。下一步是将阵列分成两个子阵列。这样做是为了使小于轴心的所有元素位于数组的左侧，而较大的元素位于右侧。在这个循环之后，pivot 元素位于数组中的固定(最终)位置。之后，我们对每个子数组递归地执行这个过程。为了简单起见，我们将每个子数组的第一个元素作为支点。

# 它是如何工作的？

1.  选择第一个元素作为轴心。
2.  对数组进行分区，使所有较小的元素位于数组的左边，较大的元素位于右边。
3.  递归地执行步骤 1 和 2，直到数组排序完毕。

有许多分区操作可用，最流行的两个是 Hoare 分区方案和 Lomuto 分区方案。Hoare 划分方案比 Lomuto 划分方案更有效。这就是为什么我们将在快速排序算法中应用霍尔划分方案。

# 快速排序示例

像往常一样，我们将首先从伪代码开始。

> 快速排序伪代码

现在我们将看看 Python、C 和 JavaScript 中的算法代码。

> Python 中的快速排序代码

> C 语言中的快速排序代码

> JavaScript 中的快速排序代码

# 快速排序的时间复杂度

快速排序最佳情况时间复杂度发生在分区均匀平衡时(主元固定位置在子数组的中间)。在这种情况下，最佳时间复杂度为 O(n log n)。最坏的情况是，当数组已经排序，或者轴心总是最小或最大的元素时，就会发生这种情况。快速排序将以 O(n)时间复杂度运行，与我们之前学习的其他排序算法相当。好消息是快速排序的平均时间复杂度也是 O(n log n)。一般情况下，枢轴位于数组中的 1/4 或 3/4 位置。

# **临别赠言**

在我们的实现中，选择最左边的元素作为枢纽，当数组已经排序时，时间复杂度为 O(n)。幸运的是，这个问题可以很容易地通过选择一个随机索引作为轴心或者选择中间索引作为轴心来克服。那么最坏的情况下时间复杂度会变成 O(n log n)。

记住，在编程中，总有你可以改进的地方。你应该从批判性地思考我们如何做出必要的改进开始，这值得我们花时间吗？对于快速排序的情况，这确实是值得的，我们只需要采取中间位置而不是第一个位置，这可以显著提高我们算法的效率。

> “你总能改善你的处境。但你要面对它，而不是逃避。”—布拉德·华纳

让我们一起提高编程的技巧吧！

问候，

**弧度克里斯诺**