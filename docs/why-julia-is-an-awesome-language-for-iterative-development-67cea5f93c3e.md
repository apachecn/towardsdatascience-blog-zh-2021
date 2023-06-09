# 为什么 Julia 是迭代开发的绝佳语言

> 原文：<https://towardsdatascience.com/why-julia-is-an-awesome-language-for-iterative-development-67cea5f93c3e?source=collection_archive---------32----------------------->

## 意见

## 扔掉旧的大开发解决方案，因为这个更好

![](img/be89e6609940278ef26310a911a64b40.png)

[https://pixabay.com/images/id-516559/](https://pixabay.com/images/id-516559/)

# 介绍

TJulia 编程语言是一种相当新的语言，它已经在软件工程和科学计算社区掀起了一场风暴。这有很多不同的原因，因为 Julia 编程语言是可用的最快的语言之一，当然也是如此高水平的最快语言。这种语言编码像一种脚本语言，语法非常类似于 Python 或 MATLAB 的语法，同时还保持令人难以置信的速度。这是古老的格言“像 Python 一样行走，像 c 一样运行”的地方。然而，尽管 Julia 是一种编译速度相当快的语言，但这肯定不是该语言唯一的吸引力。

该语言使用多重分派作为范例。这可以用编程创造出一些你在其他地方根本找不到的非常显著的结果。多调度往往被当作语言的主干，在语言的多个方面展现着自己的美丽。多重分派极大地影响了 Julia 编程语言的一个方面是在整个 Julian 生态系统中扩展模块的能力。这很酷，因为它创建了您可以添加的包，并且您已经知道一些方法，而无需查看文档。

# 多重派遣—概述

为了理解多重分派如何促进一些非常棒的迭代开发，我们首先需要理解多重分派到底是什么。多重分派是 Julia 编程语言的核心，没有多重分派的 Julia 根本就不是 Julia。这个概念允许我们接受多种类型，并通过相同的函数调用传递它们。这些函数调用可以限制在一个类型的父类的任何部分，这意味着该函数的多个版本可以仅使用一个类型来调度。如果你想进一步了解我为什么如此喜欢多重分派，我最近写了一篇文章，你可能会感兴趣:

</why-multiple-dispatch-is-my-favorite-way-to-program-786bf78f4878>  

虽然在我看来，多重分派是一种很好的编程方式，而且比使用其他编程概念生成的代码结构更自然，但我认为它在 Julia 语言中真正与众不同的地方是它几乎可以在任何地方使用。通常在编程中，我们在正常的全局范围之外编写两种不同类型的东西:

*   构造器
*   功能

这两者如何协同工作通常由我们正在使用的语言的范例决定。在 Julia 中，这两件事都遵循完全相同的编程概念，即多重分派。这使得 Julia 成为一种非常独特的语言，因为我们既有创建类型的 dispatch，也有创建方法的 dispatch。考虑下面的例子:

```
mutable struct CoolKid
    cool_status::Int64
    function CoolKid(height::Int64, weight::Int64, n_friends::Int64)
        cool_status = height - weight * -n_friends
        new(cool_status)
    end
end
```

上面的构造函数使用 dispatch 来创建 CoolKid 类型。获取 CoolKid 类型的第一种方法是直接调用外部构造函数。外部构造函数是中间没有函数的部分。如果我们使用一个整数作为参数来调用这个函数，我们将直接得到一个 CoolKid(integer)返回。

然而，如果我们用三个都是整数的参数调用这个构造函数，我们仍然会得到相同的一致的返回，但是我们会运行函数中提供的算法。为了方便起见，使用了 new()方法。我认为这是 Julian 编程的一个非常酷的方面，因为典型的全功能编程语言不能有类型的初始化函数，使用这种形式的分派，我们可以选择最终用户是否调用这个初始化函数。

# 积木

那么是什么让 Julia 和它的多重分派概念对迭代开发如此重要呢？多分派范例有许多优点，但是我认为有一点被严重忽视了，那就是方法的扩展。使用多重分派，语言内部的任何方法都可以扩展到新类型。这包括来自 Julia 的基本模块的方法，以及来自 Julia 的整个生态系统中的其他模块的方法。

考虑到这一点，我们很快意识到 Julia 的生态系统可以非常有效地迭代开发。向已经存在的代码中添加内容可以像向这些方法分派新类型一样简单。考虑下面的例子，其中我分派加法运算符来处理一个字典和一对。

```
import Base: +
+(d::Dict, p::Pair) = push!(d, pair)
```

这只是一行代码，通过这一行代码，二进制加法运算符对字典和 pair 类型变得非常有用。当然，这也可以从我们自己的模块和环境中有效地用于我们自己的类型，我可能在一篇文章中详细介绍了如何做到这一点，您可以在这里查看:

</extending-julias-operators-with-amazing-results-96c042369349>  

> 这篇文章实际上是我最近写的最喜欢的文章之一，因为它真正展示了 Julia 编程语言的伟大之处。

现在，使用我们的一行分派和一行显式导入，我们实际上对这种方法有了一个全新的用途，这种方法通常对这种类型基本上是无用的:

```
d = Dict(:A => [5, 10, 15], :B => [10, 15, 20])
d + :C => [25, 30, 35]
```

# 结论

Julia 编程语言非常适合做很多不可思议的事情。这些概念中有很多可能更符合科学，但是我认为大多数人都同意多分派范例对软件工程来说是一个巨大的优势。它的一种应用方式是在迭代开发中。这是因为 Julia 中的大多数东西都可以建立在一个方法之上，例如 Base.push 或 Base.filter，它贯穿于整个语言，用于从多个模块中分派多种类型——我认为这非常巧妙！非常感谢您阅读我的文章，我希望它至少对展示在 Julia 中编写自己的代码并与他人的代码一起工作有所帮助。