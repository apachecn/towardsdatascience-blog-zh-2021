# 以人为中心的数据科学

> 原文：<https://towardsdatascience.com/human-centered-data-science-3d92066bf779?source=collection_archive---------33----------------------->

## 当成功的数据科学意味着与人类互动

![](img/bc074065afcc79d396190f6852e048dd.png)

奥马尔·弗洛雷斯在 [Unsplash](/s/photos/human-centered-design?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

数据科学、高级分析、机器学习、人工智能、认知计算和自然语言处理都是当今商业世界的热门词汇，因为如此多的用例已经证明了利用这些工具可以带来显著的竞争优势。

尽管这些工具的功能已得到证实，但许多人仍然难以成功实施，这不是因为这些工具正在失去其功能，而是因为许多数据科学团队、供应商和个人未能在人类决策的背景下正确集成数据科学工具。因此，伟大的数据科学产品建立起来了，但它们真正的影响却因负责使用它们的人的不理性、有偏见和难以预测而消失了。

这个问题并不新鲜，我们在这篇文章中探讨的是这样一个想法，即我们也许能够从过去学到一两件事，以便为成功的数据科学制定新的路线图。在这里，我们来看看连接产品和人的不同模型。

在数据科学和人类心理学的交叉点上，有一个多学科领域已经成熟。

# 日常数据科学的设计是什么？

1988 年，唐纳德·诺曼出版了《T4:日常事物的心理学》一书，这本书后来变成了另一本名为《日常事物的设计》的书。这些书中包含的想法简单、有力、具有颠覆性，因为在此之前，没有人正式确定如何将工程学与人类心理学相结合。这些书启发了用户设计领域或 UX，更正式地称为以人为中心的设计(HCD)。

一晃 30 年过去了，在人们开始真正将对人类的研究融入设计工程之前，数据科学在许多业务中可能会像设计一样失败。但数据科学的问题超出了日常事物的设计，因为数据科学的产品通常不是事物。相反，它们是洞察力、自动化和人类技能和能力的模型。因此，我们不仅要借鉴 HCD 的想法来改善数据科学产品的用户体验，还必须利用其他学科来全面掌握成功实施数据科学的路线图

# 日常数据科学的设计应该是怎样的？

因为数据科学的产品越来越多地与事物结合，无论是冰箱、烤面包机、汽车还是应用程序，日常数据科学的设计确实会受益于 HCD 的一些原则，这些原则是诺曼博士最初想法的基石。

在我们开始之前，有必要定义几个关键概念(来自 Bruce Tognazzini 对 HCD 的大量研究):

*   **可发现性**:“确保用户能够发现并理解系统能做什么。”
*   **启示**:“一个对象的属性和代理的能力之间的关系，决定了该对象可能如何被使用。”
*   **意符**:“启示决定了什么行为是可能的。意符传达了行动应该在哪里发生。”
*   **映射**:“控件布局和受控设备之间的空间对应关系。”
*   **反馈**:即时反应，适量反应。

为此，作为数据科学家，我们必须确保产品的可发现性。我们在这里经常失败，因为我们相信从统计模型或高级分析中获得的洞察力本身就是发现，因此已经可以被发现。然而，这种假设是不正确的，因为洞察力只有在适用于企业或用户时才有价值。因此，我们必须阐明交付更容易被发现的数据科学产品意味着什么。这包括可发现性的所有要素，包括识别启示、能指、映射和反馈机会。

数据科学产品是在与人类互动的环境中交付的，因此只有当它允许用户发现它的启示如何改善他们的体验时，它才是好的。启示不是产品的属性，而是用户和产品之间的关系(Norman，1988)。如果数据科学分类模型取代了人们点击成千上万的文档来查找信息的需要，那么它的启示就是时间、改进的质量和增强的性能。这些应该可以通过文档和符号清楚地发现。

能指向用户发出创建启示的可能使用点的信号。在数据科学中，这可能意味着交付带有模型的关键驱动因素，以便用户清楚为什么在上面的例子中，不同的文档被模型分类、标记或标注。这样做有助于发现启示，如提高质量和增强性能。

诺曼博士提到了不同的设计元素如何映射到它们的设计功能。例如，灯光开关通过打开或关闭灯泡来映射到灯泡。在数据科学中，我们经常将模型的功能映射到它们的概率或决策，如 1 和 0，但对于用户来说，这通常并不直观，因此这种映射通常并不那么有用。因此，我们可以调整我们的映射，以包含表示我们的数据科学产品的更直观应用的限定符。例如，概率成为“高风险”、“中等风险”和“低风险”值标签的桶，这些标签提高了用户将我们的模型的输出映射到它们的功能的能力。

在许多方面，直到我们有机会从用户那里获得反馈，最佳映射才会变得明显。对于商业用户来说，反馈可以是明确的，并遵循好的设计原则(简单、容易、不唐突)。在极少数情况下，我们的用户实际上是我们洞察力(一种预测某人获得工作或在关系中获得成功的可能性的模型)的客户，那么反馈也必须是直观的和响应性的(另见下文，我们通过语音扩展了响应性反馈设计)。

![](img/2b97678e485987ecde1ef50f0c4f1a0d.png)

由 [Breakslow](https://unsplash.com/@breakslow?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 在 [Unsplash](/s/photos/application?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄

# 更多心理学！！！

但是仅仅借用 HCD 的概念来提高数据科学产品的成功是不够的。因为这些产品被部署来与人互动，包括客户和企业用户，我们的成功管道必须对政治和社会心理关系敏感，这些关系定义了这些个人如何相互互动以及如何与我们的产品互动。

例如，为商业用户提供自动化甚至增强功能的机器可能会感到威胁。威胁的形式可以是对工作安全的威胁，也可以是对个人效能感和专业知识的威胁。因此，我们的数据科学渠道必须对这一结果保持敏感，直接应对威胁感，以获得认同。社会心理学家很早就认识到，为了增加认同，人们需要感觉到一个新的过程是公平的，为了确保公平，变革过程需要发言权。声音是给予用户参与过程实际如何展开的机会。从数据科学的角度来看，这意味着我们创造机会，不仅仅是像我们从 HCD 那里学到的那样提供反馈，而是展示反馈如何真正为我们的产品带来变化。

例如，向用户解释关键的模型特征，并征求反馈，以不同的方式将这些特征分组为有意义的和可操作的分组。在一个这样的例子中，一个客户想出了通过不同的外展媒体(例如，个人电话、电子邮件微移等)对可能受到影响的功能进行分组的主意。).通过将这种反馈整合到产品中，用户已经在思考如何创造性地开发可以解决这些差异的内容，当他们看到高概率(例如风险评分)以及更好地匹配不同外联模式的关键驱动因素时。用户看到了启示，因为他们现在是使用产品来提高自己影响力的积极参与者。

但声音并不是心理学中可以帮助开发成功的数据科学产品管道的唯一视角。事实上，人们可以结合政治心理学或动机的概念来理解他们产品成功的相关方面。我们把这留给读者，你们的想象力和创造力。欢迎在下面发表评论，继续这一对话，并在追求更有效的数据科学成功模式方面更进一步。

# 端到端成功清单

在开发成功的数据科学管道时，可以考虑一个有用的清单，如下所示:

*   该产品的主要用户群有哪些特征？
*   这些特征如何暗示我的产品的不同的可能的启示？我的产品为那些特定用户启用或阻止了什么(反启示)？
*   什么样的交付或部署方法对实现这些启示最有意义？
*   我如何向我的用户群传达这些启示？
*   从我的用户的角度来看，什么映射最有意义？
*   我是否提供了简单、容易且不唐突的反馈机会？
*   我能证明反馈如何改变了产品吗？

我们关于成功的数据科学产品管道的帖子到此结束。我们感谢您花时间阅读这篇文章，并期待在下面的评论中看到您的后续想法。虽然这篇文章是高层次的，理论性的，请继续关注，因为我们将包括未来的主题，探索数据科学和人类决策编码中更实际的问题。

我还要强调的是，这仅仅是一个试图合并不同领域的应用程序，但还有许多其他方法。关键是要认识到数据科学、数据工程、应用程序开发、用户体验和心理学等不同领域交叉授粉的价值。干杯！

参考

通过 [Fastdatascience.ai](https://www.fastdatascience.ai) 学习数据科学开发、领导力和战略

诺曼博士(2013 年)。*日常用品设计:修订扩充版*。星座。

Tognazzini，B. (2014 年)。交互设计的基本原则(修订和扩展)。 *AskTog* 。