# 单元 2)进化计算简介

> 原文：<https://towardsdatascience.com/unit-2-introduction-to-evolutionary-computation-85764137c05a?source=collection_archive---------19----------------------->

## 进化计算课程

## 进化计算和遗传算法概述！

大家好，欢迎回到进化计算的完整课程！在这篇文章中，我们将讨论课程的第二单元，进化计算导论。在上一篇文章中，我们讨论了单元 1，最优化理论，你可以在这里查看:

</unit-1-optimization-theory-e416dcf30ba8>  

在这篇文章中，我将从整体上介绍进化计算的基本概况。从生物学的灵感开始，我们将看到 EC 如何寻求解决问题，然后我们将移动到进化算法的基本概述并解释主要细节。在下一单元中，我们将真正看到遗传算法的复杂性。

# 目录

*   生物灵感
*   进化算法综述
*   染色体的表示
*   原始群体
*   选择适应度函数
*   选拔过程
*   复制运算符
*   停止条件
*   进化算法的差异
*   结论

# 生物灵感

进化可以被描述为一个过程，通过适应、自然选择和选择性繁殖，个体在不同的环境中变得“更适合”。这里有一张查尔斯·达尔文在加拉帕戈斯岛上的日记中描述的著名雀鸟的照片。他注意到了这一物种喙大小的极端多样性。这是一个突变的例子。

![](img/96a7aa72f9bd53389d2e6898a546bf2f.png)

[https://commons . wikimedia . org/wiki/File:Darwin % 27s _ finches _ by _ Gould . jpg](https://commons.wikimedia.org/wiki/File:Darwin%27s_finches_by_Gould.jpg)

这是自然选择、适应和选择性繁殖的一个简单例子。

![](img/285d6980e990424808b04c72d0d724a6.png)

[https://commons . wikimedia . org/wiki/File:Darwin smoa _ jirafaren _ adibidea . png](https://commons.wikimedia.org/wiki/File:Darwinismoa_jirafaren_adibidea.png)

我们可以看到长颈鹿的植被位于高海拔，这使得脖子较长的长颈鹿更容易够到。因为环境的原因，脖子较短的长颈鹿无法进食，因此饿死，自然选择的例子。另一方面，因为只有脖子更长的长颈鹿存活下来，我们有一定程度的选择性繁殖，只有“最适合”的个体才能繁殖。因为只有“最适合”的个体才会繁殖(脖子更长的个体)，后代天生就适应环境(脖子更长)。

在进化计算中，我们试图对这些原则进行建模，以找到问题的最佳解决方案。一个问题的每一个可能的解决方案都被表示为一群人中的一个个体，在那里我们对那些可能的解决方案进行适应、自然选择和选择性繁殖，以最终找到问题的最佳解决方案。

# 进化算法综述

对于**规范遗传算法**的简要概述，我们从初始种群开始，然后选择如何将这些解编码为染色体，然后选择我们的适应度函数，大多数情况下是优化函数本身，最后我们选择如何选择哪些个体能够生存和繁殖。

![](img/4197453fe76015d6085a8ab4c1653605.png)

作者图片

上面我们有一个关于这个算法如何工作的基本图表。如果你一开始不明白所有的事情，那也没关系，我们以后会回来的。首先，我们随机初始化我们的种群，然后我们选择那些最适合繁殖的。然后，我们通过杂交在两个父母之间交换等位基因，并通过突变引入新的遗传物质。在这之后，我们有某种生存机制来决定谁能生存，谁不能。我们重复这个交配、繁殖和存活的过程，直到达到终止标准。

# 染色体的表示

细胞是生物体最基本的组成部分之一。每个细胞都是由 DNA 链构成的。染色体是 DNA 的主要结构，包含大量的基因，每个基因代表某种类型的遗传特征。在 EC 中，我们希望将这些特征建模到我们的优化问题中。在进化计算中，一个个体只是优化问题领域空间中的一个点，其中函数的每个变量值由一个基因表示。因此，每个点指的是个体，其中该点的每个组成部分，即变量值，被编码为基因组中的一个基因。基因型描述了个体的基因构成。另一方面，表现型定义了个体在环境中的样子。

例如，优化问题的域空间中的单个点在其基因组中由其变量的分量值表示；然而，它的表现型是函数的曲面空间中的实际点本身。后来，当我们介绍**遗传编程**时，它不是将个体表示为一个点，而是一个实际程序或决策树的树形图表示。此外，对于其他类型的 EC 算法，表现型可以是神经网络、设计布局、机器人等。关键在于，基因型代表了个体的构成，而表现型代表了个体在其环境中的物理外观。作为一个具体的例子，下面我们有一个点(红色)在其函数空间中的表现型:

![](img/eb77d20116fd96be6c0505c27dd00660.png)

作者图片

然而，上述点的基因型由其变量值组成:

![](img/16b4070b436ad0fb134da4d5304def78.png)

作者图片

在 EC 中，代表个体(即输入空间中的点)的经典方法是使用二进制编码。二进制编码是用于编码个体的第一种方法，因为它受到实际 DNA 化合物的启发，其中基因由用于描述氨基酸的三种可能的碱基组成。

![](img/183b44d94e98636eeb8a0ccdd3ef3e54.png)

[https://commons . wikimedia . org/wiki/File:DNA _ replication _ en . SVG](https://commons.wikimedia.org/wiki/File:DNA_replication_en.svg)

因此，从这个生物灵感中，我们可以用二进制编码我们潜在的解决方案，以最好地代表 DNA。下面我们可以看到，我们用 32 位二进制编码浮点数有三个部分，即符号位，8 位表示指数，23 位表示分数。

![](img/7bd62974852df54caab70fb80dca9b1e.png)

[https://en . Wikipedia . org/wiki/Single-precision _ floating-point _ format](https://en.wikipedia.org/wiki/Single-precision_floating-point_format)

然而，在现代实践中，二进制表示已经被浮点表示所取代，我们将在下一单元讨论这一点。

简单的二进制表示有两个主要问题。首先，二进制表示导致了所谓的**海明悬崖**。我们可以看到这样一个例子:

![](img/b7ec74e3ae6389f9e9baa1578a772269.png)

作者图片

测量二进制向量之间差异的方法是通过**汉明距离**，它简单地计算不相交的比特数。比如第 7 位= 0111，第 8 位= 1000；它们没有相似的位，因此它们的汉明距离为 4。问题是 7 和 8 彼此相邻，但由于它们的比特不同，它们在二进制编码中的汉明距离很大，导致汉明悬崖。作为回应， **gray encoding** 通过在比特的 NOT 之间进行逻辑 OR 和 and 运算来创建替代编码，从而解决了这个问题。通过使用格雷编码，我们将任意两个相邻数字之间的汉明距离限制为 1。以下是数字 0 到 7 的二进制编码和相应的格雷编码的示例:

![](img/63b048c9f52dce0bcd96f4a96596a995.png)

作者图片

然而，尽管有这种解决方案，将解决方案编码成二进制是非常耗时的。

# 原始群体

EC 算法的初始种群非常重要。进化算法(EA)是一种基于群体的搜索算法，这意味着它通过收集初始点并并行搜索这些点来工作。不像标准的数值方法，如牛顿法，你只给它一个初始值，EA 的工作是利用群体的多样性来搜索更好的解决方案。此外，我们还需要一种方法来表示问题的整个搜索空间/领域。如果我们的初始群体仅包括来自位于搜索空间中心部分的值，那么我们的算法将仅在该搜索空间附近找到最优解。

因此，为了确保多样性，我们需要从我们的领域空间中随机均匀采样。现在，每当我们处理约束问题时，其中的边界是不同的，依赖于变量值，我们最初的均匀采样可能会导致不可行的解决方案。为了解决这个问题，我们要么必须为我们的统一采样硬编码这个约束，要么只在整个输入空间采样，但只保留可行的解决方案。

最后，初始种群规模的选择对算法的收敛性和复杂性至关重要。较大的群体规模增加了初始多样性，并能维持这种多样性；然而，它给计算复杂性带来了沉重的负担。另一方面，较小的尺寸降低了初始多样性和世代间保持的多样性，但它需要较少的计算，提供了更快的替代方案。初始种群大小的选择取决于问题的复杂性、适应度函数的计算成本和可用的等待时间。

# 选择适应度函数

在进化中，格言是只有环境中最适合的个体才能生存。我们如何确定哪些人是合适的？在 EC 中，适应度函数是优化问题本身，其中具有较大值的值具有较好的适应度。在最小化的情况下，我们可以缩放函数值，使得较小的值产生较大的适应值。适应度函数的选择直接取决于需要优化什么问题。从单元 1，最优化理论，有四种主要类型的问题，无约束，约束，多目标和多解。EA 可以处理所有这些类型的问题，但是可能难以处理两个、受限和多个解决方案。因为域在约束环境中是动态的，所以我们的算法可能会遇到不可行解。为了解决这个问题，我们有两个主要的解决方案。一种是为不可行的个体在函数值上增加一个**惩罚项**。这样，我们降低了不可行解的适应度。惩罚条款的唯一问题是它们改变了我们搜索空间的适合度。这里我们有一个惩罚项的精确定义:

![](img/40ee5f589025769e6cc2116b0a27c3f6.png)

作者图片

另一方面，我们可以调整我们的繁殖算子，使它只产生可行的解；然而，由于许多限制，这可能会成为问题。

最后，进化算法在多解性问题上有问题，因为进化算法倾向于收敛到奇点或一组点。在有许多解决方案需要返回的情况下，EA 可能会在这种情况下挣扎。为了解决这个问题，我们可以引入欧几里德距离，这样一旦找到一个全局极值，我们就添加一个惩罚项，阻止个体接近欧几里德空间中的那个精确点。我们将在后面讨论这个应用程序。

# 选择

一旦我们有了初始种群并计算出每个个体的适应度，我们需要一种方法来决定谁将被选择来生存和繁衍。在 EA 中，在开发和探索之间有一个权衡。**剥削**简单来说就是指算法的收敛质量。如果我们选择一种算法，它总是选择最适合的个体来生存，那么我们就表现出高开发性而低探索性。高剥削导致快速收敛；但是，这也可能导致过早收敛。

![](img/b2d109d47a5f7bf5e78da2b81f084356.png)

[https://commons . wikimedia . org/wiki/File:健身-风景-卡通. png](https://commons.wikimedia.org/wiki/File:Fitness-landscape-cartoon.png)

例如，在上面的图片中(假设最大化)，全局最大值在 B 处，但是如果该位置没有被我们的算法探测到，那么它可能会过早地收敛到 A 或 C，这取决于已经探测了多少输入空间。然而，在图中，初始点位于 A 和 B 之间。因此，它将收敛到 A 或 B，这取决于来自算法的随机机会。与剥削相对的是**探索**，这种选择类型并不总是选择最适合的个体来交配，鼓励对输入空间的探索。然而，通过鼓励探索，该算法可能具有较差的收敛质量。

在实践中，有时最好两者都利用，开始时探索，然后到最后开发。有许多选择方法，但这里是最受欢迎的:

*   随机选择
*   比例选择(轮盘赌)
*   基于等级的选择
*   锦标赛选择
*   玻尔兹曼选择

**选择压力**指的是产生一个统一的种群需要多长时间，因此高选择压力会减少多样性，而低选择压力会鼓励探索。在这个系列中，我们将讨论随机选择、比例选择、基于等级的选择、锦标赛风格选择和波尔兹曼选择。然而，在应用中，我们将主要关注随机、比例和锦标赛，因为它们是最常见的。除了这些方法，我们还有一些可以利用的机制，比如**精英主义**和**名人堂**。

![](img/b38bfead26cf71422c83f1967f6f68e7.png)

[https://commons . wikimedia . org/wiki/File:Simple _ random _ sampling。PNG](https://commons.wikimedia.org/wiki/File:Simple_random_sampling.PNG)

**随机选择**是一种简单的方法，具有良好的探索品质，因为它随机选择个体生存；但是，正因为如此，它并不能保证当前的最佳解决方案会保留下来，从而导致可能的解决方案丢失。正如我们马上会看到的，它通常与精英主义结合在一起。

![](img/c1a21afcbe140a4365bbe2d81b007dad.png)

作者图片

**比例选择**，正如我们在上面看到的，通过将每个适应值除以适应值的总和，从适应值中创建一个概率分布。因为选择是基于概率的，所以它确保了良好的多样性，同时也确保了良好的收敛性；然而，因为概率是基于适应值与其余适应值的比例，所以早期具有大适应值的个体似乎可以支配选择过程。

![](img/bc9287b91cf715fe8daf13e9d0980e8a.png)

作者图片

为了缓解大的适应值在比例选择中支配再生空间的问题，已经提出了**基于等级的选择**。除了被选中的概率不是基于原始的适应值，而是基于个人的排名之外，它类似于比例。根据适合度值，个体从最差到最佳排序，其中最佳排序为 1，然后对于具有较高排序的个体，比例线性或非线性地降低。上面，我们有一个基于排名的选择的例子，除了最好的排名最高，最差的排名最低。个人的确切排名取决于您使用的基于排名的选择方程的类型。

![](img/7568d2a6e8731462c73b2f47a4fd4c1d.png)

[https://commons . wikimedia . org/wiki/File:Deterministic-tournament-selection-3 . SVG](https://commons.wikimedia.org/wiki/File:Deterministic-tournament-selection-3.svg)

**锦标赛选择**另一方面，随机选择一组个体，其中的数量称为锦标赛规模，从锦标赛中选择具有最佳适应值的解决方案来生存。这样做是为了确保良好的收敛质量，因为最佳的个体被选择，而且通过锦标赛的规模具有多样性的成分。请注意，锦标赛规模 1 基本上等同于随机选择；因此，较小的锦标赛规模可确保良好的多样性，而较大的锦标赛规模可确保选择最佳的适合度值。

**玻尔兹曼选择**是另一种形式的选择，其中被选中的概率基于**模拟退火方程**。我们将在下一单元讨论如何在后代和父母之间选择生存时涉及玻尔兹曼选择。

精英主义只不过是从当前人口中挑选出最优秀的一部分，并总是把他们带到下一代。这保证了良好的收敛性，但如果精英比例很大，也会导致较差的多样性。精英主义通常与随机选择或任何其他技术相结合，以获得良好的多样性和收敛性。

最后，**名人堂**是一种机制，其中群体中的最佳个体被留在名人堂中，在算法停止后，从名人堂中选择最佳解决方案。通过这样做，它允许算法通过随机选择来支持良好的探索，而不用担心失去最佳个体。然而请注意，精英主义和名人堂的区别在于精英主义从人口中挑选出最优秀的 x %的人，并将他们带入下一代；另一方面，名人堂只选择最优秀的个体，并把他们放在一边，因此留下了不被选择生存的可能性，允许良好的探索，同时也不会在技术上丢失每一代的最佳解决方案，因为它存储在名人堂中。

注意，所有这些方法都是基于选择的概率，因此一个个体可以被选择多次以生存和繁殖。

# **再现**

既然我们已经选择了要繁殖的个体，我们需要一种方法在父母之间共享遗传物质并引入更多。在 EA 中，这是通过**突变**和**交叉完成的。**杂交是父母双方的基因组混合在一起创造后代的方式。它的工作原理是选择一个交叉点，然后在父母之间的基因组上交叉，产生两个新的后代。我们可以通过下面的例子看到这一点:

![](img/fbd9b2f41b399e9b550bcf8a7bde061b.png)

[https://commons . wikimedia . org/wiki/File:computational . science . genetic . algorithm . crossover . cut . and . splice . SVG](https://commons.wikimedia.org/wiki/File:Computational.science.Genetic.algorithm.Crossover.Cut.and.Splice.svg)

另一方面，突变通过随机翻转位来突变后代基因组中的一个或多个基因，从而引入新的遗传物质。在实践中，变异主要用于差的个体，以鼓励探索，而不是对好的解决方案进行太多的变异，以确保良好的收敛性。

# 停止条件

既然我们已经定义了复制操作符，我们只需重复选择和复制的整个过程，直到满足停止条件。以下是四种最常见的停止标准:

*   最佳适应值没有变化
*   平均健康值没有变化
*   可接受的解决方案
*   已达到最大代数

常用的停止标准是在一定数量的代之后最佳适应值没有变化时。然而，由于最佳解决方案的值会波动，这可能会出现精英主义未被使用或每代未选择最佳解决方案的问题。此外，如果使用精英主义，可以证明在找到更好的解决方案之前，EA 可以在停滞状态下工作很长时间。

如同在最佳适应值没有变化时停止一样，可以改为在平均适应值没有变化时停止，这表明群体已经在某个区域附近收敛。然而，如果选择和繁殖算子鼓励探索而不是开发，那么种群的平均适应值将会以如此大的方差波动，以至于这个条件永远不会满足。另一方面，当找到可接受的解决方案时，可以停止，例如当 MSE 低于 1 时使用神经网络训练，或者当交叉熵对数损失接近零时用于分类。然而，这可能导致过早地退出该算法，在该算法中可能已经找到了未来更好的可能解决方案。

最后，在实践中最常见的一种方法是对算法进行多次模拟，并在达到最大代数时终止。

# 进化算法的差异

进化计算有许多不同的领域，这里是我们将在本系列中涉及的六个领域及其差异。

单元 3)遗传算法:模拟遗传进化

单元 4)遗传规划(GP):遗传基因的子集，但个体被表示为树或图

单元 5)进化规划(EP):关注行为，进化个体的表现型

进化策略:进化行为、表现型和基因型

单元 7)差分进化(DE):使用距离和单位向量进行繁殖

共同进化:个体通过合作或竞争进化

# 结论

概括地说，进化算法都是建立在以下设计选择之上的:

原始群体

适应度函数

染色体编码

选拔过程

复制过程

结束

初始群体的重要性在于确保良好的初始多样性，以及群体大小的选择。大多数情况下的适应度函数将是优化问题本身。接下来，我们需要决定如何编码染色体，以及表型是什么。接下来，我们需要选择我们的选择和复制操作符。有了这两个，记住剥削和探索之间的权衡。最后，我们需要选择何时停止我们的算法。

既然我们已经检查了规范遗传算法的初始图中包含的所有材料，让我们回到它:

![](img/4197453fe76015d6085a8ab4c1653605.png)

作者图片

首先，我们随机初始化我们的种群，然后我们选择那些最适合繁殖的。然后，我们通过交叉交换两个父母之间的等位基因，并通过突变引入新的遗传物质。在这之后，我们有某种类型的生存机制来决定谁能生存，谁不能(我们将在后面讨论)。然后，我们重复这个选择、繁殖和生存的过程，直到达到终止标准。

然而，还有一些其他的设计问题，我们没有涉及，即谁将在复制后生存。在简单的算法中，那些没有被选择交配的是那些没有存活下来的，其中后代取代了父母。然而，在一些算法中，生存可能是一个完全不同的选择过程，要么通过混合后代和父母的另一个选择程序，要么在后代和父母之间进行某种类型的“战斗”，以确定谁能生存下来。我们将在后面的单元中讨论这些可能性。因为这一单元是进化算法的介绍，所以没有应用部分，但是在下一部分我们会这样做。

第二单元的进化计算介绍到此结束，请继续关注第三单元，我们将在第三单元讲述遗传算法:

</unit-3-genetic-algorithms-part-1-986e3b4666d7> 