# 在 Python 中使用管道操作以获得更好的可读性和更快的编码

> 原文：<https://towardsdatascience.com/pipe-operations-in-python-1e8f8debe26?source=collection_archive---------6----------------------->

## 一个方便的 Python 包，可以节省大量的编码时间，并提高 shell 风格管道操作的可读性

![](img/292985669ff97aba8eae39514cd03e19.png)

使用管道操作在单个语句中创建多个数据操作的链。照片由来自 Pexels 的 Joey Kyber 拍摄

Python 已经是一种优雅的编程语言。但不代表没有进步的空间。

Pipe 是一个漂亮的包，它将 Python 处理数据的能力提升到了一个新的水平。它采用类似 SQL 的声明性方法来操作集合中的元素。它可以过滤、转换、排序、删除重复项、执行分组操作等等，而不需要编写大量代码。

在这篇小文章中，让我们讨论如何用管道简化我们的 python 代码。最重要的是，我们将构建定制的可重用管道操作，以便在我们的项目中重用。

让我们从

*   一个励志的例子；
*   一些有用的开箱即用管道操作，以及；
*   构建我们自己的管道运营。

如果您想知道如何设置它，您可以很容易地用 PyPI 安装[管道](https://github.com/JulienPalard/Pipe)。这是你需要做的。

```
pip install pipe
```

# 开始在 Python 中使用管道。

这里有一个使用管道的例子。假设我们有一个数字列表，我们想，

*   删除所有重复项；
*   仅过滤奇数；
*   平方列表中的每个元素，以及；
*   按升序对值进行排序；

这是我们在普通 Python 中通常会做的事情。

一些使用基本 Python 的数据争论——由[作者](https://thuwarakesh.medium.com)编写的代码片段。

```
[1, 49, 169, 361, 441, 729]
```

上面的代码非常易读。但是这里有一个更好的使用管道的方法。

Pipe 如何提高 Python 中代码的可读性——作者[的代码片段](https://thuwarakesh.medium.com)。

```
[1, 49, 169, 361, 441, 729]
```

两种代码产生相同的结果。然而第二个比第一个更直观。显然，它的代码行也更少了。

这就是 Pipe 帮助我们简化代码的方式。我们可以对集合进行链式操作，而无需编写单独的代码行。

</python-code-formatting-made-simple-with-git-pre-commit-hooks-9233268cdf64>  

但是在 Pipe 中有更酷的操作，就像我们在上面的例子中使用的那样。此外，如果我们需要非常独特的东西，我们可以创建一个。我们先来探讨一些预置的操作。

# 最有用的管道操作

我们已经看到了几个管道在工作。但是还有更多。在这一节中，让我们讨论一些其他有用的现成数据操作。

这些并不是管道安装的完整操作列表。要获得详细的清单，请参考 GitHub 上的[管道库。](https://github.com/JulienPalard/Pipe)

## 分组依据

我相信这是对数据科学家最有用的管道。我们更喜欢在熊猫身上做，我仍然喜欢用它。但是将一个列表转换成一个数据集有时感觉有点矫枉过正。在所有这些情况下，我都可以随时使用这种按管道分组的操作。

使用 group by pipe 操作—作者为[的代码片段](https://thuwarakesh.medium.com)。

上面的代码将我们的数据集分组为奇数和偶数。它创建一个二元组列表。每个元组都有在 lambda 函数和分组对象中指定的名称。因此，上面的代码产生了下面的组。

```
[
    ('Even', <itertools._grouper object at 0x7fdc05ed0310>),
    ('Odd', <itertools._grouper object at 0x7fdc05f88700>),
]
```

我们现在可以为我们创建的每个组分别执行操作。这里有一个例子，它从每组中取出元素，然后将它们平方。

将变换应用到组——由[作者](https://thuwarakesh.medium.com)编写的代码片段。

```
[
    {'Even': [16, 4, 36, 64, 100, 400, 324]}, 
    {'Odd': [1, 729, 49, 169, 361, 441, 49, 729]},
]
```

## 链条和导线

这两个操作使得展开一个嵌套列表变得很容易。该链一步一步地执行，递归地遍历，直到列表不再扩展。

下面是链条的工作原理。

使用链式管道操作在 Python 中展开嵌套列表—代码片段由[作者](https://thuwarakesh.medium.com)编写。

```
[1, 2, 3, 4, 5, 6, 7, [8, 9]]
```

正如我们所看到的，chain 展开了列表的最外层。8 和 9 保留在嵌套列表中，因为它们已经向下嵌套了一层。

以下是使用 traverse 的结果。

使用遍历管道操作递归展开多层嵌套列表——作者[的代码片段](https://thuwarakesh.medium.com)。

```
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

特拉弗斯展开了它能展开的一切。

我主要用列表理解来展开列表。但是阅读和理解代码中发生的事情变得越来越困难。此外，当我们不知道有多少嵌套层时，很难像上面例子中的遍历操作那样递归扩展。

我老派的展开嵌套列表的方式——作者[作者](https://thuwarakesh.medium.com)的代码片段。

## Take_while 和 Skip_while

这两个操作类似于我们前面使用的“where”操作。关键的区别在于，如果满足某些条件，take_while 和 skip_while 会停止查看集合中的其他元素。而另一方面，计算列表中的每个元素。

下面是 take_while 和 where 在过滤小于 5 的值的简单任务中的工作方式。

使用 take_while 管道操作在满足特定条件时停止执行—代码片段由[作者](https://thuwarakesh.medium.com)编写。

上述代码的结果如下:

```
take_while: [5, 3]
where: [3, 4, 3]
```

请注意，take_while 操作跳过了最终的“3 ”,而“where”进程包含了它。

Skip_while 的工作方式很像 take_while，只是它只在满足某些条件时包含元素。

满足特定条件时使用 skip_while 管道开始执行——作者[作者](https://thuwarakesh.medium.com)的代码片段。

```
[5, 3]
```

正如我前面提到的，这些并不是您可以使用管道库做的事情的完整列表。更多的内置函数和例子请查看资源库。

# 创建新的管道操作

创建新的管道操作相对容易。我们所需要的就是用 Pipe 类来注释一个函数。

在下面的例子中，我们将一个常规的 Python 函数转换成一个管道操作。它接受一个整数作为输入，并返回它的平方值。

用 Python 创建新的管道操作——作者[作者](https://thuwarakesh.medium.com)的代码片段。

因为我们已经用`@Pipe`类注释了这个函数，所以它变成了一个管道操作。在第 9 行，我们用它来计算一个数字的平方。

管道操作也可以接受额外的参数。第一个参数总是链中上一个操作的输出。我们可以有任何额外的参数，并在链中使用它们时指定它们。

额外的参数甚至可以是一个函数。

在下面的示例中，我们创建了一个采用附加参数的管道操作。附加参数是一个函数。我们的管道操作是使用函数转换列表中的每个元素。

使用额外参数创建管道操作——作者[的代码片段](https://thuwarakesh.medium.com)。

# 最后的想法

看到 Python 如何进一步改进，令人印象深刻。

作为一名实践数据科学家，我发现 Pipe 在许多日常任务中非常有用。我们也可以用熊猫来完成这些任务。然而，管道在提高代码可读性方面表现出色。即使是编程新手也能理解这种转变。

这里需要注意的是，我还没有在大型项目中使用过 Pipe。我还没有探索它在大规模数据集和数据管道上的表现。但我确实相信这个包将在离线分析中发挥重要作用。

</python-project-structure-best-practices-d9d0b174ad5d>  

> *感谢阅读，朋友！跟我打招呼上*[***LinkedIn***](https://www.linkedin.com/in/thuwarakesh/)*[***Twitter***](https://twitter.com/Thuwarakesh)*，以及* [***中***](https://thuwarakesh.medium.com/) *。**
> 
> **还不是中等会员？请使用此链接* [***成为会员***](https://thuwarakesh.medium.com/membership) *因为，在不为你额外付费的情况下，我为你引荐赚取一小笔佣金。**