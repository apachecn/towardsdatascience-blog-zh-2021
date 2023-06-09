# 数据科学中更好的软件编写技巧:工具和错误

> 原文：<https://towardsdatascience.com/better-software-writing-skills-in-data-science-tools-bugs-8cbf94c2c456?source=collection_archive---------43----------------------->

## 实用程序设计员的每周指导章节阅读

![](img/bb063fab567f2ed1e8862e8c68762bdd.png)

由[尼姆罗德·柳文欢](https://pixabay.com/users/nimrodins-12874542/)在[皮克斯贝](http://pixabay.com)拍摄的封面图片。

本周的指导和帖子基于“务实的程序员:从熟练工到大师”的第三章:务实的方法。那一章的重点之一是关于交易的工具，以及掌握这些工具。

如果你现在习惯的唯一工具是 Jupyter 或者另一个类似笔记本的环境，也许是时候尝试不同的方法了。只使用类似笔记本的环境可能会给你带来不好的编程习惯，这可能很难改变。尝试使用支持 IDE 的 Python 来编写一些 Python 代码，比如 PyCharm 就是其中之一，或者甚至是您将在命令行上执行的纯文本。学习不同的编码方法，这将帮助你理解这些方法的成本和收益。

作为一名数据科学家，尝试不同的方法来查询数据，也许你的组织已经支持不同的数据库？学习如何使用 pyspark、SQL……如果这适用于你的工作，尝试不同的深度学习框架。工具是无穷无尽的，你不需要对它们都有很深的了解，但你应该尝试一下，看看它们的优缺点，有意识地选择哪一个最适合你和手头的任务。

工具很重要的另一个领域是调试他们的代码(或查询)，我在这个领域看到了许多初级程序员和数据科学家要解决的问题。

本周我的文章的重点是调试。Python 练习将包括调试一个小的 Python 函数。如果你发现 bug 比较早，你在 Python 里面大概也没那么初级吧！尽管如此，我还是鼓励你把这些步骤当作练习来完成。记住，熟能生巧！

将这段代码放在您最喜欢的 Python 执行环境中，让我们按照书中概述的调试过程进行调试。

1.  干净地编译代码:对于 Python 来说，这应该不成问题… Python 是一种解释型语言。但是，例如，如果您将代码保存在 Jupyter 笔记本中，您可能会忘记之前运行了什么。因此，一个好的方法是重启内核，一个单元一个单元地重新执行代码。你的 Jupyter 笔记本电池坏了吗？也许你可以花时间把它们按照你想要的顺序排列。
2.  理解错误报告:通读函数意图和三个“测试”语句。你能理解什么是预期的行为吗？也许你能马上发现这个错误！
3.  重现 bug:bug 可重现吗？在这个具体的例子中，它应该已经很容易被复制了，但是在现实生活中，你可能需要做一些工作来使它在一个步骤中被复制。为了更好地理解您看到的行为，您还想添加其他测试吗？你能运行这些测试并一步再现问题吗？
4.  可视化你的数据:这里有许多方法是可行的。您可以决定使用 pdb，Python 调试器(如果您还不了解调试器，了解它可能是个好主意)。例如，如果您正在处理 ETL，您可能必须查询由 Python 文件生成的数据。如果您的 ETL 正在为一些机器学习阶段准备数据，您可能希望创建一种自定义的方式来可视化那些“错误的”数据。
5.  跟踪:除了使用调试器之外，或者在这种情况下，您可以在代码中添加一些跟踪。可以通过日志文件进行跟踪(在这种情况下，我强烈建议使用支持跟踪级别的日志框架，例如 INFO、ERROR、DEBUG……以便您可以保留设计良好的跟踪，供将来调试使用)，或者对于像这样的简单问题，您可以简单地决定添加一些打印语句来跟踪数据流。
6.  查看损坏的变量:这不是你通常用 Python 必须做的事情，但是如果你使用其他编程语言，要注意这是可能发生的事情。例如，在 C 语言中，你可以在内存中的任何地方写任何东西，所以一个来自程序另一部分的简单的索引错误可能会破坏“你的”变量。

你还没发现窃听器吗？不要绝望，还有几步路可以走！

1.  橡皮鸭:向其他人解释问题，或者如果你像我们许多人一样因为 COVID 而被禁闭，向你的猫解释，或者如果你独自被困在一个荒岛上，向威尔逊解释！大声说出来也许能帮你想明白。
2.  排除过程:正如作者在书中所说，错误可能出现在操作系统、编译器或第三方产品中。然而，在我 25 年以上的软件职业生涯中，只有一次我遇到的错误可以追溯到编译器，那是很久以前的事了，在 Fortran 编译器中。而且只有一次错误可以追溯到计算机主板的错误硬件设计。这些错误通常很难发现，所以它们不经常发生是件好事。通常情况下，如果你的 bug 涉及到软件的其他部分，可能是你没有以正确的方式解释第三方文档。
3.  惊奇元素:当你发现自己认为这个 bug 是不可能的，是时候重新评估你所坚持的真理了。*微妙的暗示，这里可能就是这样。*

这里发生了什么？在这种情况下，当你知道 Python 是如何工作的时候就很简单了。Python 中的默认参数不会在每次调用函数时重新计算，而是在解析函数定义时才重新计算一次。每次在没有第二个参数的情况下调用该函数时，对同一个“空”列表的引用将被用作默认参数。对“空”列表所做的任何更改都将成为后续调用的“新”默认参数，这些调用不会提供第二个参数。

了解交易工具包括了解你使用的编程语言。Python 有很多好的特性，因为它是一种多范例编程语言。在 Python 中，您可以使用过程式编程方法、面向对象方法或函数式编程方法。这些给了 Python 很大的灵活性，也给了你很大的伤害自己的可能性！花时间学习你使用的编程语言，它使什么变得容易，以及它在什么地方使事情变得困难。

这是我对《实用程序员:从熟练工到大师》第三章阅读的补充，作为提高数据科学中软件写作技能的媒介。下周我们将看一看第四章:务实的偏执狂。

![](img/fdb5deb3f9f52d42535a8870633d5fb3.png)

在软件领域 20 多年了。目前在 Shopify 担任数据科学家。在深度学习、机器学习/分析、云计算、物联网、领域特定语言、遗传算法和编程、人工生命/智能以及所有技术领域的研究兴趣！[通过点击](https://thelonenutblog.wordpress.com/author/potvinpascal/)查看所有帖子

*原载于 2021 年 4 月 7 日*[*【http://thelonenutblog.wordpress.com】*](https://thelonenutblog.wordpress.com/2021/04/07/better-software-writing-skills-in-data-science-tools-bugs/)*。*