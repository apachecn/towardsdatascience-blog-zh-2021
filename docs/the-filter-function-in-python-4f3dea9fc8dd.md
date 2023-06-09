# Python 中的过滤函数

> 原文：<https://towardsdatascience.com/the-filter-function-in-python-4f3dea9fc8dd?source=collection_archive---------8----------------------->

## 了解如何使用 Python 中的过滤器函数

![](img/b7026c08918fd8527ee34ee144d3e744.png)

约书亚·雷德科普在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

尽管 Python 是一种面向对象的语言，但它仍然提供了提供函数式编程风格的函数。在上一篇文章中，我们讨论了其中的一个函数， ***映射*** 。在本文中，我们将讨论这些 Python 内置函数中的另一个，即 ***过滤器*** 函数。

在本教程中，我们将学习 Python 中的 ***滤镜*** 函数是什么以及如何使用。

*地图上的文章功能:*

</the-map-function-in-python-eb9a90707d17>  

## 使用 for 循环

假设我们想用一个已经有的列表来创建一个列表。但是我们希望我们的新列表只包含满足给定条件的元素。例如，我们有一个数字列表，我们想创建一个只包含偶数的新列表。我们可以使用 for 循环来完成这项任务，如下所示:

> 我们有一个数字列表， **list_of_nums** ，包含数字 1、2、3、4、5 和 6。我们想要创建一个新的数字列表， **list_of_even_nums** ，它只包含来自 **list_of_nums** 的偶数。所以我们创建了一个函数， **is_even** ，它接受一个输入，如果输入是偶数，则返回 True，否则返回 False。然后，我们创建了一个 for 循环，该循环遍历 **list_of_nums** ，并通过将该元素传递给 **is_even** 函数来检查列表中的每个数字是否都是偶数。如果 **is_even** 函数返回 True，则该数字被追加到 **list_of_even_nums** 中。如果 **is_even** 返回 False，则该数字不会追加到 **list_of_even_nums** 中。

另一种实现方式是使用内置的 Python ***过滤器*** 函数。

</two-cool-functions-to-know-in-python-7c36da49f884>  

## 滤波函数

[***filter***](https://docs.python.org/3/library/functions.html#filter)*函数接受两个参数:一个返回`True`或`False`的函数(检查特定条件)和我们想要应用它的 iterable 对象(如本例中的 list)。*

> *过滤器(函数，可迭代)*

*filter 函数从我们的列表(或者我们传入的任何 iterable)中获取每个元素，并将其传入我们给它的函数。如果将该特定元素作为参数的函数返回`True`，则过滤函数会将该值添加到**过滤对象**(然后我们可以创建一个列表，就像我们对由 ***map*** 函数返回的 map 对象所做的那样)。如果函数返回`False`，那么该元素将不会被添加到我们的**过滤器对象**中。换句话说，我们可以认为过滤函数是基于某种条件过滤我们的列表或序列。*

> *[x，y，z] → filter → [x(如果 f(x)返回 True)，y(如果 f(y)返回 True)，z(如果 f(z)返回 True)]*

> *如果我们有一个[x，y，z]的列表，那么如果 f(x)返回`True`，x 将被添加到**过滤器对象**。如果返回`False`，则不会添加到**过滤对象**中。 **f** 是我们传递给过滤函数的函数。如果 f(y)返回`True`，它将被添加到 filter 对象中。诸如此类…*

*同样， ***filter*** 函数会返回一个 **filter 对象**，它是一个迭代器。如果我们想从这个过滤器对象创建一个列表，我们需要将我们的**过滤器对象**传递给内置的 ***列表*** 函数(就像我们对地图对象所做的那样)，如下所示:*

> *列表(过滤器(函数，序列))*

## *使用过滤功能*

*然后我们可以使用 ***过滤器*** 功能创建上面的列表如下:*

> ***过滤器**函数从 **list_of_nums** 中获取第一个元素，即 1，并将其作为参数传递给 **is_even** 函数(因为我们将该函数作为第一个参数传递给了**过滤器**函数)。 **is_even** 函数然后返回`False`，由于 1 不是偶数，所以 1 不加到我们的 **filter 对象**中。然后， **filter** 函数从 **list_of_nums** 中获取第二个元素，即 2，并将其作为参数传递给 **is_even** 函数。 **is_even** 函数返回`True`，因为 2 是偶数，因此 2 被添加到我们的**过滤对象**中。在遍历完 **list_of_nums** 中的其余元素并且将其余偶数添加到我们的**过滤器对象**中之后， **list** 函数将这个**过滤器对象**转换为一个列表，并且该列表被分配给变量 **list_of_even_nums** 。*

## *使用 lambda 表达式*

*我们可以通过传入一个 lambda 表达式作为我们的函数来进一步缩短代码:*

**了解****λ****函数在这里:**

*</lambda-expressions-in-python-9ad476c75438> * 

## *列表理解与映射和过滤*

*如果我们回想一下，列表理解被用来从其他序列中创建列表，或者通过对元素应用某种操作，或者通过对元素进行过滤，或者两者的某种组合。换句话说，列表综合可以具有与内置的 ***映射*** 和 ***过滤器*** 功能相同的功能。应用于每个元素的操作类似于 ***映射*** 函数，而如果我们在列表理解中添加一个条件来将哪些元素添加到列表中，那就类似于 ***过滤*** 函数。此外，添加到列表理解开头的表达式类似于可以在映射和过滤函数中使用的***λ***表达式。*

## *例子*

*这是一个列表理解，仅当元素是偶数时，才添加从 0 到 9 的元素的平方:*

```
*[x**2 for x in range(10) if x%2==0]# [0,4,16,36,64]*
```

*我们可以使用 ***映射*** 和 ***过滤*** 函数，以及 lambda 函数，来完成同样的事情:*

```
*list(map(lambda x:x**2, filter(lambda x:x%2==0, range(10))))# [0,4,16,36,64]*
```

> *传递给 **map** 函数的函数是一个 lambda 表达式，它接受输入 x 并返回它的平方。传递给**映射**函数的列表是一个过滤列表，包含从 0 到 9 的偶数元素。*

**如果你喜欢阅读这样的故事，并想支持我成为一名作家，可以考虑注册成为一名灵媒会员。每月 5 美元，你可以无限制地阅读媒体上的故事。如果你用我的* [*链接*](https://lmatalka90.medium.com/membership) *注册，我会赚一小笔佣金。**

*<https://lmatalka90.medium.com/membership> * 

**希望你喜欢这篇关于 Python 中* ***滤镜*** *功能的文章。感谢您的阅读！**