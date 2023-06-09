# 赢得任何动态编程面试的一个奇怪技巧

> 原文：<https://towardsdatascience.com/one-weird-trick-to-ace-any-dynamic-programming-interview-4584096a3f9f?source=collection_archive---------38----------------------->

## 八行 Python 代码来记忆任何动态编程问题。只有一个，如果你觉得刻薄

![](img/40686022019306ba414c15db526f78ce.png)

难道你不想成为像他一样酷的动态编程奇才吗？尼古拉·伊万诺夫摄于 [Pexels](https://www.pexels.com/photo/actor-adult-business-cards-547593/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

# 介绍

如今，技术面试是一种文化现象，已经渗透到几乎所有科技公司的核心。如果不回答二年级算法和数据结构课程中的一些晦涩难懂的问题，几乎不可能找到一份软件工作。

当我第一次开始面试时，我记得最大的麻烦是动态编程问题。你知道，如何找到一个最大的子列表，或者计算出给定一组硬币和一个愤怒的顾客，你是否能做出改变。那些真正有用的问题，我在日常工作中一直都在使用...最近，我在一次采访中对自己说，“这太愚蠢了，它到底在测试什么？他们为什么要让我这么做？”所以我选择拿这个问题开个小玩笑。在本教程中，我将通过一种有点开玩笑的方式来记忆问题的任何递归解决方案。这将允许您学习一种技术，并能够记忆任何具有不可变输入的递归函数。是的，你听到了，任何具有不可变输入的递归函数。

我们开始吧！我们将看看子集和问题。

# 子集和问题

> 给定一个正整数列表`ls=(1..n)`和一个整数`k`，有没有某个`ls`的子集的总和正好是`k`？

# 初始解

从构造这个问题的简单递归解决方案开始，不要担心时间复杂性。让我们想一想，最简单的方法是构造所有可能的子列表，并对每个子列表求和。如果一个子列表的总和等于我们想要的值`k`，那么我们就完成了，我们返回 True，否则返回 False。看起来很简单，对吗？我们只用下面几行代码就可以完成。

```
def subset_sum(ls: Tuple[int], total: int, total_sum: int) -> bool:

    if total == total_sum:
        return True

    for idx, val in enumerate(ls):

        new_ls = ls[:idx] + ls[idx + 1:],
        if subset_sum(new_ls, total, val + total_sum):
            return True

    return False
```

建立一个基本案例，查看`total_sum`是否等于期望的`total`。这将告诉我们是否达到了目标，我们应该返回 True。有了基本案例，我们就可以专注于主要逻辑了。这也很简单。我们只需要遍历列表中的每个元素，然后:

1.  创建一个删除当前索引的新列表
2.  将我们的当前值添加到我们的`total_sum`
3.  从新列表中向下递归所有子集。

Tada！我们已经解决了这个问题，并证明了我们可以对我们未来的新公司练习面试问题！他们现在肯定会雇用我们的！

但是等等！精明的受访者会注意到这个算法在时间复杂度方面很糟糕，它将在`O(n!)`运行🙀。没有人会雇佣表现如此糟糕的我们。但是我们很聪明，我们知道这个问题是一个动态规划问题，所以我们要做的就是记住它。引用维基百科:

> 记忆化是一种优化技术，主要用于通过存储昂贵的函数调用的结果并在相同的输入再次出现时返回缓存的结果来加速计算机程序。

所以真正的关键是缓存我们已经运行的执行。举例来说，这意味着当我们执行`subset_sum`时，我们需要记住计算的结果。假设我们运行输入如下的函数:

```
total_sum = 5
total = 10
ls = (3)
```

我们的函数将 3 加 5 得到 8，我们的列表是空的，所以我们不会达到 10 并返回 False。记忆化就是记住，对于 5，10 和(3)的输入，我们得到 false，所以我们可以不做计算，只查找我们缓存的 False 值。

Python 的`functools` 模块有一个装饰器就是做这个的！如果以前见过该输入组合，它会自动记住函数返回的内容。我们可以用一行 python 来记忆我们的整个函数…

```
from functools import lru_cache

@lru_cache(None)
def subset_sum(ls: Tuple[int], total: int, total_sum: int) -> bool: # All the previous code.
```

就是这样。我们完了。我们记住了它，并有了一个完全动态的解决方案。现在，这可能不是面试官想要的。他们对这些问题的解决方案不感兴趣，他们感兴趣的是出于某种原因看你编码🤷‍♀.所以我们假设的采访者反驳道，“非常有趣，但是让我们记住这个解决方案。假设你没有`lru_cache`功能。”

对此你的回答是，“好的，女士/先生，我很乐意效劳。那我们就实施`lru_cache`怎么样？这样，我们的记忆可以应用于你的组织中任何人可能面临的任何问题。该解决方案将优于仅仅记忆这个问题，因为它在一般情况下是有效的。”

面试官笑了笑，同意了你的提议，认为你是个傻瓜，认为你不可能在剩下的时间里实现这么好的裤子功能。但你不是在玩，你是个坏蛋。💪

让我们从简单的开始。我们需要一些方法来知道我们正在记忆哪个函数，我们也需要一些方法来存储我们已经看过的以前的函数运行。我们首先创建一个包含两个初始化变量的类:

```
class Memoize:

    def __init__(self, f):
        self.f = f
        self.memoized = {}
```

`f`存储我们将要执行的函数在我们的例子中`subset_sum,` `memoized`是一个字典，其中的键是我们函数的参数，值是给定这些参数的函数的返回值。现在你明白了为什么函数的输入必须是不可变的，因为我们在字典中散列它们。

我们已经成功了一半……现在我们想让它像装饰器一样工作，包装任何函数，所以我们将添加一个`__call__`方法。这个方法应该接受一组任意的参数，所以它需要接受`*args`作为它的输入。如果我们从来没有在记忆的字典中看到过那组参数，用那些参数执行函数，那么逻辑就不成立了。否则，我们只返回存储在字典中的缓存值。

```
class Memoize:

    def __init__(self, f):
        self.f = f
        self.memoized = {}

    def __call__(self, *args):
        if args not in self.memoized:
            self.memoized[args] = self.f(*args)
        return self.memoized[args]
```

就是这样…我们现在可以把我们的原始函数记为:

```
@Memoize
def subset_sum(ls: Tuple[int], total: int, total_sum: int) -> bool: # All the previous code.
```

面试官很惊讶，因为他们从来没有想过在每个具体的案例中解决记忆问题。你得到了这份工作和 10 分钟的生活。这对每个人都是双赢的。

# 最后的想法

需要记住的一点是，这依赖于你可以为你的函数创建一个输入散列。这就是为什么我使用元组而不是列表。如果对象不能被散列，它就不能被缓存，至少在这种情况下是这样。