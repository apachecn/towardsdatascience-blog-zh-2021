# Julia 算子概述

> 原文：<https://towardsdatascience.com/an-overview-of-julias-operators-3db925db38d1?source=collection_archive---------27----------------------->

## 快速浏览 Julia 编程语言中的所有操作符及其用法

![](img/46c6bd772d63f53def75ace848910d7e.png)

[https://unsplash.com/photos/Mmk63saBhDM](https://unsplash.com/photos/Mmk63saBhDM)

# 介绍

对于那些对朱丽亚感兴趣的人来说，进入朱丽亚的世界可能会感到困惑和恐惧。这不仅适用于 Julia 通常使用的方法，利用不同的编程概念，如多重分派，而且适用于更基本的数学函数，如加法或减法。

当学习一门新的编程语言时，最重要的事情之一就是学习这门语言中的操作符。Julia 有一些非常独特的操作符，它们不一定在整个计算机编程范围内都是标准化的。记住这一点，让我们看看这些操作符，以及它们在语言中的作用。

# 算术运算符

Julia 中最重要和最基本的操作符是算术操作符。这些运算符用于 Julia 中的断言和数学表达式，执行与用于表示 Julia 中运算符的字符相关的精确运算。

## 断言操作符

断言操作符是大多数程序员可能都熟悉的一种操作符。这由=符号表示，通常用于将变量别名设置为某种类型。

## 一元加号

一元加号是加法运算符的典型用法，只放在一个变量上。这将执行标识操作。恒等运算是表示给定数量和另一数量的组合的运算，其中该数量保持不变。例如，加法恒等式是 0，因为 x + 0 = 0 + x = x。这在 Julia 中表示为一元运算符，这意味着它只用于一个参数。我们可以在变量调用之前使用+ char 来调用它，就像这样:

```
+x
```

## 一元减操作

一元减号运算符的表示方式与一元加号运算符相同。然而，这个操作符执行的是完全不同的运算。该运算符用于将值映射到它们的加法逆运算。这基本上意味着它否定了这个数。换句话说，在《朱莉娅》中，我们可以用一元减号来表示否定——我认为这很自然也很酷。这真的符合他们“就像在报纸上一样”的方法论，我认为这很酷。

```
-x
```

## 二进制加号

二进制加法执行普通加法。

```
x + y
```

## 二进制减

二进制减执行正常的减法。

```
x - y
```

## 时间运算符

乘以运算符用于执行普通乘法。

```
x * y
```

## 除法算符

谁能想到呢？除法运算符是用来执行除法的！

```
x / y
```

## 整数除法运算符

该运算符将执行除法，但将始终返回一个四舍五入的整数:

```
x ÷ y
```

我认为这个很没用，因为我不知道按什么 numpad 键来创建这个符号，你可以简单地使用 round()方法来将一个浮点数转换成一个整数。

## 反向除法

反向除法运算符将第二个参数除以第一个参数，而不是相反。

```
x \ y
```

## 力量

Julia 中的幂运算符是^，每当我使用 Python 并试图调用 Xor 运算符^，以为它会给我一个指数时，这总是让我感到困惑。

```
x ^ 2
```

## 剩余物

余数运算符将返回两个参数相除的余数。

```
x % y
```

# 布尔运算符

虽然不是很令人兴奋，布尔运算符也很重要。正如所料，这些操作符专门用于 bool 类型。坦率地说，我知道最有可能知道我们到目前为止所看到的所有运算符，但是要获得朱利安运算符的真正内容，我们必须首先通过相对基本的东西。

## 否认

否定运算符是另一个一元运算符，它将给定的布尔值改为相反的值。用一个解释点来表示。

```
!x
```

## 和

布尔 and 操作符是直接从 Julia 的 Bash 中提取出来的。它被表示为&&。

```
x && y
```

## 或者

另一个连接操作符是 or 操作符，用||表示。

# 按位运算符

在计算机程序设计中，按位操作是在位串、位数组或二进制数的单个位的层次上进行操作。这通常意味着操作符用于改变操作符中的单个位。

## 按位非

按位 not 运算符用~表示，是一元运算符。

```
~100
```

## 按位 and

按位 and 运算符用“与”符号表示，是一种二元运算符。

```
x & y
```

## 按位或

按位“或”运算符用一个管道表示，也是一个二元运算符。

```
x | y
```

## 按位异或

按位异或用⊻表示，但是你也可以使用 xor()方法，这是我通常做的。

```
x ⊻ y
```

## 逻辑右移

逻辑右移运算符用三个向右箭头表示，是一个二元运算符。

```
x >>> y
```

## 算术右移

算术右移只用两个右箭头表示，也是一个二元运算符。

```
x >> y
```

## 逻辑或算术左移

逻辑和算术左移组合成两个向左的箭头。这当然也是一个二元运算符。

```
x << y
```

# 更新运算符

Julia 语言中的每个二进制位或算术运算符都有一个更新的对应部分。这些运算符用于用新类型更新变量别名。我们刚刚讨论的操作符的更新版本是

```
+=  -=  *=  /=  \=  ÷=  %=  ^=  &=  |=  ⊻=  >>>=  >>=  <<=
```

# 矢量化运算符

基本运算符的最后一种形式是任何二进制算术运算的矢量化版本。这由操作符前面的点表示。这些当然意味着用在可迭代的向量或数组上。这些运算符的矢量化版本如下:

```
.+ .- .* ./ .\ .% .^
```

# 比较运算符

比较运算符用于根据某种条件从两个参数返回布尔类型。这个条件可以是数字、等式，甚至更多。

## 等式运算符

如果值相等，相等运算符返回 true。

```
x == y
```

## 不等式算子

如果值不相等，不等式运算符返回 true。

```
x != y
```

## 小于运算符

如果第一个参数小于第二个参数，则小于运算符返回 true。

```
x < y
```

## 大于运算符

如果第二个参数小于第一个参数，则大于运算符返回 true。

```
x > y
```

## 或等于运算符

我们可以通过简单地在运算符后添加一个等号，使小于和大于运算符都变成小于或等于和大于或等于运算符。

```
x >= y
y <= x
```

## 子类型运算符

不幸的是，这个列表中最令人兴奋的是子类型操作符。子类型运算符有两种用途。它是一个接受类型的二元运算符。该运算符用<:/>

```
abstract type AbstractTuber end
struct Potato <: AbstractTuber data::Array end
```

该运算符也可用于返回用于比较的布尔值，这也是它出现在本节中的原因:

```
x <: y
```

我们可以假设这个操作符的意思是“是的子类型。”如果您想了解更多关于 Julia 中子类型的一般概念，以及这个操作符在 Julia 类型层次结构中的用法，我写了一整篇文章，您可以在这里查看:

</overview-abstract-super-type-heirarchies-in-julia-26b7e64c9d10>  

# 结论

我决定写这篇文章，因为 Julia 语言在它的领域中与许多其他竞争语言有一些显著的不同。当从一种语言切换到另一种语言并使用不同的操作符时，经常会感到困惑，此外，对于新程序员来说，了解他们语言中的所有操作符可能是件好事。虽然写起来很无聊，但我确实认为它可能对任何打算学习这门语言的人有所帮助。非常感谢你阅读我的文章，我很感激！