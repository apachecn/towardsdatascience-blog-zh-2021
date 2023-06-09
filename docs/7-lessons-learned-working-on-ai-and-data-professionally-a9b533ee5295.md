# 考虑不用 AI

> 原文：<https://towardsdatascience.com/7-lessons-learned-working-on-ai-and-data-professionally-a9b533ee5295?source=collection_archive---------15----------------------->

## 给数据科学家的专业建议

![](img/553bef3acd5a425025272f52de603c59.png)

[斯科特·格雷厄姆](https://unsplash.com/@homajob?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍照

答在从事了近六年的机器学习、人工智能和开发工作后，我列出了这些年来我从成功和失败的项目中获得的七点见解。这里的中心主题是，尽管学习了无数的模型和技术，但作为一名有效的人工智能专业人员，如何尽可能地避免复杂性。推动商业价值是关于解决紧迫的问题，而不是最先进的。

更具体的说，做生意总有需要注意的事项。从来没有一个问题需要解决。您可以改进现有的模型，部署一个新的模型，重做一个特定的步骤，或者做其他事情。经验告诉我，人们倾向于陷入模型，忘记其他一切——这通常是最重要的部分。

让你对我有更多的看法，自 2015 年以来，我一直断断续续地与人工智能、企业和研究合作，要么领导人工智能产品或计划，要么是唯一的开发者。这对我的职业发展有两个主要因素:(1)我必须自己解决大部分问题，以及(2)大多数时候，我与那些对人工智能真正能做什么或能从它那里得到什么一无所知的人一起工作。

我们走吧:

# 摘要

1.  **简单款最好**
2.  **ResNet-50 仍然是最好的网络**
3.  **生活中的一切都是可以改善的。
    百万美元的问题是首先改进什么**
4.  **模型是<工作的 10%**
5.  **你的结果和你的代码一样好**
6.  **其实避开 AI**
7.  **没有指标，就没有收获**

# #1 简单的模型是最好的

并非所有的问题都是平等的。有些需要神经网络来解决。XGBoost 可以驯服别人。然而，使用[决策树](https://scikit-learn.org/stable/modules/tree.html)、[逻辑回归](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)和[线性回归](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html)可以合理地解决一组特殊的问题。

在学习了周围所有奇妙的技术之后，总是去寻找科幻小说中的新成员是很有诱惑力的——但是不要。相反，从你可以使用的最简单的模型开始，然后看看效果如何。如果线性插值解决了你的问题:*坚持下去。去花里胡哨不会得到任何额外的东西。*

在实践中，更简单的方法不会像其他方法那样解决很多问题，但无论何时，它们都有优势。模型越简单，就越容易解释它是如何工作的，解释它如何符合数据，解释它的预测的原因，调整它，等等。只有好处，真的。

然而，相反的是错误的。使用花哨的[高斯过程](https://scikit-learn.org/stable/modules/gaussian_process.html)或最先进的网络不会带来额外的好处。只要有可能，就使用线性插值。你的第二个尝试是逻辑回归，决策树是第三个。一切都将是对上述任何功能的妥协。

**要点:**你花了几个月时间学习复杂的分类器、校准和预处理，找出最不酷的方法是最好的。

# #2 ResNet-50 仍然是最好的网络

假设你一直在研究神经网络。忘掉所有那些每天在代码为的报纸上发布的[新奇的新网络。所有的铃铛和哨子都是铃铛和哨子。我们都需要一个久经考验、行之有效的模型，这个模型几乎可以在任何开箱即用的东西上运行良好。](https://paperswithcode.com/latest)

[ResNet](https://arxiv.org/abs/1512.03385) 恰恰是:*屡试不爽。*

神经网络的现实是，它们非常不可靠，而且调整起来非常耗时。然而，有一个简单的实验你可以在家尝试。获取你训练过的任何网络。假设它在某些指标上达到了 89%。再训练一次。又是 89 还是 88？可能 90？现在，再次重新训练最后一个网络(相同的参数，最后一个检查点)。可能是你得到了 91%。

在我几乎每天与训练网络一起工作的三年经验中，我总是在项目时间表中选择一天来寻找新的损失、激活函数、新的花式层和最新的亚当杀手来尝试这个问题。想知道我学到了什么吗？几乎 95%的情况下，我用交叉熵/L2、ReLU、plain-old-convolutions 和 Adam 得到的结果都差不多(1%的波动)。

我们应该永远不尝试新事物吗？*当然不是*。然而，请记住，坚持使用久经考验的方法永远是最安全的选择。

# #3 生活中的一切都可以改善。最重要的问题是首先要改进什么

老实说，这可能是我在这篇文章中得到的最重要的提示。

你可以*总是*改进模型。你可以*总是*让事情跑得更快。问题是*先做什么*。

我已经记不清有多频繁地看到会议讨论不存在的可伸缩性问题，或者计划减轻一些永远不会到来的潜在变化。现实是大多数人并不需要 10%更好的模型——他们需要 10%更多的客户。

花几天时间调整这些我们称之为网络的疯狂野兽是令人愉快的。然而，这很少是商业价值所在——或者获得额外 10%的最佳方式。[以数据为中心的人工智能运动](https://datacentricai.org/)在这里证明，收集多一点的数据比盲目寻找新模型更有效。

当开始一个人工智能项目时，最紧迫的问题是…拥有一个人工智能。之后，下一个关键点是获取更多数据或将其投入生产。一旦这两个问题都解决了，其他地方缺乏人工智能是最有可能的新的紧迫问题。将人工智能添加到普通产品中几乎总是比改进现有管道有更高的投资回报率。

坦率地说，通常情况下，商业人士对人工智能到底是什么或它能做什么几乎没有任何概念——他们肯定会想象它在做超人的壮举。所以让你的手离开模型，教育你周围的人是值得的。[那个](https://www.coursera.org/learn/ai-for-everyone)有免费课程。如果有人反抗，不要推。去别的地方。这家公司做 AI 还不成熟。

**要点:**认真审视你所做的和拥有的一切。最薄弱的环节是什么？什么如果改变，会带来最大的价值？改进迭代。

# #4 车型是< 10% of the Work

Continuing from the previous tip, in my experience, improving the model is often a low-priority task. However, in good operating conditions, you might be getting a constant influx of data to retrain it every week and, *voilá* ，比较好的车型。

如果你的渠道没有这样的反馈循环，也许你可以在下一次会议上提出这一点。如果这太遥不可及，也许您可以投资于更好的数据扩充策略，或者简单地投资于如何及时获取更多数据。

然而，更常见的是，附近还有另一个问题，还没有人工智能解决方案，可以提供比改进其他一些已经启用人工智能并正在运行的产品更大的商业价值——新问题意味着清理数据，查看数据，找到模型适合的位置，训练模型，将其连接到生产中，看看会发生什么……

**要点:**尽管我们愿意花时间改进模型，但真正的商业价值往往在其他地方找到。接受这一点是成为一名有效的人工智能专家最显著的变化之一。

# #5 你的结果和你的代码一样好

人工智能对常见错误有很高的容忍度，特别是关于数字导向的方法，如梯度助推器，支持向量机和神经网络，如糟糕的数学或丢失步骤。例如，假设您忘记了规范化您的输入，模型将从未规范化的数据中学习。

问题是，人工智能模型通常有两条独立的代码路径:训练和推理。假设您的代码在其训练代码中有一个数学错误，但在其推理脚本中没有。结果是灾难性的。该模型将适合损坏的数据，显示良好的指标，并在稍后向客户端泄漏虚假的输出。也许你得到了一个错误的自定义数据扩充，使你的模型加倍努力地解码那些实际上永远不会出现的条目。

有许多方法缺陷隐藏在训练和推理脚本中。缺少规范化、不正确的数据类型、不完整的扩充等。确保你确信一切都是正确的，并且有直观的方法来检查一切。

最后但同样重要的是:90%的准确率并不是工作代码的同义词。准确性代码本身可能是一个错误。不要相信任何人。

**要点:**现在你的代码中可能有一些可怕的错误没有被注意到，因为它们不足以推翻系统。他们将在生产中脱颖而出。*认真对待测试。*

# #6 事实上，避免人工智能

是的，我说了。

说实话，有些问题可以用传统代码来处理。代码是可读的、确定的、可理解的，最重要的是，精确地工作*。当我们对一个数组排序时，我们不是在处理一个有 89%机会排序的数组。*代码工作*。*

*当然，有些问题不能只靠代码来推理，比如物体检测或者图像生成。然而，对于所有我们可以用代码做的事情:用代码做。*

*人工智能的主要问题是它永远不会完美。*一个 90%准确的模型仍然有 10%的时间是错误的*，而且你无法控制错误发生的时间。你用的人工智能越多，出错的空间就越大。*

*假设你用两个模型预测年龄和性别，每个模型都有 90%的准确率。有 81%的可能性两个模型都有效，18%的可能性至少有一个会失败，1%的可能性两个都会失败。这归结为五分之一的用户得到了错误的预测。如果准确率为 80%，将近五分之二的人会得到错误的输出。*

**顺序使用 AI 是一场噩梦*。假设在预测年龄和性别之前，您使用对象检测找到一幅图像中的所有人，准确率为 90%。正确归类某人的几率现在约为 73%。最重要的是，有 10%的可能性这个人甚至没有被找到。*

*缩放多人，正确检测+分类 2、3、4、5 人的几率分别为 53%、38%、28%、20%。为了达到五个人 80%的可靠性，所有模型都需要高达 98.52%的准确率。这远远超过了 ImageNet 上最先进的顶级准确性——这是当今人工智能中最过度研究和修补的问题。*

***要点:**永远考虑用非人工智能的方法来解决你的问题。例如，对于分割任务，您总是可以使用图像处理操作来改进/连接/丢弃发现。此外，在处理视频时，考虑利用以前的帧结果作为备份。这些微小的变化会对减轻您无法控制的小错误产生很大的影响。*

# *#7 没有指标，就没有收获*

*在整篇文章中，应该清楚的是，与人工智能和数据打交道并不是为了展示你令人难以置信的机器学习能力或你对神经网络的掌握。相反，它是通过外科手术般地将人工智能原理应用于非常规任务来驱动商业价值。在这种背景下，还缺少一点:*如何衡量商业价值？**

*大多数模型都有一些精确的衡量标准:正确预测的数量、发现的对象、检测到的关节等。然而，这些都是局部测量:它们判断模型在解决其任务时的局部影响。另一方面，商业价值来自于对全球价值的影响，如利润、转换、流失等。*

*追踪单一干预(人工智能与否)对全球商业变量波动的贡献非常困难。在这方面，通常有一些中间地带可以作为业务价值的指标。对于任何人工智能企业的成功来说，最重要的是确定它应该跟踪的相关变量，并表明它对这些变量有一定的驱动力。*

*在这种情况下，保持一些可行的基线方法进行比较也是至关重要的。例如，假设您正在跟踪销售数字。由于季节性事件，销售额会上升或下降。如果没有并行运行的基线，有效地显示任何上升或下降都是由于应用程序上的一些修改，这是非常重要的。*

*回想一下，我之前说过，大多数企业不需要额外的 10%的准确率，他们需要多 10%的客户。有人会说，10%更准确的解决方案可能会推动 10%(或更多)的新客户获得用户，这是有可能的。然而，这只能通过展示这种关系的坚实的度量工作来论证。*

*比人工智能本身更重要的是如何衡量它对应用/业务/用户生活的影响。准确性是一个很好的局部度量，但是它不能代表商业价值。建立一个人工智能管道需要钱，保持它的运行需要更多的钱。一个人工智能团队应该能够有效地展示他们的产品带来的价值。*

*离开人工智能一段时间后，我在科技领域学到的最重要的一课是，伟大的专业人士是由共享的知识组成的。如果没有从任何地方学到一些技巧，没有人能独自到达那里。正是通过给予和被赋予知识，我们才能茁壮成长——这是我写作的主要原因:我每天学到的小东西不应该只属于我或少数人。知识应该共享。*

*同样，我邀请你，读者，也分享你自己的发现，或者在这里作为一个评论，或者成为一个作家。在你的职业生涯中，哪些技巧与你有关？你认为哪些是垃圾，为什么？代替他们做什么？*

*暂时就这些了。如果你对这篇文章有任何问题，欢迎评论或[联系我](https://www.linkedin.com/in/ygorreboucas/)。你也可以订阅我在你的收件箱[这里](https://ygorserpa.medium.com/subscribe)发布的消息。你也可以通过[请我喝杯咖啡](https://www.buymeacoffee.com/ygorreboucas):)来直接支持我*

*如果你是中新，我强烈推荐[订阅](https://ygorserpa.medium.com/membership)。对于数据和 IT 专业人员来说，中型文章是 StackOverflow 的完美组合，对于新手来说更是如此。注册时请考虑使用[我的会员链接。](https://ygorserpa.medium.com/membership)*

*感谢阅读:)*