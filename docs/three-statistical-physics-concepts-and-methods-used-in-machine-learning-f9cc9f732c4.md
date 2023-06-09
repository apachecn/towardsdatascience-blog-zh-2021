# 机器学习中使用的三个统计物理概念和方法

> 原文：<https://towardsdatascience.com/three-statistical-physics-concepts-and-methods-used-in-machine-learning-f9cc9f732c4?source=collection_archive---------16----------------------->

## 许多其他的概念正在形成

![](img/2e75b88d9c10fbde8ed110632ab9379f.png)

马克斯·希洛夫在 [Unsplash](https://unsplash.com/s/photos/physics?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

物理学是现存的最重要的自然科学之一，许多重要的概念被用于数学和其他领域，如化学、生物学等。，直接来自物理学。

其他科学中使用的物理概念和方法的列表很长，我在本文中不讨论它们。另一方面，在这篇文章中，我讨论了机器学习、深度学习和人工智能领域中使用的一些重要的物理概念、理论或方法。

机器学习和物理学是不同的研究领域，但这两个领域有许多交集或“交叉受精”，了解这些非常重要。有许多机器学习概念源于物理学，尤其是统计物理学，在这篇文章中我讨论了其中最重要的(在我看来)。我下面讨论的概念/方法或算法并不是按照重要性排序的，并且这个列表并不详尽。

# 1.逆伊辛模型

**玻尔兹曼机器(BM)** 或**受限玻尔兹曼机器(RBM)** 是在机器/深度学习中经常使用的无监督学习类型。

BM 和 RBM 方法/算法起源于统计物理学，在物理学文献中它们有不同的名称，如**逆伊辛模型**、**随机伊辛-楞次-利特尔模型、**等。BM 和 SMB 方法基于所谓的谢灵顿-柯克帕特里克随机[伊辛模型](https://en.wikipedia.org/wiki/Ising_Model)的自旋玻璃模型。

伊辛模型是一种广泛应用于统计物理和凝聚态物质的物理模型，它模拟了基本磁体(电子、原子、分子等)的相互作用。)，目的是导出物理可观测性，例如这些相互作用单元的自旋磁化强度和相关函数。

另一方面，逆伊辛模型(或逆伊辛问题)顾名思义是一个逆过程，其中自旋磁化强度和相关函数等物理可观测值是已知的，但基本单元之间的相互作用是未知的。在这种情况下，人们试图从物理观测值/数据中推断出相互作用单元的相互作用哈密顿量。你可以看到，这正是一般机器学习的目标，因此，逆伊辛模型(或一般逆物理模型)和机器学习有着相同的目标。

BM 是逆伊辛模型，其中数据样本被视为来自成对网络单元的玻尔兹曼分布的样本。目标是学习这些网络单元的能量函数或哈密顿量，因此，观察数据的可能性(玻尔兹曼测量中的概率)很大。BM 方法的一个大问题是“学习”几乎是不可行的，因为它允许可见单元( *v_i* )和隐藏单元( *h_i* )之间的层间交互

RBM 是 BM 的一个特例，其中可见单元( *v_i* )和隐藏单元( *h_i* )通过有效耦合相互作用。该模型不允许可见单元( *v_i* )和隐藏单元( *h_i* )之间的层间交互，即可见到可见和隐藏到隐藏单元之间没有联系。在这种情况下，相互作用仅在可见和隐藏单元之间，并且被调整以便在学习过程中最大化波尔兹曼似然概率函数

![](img/7ab1bf13e6c27053b04036c1a8faab07.png)

为了学习模型参数，需要最大化训练数据集 v 上的边际概率分布函数 P(v)。在等式(1)中，H 是哈密尔顿函数/能量函数，v 和 H 是布尔网络向量，W 是权重矩阵，a 和 b 是权重偏差参数，Z 是配分函数。

![](img/2c6cedf985c61a1f31cbc0ae220de8e7.png)

隐藏和可见单元之间的 SBM 交互。在知识共享许可下，图片来源于[维基百科](https://en.wikipedia.org/wiki/Restricted_Boltzmann_machine#/media/File:Restricted_Boltzmann_machine.svg)。

# 2.GBF 不等式

GBF (Gibbs-Bogolyubov-Feynmann)不等式是统计物理中非常重要的概念。GBF 不等式是由统计力学的乔赛亚·w·吉布斯在 19 世纪末发现的，后来在 60 年代由量子力学的尼古拉·博戈柳博夫和理查德·费曼分别发现。

现实中的 GBF 不等式有很多面，它可以被证明是热力学第二定律的重新陈述。在统计物理学的背景下，有一个定理叫做 **GBF 定理**，它陈述:

> 给定某给定系统 S 的两个哈密顿量*h0(S)*和 H(S)*，*，并给定它们相应的自由能 F0(S)和 F(S) *，*，下列不等式成立

![](img/93445619f3f73cccd958fcefd465d836.png)

在等式(2)中，括号<..>表示在 *H_0(S)* 上的热平均值。这里，我不期望你知道这些概念，因为一般来说，它们是非常复杂的，但是我相信方程(2)的形式非常容易理解。这是一个不等式方程，原则上可以用不同的形式来表达，其中一种形式利用了部分函数 *Z* 。

**GBF 不等式(2)和机器学习有什么关系？**

为了回答这个问题，我必须首先讨论**变分贝叶斯方法或变分推理方法**，它们是统计学中的重要概念，或者更准确地说，是贝叶斯推理和机器学习中的重要概念。这种方法用于近似贝叶斯推理中出现的非常复杂的积分。

贝叶斯推理中的一个大问题是分母积分函数的计算，它也称为出现在贝叶斯定理中的边际概率。这里我假设读者知道贝叶斯定理。

为了计算贝叶斯定理中出现的后验概率或边际概率，在这一点上使用近似方法。利用统计学中存在的一个重要定理，称为 [**库尔贝克-莱布勒定理**](https://en.wikipedia.org/wiki/Kullback–Leibler_divergence) **或库尔贝克-莱布勒散度。这个定理允许我们通过使用近似方法来估计我们在近似贝叶斯定理中的后验概率时所产生的误差。**

当我们试图使用机器学习来评估我们的模型表现如何时，我们面临着许多**潜在变量 *Z*** 或未知变量对我们的模型的表现产生影响。这些潜在的变量是随机的，会在我们的模型上产生意想不到的特征。潜变量的作用包含在贝叶斯定理中出现的后验概率函数*p(****Z****|****X****)*中，其中 ***X*** 为给定数据。

要计算*p(****Z****|****X****)*在贝叶斯定理中，需要计算出现在分母*、p(****X****中的积分函数。*后一个函数可以用**Kullback-Leibler 散度定理来近似。**

印象最深的是*p(****X****)*满足一个与上面 GBF 定理给出的类似的结果。我没有在这里展示这些结果，因为它们不是微不足道的，但要记住的最重要的事情是，GBF 定理已经在机器学习中用于给*p(****X****)设定一个下限。所以不需要计算复杂的函数 p(****X****)而是利用 GBF 定理得到它的一个下界。*

因此人们可以看到，由三位不同的物理学家独立导出的 GBF 定理是如何渗透到机器学习中的，并且它已被用来对*p(****X****)*或其对数函数*log(p(****X****)设定下界。*

# 3.复制品戏法

另一种广泛用于机器学习的重要方法起源于统计物理，即所谓的复制“技巧”，首先由乔治·帕里西**提出。在统计物理中，经常需要计算所谓的配分函数，用 *Z* 表示。借助于配分函数，计算自由能函数成为可能，自由能函数是统计物理中最重要的量之一。**

自由能和配分函数之间的关系由下式给出

![](img/c1c86af56b351be41a58b804cc804ad9.png)

自由能函数 F

其中 *k_B* 是玻尔兹曼常数，而 *T* 是系统的温度，单位为开尔文度。由于对于复杂系统，配分函数 *Z* 通常相当复杂，因此 *F* 的计算通常非常复杂。

在统计物理学的背景下，并使用自旋玻璃理论的结果，理论物理学家**乔治·帕里西**通过使用计算方程(3)中的 *ln(Z)* ，这是一个非常简单而强大的数学技巧，在统计物理学中通常称为*复制技巧*。诀窍在于写作

![](img/3316b93e4f2111404b31dca10d8fb8b5.png)

复制品戏法

除了在等式(4)的 l.h.s 上计算 *ln(Z)* 之外，还可以在 r.h.s 上计算它的等价表达式。r.h.s 上出现 *Z* 的幂 *n，*并且在许多情况下，在系统变量中计算等式(4)的 r.h.s 上的平均值要容易得多。这是通过创建系统的 *n* 个副本或 *n* 个副本来完成的，每个副本都有其分区函数 *Z* 。因此，在使用复制技巧时，一个重要的隐含假设是 *n* 被假设为正整数，并且等式(4)中的极限被假设存在。

在机器学习的背景下，在许多情况下，有必要最小化训练和测试数据成本函数 *C* 。例如，在监督学习中，成本函数 *C* 可以是一组神经网络 *x* 在点 *D、*即 *C(x，D)* 的数据集上的函数，并且计算其期望值 *E(C(x，D))* 可能非常困难。在这种情况下，可以将期望值 *E(C(x，D))* 降低到与 *ln(Z)* 成比例的吉布斯采样函数，其中后者被表示为成本函数 *C* 的指数积分。通过使用等式(4)中的技巧，只要存在趋于零的 *n* 的极限，就更容易计算 *ln(Z)* 。整个过程实际上很复杂，我不会在这里讨论细节，因为这会使本文的目标复杂化。

# 结论

在这篇文章中，我讨论了进入机器学习的最重要的统计物理学结果。还有其他没有提到的结果被使用，但我认为上面讨论的三个概念和方法是最重要的一个。很有可能，在未来，许多其他物理方法将被用于机器学习，它们的数量可能会增加。

另一方面，机器学习也影响了物理学，许多重要的机器学习概念现在正在物理学中使用。我将在以后的另一篇文章中讨论这些概念。

# 如果你喜欢我的文章，请与你可能对这个话题感兴趣的朋友分享，并在你的研究中引用/参考我的文章。不要忘记订阅将来会发布的其他相关主题。