# 使用 Python 进行模糊字符串匹配

> 原文：<https://towardsdatascience.com/fuzzy-string-matching-using-python-e0d1ff142dd0?source=collection_archive---------34----------------------->

## 在本文中，我们将探索如何使用 Python 执行模糊字符串匹配。

![](img/163dfe338ab583a36b601b0d83fde721.png)

在 [Unsplash](https://unsplash.com/s/photos/matching-colors?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上由[S O C I A L C U T](https://unsplash.com/@socialcut?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)拍摄

**目录**

*   介绍
*   莱文斯坦距离
*   简单模糊字符串匹配
*   部分模糊字符串匹配
*   无序模糊字符串匹配
*   结论

# 介绍

当处理字符串匹配或文本分析时，我们经常希望在一些变量或文本中找到匹配的部分。我们自己看文字就知道*多伦多机场*和*多伦多机场*指的是同一个东西，而 *Torotno* 只是拼错了*多伦多*。

但是我们如何通过编程解决这个问题，并让 Python 识别这些情况呢？我们使用模糊字符串匹配！

为了继续学习本教程，我们需要以下 Python 库:fuzzywuzzy 和 python-Levenshtein。

如果您没有安装它，请打开“命令提示符”(在 Windows 上)并使用以下代码安装它:

```
pip install fuzzywuzzy
pip install python-Levenshtein
```

# 莱文斯坦距离

为了理解字符串匹配背后的底层计算，让我们讨论一下 Levenshtein 距离。

在计算机科学中，Levenshtein 距离是两个序列(在我们的例子中是字符串)之间相似性的度量。它通常被称为“编辑距离”。

为什么简单地说，它计算两个字符串之间应该发生的最小编辑次数，以使它们相同。现在，需要编辑的次数越少，两个字符串就越相似。

要了解关于 Levenshtein 距离及其计算的更多信息，请查看本文。

# 简单模糊字符串匹配

fuzzywuzzy 库中的简单比率方法计算两个字符串之间的标准 Levenshtein 距离相似性比率，这是使用 Python 进行模糊字符串匹配的过程。

假设我们有两个非常相似的单词(有些拼写错误): *Airport* 和 *Airprot* 。仅仅看这些，我们就能知道除了拼写错误之外，它们可能是一样的。现在，让我们尝试使用简单的比率字符串匹配来量化相似性:

我们得到了:

```
86
```

因此，计算出的两个单词之间的相似度是 86%,对于一个拼写错误的单词来说，这是相当不错的。

这种方法适用于短字符串和长度相对相似的字符串，但不适用于不同长度的字符串。例如，您认为*机场*和*多伦多机场*的相似之处会是什么？实际上比你想象的要低:

我们得到了:

```
64
```

这里发生的是，绳子长度的差异起了作用。幸运的是，fuzzywuzzy 图书馆有一个解决方案:**。【partial _ ratio()方法。**

# 部分模糊字符串匹配

回想一下上一节，当比较*机场*和*多伦多机场*时，我们通过简单的字符串匹配只得到 64%的相似度。事实上，在这两种情况下，我们指的是一个机场，这也是我们作为读者将会看到的。

由于字符串的长度差异很大，我们应该进行部分字符串匹配。我们感兴趣的是一个较短的字符串和一个较长的字符串的最佳匹配。

逻辑上是怎么运作的？考虑两串:*机场*和*多伦多机场*。我们可以马上看出第一个字符串是第二个字符串的子字符串，即 *Airport* 是 *Toronto Airport* 的子字符串，这是一个完美的匹配:

我们得到了:

```
100
```

# 无序模糊字符串匹配

我们在处理字符串时可能会遇到的一个常见问题是单词的顺序。例如，您认为多伦多*机场*与多伦多*机场*有多相似？100%?

使用上述部分的技术，我们发现结果低得惊人:

我们得到了:

```
47
48
```

这可能比你预期的要低得多？只有 47%-48%。

我们发现不仅子串的相似度很重要，它们的顺序也很重要。

# 相同长度的字符串

对于这种情况，fuzzywuzzy 库有一个解决方案:**。token_sort_ratio()** 方法。它所做的是将字符串标记化，然后按字母顺序对标记进行排序，然后进行字符串匹配。

在我们的例子中，标记*多伦多机场*将保持同样的方式，但是标记*多伦多机场*将按字母顺序排列子字符串以得到*多伦多机场*。现在我们正在比较*多伦多机场*和*多伦多机场*，你可以猜测我们可能会得到 100%的相似性:

我们得到了:

```
100
```

# 不同长度的字符串

对于这种情况，fuzzywuzzy 库有一个解决方案:**。token_set_ratio()** 方法。它所做的是将字符串标记化，然后分成[交集]和[余数]，然后按字母顺序对每个组中的字符串进行排序，然后进行字符串匹配。

考虑两串:*多伦多机场*和*多伦多机场关闭*。在这种情况下，[交叉点]组将是*机场*，第一串的[剩余部分]将是空的，第二串的[剩余部分]将是*关闭的*。

从逻辑上讲，我们可以看到，具有较大[交集]组的字符串对的得分会更高，因为将会有完美的匹配，并且可变性来自[剩余]组的比较:

我们得到了:

```
100
```

# 结论

在本文中，我们探讨了如何使用 Python 执行模糊字符串匹配。

我也鼓励你看看我关于 [Python 编程](https://pyshark.com/category/python-programming/)的其他帖子。

如果你有任何问题或者对编辑有任何建议，请在下面留下你的评论。

*原载于 2021 年 2 月 6 日 https://pyshark.com*<https://pyshark.com/fuzzy-string-matching-using-python/>**。**