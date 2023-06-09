# Python 程序员的快速迭代技巧

> 原文：<https://towardsdatascience.com/lightning-fast-iteration-tips-for-python-programmers-61d4f72bf4f0?source=collection_archive---------15----------------------->

## 我最喜欢的一些提高 Python 迭代性能的技术

![](img/d1eaf32ecb88450d6173b480f88f8a96.png)

(src =[https://pixabay.com/images/id-1036469/](https://pixabay.com/images/id-1036469/)

# 介绍

迭代是许多基本的编程技术之一，可以用来解决使用可迭代类型的问题。它是计算机编程的基础支柱之一，也是任何想加入计算机编程世界的人的一项基本技能。也就是说，迭代也可能令人困惑。当一个人不熟悉这项技术的来龙去脉时，情况尤其如此。

也就是说，在 Python 中使用迭代有很多重要的事情需要了解。我想提供一些我最喜欢的 Python 迭代技巧，因为编程的这一重要部分需要不断开发才能掌握。这些技巧中的一些将有助于加快您的算法，并且肯定会对您的 Python 技能有很大的帮助。其他一些技巧是在不同的用例中使用迭代的好方法。总的来说，这个列表肯定会给你的 Python 能力增加一些价值！此外，一如既往，Github 上有一个包含所有这些代码的笔记本，您可以在这里查看:

<https://github.com/emmettgb/Emmetts-DS-NoteBooks/blob/master/Python3/Python%20Iteration%20Tricks.ipynb>  

# 1 号:Zip

我想讨论的第一个迭代技巧是使用 zip()类。该方法可用于有效地将两个 iterable 合并成一个 iterable，并同时遍历它们。不用说，对于编程来说，能够实现这种功能的技术是非常有价值的。此外，压缩相对容易和直接使用，所以不像这个列表中的其他选项，这是非常友好的初学者。这不仅可以用于加速算法，还可以使新类型的算法成为可能。

正如我之前简单提到的，在 Python 中使用 zip()类非常简单。首先，我们当然需要两个 iterables。需要注意的一点是，如果一个 iterable 比另一个 iterable 长，那么循环将在该值处停止。当这种情况发生时，我们可以通过使用惰性压缩来避免循环中断。如果你想了解更多关于懒惰压缩的知识，并真正深入了解这种技术，我实际上写了一篇文章，你可以在这里阅读关于这个主题的所有内容:

</everything-you-need-to-know-about-zip-in-python-5da1416f3626> [## 关于 Python 中的 Zip，您需要了解的一切

towardsdatascience.com](/everything-you-need-to-know-about-zip-in-python-5da1416f3626) 

不管怎样，回到我们的文学作品。我决定用两个列表，你不需要像我一样在这里写转换，但是无论哪种方式都没有什么区别:

```
z = list([1, 2, 3, 4, 5, 6])
z2 = list([1, 2, 3, 4, 5, 6])
```

现在我们有两个可迭代的，z 和 z2。我们可以通过调用 zip 方法创建一个新的 zip 迭代器类，如下所示:

```
bothlsts = zip(z, z2)
```

或者我们可以在 for 循环定义中直接调用 zip()类。这纯粹是口味问题，或者说是环境问题。这两个例子当然会产生相同的结果:

```
for i, c in bothlsts: print(i + c)for i, c in zip(z, z2): print(i + c)
```

# №2:迭代工具

另一个加速 Python 迭代的非常酷的选项是令人惊叹的 Itertools 模块。这个模块在标准库中可用，这意味着如果你有 Python，你已经有 itertools 了——你只需要导入它。谈到迭代循环，Itertools 可以用于多种用途。Itertools 在某些情况下甚至可以用在非常规 for 循环的应用程序中。itertools 的伟大之处在于，它是一套非常快速、性能良好的迭代工具，适用于已经移植到 Python 的不同应用程序。这意味着任何时候你想做 x 或者 y，你都在使用最好的算法。不用说，在 Python 这样的语言中，速度不一定是该语言的强项，当然有理由使用 itertools。让我们导入模块:

```
import itertools as its
```

我可以用很多很好的例子来展示 itertools 的强大，但是我特别喜欢一个例子。这个例子是典型的编程测试，使用 itertools 超出了通过测试的典型要求。如果教授或雇主看到你做出比答案更快的算法，他们可能会印象深刻。无论如何，这是嘶嘶声的例子:

```
def fizz_buzz(n):
    fizzes = its.cycle([""] * 2 + ["Fizz"])
    buzzes = its.cycle([""] * 4 + ["Buzz"])
    fizzes_buzzes = (fizz + buzz for fizz, buzz in zip(fizzes, buzzes))
    result = (word or n for word, n in zip(fizzes_buzzes, its.count(1)))
    for i in its.islice(result, 100):
        print(i)
```

如果您想阅读更多关于这个令人惊奇的标准库工具的内容，并更全面地了解上面演示的代码，那么我强烈推荐我不久前写的一篇文章，这篇文章是关于 itertools 以及它为什么如此伟大的:

</wicked-fast-python-with-itertools-55c77443f84c>  

# №3:停止嵌套

新手程序员经常犯的一个错误，也是我年轻时犯的一个错误，就是嵌套。嵌套是危险的，因为它会严重影响算法的性能，并使代码几乎无法阅读。没有人喜欢回溯来查看你的代码到底在做什么。在很多方面，我们可以把嵌套看作给定代码块的层。关于嵌套要记住的重要事情是，它本身就是一个循环，不管这个循环是否重复。任何嵌套的东西都可能有自己的作用域，这意味着在其作用域中声明的值不会是全局的。

这就是为什么嵌套如此成问题的核心。每次创建 for 循环时，仅仅循环遍历 iterable 是不够的。此外，每次我们调用另一个 iterable 的索引时，在 iterable 上调用循环是一件非常麻烦的事情。当然，有些情况下这是不可避免的——所以不要误解我的意思，这不是对所有嵌套 for 循环的讨伐。然而，我碰巧认为在许多情况下，嵌套是可以避免的。

我的第一个技巧可能有助于避免编写嵌套的 for 循环，那就是使用索引。如果需要调用索引，可以在迭代器上使用 enumerate()类，方式与上面使用 zip()的方式类似。说到 zip()，这个类也是避免嵌套循环的另一个好方法。这是因为使用 zip()可以通过迭代一次处理多个列表，有时不需要在当前列表下运行另一个 for 循环。当然，在这方面，压缩和索引基本上可以互换使用。

# №4:不要压缩()字典！

另一个很好的技巧是在使用字典时不要使用 zip()类。原因是没有必要这样做。在我解释原因之前，让我们用字典快速写一个循环，看看 Python 在迭代时做了什么:

```
dct = {"A" : [5, 6, 7, 8], "B" : [5, 6, 7, 9]}
for i in dct: print(i)A
B
```

每当我们进行这个调用时，它都会迭代字典的键。字典的键的伟大之处在于它们直接连接到 Python 语言的内置 get 索引函数。这意味着，如果我们想要获取值，我们不需要创建一个全新的 zip 迭代器类来实现。这将避免运行全新的初始化方法，并在内存中存储全新的对象定义。相反，我们可以用键的索引来调用值。

```
for i in dct: print(dct[i])[5, 6, 7, 8]
[5, 6, 7, 9]
```

此外，如果我们只想处理值，我们可以简单地调用 dct.values():

```
for i in dct.values(): print(i)
[5, 6, 7, 8]
[5, 6, 7, 9]
```

# №5:过滤器()

我的最后一个循环技巧是利用 Python 的内置 filter()方法。这种方法可以用来以最小的性能代价消除 iterable 的某些部分。这意味着，如果你实际上不需要循环，你可以完全避免循环。不用说，特别是在数据科学领域，这经常会派上用场。该方法可以在 for 循环定义之前或内部调用，就像这个列表中的许多其他示例一样。

当然，这并不是这种方法的唯一应用。也就是说，对于那些想用 Python 处理数据的人来说，这是一个很好的学习方法。下面是一个例子，通过在循环之前过滤掉一些不需要的值，for 循环变得更快:

```
people = [{"name": "John", "id": 1}, {"name": "Mike", "id": 4}, {"name": "Sandra", "id": 2}, {"name": "Jennifer", "id": 3}]
for person in filter(lambda i: i["id"] % 2 == 0, people):
...     print(person)
... 
{'name': 'Mike', 'id': 4}
{'name': 'Sandra', 'id': 2}
```

# 结论

迭代是一种复杂的野兽，只需要五分钟左右就可以学会，但很可能需要几年才能掌握。幸运的是，对于 Python 来说，这种语言的高级本质确实有助于简化这种计算。也就是说，虽然在这样一种声明式语言中，性能可能是人们很少担心的事情，但它总是很重要，利用这些有用的技巧可能会有所帮助。非常感谢您的阅读，我希望其中的一些技巧在您下一次编程冒险中派上用场！