# Rust 编程语言的简短介绍

> 原文：<https://towardsdatascience.com/a-not-so-short-introduction-to-the-rust-programming-language-2e8542a06b76?source=collection_archive---------2----------------------->

## 从这里开始，快速学习一门快速、安全、现代的语言

![](img/ced74389caf8f9cef177b23773b30c3d.png)

图片来自[维基共享资源](https://commons.wikimedia.org/wiki/File:RED_RUST_TEXTURE.jpg)

你最喜欢的编程语言是什么？

如果你的答案不是生锈，那么请阅读这篇文章。最后，你的答案可能会改变！

在这篇文章中，我将教你 Rust 编程的基础知识。足以让你开始并创建自己的程序。

在文章的最后，我会指导你一些非常好的深造方向。

您可以在 Rust 培训期间以小词典或查找文章的形式回到本文。

学习一门新的编程语言就像学习任何其他语言一样。最快的方法是尝试一下，在这种情况下，你不需要来自不同国家的朋友或飞机。你只需要你的新朋友 Rust 编译器。相信我，它会是一个真正的好朋友。

因此，请随意编写代码，尝试自己的例子，或者像阅读任何其他文章或书籍一样，简单地用一杯浓咖啡阅读这篇文章。

让我们开始吧…

# 目录

[安装和第一个项目](#cdf0)
[变量](#8cb5)
[数据类型](#97ff)
∘ [数字](#cf00)
∘ [布尔值](#1cb8)
∘ [字符串、 & str 和字符](#260e)
[集合](#40cf)
∘ [数组](#c68c)
∘ [元组](#6e43)
∘ [向量](#ccf2)
∘ [哈希映射](#1abe)
[函数](#316f)
[控制流和循环](#25cf)
∘ [条件](#7af5)
∘ [循环](#95ce)

Rust 已经存在，如果你想学习一门既安全又经得起未来考验的现代表演语言，Rust 是一个不错的选择。

Rust 是一种系统编程语言，运行速度极快，几乎可以防止所有的崩溃，并消除数据竞争。

尽管 Rust 被归类为系统编程语言，但你真的可以在 Rust 中构建任何东西。你只需要牺牲一些时间。作为回报，你得到的是安全和惊人的速度。

Rust 以难学而闻名，但我认为这实际上取决于最初的方法和心态。

你只需要在编码时有一点不同的想法——就像一个乡下人！

# 安装和第一个项目

Rust 的安装没有痛苦，这要感谢一个叫做 rustup 的小工具。

你可以按照这里的说明[安装 Rust](https://doc.rust-lang.org/book/ch01-01-installation.html)或者只是通过谷歌搜索。

当你安装了 Rust 和它神奇的软件包管理器——Cargo——之后，你就可以开始工作了。

假设您想要创建一个名为“rusty_cli”的项目。

在您的文件系统上找到一个您想要放置项目的位置。然后将自己“cd”到*命令/终端*中的位置。

当您在想要放置项目的文件夹中时，只需使用`cargo new rusty_cli`。

Cargo 将施展它的魔法，创建一个它理解的项目结构，包括一个名为`src`的文件夹，里面是一个名为`main.rs`的文件。

文件`main.rs`是程序的入口点。为了运行程序，你有几个不同的选择使用货物。

您可以使用`cargo run`在调试模式下运行主文件，或者使用`cargo build` 创建可执行文件。这个可执行文件将存储在`target/debug`中。

> 你不必使用 cargo 来编译和运行 Rust 程序，但它是一个非常友好的工具，我强烈推荐使用它。

当您准备好构建最终的可执行文件时，您可以使用命令`cargo build --release`对其进行编译和优化。该命令将在`target/release`而不是`target/debug`中创建一个可执行文件。

这些优化使 Rust 代码运行得更快，但编译时间上的损失很小。

# 变量

Rust 中的变量是使用`let`关键字定义的，默认情况下是不可变的。我们来举个例子。下面的代码将*还没有*编译。

如果你一直跟随，那么你会看到编译器抱怨类似“*不能给不可变变量*赋值两次”。

为了解决这个问题，我们可以采取以下措施:

注意，如果我们把关键字`mut`放在变量名的前面，那么变量就变得可变了。

另外，请注意 Rust 中的表达式是如何工作的。表达式是返回值的东西。如果你加上分号，你就抑制了这个表达式的结果，这在大多数情况下是你想要的。

当我们一会儿谈到函数时，这一点会更清楚。

# 数据类型

数据类型通常与算术运算密切相关，但我不会花太多篇幅来讨论这个问题，因为对数字的常见运算也适用于 Rust。

Rust 中的许多数据类型与其他语言共享。我们有整数类型，如`i32`或`i64`，也有浮点数类型，如`f64`。

我们还有数据类型`bool`，它可以包含值`true`或`false` *，*我们有`string` *，* `*&str*`和`char`用于存储文本数据，还有`tuple`，`array`，`vector`和`hash map`作为一些常见的集合。

在此之上，我们有`structs` *、* `*methods*` 和`associated functions`作为 *OOP* 语言中类和方法的替代，还有一个有趣的类型叫做`trait`，有点像*接口*，例如 *Go* 。

除了用于结构化相关数据的结构和元组结构，我们还有在 Rust 语言中起核心作用的类型`enum`。

其中一些类型的用法最好通过例子和自己的实验来学习，但是，我认为在这一点上一些最初的解释和例子是合适的。

## 数字

请注意，当您声明变量时，您可以选择通过在声明中显式声明来指定数据类型。

如果我们想存储一个包含大小为 8 位的无符号整数的变量，我们必须像下面这样做:

如果你刚刚写了`let age = 18;`，那么 Rust 会推断出年龄的类型是`i32`。

## 布尔运算

Rust 中称为“布尔”的布尔与其他语言中的布尔相似。语法是`true`和`false`(注意小写)，一个例子是`let b = true;`。

## 字符串、字符串和字符

字符类型用单引号写成，如*‘c’*，表示数据类型的关键字是`char`。

Rust 中的字符串比 Python 中的要复杂一些，但这是因为 Python 中隐藏了很多细节。嗯，没有那么多铁锈！

这样做的原因是为了防止将来处理字符串时出现错误。Rust 中的一个常见概念是，该语言通过处理编译时可能出现的错误来确保安全性。无论如何，这是一件好事，但它对程序员提出了一些要求。

字符串被实现为字节的集合，当这些字节被解释为文本时，还有一些方法提供有用的功能。

字符串比许多程序员认为的更复杂。这是因为它们对程序员来说很自然——毕竟，我们现代人习惯于在日常生活中处理文本。

然而，由于我们认为有意义的子串和机器如何解释子串之间存在差异，事情并不像看起来那么简单。我们需要一种叫做编码的东西作为机器和大脑之间的桥梁。

我们不会深入编码世界的细节，但是如果你发现自己有一天晚上无法入睡，那么尽一切办法进行一次研究之旅，深入研究编码，它比你想象的更令人着迷！

Rust 在`UTF-8`中对字符串进行编码，与 Python 不同，我们可以让字符串在 Rust 中生长。

如上所述，Rust 有不止一种类型的字符串。类型`String`和类型`str`，后者通常以`&str` *、*的形式出现，被称为*字符串片*或*字符串文字*。

一个`String`被存储为一个字节`Vec<u8>`的向量，并带有方便的方法:

我们将很快处理向量。现在，你可以把它们看作一个典型的数组。

这两种类型的字符串之间到底有什么区别，现在就跳过，但是我能说的是，如果你做一个如下的变量:

```
let s = "Towards Data Science";
```

那么 *s* 将是`&str`类型。如果你想将`"Towards Data Science"`存储为一个字符串类型，你可以

```
let s = "Towards Data Science".to_string();
```

或者相当于:

```
let s = String::from("Towards Data Science");
```

这两种类型的主要区别在于`&str`是不可变的，存储在堆栈上，而字符串类型可以是可变的，因此存储在堆上。

如果你不知道栈和堆，不要担心。了解它们最重要的一点是，访问和写入堆栈要比堆快得多。

在整个运行期间，存储在堆栈上的数据需要具有固定的大小。这意味着如果一个变量被允许增加大小，那么它需要被存储在堆中。

这两种类型也是相关的，正如名称 string slice 所表明的那样，`&str`是一个字符串类型的子串，不管这意味着什么(试着自己找出答案)。

由于这是一个简短的介绍，我们现在将离开这个主题和这个数据类型，但字符串的数据类型是一个丰富而令人兴奋的主题，我鼓励你在阅读完这篇文章后深入研究这个主题。

# 收集

在 Rust 中，我们有许多集合，但其中一些比另一些使用得更多。

## 排列

例如，Rust 中的数组就像 Go 中的数组。它的大小是固定的，因此可以存储在堆栈中，这意味着快速访问。

在数组中，一次只能存储一种数据类型。

语法类似于 Python 的 list:

```
let rust_array = [1, 2, 3];
```

您可以像在 Python 中一样访问特定的元素。`rust_array[0]`给了我们第一个元素，在这个例子中是 *1* 。

## 元组

tuple 类型通常在 Rust 中用于在一个集合中存储不同的数据类型。

我们可以用点符号来访问元素:

## 矢量

Vectors 是 Rust 中最常用的集合之一，因为就像 *Python* 的列表或 *Go* 的切片一样，Rust 中的 vector 的大小可以增长。

它只能保存一种数据类型，但是正如您稍后将看到的，有一些方法可以解决这个问题。不过，我们必须知道一种叫做`enum`的类型，才能开始写这方面的内容。

正如你所想象的，向量可以增长的事实使它成为一个非常重要的类型。

要创建一个新的空向量，我们可以调用`Vec::new`函数:

```
let mut v: Vec<i32> = Vec::new();
```

一旦创建完成，我们现在就可以将元素放入其中。例如，`v.push(1)`将在`v`后追加 1，现在大小已经增大。

如果您想实例化包含元素的向量，我们有一个方便的宏:

```
let v = vec![1, 2, 3];
```

稍后我们会看到更多的宏。

从向量中获取元素有两种方法。在这种情况下，我们可以像在 *Python* 中那样用 *v[i]* 符号获取第 *i* 个元素。但是我们需要小心，向量实际上有足够的元素。

如果它有更少的元素，而我们试图访问一个不存在的元素，那么我们将在运行时得到一个错误！这很危险，所以 Rust 有另一种方法来访问 vector 中的元素。

我们像`let second = v.get(1);`一样访问它

现在`second`将属于`Option<T>`类型，我还没有介绍过，但是很快你就会知道这意味着什么，以及如何获取值。

我们也可以在 for 循环中迭代向量，但是因为我还没有讨论循环，所以我会向你展示语法。

## 哈希映射

哈希映射就像 Python 中的字典或 Go 中的映射，类型用`HashMap<K, V>`表示。它存储了类型为`K`的键到类型为`V.`的值的映射

要初始化和填充散列映射，我们可以执行以下操作:

`insert`方法通过一组键和值作为参数将数据推入散列映射。

如果您想访问哈希表中的数据，我们也有`get`方法。具体来说，

```
let a = articles.get(&String::from("Python Graph"));
```

将返回一个`Option`类型，我们可以从中获取值。符号`&`也将很快被涵盖。

当我们想通过一个键来更新哈希表，并且不确定它是否已经存在时，我们有几种选择。其中之一是方便的`entry`方法:

```
articles.entry(String::from("Rust")).or_insert("https://www.cantorsparadise.com/the-most-loved-programming-language-in-the-world-5220475fcc22");
```

如果这个键已经在散列映射中，那么我们将得到一个对它的*可变引用*，如果没有，那么我们将把参数中指定的数据插入到`or_insert`中。参考文献将在稍后解释。

# 功能

功能是 Rust 最重要的特征之一。

我们已经看到了起特殊作用的 *main* 函数，但是我们当然也能够创建其他函数。

语法很简单。下面是 Rust 中另一个函数的例子:

注意，我们需要告诉 Rust 函数接受哪种数据类型作为输入，以及它将输出哪种类型。这是一件好事，因为它可以防止许多错误。

关于 Rust 的另一个有趣的事情是，你不必通过一个`return`关键字显式地告诉 Rust 你返回了什么。如果函数中的最后一条语句没有尾随分号，那么这就是函数返回的内容。

这通常也适用于花括号中的代码块。很像 Scala。

在上面的例子中。函数`plus_one`返回`x+1`，其中 x 是函数作为参数接受的整数。

在 Rust 中，我们有一个`return`关键字，但它通常只在你想提前返回某个东西时使用。

# 控制流程和循环

控制流操作的语法通常最好通过自己做一些小练习来学习。

## 情况

看看下面的程序，并尝试修改它:

我们看到 Rust 中的注释是用双斜线或者多行注释的`/* blah blah */`来完成的。还要注意我们如何能够用关键字`return`提前返回一些东西。

`if, else if, else`的语法类似于 *Go* 的。布尔表达式周围不需要括号，这对可读性很好。

## 环

在 Rust 中，我们有几种不同的循环。

如果你想要一个无限循环，我们有`loop`，它当然应该在某个时候被打破。因此，Rust 还有一个方便的特性，使您能够打破特定的循环，而不仅仅是内部循环。

下面的例子是从《锈书》中借来的，我们都应该把它放在枕头下(或者在这个时代保存为书签)。

请注意，我们如何通过`'label: loop`语法标记循环，并通过稍后基于某些条件调用该标记来中断特定的循环。

我们还有一个 while 循环，使用起来非常直观:

接下来当然是 for 循环，其语法如下:

我们能够在迭代器上循环，你是否必须让你的数据类型成为迭代器当然取决于类型本身。注意，这种语法很像 Python 中的语法，只是在 Python 中很少需要改变类型。

# 所有权和借款

Rust 真正区别于其他语言的一个特征是它处理内存的聪明的所有权系统。

你看，不同的编程语言以不同的方式处理内存。在一些语言中，你必须自己分配和释放内存，这使得你的代码很快，并给你低级别的控制。可以说你“离金属更近了”。这方面的一个例子是 **C** 。

在其他语言中，你有一个垃圾收集器，它可以确保你的安全并自动清理内存。这既方便又安全，但不是免费的。它会减慢程序的速度。这方面的例子包括 **Python** 、 **Java** 和 **Go** 以及许多其他的。

Rust 采取了一种完全不同的内存管理方法。Rust 在一个被称为所有权的系统中结合了安全性和速度。

正如铁锈书所说:

> 因为所有权对于许多程序员来说是一个新概念，所以确实需要一些时间来适应。好消息是，你对 Rust 和所有权系统的规则越有经验，你就越能自然地开发出安全高效的代码。坚持下去！
> 
> ——[锈书](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html)。

首先，让我们陈述所有权的规则:

*   Rust 中的每个值都有一个变量，称为它的*所有者*。
*   一次只能有一个所有者。
*   当所有者超出范围时，该值将被丢弃。

有意思…是什么意思？

考虑以下代码:

这实际上将**而不是**编译。为了理解这一点，让我们从所有权的角度来看。

首先，变量`s1`通过取得值`String::from("Hi")`的所有权而进入范围。然后变量`s2`获得该值的所有权，我们从所有权规则中知道，只能有一个所有者。

这意味着变量`s1`不再有效。在《铁锈》中，我们谈到了“一个被移动的价值”。所以真正发生的是所有权或价值被转移到了`s2`，因此在那之后我们无法访问`s1`。

如果`s1`和`s2`是例如`i32`，那么这就不会发生，因为它们的值会被复制。这与 Rust 如何存储不同的值有关。如果一个值存储在堆上，那么这些规则适用，但是如果它存储在栈上，因此实现了`Copy`特征，那么将会发生一个简单的值拷贝。

让我们看另一个例子，在这里我们将看到函数也可以获得所有权。

下面的例子也是来自铁锈书。

你可以通过查看评论清楚地看到发生了什么。当一个变量作为参数传递给一个函数时，该变量的所有权被转移到该函数，并且该变量在当前范围内变得不可访问。

另外，请注意，如果存储在堆上的变量(例如字符串或向量)超出范围，那么只有在所有权在此之前没有移动的情况下，才会释放内存。

在这一点上，我确信这看起来有点限制和麻烦，你甚至不能在不转移所有权的情况下打印出变量，从而使变量不可访问。

当然，有一个系统可以解决这个问题。

这个系统叫做*借力。任何其他语言都有指针。Rust 有引用，这些引用与借用规则配合得很好。*

考虑以下代码:

这实际上编译和运行没有任何问题。前缀被称为引用，当一个函数被赋予一个引用或者一个变量被赋予一个引用时，它们并不拥有它的所有权。

在上面的例子中，我们需要在`println!`宏中使用变量`s1`，因此我们不能让函数`calculate_lenght`获得所有权。这个函数只是借用了一个不可变的引用，这个引用的值被分配给了我们想要的`s1`。

我们也可以有可变的引用，但是有一些规则来管理这个特性，以避免诸如竞争条件等讨厌的问题。

引用的规则如下:

*   在任何给定的时间，你可以拥有*或者*一个可变引用*或者*任意数量的不可变引用。
*   参考必须始终有效。

记住这一点的方法是，它就像任何其他文件。一次将读权限分配给几个不同的人是没问题的，因为在这种情况下不会发生任何不好的事情。但是，如果您同时授予几个人对一个文件的写访问权限，可能会出现很多问题。

这就是当你在 Git 中遇到合并冲突时发生的事情，对吗？我们不应该在代码中出现这个问题，因为 Rust 不知道如何处理这个问题。因此，在任何给定时间最多只能有一个可变引用。

# 结构、枚举和方法

结构和枚举在很多方面都是 Rust 的核心构件。如果你来自面向对象的语言，你会有宾至如归的感觉。

当我们引入哈希映射时，我们创建了一个`articles`哈希映射来存储文章。然而，如果我们想保存更多关于它们的信息，比如出版商或长度(分钟)呢？

我们可以定制包含这种结构化信息的数据类型吗？嗯，是的。

看一看以下内容:

在文件的底部，我们创建了一个名为`Article`的结构。我们现在能够在一个容器中存储相关数据。链接、料盒和长度数据称为字段，我们可以用点符号来访问它们，稍后我们会看到。

让我们看看如何使用`impl`语法在结构上实现方法。

该程序的输出如下:

```
The article "The Most Loved Programming Language in the World" is about 4 minutes long and is published in Cantors's Paradise.Please go to https://www.cantorsparadise.com/the-most-loved-programming-language-in-the-world-5220475fcc22 to read it.The article "How to Give Your Python Code a Magic Touch" is about 6 minutes long and is published in Towards Data Science.Please go to https://towardsdatascience.com/how-to-give-your-python-code-a-magic-touch-c778eeb9ac57 to read it. 
```

枚举很像结构，但是在枚举中，可以有给定数据类型的子类型，这非常有用。

请考虑对我们的代码进行以下更改:

这个程序的输出是:

```
The article "How to Give Your Python Code a Magic Touch" is about 6 minutes long and is published in Towards Data Science.Please go to https://towardsdatascience.com/how-to-give-your-python-code-a-magic-touch-c778eeb9ac57 to read it.Programming article coming up!The article "The Most Loved Programming Language in the World" is about 4 minutes long and is published in Cantors's Paradise.Please go to https://www.cantorsparadise.com/the-most-loved-programming-language-in-the-world-5220475fcc22 to read it.
```

这里介绍了几个新特性，同时也收集了一些旧特性。

首先，注意我们如何创建了一个包含两个变量的`Story`枚举:`Mathematics`和`DataScience`。这很方便，因为回想一下在上面的 vector 小节中，我们说过 vector 只能保存一种类型。嗯，我们已经创建了一个保存类型`Story`的向量，但是它有一些变体，这些变体不一定包含相同的类型。

`DataScience`和`Mathematics`都包含类型`Article`，但是如果我们愿意，我们也可以选择`String`和`f64`。

然后我们还引入了`match`控制流操作符，它在这种情况下接受一个 enum 并检查它的变量。如果找到匹配，我们就执行一些代码。

非常简单，但是非常强大。

回想一下，vectors 和 hash maps 上的 get-method 都返回了某种叫做`Option`的类型。

`Option`是一个有两个变体的枚举:`Some`和`None`。

Rust 迫使你以可控和安全的方式处理`None`值，不像其他语言。

注意，我们可以有嵌套的匹配子句。此代码的输出将与之前相同，但也是一行:

```
We have less than three elements...
```

这样，我们可以安全地处理丢失的值。

# 错误处理

Rust 需要像其他编程语言一样处理错误。没有不出错的软件。

但是在 Rust 中，我们有 enums 供我们使用，这意味着安全的错误处理！

有时候我们真的需要让程序崩溃。这听起来可能很奇怪，但是如果一个错误是不可恢复的和危险的，那么最好关闭它。

这可以通过`panic!`宏来完成。

`panic!`宏通过在关闭前清除内存来结束。这需要一点时间，这个行为是可以修改的。

大多数时候，我们实际上能够优雅地处理错误。这是通过`Result`枚举完成的。

我们还没有谈到泛型，所以这对你来说应该没什么意义。

只需将`T`替换为任何数据类型，将`E`替换为任何错误类型。

你现在不需要得到所有这些。但是我认为你已经抓住了要点。`File::open`返回一个`Result`枚举，它可能包含错误，也可能不包含错误。

可以用模式匹配来提取和处理。一旦你学会了闭包，你将有更多的选择。

# 试验

Rust 中的测试内置于语言本身的结构中。看看下面的片段:

您应该为您编写的每个文件添加一个测试模块。我们还没有讨论 Rust 中的模块，但是你已经明白了。

如果你运行`cargo test`，所有的测试都会自动运行。

在 Rust 中测试的巨大优势是极其有用的编译器。事实上，Rust 开发软件的最佳实践是使用测试驱动开发(TDD)。

这是因为编译器为您的问题提供了很好的解决方案。以至于它几乎可以帮你写代码。

看看这个小教程，明白我的意思:

  

# 高级概念:一般类型、特征、生存期、闭包和并发性

关于 Rust 还有很多需要学习的地方，但是如果你一直这么做，你肯定是在正确的轨道上。

这个标题中的特性是你接下来应该关注的，但我会从这里重新引导你，因为这只是一篇介绍性的文章，而不是一本成熟的书。

如果您还不是 Medium 的成员，但想要无限制地访问像这样的故事，您只需点击下面的:

<https://kaspermuller.medium.com/membership>  

进一步阅读的资源:

**锈书:**

  

**铁锈举例:**

  

**文档**:

  

**让我们生锈吧:**

<https://www.youtube.com/channel/UCSp-OaMpsO8K0KkOqyBl7_w> 