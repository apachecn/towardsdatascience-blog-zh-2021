# 让你脱颖而出的数据分析实践

> 原文：<https://towardsdatascience.com/data-analysis-best-practices-d4f5b3d8e222?source=collection_archive---------19----------------------->

![](img/625be9afa8055f130eb05a93bdd36f22.png)

并非所有的云都与数据有关，但导航可能同样困难。(作者供图)

到目前为止，数据分析是业务和技术中最常见的任务之一。它是成千上万的学术研究人员、银行家、工程师和数据科学家的日常面包。有趣的是，尽管这是一项如此受欢迎的活动，但对于什么应该是黄金标准似乎还没有达成一致。没错，比如说，将客户调查分析与强子对撞机的实验结果进行比较，至少是很难的。同样真实的是，在这两种情况下，人们可以看出这个过程进行得好还是不好。

在本文中，我将重点介绍如何进行良好的数据分析过程。作为底线，我们将把自己限制在那些证明使用编程方法是正确的情况下，从而留下“excel 工程”或准备好的仪表板。

我将与你分享一些建议——这些建议在我过去十年在 R&D 的职业生涯中一直对我有效。虽然这篇文章绝不是主张设定黄金标准。我相信你很快会读到的提示会为你节省很多时间。

# 保持冷静，分析数据

数据分析是一项探索性很强的工作。不像在软件开发中，很少有人能给你写一份精确的“待办事项”清单。更多的时候，你面对的是一个已经定义好的问题和一系列需要检查的愿望或假设。找到正确的见解可能需要几个小时，或者几个星期。这取决于许多因素，如数据质量、潜在问题的复杂性、来回沟通的需要以及您的技术技能。这是一个耗费脑力的过程，有许多不确定因素，包括选择合适的问题来提问。

因为分析是一个调查过程，没有一个明确定义的假设就期望成功是幼稚的。除非它是任务描述的一部分，否则制定它是你的工作。正是形成它的过程会让你的注意力集中，让你的时间更有效率。如果你的分析主题是复杂的，你甚至可能想要制定一整套假设。不管你怎么做，都要保持工作的系统性。把假设变成你的征服计划，记住，消极的结果仍然是结果！

# 消灭，消灭，消灭

我提到过这是一个精神消耗的过程吗？我敢打赌，如果你还能理解晚上的运动，你就没有在工作……数字和小数对你大脑的影响绝对是一场灾难。因此，如果仔细检查数据并消除任何潜在的冗余信息，至少可以引入某种程度的保护。我知道找出哪些信息可能是重复的或多余的可能很有挑战性，但是你应该试一试。只要有可能，就在更小的数据集上工作，消除任何你能很快证明是不相关的东西。

我通常的做法是区分我分析的几个阶段。当我处于某个阶段时，我不会让我的大脑从事与其他步骤相关的工作。例如，当我获取数据时，我不会过多地关注它。我甚至没有试图阐述观察！当我清理数据时，我只专注于使我的数据集一致，包括删除不必要的列，处理丢失的值等。总结性的观察时，我依赖于自己早期的作品，放下了更多的“工程的一面”。

所有这些，我更喜欢在单独的笔记本(或脚本)中完成，如果我不得不重新处理一个问题，我会返回到更早的阶段。这个过程反映了最小化数据集和最小化工作范围。俗话说“一次做一件事”。

# 再现性取代了稳健性

软件工程师关注健壮性。他们必须这样做，因为他们交付的代码是要在生产中使用的。一旦部署，它就成为一种数字产品或服务。因此，他们开发了各种方法和工具，如同行评审、单元测试、集成测试、版本控制、linters、CI-pipelines 等。帮助他们开发可靠的软件。

数据分析代码很少在生产中使用。它的可靠性定义与数值结果的再现性更有关系。大多数情况下，这样的代码是一次性的，永远不会被维护。更糟糕的是，即使是在一个单一的任务中，分析代码也可能很快失去控制并自我吞噬。在单元测试上投入时间很难证明是合理的，当讨论洞察力而不是性能问题时，同行评审似乎更有意义(有例外)。在这种情况下，确保再现性是一项挑战。

有时，数据分析任务会作为其他人过去所做工作的延续而开始。当这种情况发生时，至少有两个理由让你变得暴躁:

*   “他/她做这个或展示那个的时候(到底)是什么意思？”
*   “我该如何运行这一部分？

第一个问题与分析的方式有关。一个做得不好的分析会显示不完整的片段或死代码，这是失败尝试的结果。它会用许多没有意义的彩色情节把画面弄得乱七八糟。最后，评论和观察，如果有的话，会陈述明显的事实而不解释推理背后的意图。即使重复所有的步骤，也很可能得出不同的结论。

第二个问题是一个更“工程化”的问题。代码就是代码，要运行它，你应该复制它被创建的环境。分析代码倾向于快速漂移。因此，捕获、冻结和归档所有的依赖关系非常重要——除非您想要启动一个计划外的黑客马拉松。

# 不要让事情变得不必要的困难

系统化的工作、减少精神负担和尊重可再现性还不能定义一个过程，特别是当这个过程在不同的场景下看起来非常不同的时候。然而，将正确的重点放在诸如形成工作假设、分阶段工作和清晰性等事情上有助于创建良好的实践。

下面，我列出了一些你可以改进的建议——我希望我能早点知道的事情:

*   指出什么是草稿，什么是干净的报告。这与使用 git 不同，因为通常情况下，您可能希望保留草稿。记住数据分析的本质是记录你的推理。因此，试着从多余的信息中剥离出来，或者至少给你的同事一个提示，哪些部分不是关键结果。
*   优先考虑代码的清晰性而不是性能。如果您的某些代码需要很长时间才能运行，可以考虑将它转移到一个单独的脚本中。
*   不要害怕使用注释或减价，尤其是当代码没有直接传达这些见解的时候。
*   让笔记本无条件流动。很多时候，人们只会看着它们来学习结果，而不会去执行它们。脚本级别的一些“if-else”语句会很快模糊画面。
*   提交前重新生成笔记本。Git 不知道你的名称空间中的变量。因此，重启笔记本可能有助于避免突然出现的“名字错误”。
*   用图来传达数据，而不是自我。这个世界充满了提供看起来很漂亮的情节的包。更重要的是，你要注意坐标轴和图例上的单位和标签，而不是嵌入吸引人的小部件。如果一个排序的表格显示了你想要的，甚至不要为图表费心。
*   写一个简短的自述文件来讨论内容和如何运行代码总是受欢迎的。
*   在数据上放置断言也没有错。我急切地把它们放在笔记本的开头，尤其是在有更广泛计算的部分之前。
*   使用随机数生成器时使用“种子”。
*   展示你的过程中表格的“头”,最好是在之前和之后。这有助于理解处理过程，而不必执行它。

# 最后的想法

我知道数据分析并不适合所有人。这是一种精神消耗…哦，等等…我提到过。这需要耐心和直觉，而且很难达成一个标准化的流程。然而，正如我所展示的，你可以采取一些行动让它不那么痛苦，更有成就感。

我相信，你可以想出更多的方法来加强这项活动。无论如何，我在这里给出的列表是可扩展的。请不要害羞，在评论中分享你的想法吧！