# 奖励最大化对于完全智能是不够的

> 原文：<https://towardsdatascience.com/reward-maximization-is-not-enough-for-complete-intelligence-d1afecde097a?source=collection_archive---------27----------------------->

## 多代理场景使得报酬最大化成为一种风险。讨论何时，而不是是否，我们应该相信奖励假说。

[**多巴胺**](https://en.wikipedia.org/wiki/Dopamine) (下图)是人类体验的核心。众所周知，它与感受当前的快乐有关——那是你正在经历和享受的事情。多巴胺在预测未来方面也起着至关重要的作用——这是在计划中完成的，当你计划做你喜欢的事情时，释放出同样的快乐感。人体有一个超级复杂的基础设施，围绕着享受、愉悦、目标设定、生殖等等，所有这些都与这个分子有关。

![](img/ccdbbe790b9eb9075d11e757f2cdb7a0.png)

来源，维基百科。

试图模拟多巴胺的作用可能是理解人类如何学习的一条途径。这个信号是我个人对强化学习如何与神经科学和生化系统联系起来的评论的中心(博客 TBD)。声称我们可以通过“求解”多巴胺来理解人类意图的目标，与我们可以从一个测量信号中优化任何复杂系统的目标非常相似(古德哈特定律源于人性)。

我们可以将我们需要的所有指标封装在一个单一的奖励函数中的想法是深度学习的当前技术应用所特有的。特别是在强化学习中，有一种理论认为，任何智能体都可以通过合适的标量奖励函数来学习解决其可达空间中的任何任务。这个 ***奖励假设*** ( [链接](http://incompleteideas.net/rlai.cs.ualberta.ca/RLAI/rewardhypothesis.html))是在说，对于任何强化学习主体(通常被视为个体)，我们都可以将多目标优化归结为标量优化。奖励假说，或者这篇文章中的假说，是由一些“创始人”或 RL 提出的，所以它是有分量的。

最初是在 Rich Sutton 的博客上说的:

> 我们所说的目标和目的都可以被认为是接收到的标量信号(奖励)的累积和的期望值的最大化。

在将这种方法应用于更复杂的互联网系统时，所有可以采取的行动(跨许多用户)都包含在同一个代理下，这扩展了最初想法的范围，并导致其有效性受到质疑。这篇文章旨在梳理[奖励假说](http://incompleteideas.net/rlai.cs.ualberta.ca/RLAI/rewardhypothesis.html)背后的一些关键思想，并指出我们应该在这个假说的适用性上划一条线。

在理解可以由标量奖励函数合理定义的行为时，有哪些限制？可能有一个精确的函数来描述任何尺度下的人类意图，但它可能对扰动过于敏感，试图找到它会弊大于利。

# 假设

由于实数和表达式的无限性，奖励假说有了很好的基础。该理论的支持者说，对于一个智能体来说，必然有一个高度精确的函数来满足它的需求。我并不否认这种函数的存在，而是我们是否应该费心去寻找它们。

下面是对假设的两个低层次的批评(即假设在任何情况下都是合理的主张)。首先，我们应该考虑这些标量奖励函数是否可能**永远不会是静态的**，因此，如果它们存在，我们在事后发现的那个将永远是错误的。此外，由于存在无限可能的奖励函数，所以也可能**无限难以找到代理的奖励规格**。如果我们知道我们不太可能找到正确的表示，那么将每一个可能的回报都包含在标量函数中又有什么意义呢？

对于提供分数和排行榜的游戏，奖励函数很直观:最大化分数。对于具有多个优先级的代理，例如健康和事业，通过**关系**优化找到奖励函数变得更具挑战性。我假设对个人来说，这样做更合理，但不值得，因为我们可以扩展状态-行动空间，以轻松解释多模态行为。这就是说，当阅读或锻炼时，人类可能采取非常不同的行动，并且他们可能以相关的方式对奖励函数做出贡献(奖励函数通常被定义为当前状态和行动的函数)。

奖励假说的真正挑战在于更多的存在性问题:

*   **这对关系回报有用吗**:标量函数能代表不同的人对不同的东西的价值吗，特别是当这些人相互作用或者系统必须决定一个人更想要它的时候？
*   控制和政治经济:让一家公司或一些机器理解、支配和执行特别调整的报酬，值得吗？考虑到以上所有因素，可以说，像营利性公司这样的公司正通过努力学习并根据你的奖励偏好和你最亲密朋友的偏好采取行动而使你受益。

学习别人的价值观并不一定是对我们某种形式的社会目标的侵犯。*知道这样的近似是由设置将有错误，并采取行动，好像学习奖励无论如何是真的可能是*。当公司超越基于点击的指标时，理解用户目标是参与度和价值最大化的合乎逻辑的下一步。

大卫·西尔弗、萨汀德·辛格、多伊娜·普雷科普和理查德·萨顿最近发表的[论文](https://www.sciencedirect.com/science/article/pii/S0004370221000862)、*奖励就够了*，通过大卫·西尔弗(领导了许多 DeepMind 的游戏研发工作；迄今为止 ML 的一些最引人注目的成功)和 Richard Sutton(80 年代 RL 领域的创始人)。在我看来，在这些系统上工作的人需要有一个更加多样化的话语，来说明 **RL 被大规模使用的意义**。是的，回报最大化可能在所有这些应用中都有用，但是人们需要考虑界限、红线、最终目标、价值等等。

论文中的许多观点都是合理的，但是那些认为回报最大化是建模和理解“社会智力、语言、概括”的唯一视角的观点就很难得到支持了。遵循这些对设计这样的关系系统有用的回报最大化和优化框架的主张，是对什么样的结构应该控制我们的生活的强有力的陈述。

## (生物)逻辑代理和标量最大化

多巴胺在人类主观体验中起着核心作用的假设被创造为[快感缺失假说](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3155128/) (1982):

> 快感缺失假说——大脑多巴胺在与积极奖励相关的主观快乐中起着关键作用——旨在吸引精神病学家的注意，越来越多的证据表明，多巴胺在与食物和水、大脑刺激奖励、精神运动兴奋剂和鸦片奖励相关的客观强化和激励动机中起着关键作用。

多巴胺现在稍微为人所知:

> 在学习和记忆的细胞模型中，大脑多巴胺在强化反应习惯、条件偏好和突触可塑性方面起着非常重要的作用。多巴胺在强化中起主导作用的概念是成瘾的精神运动兴奋剂理论、大多数成瘾的神经适应理论以及当前条件强化和奖励预测理论的基础。正确理解的话，它也是最近的激励理论的基础。

这种**激励动机**渗透在许多学习代理中，作为预期回报的升华，转化为控制行动的参数:

![](img/5a868b2811155b71d99ed213a7209180.png)

一个强有力的论点是，个人的行为就好像生命是一个精细调整的奖励系统，优先考虑繁衍后代。一个人的遗传和环境决定了某种条件，这种条件会重新权衡多巴胺回路中不同的优先级。

我们的大脑可能会在其已知行为范围内非常迅速地适应它在社交媒体中面临的变化，并通过进化慢得难以想象。如果社交媒体处于泡沫中，我们与它的互动不会相互影响，那可能没问题。当我们在社会的尺度上研究它，并试图比较不同群体的动机时，多巴胺预测和代理的标量优化的原则就失效了。

# [将优化应用于现实决策](https://cdn.substack.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2Fd35a2437-1967-44eb-bf5e-f4b8ddee26a5_1218x342.png)

这篇文章真正开始的地方是思考，更现实地希望，基于注意力的度量最大化时代的结束。基于注意力的指标优化是:技术公司如何使用一些简单的指标来推动他们平台上的参与度(短期内，持续地)。目标是考虑系统如何更好地平衡和共同优化用户的长期利益。

通过在伯克利举行的关于人工智能未来影响的会议，我听到了多个关于用户计量跟踪的大规模改革不太可能在短期内发生的第一手报道。

对这些公司来说高利润的东西暂时还会起作用，至少在任何监管通过之前。最终，我怀疑大型社交媒体公司会希望过渡到一种模式，使其平台的行为与用户的目标相匹配。

大多数认识到他们或者他们亲近的人沉迷于他们的手机的人不喜欢它，因此优化的改变是应该的。不再有点击率，犹豫时间，像数数等。！虽然，可能的结果是公司将当前的方法转变为不同的奖励功能，优化长期计划，但如果社交媒体应用的奖励功能旨在激励某些类型的生活方式，优化可能是不适定的。

看过去的短期指标使这些算法在屏幕上的行为(计算秒、分、小时)和生活方式结构(天、周、年)之间取得平衡。多目标优化领域非常清楚地说明了为什么这很难做到:

> 对于一个[非平凡的](https://en.wikipedia.org/wiki/Nontrivial)多目标优化问题，不存在同时优化每个目标的单一解决方案。在这种情况下，目标函数被认为是冲突的，并且存在(可能无限)个 Pareto 最优解。如果没有一个目标函数的值可以在不降低其他一些目标值的情况下得到提高，那么一个解决方案被称为[非支配](https://en.wikipedia.org/wiki/Maxima_of_a_point_set)、帕累托最优、[帕累托有效](https://en.wikipedia.org/wiki/Pareto_efficient)或非劣解。如果没有额外的[主观](https://en.wikipedia.org/wiki/Subjectivity)偏好信息，所有的帕累托最优解都被认为是同样好的……目标可能是找到一组有代表性的帕累托最优解，和/或量化满足不同目标的权衡，和/或找到满足人类决策者(DM)主观偏好的单一解决方案。

有无限多种解决方案。帕累托最优看起来不像是人类可以实际追求的东西。 ***我不希望我的应用程序在帕累托方案之间做出选择。***

任何用户都应该有能力说明他们的目标是什么，并让算法调整他们的行为以匹配这一点。无论有多少反思，公司在不告诉我们的情况下定期在我们生活的幕后改变优化问题的事实是家长式的，不可取的。

由于盈利能力存在问题，用户的选择可能会受到限制。在这些系统的规模下，任何用户都可能看起来更像噪音，而不是公司优化的真实信号。用户之间的交互，以及他们经常使用的列举的应用程序，将在很大程度上决定这些系统的轨迹。

## 作为多目标优化的社会和系统

任何在社会中定义奖励功能的尝试都会侵犯我们认为不可剥夺的权利。人类社会作为一种新出现的进化行为，其稳定性还没有得到很好的研究。很快，将会对我们最重要的进化技能应用更多的测试案例。

如上所述，比较动机将转化为根据手头的权重对某些用户进行优先排序。考虑一个不祥的场景，某些应用程序可以准确预测我们的多巴胺水平，并利用它来调整个人及其最亲密朋友的行动。多巴胺峰值水平较高的人会优先于基线水平较低的人吗？反驳这一论点可以揭示更多的缺点，比如社交媒体永远不知道你的过去，不知道某人被某种形式的创伤所阻碍的巅峰幸福。

如果所有个体代理都同意这个目标，那么类似奖励假设的系统运行大型系统可能是有意义的，但事实并非如此。在大规模推荐的情况下(例如 YouTube、脸书……)，从工程的角度来看问题有很多方法。这些系统设计中的每一个在高层次上都是合理的，但对下游的影响却大相径庭:

*   部署一个全局策略(累积推荐器是随着用户数量增长而拥有巨大行动空间的代理)，人是环境。
*   改变奖励机制，使人们在包含推荐的环境中行动(可能是一种反向 RL)。
*   坚持一对一优化，其中用户查询一组权重，并且他们的体验对其他用户的数字选择封闭(交互仍然存在于现实世界中，在这种方法的预期抽象之外)。

许多观点和几个令人信服的答案都集中在人类排列上，特别是从个人的角度，这让我担心。更加集成和先进的数据驱动系统正在将我们推向那个方向，目前还不清楚我们何时会通过**重新安排我们的偏好和目标**而达到某个重要社会结构的**临界点**。

这些*奖励不够*的情况可能没有一个工具可以最优解决。有些问题最好不要优化。

*这个原本出现在我的自由子栈* [***民主化自动化***](https://robotic.substack.com/) *。请查看或关注我的* [*推特*](https://twitter.com/natolambert) *！*