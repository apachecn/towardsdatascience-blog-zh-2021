# 赌徒的破产问题

> 原文：<https://towardsdatascience.com/the-gamblers-ruin-problem-9c97a7747171?source=collection_archive---------4----------------------->

## 马尔可夫链的一个独特应用

![](img/b76e5938754968e419ef857ad36b6de9.png)

乔纳森·彼得森在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

# 介绍

条件概率理论经常导致某些数学问题的独特而有趣的解决方案。当一个复杂的概率问题能够以相对简单的方式解决时，人们既兴奋又难以置信。赌徒的破产问题就是如此，这是一个围绕条件概率和实验结果的著名统计场景。这个问题可能更令人着迷的是，它的结构超越了条件概率，扩展到随机变量和分布，特别是作为具有有趣性质的独特马尔可夫链的应用。

初等概率问题基于对不确定结果的数学描述。初等统计学为我们提供了一套工具，我们可以使用这些工具通过定理来确定不确定结果的概率，并揭示复杂的情况。解决赌徒的破产问题不是我们必须每天完成的任务，但理解其结构有助于我们在处理植根于不确定性的情况时培养批判和数学思维。

> N **注:**这篇文章要求读者理解初等概率和统计理论，这本身就要求接触微积分和线性代数。还假设读者对马氏链有一定的基础知识。

# 问题陈述

赌徒的破产问题最基本的形式是由两个赌徒 A 和 B 组成，他们相互之间进行多次概率游戏。每次游戏都有一个概率*p*(0<p1)赌徒 *A* 会赢赌徒 *B* 。同样，使用基本的概率公理，赌徒 B 赢的概率是 1-*p。*每个赌徒都有一个初始财富，限制他们能下多少注。总组合财富由 *k* 表示，赌徒 *A* 的初始财富由 *i* 表示，这意味着赌徒 *B* 的初始财富为 *k - i* 。财富要求为正。我们应用于这个问题的最后一个条件是，两个赌徒都将无限期地玩下去，直到其中一个失去了他们所有的初始财富，从而不能再玩下去。

想象一下，赌徒 A 的初始财富 *i* 是整数美元，并且每场游戏都是一美元。这意味着赌徒 *A* 至少要玩 *i* 游戏，他们的财富才会降到零。他们每局赢一块钱的概率是 *p* ，如果游戏对两个赌客都公平的话，那就等于 1/2。如果 *p* > 1/2，那么赌徒 *A* 具有系统优势，如果 *p* < 1/2，那么赌徒 *A* 具有系统劣势。系列游戏只能以两种结局收场:赌徒 *A* 拥有财富 *k* 美元(赌徒 *B* 输光了所有的钱)，或者赌徒 *A* 拥有财富 0 美元(赌徒 *B* 拥有所有的财富)。分析的主要焦点是确定赌徒 A 最终获得财富 k 而不是 0 美元的概率。无论结果如何，其中一个赌徒将以金融*破产*告终，因此得名*赌徒的破产*。

# 问题解决方案

继续上面概述的相同结构，我们现在想要确定赌徒*aᵢ*a*a*将会以 *k* 美元结束的概率，假设他们以 *i* 美元开始。为了简单起见，我们在这里会增加一个额外的假设:所有的游戏都是相同且独立的。每一次赌徒玩一个新的游戏，它可以被解释为一个新的迭代的赌徒的破产问题，其中每个赌徒的初始财富是不同的，取决于最近游戏的结果。从数学上来说，我们可以认为每一个游戏序列都以赌徒 *A* 拥有 *j* 美元结束，其中 *j* = 0，…， *k* 。假设一个特定的序列发生，赌徒 *A* 赢的概率是 *aⱼ* 。任何以赌徒 a 有 k 美元结束的序列都意味着他们赢了，所以 aₖ= 1。同样地，任何以 0 美元结束的序列都意味着他们破产了，所以₀=0.我们感兴趣的是确定 *i=1，…，k -* 1 的所有值的概率。

使用事件符号，我们可以将 *A* ₁表示为游戏者 *A* 赢得游戏 1 的事件。类似地， *B* ₁是赌徒 *B* 赢得第一场比赛的事件。事件 *W* 发生在赌徒 *A* 以 *k* 美元结束时，在他们以 0 美元结束之前。此事件发生的概率可以使用条件概率的属性来推导。

使用条件概率的获胜概率

假设赌徒 a 从美元开始，他们赢的概率是 P(W)=aᵢ。如果赌徒 A 在第一局赢了 1 美元，那么他们的财富就变成了 1 美元。如果他们在第一局输了一美元，他们的财富就会变成 1。他们赢得整个序列的概率将取决于他们是否赢得了第一场比赛。当我们将这一逻辑应用于前面的等式时，我们知道有一个赢得整个游戏序列的概率的表达式，它取决于每场游戏赢得一美元的概率和给定赌徒财富的赢得序列的条件概率。

使用问题符号的获胜概率

在任何给定的时间点，赌徒 A 的财富在两个赌徒的总初始财富和零之间变化。换句话说，给定 *i=* 1，…， *k -* 1，我们可以将 *i* 的所有可能值代入上式，得到 *k -* 1 个方程，根据 *i* 的相邻值确定中奖概率。我们可以用初等代数将这些方程集合成一个标准化的格式，可以简化成一个公式。这个公式规定了每场游戏的获胜概率 p、两个赌徒的总初始财富 k 和给定一美元财富 a 的获胜概率之间的基本关系一旦我们已经确定了 *a* ₁，我们可以迭代地遍历所有的 *k -* 1，以导出 *aᵢ* 对于 *i.* 的所有可能值的概率

基本关系

我们现在将考虑两种可能性:公平游戏和不公平游戏，这取决于我们代入上述等式的 *p* 的值。在一个公平的游戏中，其中 *p* =1/2，等式右边的指数的底数可以简化为(1 - *p* )/ *p* =1。然后我们可以将整个方程简化如下:1-*a*₁=(*k*-1)*a*₁，可以重新排列为 *a* ₁=1/ *k* 。如果我们迭代所有先前的方程，这些方程决定了不同的 *i，*I 值的获胜概率，我们就得到公平游戏的一般解。

公平游戏的解决方案

上面的等式是一个显著的结果:假设游戏是公平的，赌徒 A 在以零美元结束之前以 k 美元结束的概率等于他们最初的财富除以两个赌徒的总财富。

如果 p 不等于 1/2，这个游戏就是不公平的，因为两个赌徒中的一个有系统优势。我们可以类似地推导出一个依赖于 *p* 的值和财富参数的一般解。

不公平游戏的解决方案

> **注**:如果读者有兴趣学习数学证明以得出通解，请查阅最后的参考文献。

# 马尔可夫链

![](img/f5ac5c17d18f6fe29beb1d728ee5a83d.png)

由[郭佳欣·阿维蒂斯扬](https://unsplash.com/@kar111?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄的照片

代表由离散时间间隔定义的不同时间点的随机变量序列 *X* 可以被称为随机过程。流程中的第一个随机变量称为*初始状态*，流程中的其余随机变量定义了每个流程在时间 *n* 的状态。马尔可夫链是一种特殊的随机过程，其中未来状态的条件分布只取决于当前状态。也就是说， *X* 在时间 *n + j* 对于 *j > 0* 的条件分布仅取决于时间 *n* 的进程状态，而不取决于直到 *n* - 1 *的任何更早的状态。我们可以用下面的符号来表达这一点。*

马尔可夫链

如果在任意时间点可能出现的状态数是无限的，那么马尔可夫链是有限的。考虑一个有 k 个*状态的链。给定在时间 *n* 的状态，在时间 *n+1* 取特定值 *j* 的状态的概率分布被称为马尔可夫链的*转移分布*。如果每次 *n* 的分布都相同，则认为这些分布是稳定的。我们可以用符号 *pᵢⱼ* 来表示这些分布。*

平稳转移分布

*pᵢⱼ* 可以取的不同值的总数取决于可能状态 *k* 的总数，我们可以通过 *k* 矩阵 ***P*** 将其排列在一个 *k* 中，称为马尔可夫链的转移矩阵。

跃迁矩阵

转移矩阵具有重要的性质，使它们是唯一的。因为矩阵的每个元素都代表一个概率，所以所有元素都是正的。由于给定前一个状态的值，每一行代表下一个状态的整个条件分布，因此每一行中的值总和为 1。通过使用转移矩阵，我们可以直接将概率计算扩展到多个步骤。也就是说，我们可以通过取转移矩阵***【p】****的幂来计算马尔可夫链从一个状态 *i* 多步移动到一个状态*j*m 的概率。也就是说，可以用 *m 步转移矩阵* ***P*** ᵐ来计算特定状态的概率*

*如果我们有一个转移矩阵，其中任何对角线 *pᵢᵢ* 等于 1，那么状态 *i* 被认为是*吸收状态*。一旦马尔可夫链进入吸收状态，它就不能再进入任何其它状态。另一个有趣的性质是，如果一个马尔可夫链有一个或多个吸收态，那么这个链最终会被吸收到这些吸收态中的一个。*

*在时间 1 的马尔可夫链的开始，我们可以指定一个向量，它的元素表示该链将处于每个状态的概率。这就是所谓的*初始概率向量* ***v*** 。我们可以通过初始概率向量 ***v*** 乘以转移矩阵 ***P*** 的 *n* - 1 次方来确定链在任意时刻的边际分布。例如，我们可以通过表达式 ***vP*** 求出链在时刻 2 的边际分布。*

*当一个概率向量乘以转移矩阵等于其自身时会出现一种特殊情况:***vP***=***v .***出现这种情况时，我们称该概率向量为马尔可夫链的*平稳分布*。*

# *赌徒的破产马尔可夫链*

*使用马尔可夫链的理论框架，我们现在可以将这些概念应用于赌徒的破产问题。我们能够做到这一点的事实表明了概率和统计理论是如何相互交织的。我们最初使用从基本概率公理中导出的条件概率定理来设计这个问题。现在我们可以进一步形式化这个问题，并使用马尔可夫链给它更多的结构。采用抽象概念并使用各种工具对其进行分析和扩展的过程凸显了统计学的魔力。*

*赌徒的破产问题本质上是一个马尔可夫链，其中赌徒*和*在任一时间点拥有的财富数量序列决定了潜在的结构。即在任一时间点 *n* ，赌徒 *A* 都可以拥有 *i* 财富，其中 *i* 也代表链条在时间点 *n* 的状态。当游戏者达到 0 财富或 *k* 财富时，链进入吸收状态，不再玩游戏。*

*如果该链移动到剩余的 k - 1 个状态 1，…，k - 1 中的任何一个，则再次进行游戏，其中游戏者 *A* 将赢得 *p* 的概率决定了该状态在该特定时间点的边际分布。跃迁矩阵有两个吸收态。第一行对应于游戏者 *A* 拥有 0 财富的场景，该行的元素是(1，0，…，0)。同样，转移矩阵的最后一行对应于当游戏者 *A* 达到 *k* 财富并且元素为(0，…，1)时的场景。对于每隔一行的 *i* ，除了具有坐标 *i* - 1 和 *i* + 1 的项之外，元素都是零，它们分别具有值 1 - *p* 和 *p* 。*

*赌徒破产转移矩阵*

*我们还可以使用 *m 步转移矩阵* ***P*** ᵐ.来确定多步状态的概率当 m 趋于无穷大时，m 步矩阵收敛，但平稳分布不是唯一的。ᵐ的极限矩阵除了第一列和最后一列都是零。最后一列包含所有的概率 *aᵢ* 赌徒 *A* 将会以 *k* 美元结束，假设他们以 *i* 美元开始，而第一列包含所有相应的 *aᵢ.的补码*由于稳态分布不是唯一的，这意味着所有的概率都属于吸收态。*

*赌徒破产极限矩阵*

*这最后一点尤其重要，因为它证实了我们在推导赌徒破产的解决方案时最初的逻辑步骤顺序。换句话说，我们能够从整体上推导出问题的一般公式，因为问题中发生的随机过程(博弈序列)收敛到两种吸收状态之一:赌徒 *A* 带走 *k* 美元或赌徒 *A* 带走 0 美元*。*即使可以玩无限多的游戏，我们仍然可以确定这两个事件中任何一个发生的概率，因为马尔可夫链的转移矩阵收敛于两个平稳分布。*

# *结论*

*赌徒的破产问题是一个很好的例子，说明了如何利用统计工具，从一个复杂的情况中得出一个简单的总体结构。可能很难相信，给定一个公平的游戏，某人赢得足够多的游戏以获得两个玩家的总财富的概率是由他们的初始财富和总财富决定的。这不仅在序列的开始是已知的，而且在每个步骤也是已知的。使用马尔可夫链，我们可以用转移矩阵和初始状态的概率向量来确定任意博弈序列之间的相同概率。考虑到这一点，我们在这篇文章的第一部分得出的结论通过使用一个额外的概念得到了加强。对同一个问题应用不同的观点可以打开有洞察力的分析之门。这就是理论统计思维的力量。*

# *参考*

*[1] M. H. Degroot 和 M. J. Schervish，[概率与统计](https://www.pearson.com/us/higher-education/program/De-Groot-Probability-and-Statistics-4th-Edition/PGM146802.html) (2018)，皮尔森*