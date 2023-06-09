# Python 中的贝叶斯推理和马尔可夫链蒙特卡罗抽样

> 原文：<https://towardsdatascience.com/bayesian-inference-and-markov-chain-monte-carlo-sampling-in-python-bada1beabca7?source=collection_archive---------3----------------------->

## 通过一个用 Python 实现的掷硬币的深入示例，介绍如何使用贝叶斯推理和 MCMC 采样方法来预测未知参数的分布。

![](img/f3f45ee5ba7351508acc82dec08f10e4.png)

图片来自 Adobe Stock

# 介绍

本文将一个基本的抛硬币例子推广到一个更大的环境中，在这个环境中，我们可以检查贝叶斯推理和马尔可夫链蒙特卡罗抽样在预测未知值方面的用途和能力。有许多有用的软件包可以使用 MCMC 方法，但是这里我们将从头开始用 Python 构建我们自己的 MCMC，目标是理解其核心过程。

## 什么是贝叶斯推理？

[贝叶斯推断](https://en.wikipedia.org/wiki/Bayesian_inference)是一种方法，当我们收集更多的数据和证据时，我们使用贝叶斯定理来更新我们对概率或参数的理解。

## 什么是马尔可夫链蒙特卡罗抽样？

[MCMC 方法](https://en.wikipedia.org/wiki/Markov_chain_Monte_Carlo)(通常被称为)是一种用于从概率分布中取样的算法。这类算法采用随机抽样来获得数值结果，随着样本数量的增加，这些结果会收敛于事实。有许多不同的算法可以用来创建这种类型的采样链——我们在这个具体例子中使用的算法称为 [Metropolis-Hastings 算法](https://en.wikipedia.org/wiki/Metropolis%E2%80%93Hastings_algorithm)。MH 实现允许我们从一个未知的分布中抽取样本，只要我们知道一个与我们想要从中抽取样本的分布的概率密度成比例的函数。不需要知道精确的概率密度，仅仅是它的比例性就使得 MCMC-MH 特别有用。我们将在这个例子的后面描述算法的详细步骤。

# 硬币工厂问题

这个例子将模拟掷硬币的结果的概率，但是在一个扩展的上下文中。想象一下，一个全新的硬币工厂刚刚建成，生产一种新的硬币，他们让你确定工厂生产的硬币的一个参数，即硬币翻转时正面/反面落地的概率。我们称之为硬币的“偏向”。每枚硬币都有自己的偏差，但鉴于它们是在相同的过程中生产的，只有轻微的差异，我们预计工厂不会随机生产硬币，而是围绕“工厂偏差”生产。我们将使用来自特定硬币和工厂偏差的信息来创建概率分布，以确定硬币最有可能产生的偏差。用贝叶斯的话来说，我们将使用可能性(硬币数据)和先验(工厂偏差)来产生硬币偏差的后验分布。

![](img/4bb7d0e975493ab9dd48fc3acc369727.png)

图片来自 Adobe Stock

于是，工厂开张并生产了第一枚硬币。鉴于它是一种新的硬币和铸币厂，我们不知道它在翻转时会有什么表现(假装我们不知道硬币通常是如何工作的，我们试图预测一个“未知”的参数)。因此，我们用第一枚硬币做了一个实验，将它翻转 100 次，记录下它正面着地的次数——57 次。为了更新我们对工厂偏差的理解，我们将在生产更多硬币时这样做，但首先，让我们只分析第一枚硬币。

## 贝叶斯背景下的问题

在我们走得太远之前，我们需要在贝叶斯定理的背景下定义这个问题。等式的左边称为*后验；*一般来说，就是一个假设( *H* )给定一些证据( *E* )的概率。在右边的分子中，我们有我们的*可能性*(假设我们的假设为真，看到证据的概率)，乘以*先验*(假设的概率)。左边的分母是*边际可能性*或*证据*；这是观察证据的概率。幸运的是，我们将不需要使用边际可能性来抽样后验概率。

![](img/7be7c1c32cee2ec637b2b5f733cd00b4.png)

贝叶斯定理-作者图片。

在大多数实际应用中，直接计算后验分布是不可能的，这就是为什么我们采用数字采样技术，如 MCMC。

## 在后面的

那么我们对硬币厂感兴趣的后验概率是多少呢？这是概率， *P* ，工厂生产一个有偏差的硬币， *p* ，给定我们的数据， *x* 人头数— *P(p|x)* 。定理的其余部分可以写成如下:

![](img/a7f94dcaa1bced65f9baf5abf2a7a5db.png)

我们硬币工厂背景下的贝叶斯法则。

这里需要记住的是，我们预测的是后验概率分布( *P(p|x)* )一枚硬币有一定概率正面朝上，或者偏向( *p* )，这是两回事。工厂偏差是以一定偏差生产的硬币的概率分布；这是 *P(p)* ，先验。

## 可能性—二项式分布

这里的似然函数是观察到正面的概率， *x，*给定一个有偏差的硬币 *p.* 对于抛硬币，这个函数可以用[二项分布](https://en.wikipedia.org/wiki/Binomial_distribution)来精确描述。对于有偏差 *p* 的硬币，观察到 *x* 正面出 *n* 翻转的概率可以写成:

![](img/58928debf5dc91d9b783c75609b2f882.png)

二项式分布-作者图片

值得注意的是，我们目前不知道给定硬币的值 *p* 。这个值是我们的 MCMC 将随机抽样的值。用一个随机值初始化 *p* 后，经过多次采样，模型会收敛到 *p* 的真实值。

让我们开始用 Python 编写这个例子。我们需要定义第一次硬币实验中观察到的数据，以及根据给定的数据从二项分布中得出概率的似然函数。Scipy.stats 是一个很棒的 Python 库，可以很容易地定义像二项式这样的分布，这也是我在这个例子中使用的。

## 在先的；在前的

接下来，我们需要定义我们的先验函数， *P(p)* 。p 的值只能在 0 和 1 之间，0 代表硬币永远不会正面朝上，1 代表硬币永远正面朝上。请记住，工厂只生产了一枚硬币，所以我们没有任何信息可以预期 *p* 的先验概率是多少(假装我们不知道硬币是如何工作的)。在这个问题的背景下，由于只生产了一枚硬币，我们还不知道工厂偏见可能是什么。因此，我们将使用所谓的均匀先验。在贝叶斯推理的上下文中，这意味着我们赋予概率 *p* 在 0 和 1 之间的任意值相等的权重。

我们可以用 Scipy 和均匀分布 PDF 轻松做到这一点。这种默认分布只存在于 0 到 1 之间，正如我们所需要的。

既然我们已经定义了似然和先验，我们可以继续理解和编码马尔可夫链。

# 大都会-黑斯廷斯 MCMC

如上所述，这些方法从连续的随机变量中抽取样本——在我们的例子中是针对 *p* 。我们将使用的 MCMC 是随机游走类型，它随机生成样本，并根据它们与模型的拟合程度来决定是否保留它们。

## 接受比率

Metropolis-Hastings 算法相当简单，但首先，我们需要定义如何接受或拒绝新的样本抽取。每次迭代，将为 0 和 1 之间的 *p* 建议一个新值，我们将这个建议值称为*p′*。如果这个值比前一个值更好，我们只想接受并更新它。这是通过计算接受率来完成的。这个接受率是我们的贝叶斯定理对建议值与先前值的比率，如下所示。

![](img/d5516168c4c69c442e0a275a9403d566.png)

接受率， *R —作者图片*

这里有几点需要注意。首先，你可能已经注意到，这个接受率不包括贝叶斯定理的*边际似然(证据)*部分，我们也没有在上面为它定义一个函数。这是因为证据不会因为新的 *p* 值而改变，因此在这个比率中抵消了它自己。这太棒了，因为计算贝叶斯定理的边际似然部分在实践中通常是极其困难或不可能的。MCMC 和贝叶斯推理允许我们在不知道边际可能性的情况下对后验样本进行采样！

第二，这里任何大于 1 的值都意味着建议值更好，应该接受。接受新值的第二部分是将 *R* 与 0 和 1 之间的另一个随机抽取值进行比较，因此习惯上只在 R 更高时将 *R* 设为 1。

为了简单起见，我们将编写一个函数来计算这个接受率，以便在我们的采样链循环中轻松实现。

让我们明确定义 MH 算法的步骤，这样就更清楚了。

## 采样算法

我们已经定义了可能性、先验和接受概率的函数。在循环之前，我们必须做的最后一件事是用 0 到 1 范围内的随机值初始化 *p* 。

以下是我们的 Metropolis-Hastings 算法的步骤:

1.  在 0 和 1 之间随机提出一个 *p* 的新值，称之为*p′*(或 p_new)。
2.  计算接受率 r。
3.  生成另一个介于 0 和 1 之间的均匀随机数，称之为 *u* 。
4.  如果 *u < R* ，接受新值并设置*p = p′*。否则，保持 *p* 的当前值。
5.  记录该样品的 *p* 的最终值。
6.  多次重复步骤 1 到 5。

非常简单。在我们编写代码之前，让我们先来研究一下 MCMC 中使用的其他一些常见概念。

## 老化

MCMCs 是随机初始化的，必须收敛到正确的值，这通常需要相当多的样本。当绘制我们的结果和后验分布时，在模型收敛之前包含这些早期样本是无效的。因此，我们实施了所谓的“老化”,即排除第一批不太准确的样本。当整个链约为 10k–20k 时，MCMCs 的老化通常约为 2000–5000 个样本。

## 落后

MCMCs 需要考虑的另一个非常重要的问题是样本独立性。这里的新样本通常依赖于前一个样本，因为有时我们不接受新的随机值而保留旧值。为了解决这个问题，我们实现了所谓的“滞后”。滞后是指我们不是记录每一个样本，而是每隔一个，或者每五个或十个样本记录一次。

## 模拟

太好了，我们现在拥有了编写和运行 MCMC 所需的一切。

## 可视化结果

MCMC 结果通常以两种方式绘制——后验分布和迹线图。后验概率可以显示在直方图中，在直方图中我们可以直观地检查最可能的值和方差。轨迹图显示了每个样本迭代的 *p* 的值，并显示了 MCMC 的行为和收敛。后验分布不应包含老化样本，但包含迹线老化可以帮助我们检查模型从哪里开始，以及它收敛得如何。老化样本不包括在下面的跟踪图中。

![](img/c2b5291ad032db99b0cc20866ab40794.png)

后验分布和迹线——作者图片。

检查结果，我们可以看到我们的后验正态分布。我们还可以从跟踪图中看到，我们在收敛值附近进行了很好的随机采样，这很好。当提取后验值时，对于分布的其余部分，使用 *p* 的最后值并不总是准确的。由于这个原因，后验值通常被认为是分布的平均值。在这种情况下，我们的平均后验值是 0.569。

这个值几乎是我们预测的，如果我们把这个硬币的数据的频率概率，57/100 头。我们的 MCMC 预测这一点的原因是因为这是第一枚硬币，我们不太了解它们应该如何表现。在均匀先验的情况下，后验受似然函数(即数据)的影响更大。贝叶斯推断的下一步是用更多的数据更新我们的理解，所以让我们保持工厂运转，制造更多的硬币来测试。

![](img/fbc288b83537f3de9873fb05ab70288a.png)

照片由 [GSJJ](https://unsplash.com/@customgspromos?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 更新我们的理解

我们等一会儿，工厂生产了 500 枚硬币。我们运行同样的 100 次翻转实验，并记录每枚硬币的最可能偏差。让我们绘制一个直方图，并检查产生的偏差的分布，以了解工厂偏差。

![](img/33dae0a2558d08a4613e6c39f5646f65.png)

500 硬币工厂偏见-作者图片。

检查这些数据，我们了解到平均偏差是 0.511，标准偏差是 0.049。数据看起来是正态的，所以让我们用这些参数的正态分布对其建模，这显示为红色。

这个分布包含了我们预计在这个工厂生产的硬币更有可能出现哪些偏差的信息。像这样更新我们的理解，将会给我们一个比我们以前的，不知情的，一致的先验更准确的结果。这正是贝叶斯推理的目的——我们可以简单地更新我们的先验函数来表示工厂偏差的数据。

工厂偏见先验-作者图片。

现在我们已经用更多的先验信息改进了我们的模型，让我们生产第 501 枚硬币并进行同样的实验。在这个实验中，我们在 100 次投掷中得到 63 次投掷。我们必须像以前一样根据这些数据建立我们的似然函数:

很好，现在让我们看看包含工厂偏差的信息如何影响 MCMC 的结果，以及我们认为这枚硬币的真实偏差是多少。我已经运行了一个 MCMC，使用了与上面相同数量的样本和参数，但是使用了更新的先前和新的硬币数据。下图显示了第 501 枚硬币的后验分布和迹线。

![](img/87a7f668a9b004732126d1b0d9c22f63.png)

后验和迹线来自 MCMC，更新了前验——由作者更新。

尽管这枚硬币的数据表明偏差约为 0.63，但我们的贝叶斯推理模型表明实际值更接近 0.53。这是因为我们的知情先验函数在模型中占有权重，告诉我们即使我们观察到这种硬币有 63 个头像，鉴于硬币的平均偏差约为 0.51，我们预计第 501 个头像的偏差更接近工厂偏差。即使这枚硬币有 0.5 的偏差，观察 100 次投掷中的 63 次投掷也不是完全不可能的，我们不应该假设这个数据代表确切的值。先验函数具有权重，就像似然性具有通知后验分布的权重一样。如果我们要生产成千上万的硬币，并告知先前的分布更多，这将在模型中给予它更高的权重。这种用更多信息来更新我们的理解以预测未知参数的想法正是贝叶斯推理有用的原因。正是利用更多更好的数据来调整和操作这些可能性和先验函数，使我们能够改进和充实我们的推理模型。

## 结论

当实现贝叶斯推理和 MCMC 时，人们通常不希望知道后验分布是什么样子，因为我们在这里是编造数据的。这是推断未知参数的强大工具——只需知道后验分布与什么成比例(例如，线性模型和预测参数斜率和截距，或逻辑模型和参数α和β)。这允许我们做一些事情，比如预测我们无法解决的高维积分的结果——信不信由你，你可以只用随机性和统计学来做！

# 参考

除了上面给出的维基百科链接之外，这篇文章对于结合贝叶斯推理和 MCMC 的上下文非常有帮助。

接下来，我建议利用 PyMC3 这样的包来进行贝叶斯推理，而不是从头开始编码。Will Koehrsen 的这篇文章提供了一个很棒的真实例子，值得一看:

</markov-chain-monte-carlo-in-python-44f7e609be98>  

如果你希望深入研究使贝叶斯推理和 MCMC 成为可能的数学和推理，我强烈推荐这篇文章— [贝叶斯推理问题，MCMC 和变分推理](/bayesian-inference-problem-mcmc-and-variational-inference-25a8aa9bce29)。

如果你想了解更多关于我的实施的信息，或者想给我反馈(非常感谢)，请给我发信息或电子邮件到 jonny.hofmeister@gmail.com。

## 谢谢大家！