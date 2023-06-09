# 关于 Python 字典，您需要知道的

> 原文：<https://towardsdatascience.com/all-you-need-to-know-about-python-dictionaries-ccd05e5c61dd?source=collection_archive---------3----------------------->

## 它们是什么，何时使用它们，以及如何高效地使用它们！

![](img/27302339995fedc4b098d34c156d2662.png)

本·怀特在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

# 介绍

成功地处理数据并编写可读和高性能的代码是我们努力的目标。实现这一目标的一个关键部分是为给定的问题选择理想的数据结构。数据结构是一种组织数据的特殊方式，以便可以有效地存储、检索或更新数据。

Python 自带各种内置的数据结构，例如列表、元组、集合、队列或字典等等。在本帖中，我们将看看*词典*。我试图涵盖从新手的基本用法到专业人士的高级主题的广泛范围。让我们看看我是否能兑现💪。

# 字典

让我们从一个简单的问题开始，这个问题很可能我们所有人都已经能回答了

> 什么是字典？

字典是具有唯一键的键值映射。相应的值可以是任何类型。在其他编程语言中，您可能会发现 map、hashmap、关联数组或查找表等术语都指代同一个概念。

那么，字典有什么用呢？它们适合通过*键*以快速和可读的方式访问元素，而不必搜索整个数据集。这意味着您可以同时获得性能提升和使用字典编写更可读的代码。现在，他们有什么属性？

字典是可变的，或者如果你想骄傲的话，是可变的😃。这意味着您可以随时更新、添加或删除键值对。

此外，由于 Python 3.7 *字典保留插入顺序*。也就是说，当你迭代一个字典的元素时，元素将按照它们被添加时的顺序被遍历。如果您使用 Python 3.6 或更早版本，我希望您不要这样做😃，你必须使用一个 [OrderedDict](https://docs.python.org/3/library/collections.html#collections.OrderedDict) 来保证你的字典的顺序。

在我们开始研究真正的代码之前，我想提到的最后一点是*字典键必须是可散列的*。你也经常读到键必须是不可变的，但那只是因为不可变类型也是可散列的。可以用作键的哈希类型的例子有数字、字符串或数字或字符串的元组。您*不能*用作键的可变类型是例如列表或字典。所以你不能用字典作为字典中的键😃。顺便提一下，如果你想使用某个类的实例作为键，你必须为那个类实现[魔法函数](/how-to-write-awesome-python-classes-f2e1f05e51a9) `__hash__`。

好了，说够了，让我们把手弄脏，来有趣的部分；实码。

## 创建词典

我们需要知道的第一件事是我们如何能创造一本字典。Python 提供了各种方法来做到这一点，所以让我们看看

创建词典

创建词典有两种基本方法。首先，您可以使用花括号并向其中添加逗号分隔的`key: value`对。其次，您可以使用`dict`类并将键值对传递给构造函数。当您的键是字符串和适当的 Python 名称时，这很好。如果不是，你将不得不传递一个形式为`(key, value)`的元组的 iterable 到`dict`。这实际上是在编写第 6 行所示的`dict(zip(keys, values))`时以一种非常紧凑的方式得到的。

创建字典的另一种方法是将多个字典结合起来。你怎么能这样做？你可以通过用`**`操作符解包字典，然后用花括号把它们组合起来，见第 9 行。Python 3.9 中引入的另一种方法是使用`|`操作符来连接字典，如第 10 行所示。

如果组合字典有公共键，将使用最后添加的那个值。但是，第一个添加的将决定插入顺序。在给定的例子中，这意味着`combined`的第一个键值对是`python: 10`。听起来很疯狂，不是吗？我只能建议玩简单的玩具例子，并熟悉这些细节。

最后，我想简单提一下字典理解，如第 14 行所示。您可能已经熟悉了列表理解来创建列表，这与创建字典是一样的。因为这个概念应该是相当众所周知的，所以我只给你一个例子。

## 从字典中阅读

既然我们现在知道如何创建字典，我们应该开始利用它们存储的数据。同样，让我们从一些代码开始

从字典中读取数据

获取条目最常见的方式是使用第 1 行所示的键在字典中建立索引。这种方法的一个问题是，如果一个键不在字典中，就会引发一个`KeyError`异常。为了避免这种情况，您可以使用字典的`get`方法，如第 2 行所示。此方法或者返回与键关联的值，或者如果找不到键，则返回默认值。如果不指定默认值，它将返回`None`。

为了不仅处理单个键值对，而且处理整个数据，字典提供了不同的方法来访问所有条目。在第 3 行，您可以看到如何使用`items()`方法迭代所有的键值对。

您还可以迭代字典本身。在这样做的时候，您迭代这些键，如第 7 行所示。另一种迭代或获取所有键的方法是使用`a_dict.keys()`。

最后，如果您只对值感兴趣而对键不感兴趣，您可以使用`a_dict.values()`来获得它们。在第 10 行，你可以看到一个例子，我们计算字典中所有语言的平均等级。

## 更新词典

正如开头所说，字典是可变的。这意味着我们可以添加、删除或更新字典的条目。让我们看看 Python 为此提供了什么

如第 2 行所示的`setdefault`函数可能是 dicts 公开的最令人困惑的命令😕。那么它是做什么的，有什么帮助呢？如果在字典中没有找到给定的键，`setdefault`将带有给定默认值的键添加到字典中，并返回该值。这意味着它更新了字典。如果键存在，它将返回相应的值。尽管函数的名字令人困惑，但它可以帮助您用更少的`if-else`语句编写更少的代码。使用这种方法的另一种方法是使用集合模块中的`[defaultdict](https://docs.python.org/3/library/collections.html#collections.defaultdict)`。

现在，要更新或添加条目，我们可以使用索引操作并赋值，如第 3 行所示。如果我们想要添加或更新多个条目，我们可以使用第 4 行所示的`update`方法。或者，从 Python 3.9 开始，我们可以使用`|=`操作符，如第 5 行所示。在这两种情况下，我们都必须将要添加或更新的键值对放入另一个字典中，并将其传递给方法或操作符的左侧。

最后，要从我们的字典中删除条目，我们有两个方法，即`popitem`和`pop`。Popitem 移除最后插入的项，并以元组的形式返回相应的键值对。与此相反，`pop`删除给定键的键值对，并返回相应的值。如果不指定默认值，当找不到键时，`pop`会引发一个`KeyError`。如果指定了默认值，则在键不存在的情况下将返回该值。`popitem`和`pop`都修改调用它们的字典。

最后，还可以使用`del`删除项目。但是，我不喜欢这个语法，故意把它留在这里。抱歉，我不得不固执己见😃

## 使用字典键入注释

我喜欢现代 Python 的一点是类型注释。类型注释极大地帮助我们理解代码和接口。此外，它们提高了我们的编码速度，因为我们的 ide 在自动完成时会用到它们。最后，当使用像 [mypy](http://mypy-lang.org/) 这样的类型检查器时，您可能会在投入生产之前就发现错误。

因为我们没有讨论类型注释的细节，所以让我们继续讨论如何对我们的字典进行类型注释。您可能已经猜到了，我们从一些代码开始

我在这里做了什么？首先，我创建了一个接受字典作为输入并返回字典的函数。要进行类型注释，您可以使用来自[类型模块](https://docs.python.org/3/library/typing.html)的`Dict`，或者从 Python 3.9 开始，您可以与`dict`交换以节省一次导入。现在，必须将键的类型指定为第一个参数，将值的类型指定为第二个参数。就是这样。很简单，不是吗？我希望你们都同意，这个界面比随便输入名字更容易理解。

关于类型注释，我想介绍的最后一点是所谓的[类型注释](https://www.python.org/dev/peps/pep-0589/)。当你预先知道你的键的名字和类型时，你可以使用 TypeDict。为此，您必须编写一个从 TypedDict 继承的类，并将键定义为属性，并用相应值的类型对它们进行类型注释。然而，在我看来，它们的用途相当有限，在许多情况下，您可以使用功能更丰富的[数据类](https://docs.python.org/3/library/dataclasses.html)或[命名的元组](https://docs.python.org/3/library/typing.html)。

## 词典的替代用法

在结束这篇文章之前，我想谈谈我们如何使用字典不仅保存数据，而且提高代码库的可读性。为了说明这一点，我给你们看两个突出的例子。

首先，有了字典，我们可以替换某些 if-else 语句，使我们的代码不那么冗长，更整洁。这是怎么回事？我们来看一些代码！

在给定的示例中，我们希望构建一个函数来从三个不同的数据仓库加载数据。对于每个仓库，我们都有一个专门的功能来完成这项工作。因此，根据定义的仓库名称，目标是选择三个函数中的一个。一种简单的方法是使用一些 if 子句来检查仓库名称，以使用正确的函数。这显示在功能`load_data_verbose`中。

或者，我们可以定义一个字典，将仓库名称映射到相应的函数。现在，我们所要做的就是使用仓库名称从字典中获取函数，如`load_data.`所示，这是一个更好的接口，也更容易扩展到更多的仓库。如果必须添加一个新的，我们只需编写加载函数并更新字典。完成了。

我想提到的第二个也是最后一个例子是，我们可以在调用函数时使用字典来指定关键字参数。以上面的例子为例，我们可以定义一个字典`call_args={"data_base":"snowflake", "from_": datetime.utcnow()}`，并使用它来调用`load_data`函数，就像`data = load_data(**call_args)`。例如，当您想要有条件地覆盖关键字参数的默认值时，这种语法会非常方便。

大概就是这样。咳，那篇文章比我最初想象的要长得多😃会的。

![](img/ca81a0edafdb0cff58985fcb7f6c6ac6.png)

照片由[悉尼·瑞伊](https://unsplash.com/@srz?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 包裹

在这篇文章中，我们讨论了什么是 Python 字典以及如何有效地使用它们。我的目标是为新手和专业人士提供见解。我希望我已经做到了这一点，并且您现在已经掌握了新的知识，能够编写更棒的代码，并交付您的下一个数据项目。

感谢您关注这篇文章。一如既往，如有任何问题、意见或建议，请随时联系我或关注我，无论是在这里还是通过 [LinkedIn](https://www.linkedin.com/in/simon-hawe-75832057) 。