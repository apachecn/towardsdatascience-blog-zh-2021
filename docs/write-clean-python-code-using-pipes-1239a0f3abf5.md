# 使用管道编写干净的 Python 代码

> 原文：<https://towardsdatascience.com/write-clean-python-code-using-pipes-1239a0f3abf5?source=collection_archive---------0----------------------->

## 一种简洁明了的处理迭代的方法

# 动机

`map`和`filter`是处理 iterables 的两种有效的 Python 方法。然而，如果同时使用`map`和`filter`，代码看起来会很混乱。

![](img/af3ee0ef897b9a63f1afb32ac552ae64.png)

作者图片

如果可以使用管道`|`在一个可迭代对象上应用多种方法不是很好吗？

![](img/d053b27a95efd0b05e371c68809e1f83.png)

作者图片

库管道允许您这样做。

# 什么是管道？

管道是一个 Python 库，使你能够在 Python 中使用管道。管道(`|`)将一个方法的结果传递给另一个方法。

我喜欢 Pipe，因为它使我的代码在对 Python iterable 应用多个方法时看起来更干净。由于 Pipe 只提供了几种方法，所以学习 Pipe 也非常容易。在这篇文章中，我将向你展示一些我认为最有用的方法。

要安装管道，请键入:

```
pip install pipe
```

# 其中—可迭代中的过滤元素

与 SQL 类似，Pipe 的`where`方法也可以用来过滤 iterable 中的元素。

![](img/867fb29090379a0a91f9f8f5d2065faf.png)

作者图片

# 选择—将函数应用于可迭代对象

`select`方法类似于`map`方法。`select`对 iterable 的每个元素应用一个方法。

在下面的代码中，我使用`select`将列表中的每个元素乘以 2。

![](img/b15ece7fb1da4d9594f165d39058bc9c.png)

作者图片

现在，你可能想知道:如果方法`where`和`select`具有与`map`和`filter`相同的功能，为什么我们还需要它们？

这是因为您可以使用管道将一个方法插入到另一个方法中。因此，使用管道可以删除嵌套的括号，使代码更具可读性。

![](img/d053b27a95efd0b05e371c68809e1f83.png)

作者图片

# 展开迭代

## chain —将一系列可重复项链接起来

使用嵌套的 iterable 可能会很痛苦。幸运的是，您可以使用`chain`来链接一系列可重复项。

![](img/ca9653f343d31230b79c69f81f105b7d.png)

作者图片

即使在应用了`chain`之后 iterable 的嵌套减少了，我们仍然有一个嵌套列表。为了处理深度嵌套的列表，我们可以使用`traverse`来代替。

## 遍历-递归展开迭代

`traverse`方法可用于递归展开可重复项。因此，您可以使用此方法将深度嵌套的列表转换为平面列表。

![](img/2004fb9200cb747c1050f2dfded5ffbe.png)

作者图片

让我们将这个方法与`select`方法集成在一起，以获取字典的值并展平列表。

![](img/ae035e11977e4892ea52ebf99f7bbac9.png)

作者图片

相当酷！

# 将列表中的元素分组

有时，使用某个函数对列表中的元素进行分组可能会很有用。用`groupby`方法很容易做到这一点。

为了了解这种方法是如何工作的，让我们将一个数字列表转换成一个字典，根据数字是奇数还是偶数对其进行分组。

![](img/0ff4ad825fbcf1c0e89625176f874568.png)

作者图片

在上面的代码中，我们使用`groupby`将数字分组到`Even`组和`Odd`组。应用此方法后的输出如下所示:

```
[('Even', <itertools._grouper at 0x7fbea8030550>),
 ('Odd', <itertools._grouper at 0x7fbea80309a0>)]
```

接下来，我们使用`select`将元组列表转换为字典列表，字典的键是元组中的第一个元素，值是元组中的第二个元素。

```
[{'Even': [2, 4, 6, 8]}, {'Odd': [1, 3, 5, 7, 9]}]
```

酷！为了只获取大于 2 的值，我们可以在`select`方法中添加`where`方法:

![](img/ddc67856e62435459c2c97c0c3e64150.png)

作者图片

请注意，输出中不再有`2`和`1`。

# 重复数据删除—使用密钥删除重复数据

方法删除了列表中的重复项。

![](img/0df5d655ee2d5a4054314559cbd76f9e.png)

作者图片

这听起来可能没什么意思，因为`set`方法可以做同样的事情。但是，这种方法更加灵活，因为它使您能够使用键获得唯一的元素。

例如，您可以使用此方法获取一个小于 5 的唯一元素和另一个大于或等于 5 的唯一元素。

![](img/23510f632c02ad59643564b9bcf3c814.png)

作者图片

现在，让我们将这个方法与`select`和`where`结合起来，以获得具有重复键和`None`值的字典的值。

![](img/92ec08cc4b4ec5ccd30a26dbd63072c4.png)

作者图片

在上面的代码中，我们:

*   移除具有相同`name`的项目
*   获取`count`的值
*   只选择整数。

在几行代码中，我们可以对一个 iterable 应用多种方法，同时仍然保持代码的整洁。很酷，不是吗？

# 结论

恭喜你！您刚刚学习了如何使用管道来保持代码简洁。我希望这篇文章能给你一些知识，把复杂的迭代运算变成一行简单的代码。

随意发挥，并在这里叉这篇文章的源代码:

<https://github.com/khuyentran1401/Data-science/blob/master/productive_tools/pipe.ipynb>  

我喜欢写一些基本的数据科学概念，并尝试不同的算法和数据科学工具。你可以在 LinkedIn 和 T2 Twitter 上与我联系。

星[这个回购](https://github.com/khuyentran1401/Data-science)如果你想检查我写的所有文章的代码。在 Medium 上关注我，了解我的最新数据科学文章，例如:

</python-clean-code-6-best-practices-to-make-your-python-functions-more-readable-7ea4c6171d60>  </4-pre-commit-plugins-to-automate-code-reviewing-and-formatting-in-python-c80c6d2e9f5>  </pydash-a-bucket-of-missing-python-utilities-5d10365be4fc>  </3-python-tricks-to-read-create-and-run-multiple-files-automatically-5221ebaad2ba> 