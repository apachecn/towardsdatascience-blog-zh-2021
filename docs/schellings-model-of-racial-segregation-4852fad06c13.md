# 谢林的种族隔离模式

> 原文：<https://towardsdatascience.com/schellings-model-of-racial-segregation-4852fad06c13?source=collection_archive---------20----------------------->

## Python 中的实现和分析以及量化的出现

种族隔离已经在不同的社会中存在了几个世纪，并且经常被法律强制执行。例如，19 世纪美国的 T2 吉姆克劳法(T3)就是这种情况。当美国最高法院在 1954 年宣布它们违宪时，许多人预计种族隔离将会消失。然而，事实并非如此:相反，尽管付出了大量努力和投资，迄今为止，隔离仍然是美国和其他地方的一个主要问题[1]。

![](img/f20f6fe52176f207ed6a47d9dc6e00c1.png)

***图 1:*** *根据 2010 年的人口普查，芝加哥的种族居住隔离情况[2]。查看弗吉尼亚大学魏尔东·库珀公共服务中心的美国种族隔离地图。*

即使没有实施隔离的法律，这也可能是由许多因素造成的，包括住房和贷款歧视、偏见等。然而，当时没有考虑到的另一个因素是*涌现*，即复杂系统组成部分的微观相互作用产生的宏观特征的存在。1971 年，托马斯·谢林设计了一个最早的基于主体的模型[3],表明即使当个体不介意被不同种族包围时，只要他们仍然希望至少有一小部分人与邻居具有相同的种族背景，种族隔离也可能发生。尽管代理人愿意接受一个更加多样化的邻居，隔离仍然出现在不同个体的社会互动中。引人注目的是，即使是微弱的地方偏好也能导致从个体微观互动网络中出现重大的全球现象。此外，这些涌现的宏观规则反馈到个体代理人，约束他们的选择和行为。

正如我们将看到的，尽管简单，谢林的模型产生了迷人而复杂的动力学，有着多重且远离直觉的平衡。

# 一个简单的隔离模型

谢林隔离模型的一个最简单的版本包括一个住宅区的风格化表示，在那里，个人根据其紧邻的特征反复做出搬迁决定。该模型考虑了两种类型的代理，比如说*和 ***红色*** ，它们可能代表不同的种族、民族、经济地位等。，以及住宅位置的 ***N × N*** 网格，在其上最初随机分配多个 **Nₐ ≤ N** 代理。代理商的数量以蓝色到红色类型的比例 **B/R** 为特征，因此 **Nₐ = B + R** ，并假设为常数，因此在任何给定的时间都将有**nᵥ= nnₐ**的空置住宅位置。然后，每个代理 **i** 由同类型邻居的分数给出的*满意度参数*sᵢ来表征。注意，邻居的数量可能取决于考虑的是固定的还是周期性的边界条件，以及在计算 **Sᵢ** 时没有计算在内的空闲位置。*

*![](img/7ddc8ff5ca27d7c36881d31fc29b644b.png)*

****图 2:*** *两个智能体的邻域* ***i*** *和* ***j*** *为固定或周期性边界条件。【来源:作者图片。】**

# *力学*

*动态由全局*容差参数* **τ** 设置，该参数表示每个代理在决定重新定位之前愿意接受的不同类型邻居的最大比例。因此，每个具有**sᵢ<1-τ**的代理将随机重新定位到不同的空闲居住位置。这种动态一直持续到找到一个稳定的平衡(如果存在的话),所有的代理人都满意为止。因此，个人的决定完全是基于个人考虑，基于他们目前居住的当地社区的特点。然而，重新定位的行为，尽管是基于局部参数，但最终具有全局效应，因为一个代理的随机重新定位可能会使先前满意的其他代理不满意。
模型的替代版本可能会考虑不同的行为，不满意的代理将移动到最近的空闲位置，而不是随机位置，或者移动到最佳可用位置，或者移动到满足阈值**1-τ**的最近位置。然而，另一个行为规则将允许个人只有在有更好的位置时才搬家。请注意，不同的规则可能会对全球动态产生重要影响。考虑一个例子，其中所有不满意的个人随机移动(这是我们将在下文中使用)。显然，对于足够低的容差 **τ** 和/或足够低的空置房产比率，不存在静态平衡，因为总会有至少一个人对其位置不满意，并且无法找到另一个合适的位置。另一方面，当考虑到只有在找到更好的地点时，人们才会搬迁，静态均衡总是存在的。*

# *模拟*

*在下文中，我们在具有 ***N=60*** 的 ***N × N*** 网格上采用了谢林分离模型的 Python 实现，假设在任何给定时间 10%的所有属性是空闲的，红色与蓝色代理的比例为**1**--**1**。让我们从定义系统参数开始:*

*虽然面向对象的编程通常是基于代理的建模中最受欢迎的编程范例，但在寻找数值有效的例程时，这可能不是最合适的方法。因此，为了在模拟中保持高效率，我们将系统建模为大小为`(N, N)`的`numpy.array`，将蓝色代理占据的住宅位置编码为`0`，将红色代理占据的住宅位置编码为`1`，将空置的房产编码为`-1`。
现在需要两个主要函数:一个`rand_init`函数用于系统矩阵`M`的随机初始化，一个`evolve`函数用于对系统施加上述动态特性。前者很容易实现为*

*下面的图 3 给出了随机初始化系统的例子，具有上面指定的参数。*

*![](img/79012e068b25ae6f4917bb965e52a88a.png)*

****图 3:*** *随机初始化，集成度高。【来源:作者图片。】**

*相反，进化函数是大部分计算工作的所在，更具体地说，是满意度参数 **Sᵢ** 的计算。对于快速实现，我们可以依赖矩阵`M`与内核的卷积*

*核上的卷积运算*

*![](img/47ce5636308edcb0db534a0926e7a751.png)*

*被定义为*

*![](img/2a55454fca515720008a45aa2aee57a1.png)*

*因此，上述卷积的每个元素都包含所有相邻值的总和。考虑到这一点，我们现在可以编写一个函数来处理系统的动态演化:*

*请注意，`scipy.signal.convolve2d`的`boundary`参数提供了一种从固定(`'fill'`)切换到周期性(`'wrap'`)边界条件的简单方法。下面我们将坚持后者。*

*最后，我们能够运行模拟:图 4 示出了从具有高度集成的随机初始化状态到隔离配置的演变，其中每个区域被一层空位分隔开。请注意，由于周期性的边界条件，红色几乎形成一个单独的斑点，除了计算网格中央左侧的一个小岛，蓝色代理也是如此。*

*![](img/8d3775fdb5f98d64386ff74410151952.png)*

****图 4:*** *系统从初始随机状态演化为****1τ= 0.6****，****r = b****，***nᵥ/n*= 0.1******60×60*【来源:作者图片。】***

*不出所料，高度的不容忍导致了完全隔离的配置。然而，令人意想不到的是，即使看似不容忍的程度很低，隔离的程度也会自然出现。即使个人愿意接受高达 60%的不同邻居(**1-τ= 0.4**)，仍然会观察到隔离的出现，如下图 5 所示。换句话说，这是谢林的主要观点之一，聚合隔离甚至可以从个人的欲望中出现，不要觉得自己是极端少数。不同代理人的决策之间的相互作用，以及对其住宅区构成的如此薄弱的要求，足以导致隔离的出现。驱动涌现的自我强化机制是在一个邻居中的个体在一个个体重新安置的条件下重新安置的可能性增加中发现的。当一个少数民族离开一个社区时，这种类型的代理人在该社区变得更加稀少，因此也为其他人的迁移提供了动力。*

*![](img/364230beccbcf22917710d4be8245435.png)*

****图 5:*** *增加不容忍的系统的一些平衡。【来源:作者图片。】**

*隔离的程度可以通过个体群体的平均满意度 **⟨S⟩** 来衡量。如上所述，这增加到临界阈值，之后系统变得不稳定，并且不能找到静态平衡(见图 6)。此外，直到临界阈值，即当静态平衡存在时，人们系统地观察 **⟨S⟩≥1−τ** 。值得注意的是，平均满意度 **⟨S⟩** 通过在偏好**1-τ**的特定值处发生的离散转换来量化。*

*![](img/76c19b7f8093ab1d054e55d7bfa1004c.png)*

****图 6:*** *表示满意****⟨s⟩****表示增加不容忍****1-τ****。这些值在****200****蒙特卡洛模拟中进一步平均，阴影区域表示平均值周围的一个标准偏差。【来源:作者图片。】**

***⟨S⟩** 的量化可以追溯到每个个体的邻域的离散性(图 7)。忽略空置位置，每个人最多可以有 8 个邻居，这些邻居可能是也可能不是同一类型。因此，对于 **n ∈ ℕ : n < 8** ，可以预期 **⟨S⟩** 中的量化跳变会发生在任意 **n / 8** 处。*

*![](img/22b11836b3ebfca7b3812f05699334f5.png)*

****图 7:*******⟨s⟩****为变化分数的空位* **Nᵥ / N** *相对于不耐性****1-τ****。这里****R/B = 1****。****【⟨s⟩】****的量化很明显，随着空置物业比例的增加，出现了更精细的结构。【来源:作者图片。】***

**自然地，随着空置位置比例的增加，随着预期邻居数量的减少，出现了更好的量化结构(回想一下，空置位置不计入 **Sᵢ** 的计算)。因此，更一般地，人们可以期望在 **⟨S⟩** 的 **n/m** 处找到 **n,m∈ℕ:m≤8,n < m** 的量化跳跃。这些部分在图 7 中用红色垂直线标出；较高的线对应于较高的 **m** 值。**

# **参考**

**[1] [“种族隔离仍然是个问题”，迈克尔·卡西迪，世纪基金会，2013 年 7 月](https://tcf.org/content/commentary/racial-segregation-is-still-a-problem/)**

**[2] [“种族点阵图”，人口统计研究小组，弗吉尼亚大学魏尔东·库珀公共服务中心，2017](https://demographics.coopercenter.org/racial-dot-map)**

**[3] [“隔离的动态模型”，托马斯 C·谢林，《数理社会学杂志》，1971 年，第 1 卷，第 143–186 页](https://www.stat.berkeley.edu/~aldous/157/Papers/Schelling_Seg_Models.pdf)**

**[4]本帖也可以在[作者个人网站](https://lucamingarelli.com/Teaching/schelling.html)找到。**