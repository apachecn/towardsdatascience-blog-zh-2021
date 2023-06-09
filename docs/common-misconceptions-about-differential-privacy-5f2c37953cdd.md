# 关于差异隐私的常见误解

> 原文：<https://towardsdatascience.com/common-misconceptions-about-differential-privacy-5f2c37953cdd?source=collection_archive---------18----------------------->

## [人工智能校准和安全](https://towardsdatascience.com/tagged/ai-alignment-and-safety)

## 本文将澄清一些关于差异隐私及其保证的常见误解。

![](img/39152576359c2132103ce2d4f2ebde8f.png)

来源: [Gretel.ai](https://gretel.ai)

关于差分隐私(DP)的内容有很多，从学术著作，如 DP 创始人写的隐私书，到解释其核心原则、解释和应用的博客，如[这个系列](https://desfontain.es/privacy/friendly-intro-to-differential-privacy.html)。虽然这些都是写得很好的资源，但它们需要深入研究才能完全掌握。因此，如果你对差分隐私有一个基本的了解，但还没有机会深入研究这些资源，这篇文章将澄清一些常见的误解。

# 差分隐私不是算法。

更确切地说，DP 是算法必须满足的标准。标准很简单，算法的输出，比如计数，不应该太依赖于任何单一记录。算法通常通过某种类型的概率噪声添加来掩盖任何记录的存在，从而达到差分隐私标准。例如，可以将少量噪声添加到精确计数中，使其具有差分私密性。

# 差异隐私不能为所有敏感信息提供全面保护。

借用 [McSherry](https://github.com/frankmcsherry/blog/blob/master/posts/2016-02-03.md) 的一句话，“差别隐私是正式区分*你的秘密*和*关于你的秘密*”如果您选择贡献您的秘密，DP 将以与您不贡献您的秘密相同的方式保护您的秘密。但它并不保证你的秘密会以其他方式公之于众。

考虑这个例子。你是一名数据科学家，在雨林公司(一家实行薪酬平等的虚构公司)年薪 10 万美元。雨林的人才团队希望公布数据科学家的平均收入，以吸引更多的申请人，他们已经决定[使用差分隐私安全地共享这些聚合信息](https://desfontain.es/privacy/differential-privacy-in-practice.html)。你知道你的同龄人的收入与你相差不到 5k，但你从未与任何人分享过你的收入——你认为这是你的秘密。你想继续保护你的秘密，所以你选择不被包括在这个平均值中。几周过去了，你看到数据科学家的招聘信息更新为“平均工资约为 10.1 万美元”。任何阅读这份招聘启事的人都会推断出你大约挣 10.1 万美元，这是真的。所以即使你在计算中隐瞒了你的数据，你的秘密已经公开了。

再举一个例子，看看[这个讲座](https://youtu.be/zP5qq141wUY?t=1293)，卡马斯讲述了为什么一个广为流传的目标市场营销的故事不是侵犯隐私。

# 差别隐私不是万能的。

DP 并不适用于每一种分析。这是一种量化的方式，算法会告诉你更多关于数据集中大规模趋势的信息，而不是关于任何特定个体的信息。换句话说，它旨在帮助人们巧妙地隐藏在人群中。

如果对异常值分析感兴趣，DP 就不是保护隐私的合适工具。此外，DP 不适合研究小群体。其核心是，DP 旨在允许安全地共享大量人口的汇总信息。

# “有差别的私有数据”不是一个明确定义的术语。

“差异私有数据”是一个经常被提起的模糊术语。它可能有几个不同的意思，容易引起误解。我们来分解一下。

如果你读过一些介绍性材料，你可能会认为“差分私有”是一个形容词，适用于做一些聚合的算法，如求和、中值甚至神经网络，以及它们的输出。通常，隐私保护源于某种形式的校准的概率噪声添加。那么，对于产生数据记录而不是作为输出的集合的过程，噪声添加是如何工作的呢？

下面是对“差异私有数据”的几种可能的解释。

*   “差分私有数据”可以指本地 DP 算法的输出。如果您不熟悉中央 DP 与本地 DP，请向下滚动到附录。随机响应等局部 DP 算法会产生一个敏感问题(例如，你吸烟吗？).该算法是可证明的差分私有的，并且该算法产生的噪声数据库也可以被描述为差分私有的。
*   “有差别的私有数据”也可以指生成模型的输出，该生成模型用技术训练以满足有差别的隐私的标准。
    生成建模被[布朗利](https://machinelearningmastery.com/what-are-generative-adversarial-networks-gans/)描述为*“机器学习中的一项任务，涉及自动发现和学习输入数据中的规律或模式，以这种方式，模型可以用于生成或输出新的示例，这些示例很可能是从原始数据集中提取的。”*生成模型最常用神经网络，可以[设计成符合 DP](/differential-privacy-in-deep-learning-cf9cc3591d28) 的标准。
    差分私有生成模型的输出通常被称为差分私有合成数据。对于复杂的多变量分析，如预测建模，这些模型可以产生比随机响应更高保真的合成数据。有一个巨大的研究领域致力于开发新的技术，可以最佳地平衡高质量合成数据的需求与隐私的需求，差分隐私只是其中之一，尽管是非常受欢迎的一种。

因此，当使用差分隐私作为一个形容词来描述数据时，我鼓励你澄清所使用的算法的广泛类别，注意所产生数据的预期用途，并在适当的时候正确地将数据称为合成数据。

我希望这篇文章有助于澄清一些关于差分隐私的常见误解。如果你有任何问题或者想在 [Gretel](https://gretel.ai) 上谈论我在应用隐私领域的工作，请给我写信 [lipika@gretel.ai](mailto:lipika@gretel.ai) ！

# 附录

## 中央与地方差异隐私

有两种不同的差分隐私模型—中央和本地。隐私的标准保持不变，但是区别在于数据存储在哪里以及何时出现噪声添加。

您可能熟悉中心模型，在这种模型中，所有真实、敏感的数据都可以在某个中心位置获得。例如，你和我在西雅图一家标志性的咖啡连锁店注册奖励。我们把我们的名字、电话号码和出生日期托付给他们，他们现在把这些信息储存在某个中央数据库里。如果他们想分享在晚上 7 点后订购含咖啡因饮料的顾客的年龄中位数，他们可以通过计算真实值并添加一些校准噪声来保证不同的隐私。真实的、敏感的数据仍然被不加修改地存储，并且与差分隐私无关。它是共享中值年龄(即一种算法，参见第一个误解)的过程，而不是被查询的中央数据库。

相反，本地模型是为缺乏信任或存储原始数据的中心位置的情况而设计的。例如，我的好奇的朋友乔治正在进行一项研究，关于有抱负的数据科学家完成带回家的任务是否需要比规定时间更长的时间，并要求我贡献我的数据。虽然我也同样好奇，想知道我的同行的总体信息，但我不相信乔治会透露我花了一整天完成我的最后一次带回家，尽管时间限制是 4 个小时。所以乔治告诉我掷硬币。如果是正面，我会如实回答。否则，我再次抛硬币，如果它正面朝上，我说是，如果它反面朝上，我说不是。如果乔治要求所有调查参与者都这样做，他现在就会收集到一个嘈杂版本的数据集。这个算法叫做**随机化回答**。收集这个嘈杂数据集的目的是聚合它，乔治通过[解释第二次抛硬币引入的偏差](https://programming-dp.com/notebooks/ch13.html)来完成这个任务。请注意，如上所述，随机化回答是有差别的隐私(见[第 3.2 节](https://www.cis.upenn.edu/~aaroth/Papers/privacybook.pdf)的证明)。因此，该算法是差分隐私的，并且该算法的输出，这个嘈杂的答案数据库，也可以被描述为差分隐私。

更多关于 DP 的风格和它们之间的界限，请阅读[这篇文章](https://desfontain.es/privacy/local-global-differential-privacy.html)。