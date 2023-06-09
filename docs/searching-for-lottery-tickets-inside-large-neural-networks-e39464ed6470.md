# 在大型神经网络中搜索彩票

> 原文：<https://towardsdatascience.com/searching-for-lottery-tickets-inside-large-neural-networks-e39464ed6470?source=collection_archive---------19----------------------->

W *帽子如果每一个现代深层神经网络背后都藏着一张“彩票”呢？一个小得多的子网络，经过训练后，它将获得与整个经过训练的网络相同甚至更好的性能*

![](img/9d93512b5b5bcb09e730ba8bb11cf278.png)

(*图片作者*)

在 2019 年，Frankle 和 Carbin[1]的一篇论文提出了一个非常有趣的猜想，基于对当前大型神经网络的实验观察，似乎可以抓住同一网络的一小部分，并训练它以达到不仅相同的准确性，有时甚至比原始神经网络更好的结果。

> *“彩票假设:一个随机初始化的密集神经网络包含一个子网络，该子网络被初始化，使得在隔离训练时，它可以在最多相同次数的迭代训练后匹配原始网络的测试精度。”——j·弗兰克尔和 m·卡宾*

尽管这个猜想看起来令人难以置信，但这仅仅是个开始。同年，Ramanujan 等人[2]发表了一篇新论文，定义了一个更强的猜想，并实际展示了一个找到这个隐藏子网络的算法。研究小组开始意识到，他们工作的一些现代超大网络不仅包含“彩票”，而且实际上子网本身已经具有与其他训练过的网络相同的准确性**，只不过是随机初始化，不涉及任何训练**。

> *“隐藏在随机加权的宽 ResNet-50 [32]中，我们发现一个子网(具有随机权重)小于在 ImageNet [4]上训练的 ResNet-34 [9]的性能，但与之匹配。这些“未经训练的子网”不仅存在，而且我们提供了一种算法来有效地找到它们。”-Ramanujan 等人*

因此，更强的猜想是，给定一个足够大的神经网络，它一定包含一个子网络，即使没有训练，它也具有与原始训练的神经网络相当的准确性。

现在让我们在这里停下来一秒钟，惊叹这意味着纯粹的组合力量。想象一下，我们试图训练一个神经网络，例如作为一个简单的分类器，以区分狗和猫的图像，然后猜想说，给定一个足够大的神经网络，用随机权重初始化，你想要的神经网络一定很有可能在那里的某个地方，并且已经通过初始化单独训练过。

现在人们可能会问两个主要问题…

1.  “足够大”实际上意味着什么？
2.  如何找到这个新的更强大的子网络？

对于第一个问题，我们必须回到 2020 年初，当时马拉奇等人[3]的一篇论文给出了更强猜想的完整证明，他们已经表明，如果你有一个你想要近似的网络， 通过创建一个新网络，其大小是目标网络大小的多项式*(这意味着新网络的大小由某个多项式方程定义，该方程取决于目标网络的层数和神经元数以及您希望您的近似有多好)*，然后找到适当的子网络，您可以尽可能接近目标网络。

为了能够证明这个多项式界限，必须假设对输入和权重的规范有很强的限制，这个限制似乎是一个问题，如果去掉这个限制，那么这个界限将随着层数的增加而呈指数增长。幸运的是，故事还没有结束，在 2020 年底，一篇新的论文出现了，这一次是来自 DeepMind 的 L.Orseau 等人[4]发表的。

在本文中，他们总结了 Malach 等人[3]所做的证明的结论，以消除上述假设，并使用利用神经网络可组合性的新见解，他们能够显著提高界限:

> *“超参数化网络只需要一个对数因子(除了深度之外的所有变量)目标子网的单位权重的神经元数量。”-L.Orseau 等人*

现在我们准备尝试解决第二个问题…这一次我们不得不回到 1990 年，当时 Le Cun 等人[8]发表了一篇名为“最佳大脑损伤”(OBD)的论文。其背后的主要思想是能够通过删除网络的不重要权重来调整神经网络的大小，使其变得更小，这允许更大的泛化，需要更少的训练样本和速度提高(这种技术被称为“修剪”)

> *“OBD 的基本思想是，有可能采用一个完全合理的网络，删除一半(或更多)的权重，最终得到一个同样有效，甚至更好的网络。”——乐存等*

让我们试着理解 OBD 背后的思想。假设您想要删除参数以使网络变得更小，那么您会想要删除特定的参数以使其对训练误差的影响最小，从而保持当前的网络精度。一种方法是使用目标函数(希望最大化或最小化的函数),因此原则上可以删除一个参数并查看目标函数的变化量…..然而，这种技术太复杂，实际上无法执行，因为它需要临时删除每个参数，然后重新评估目标函数(我们可能正在处理具有数百万个参数的非常大的网络！！)

因此，这个问题的解决方案是通过逼近目标函数，然后通过二阶导数和迭代方法计算每个参数产生的变化(有关二阶导数修剪方法的更多信息，请参阅[6])

从那时起，这种从神经网络中消除不必要的权重或“修剪”的想法已经得到了很大的改进，尽管缺少理论保证，但实验表明，人们可以在不损失准确性的情况下修剪超过 90%的网络。

![](img/acb4e71ca5f862d3065e0f27054838f2.png)

一些修剪技巧(图片由作者提供)

现在有人可能会问，如果我们所做的一切都是为了缩小网络的规模，那么为什么不使用一个更小的网络呢？

现代实验似乎指出，较大的过参数化网络往往比小型网络具有更好的优势，例如 Belkin 等人[7]。定义了“双重下降”风险曲线，以解释为什么现代机器学习方法在新数据上获得非常准确的预测，同时具有非常低或零的训练风险，因此通常会返回高度过度拟合的系统，现在却给出非常好的预测

> *“虽然在插值阈值获得的学习预测值通常具有高风险，但我们表明，增加函数类容量超过该点会导致风险降低，通常会低于在“经典”机制中最佳点获得的风险。”——*贝尔金等人。

Ma 等人[5]给出了另一个有趣的例子，他们使用凸分析来解释现代大规模机器学习架构中随机梯度下降(SGD)的快速收敛现象，产生了前面提到的经验损失归零(零训练风险)。

SGD 是大多数现代神经网络算法的基础，对理解这种现象非常重要，也正是这项工作促使 Belkin 等人研究双下降风险曲线。

## 结论

> *“那么很自然会问:梯度下降最重要的任务可能是修剪吗？”-* L.Orseau 等人

随机梯度下降只是一种通过权重实现的修剪机制吗？这个猜想和界限的证明似乎表明，网络必须包含比以前显示的更多的“彩票”,学习和修剪之间的理论和联系仍有问题，Malach 等人的工作[3]表明，令人惊讶的是，给定一个随机网络，修剪在权重优化算法方面实现了竞争结果。

> “人们甚至可以推测，
> 剪枝的效果是达到全局最优的附近，之后梯度下降可以执行局部拟凸优化。” *-* L.Orseau 等人

彩票假说已经得到证明，在理解神经网络的理论能力和局限性的这个充满活力的领域中，许多工具仍有待建立，仍有许多开放的问题，修剪的未来可能仍有待观察。

## ***参考文献***

[1]J .弗兰克尔和 m .卡宾。[彩票假说:寻找稀疏的、可训练的神经网络。](https://arxiv.org/abs/1803.03635)(2019)ICLR。

[2]拉马努扬、沃特斯曼、肯巴维、法尔哈迪和拉斯特加里。[随机加权的神经网络中隐藏着什么？](https://arxiv.org/abs/1911.13299) (2019) arXiv 预印本 arXiv:1911.13299。

[3]E .马拉奇、g .耶胡代、s .沙莱夫-施瓦兹和 o .沙米尔。[证明彩票假说:修剪是你需要的全部](https://arxiv.org/abs/2002.00585)。(2020) arXiv 预印本 arXiv:2002.00585。出现在 2020 年的 ICML。

[4]L .奥尔索，M .哈特，o .里瓦斯帕拉塔。[对数修剪就是你需要的全部](https://arxiv.org/abs/2006.12156)。(2020)arXiv 预印本:2006.12156

[5]S .马、r .巴西利和 m .贝尔金。[插值的力量:理解 sgd 在现代过参数化学习中的有效性](https://arxiv.org/abs/1712.06559)。(2018)在机器学习国际会议上，第 3325–3334 页。

[6] B. Hassibi 和 D. G. Stork。网络修剪的二阶导数:最佳脑外科医生。神经信息处理系统进展。(1993 年)第 164-171 页。

[7]M .贝尔金、d .徐、s .马和 s .曼达尔[调和现代机器学习实践和偏差-方差权衡](https://arxiv.org/abs/1812.11118)。(2019)arXiv 预印本 arXiv:1812.11118

[8]扬·勒昆、易小轩·登克和萨拉·索拉最佳脑损伤。神经信息处理系统进展。(1990 年)第 598-605 页。