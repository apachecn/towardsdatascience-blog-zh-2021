# AMO 理论:为数据科学家解决黑箱问题

> 原文：<https://towardsdatascience.com/the-amo-theory-solving-the-black-box-problem-for-data-scientists-91b2d1ac9195?source=collection_archive---------15----------------------->

![](img/1bf249accb98dadec0f9edd5a5a52ff0.png)

在 [Unsplash](https://unsplash.com/s/photos/lecture?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上 [Wonderlane](https://unsplash.com/@wonderlane?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 拍摄的照片

## 当你必须解释人们如何以及为什么以某种方式行动时

在数据科学中，我们经常想要测试输入或刺激，看看这是否会对结果产生影响。但是黑箱问题介于两者之间，用来解释为什么输入会对结果产生影响。AMO 理论是解决这个问题的好方法，因为 AMO 因素被认为是解释预测结果的机制的模型。AMO 理论可以应用于许多不同的领域，如人力资源管理、市场营销、执法等。在这篇博客中，我将简要解释这个理论是关于什么的，以及它如何应用于数据科学项目。

# 1.什么是 AMO 理论

AMO 代表能力、动力和机会。我在攻读人力资源管理博士学位时了解到了这个理论。该理论是通过结合工业心理学家和社会心理学家所做的广泛研究来理解员工绩效的相关因素而发展起来的。

简而言之，AMO 认为绩效是能力(训练和选择)、动机(激励和反馈)和机会(环境)的函数。这三个因素影响员工绩效。人力资源管理研究人员通常认为 AMO 理论可以解释人力资源管理实践和员工绩效之间的联系，认为人力资源管理实践应该支持和提高员工的能力、动机和表现机会，以增加对人力资源管理项目的投资回报。

# 2.数据中的黑箱问题是什么

假设给你一个数据集，看看你能否建立一个模型来预测结果，一个典型的回归模型。通常我们会进行一系列静脉注射，看看它们是否能预测结果。假设您调整了模型，将精确度提高到可接受的水平。在向高管展示结果时，有人会问，你怎么知道这行得通，或者你怎么知道这些因素会直接影响/预测结果。此时，你可能会有麻烦。你很难解释 IVs 如何影响 DV，以及它们为什么会起作用，因为在处理数据科学中的黑箱问题时，我们经常不知道如何解释这样的事情。对于数据科学家来说，这是一个黑箱问题，因为它不容易直接测量，只能通过可观察的行为(如销售或考试分数)来推断。

# 3.AMO 理论如何解决这个问题

显然，数据科学项目有很多种类型。但是对于这个理论，让我们把注意力集中在建立一个预测人类行为的模型上。

这里有三个例子来说明如何将 AMO 理论用于你的建模。

示例 1:人力资源管理和人力资源分析

如上所述，AMO 理论被公认为是人力资源管理领域黑箱问题的答案。如果您正在研究一组输入(例如，人力资源实践、在培训、重组等方面的投资)。)为了预测性能改进收益，AMO 理论可以指导您解释这些输入如何影响性能。输入或刺激是否针对员工的能力、动机或表现机会？对于动机，你是想创造一个内在的还是外在的动机？用短期合同工取代全职员工有什么影响？

示例 2:营销和销售

如果你试图理解有人是如何以及为什么购买你的产品，AMO 理论也可以帮你一把。你的模型能识别潜在买家的购买能力吗？提议的营销活动是否激发了合适人群的购买动机？你是否考虑过合适的顾客在合适的地点做出购买决定？了解这些 amo 将有助于您设计数据科学产品和服务，从而最大化您的营销投资的影响。

例 3:某人犯罪的可能性。

我个人最近在一个类似的领域使用了这种方法。如果给你一个项目来预测某人犯罪的可能性，AMO 理论可以指导你解释这些输入将如何影响那个人执行其犯罪意图的可能性。你的模型能识别潜在罪犯的犯罪能力吗？就动机而言，他们的动机是经济利益还是报复？他们是否生活在一个很容易逃脱他们想要的东西的环境中(例如，计划好的逃跑路线)？根据这些组成部分对你的 IVs 进行分类帮助我提高了准确性和可解释性。

同样，这些都是有趣的数据科学问题，我曾多次回到 AMO 理论，作为一种指导和方法来解释人们为什么以及如何以某种方式行为的结果。当谈到大数据分析或机器学习模型时，请记住，你不只是试图预测你的客户正在发生什么；您希望能够向非数据人员解释您的模型。这就是这个理论可以帮助理解所有那些方框和箭头的地方。如果你觉得这篇文章有帮助，请在下面留下评论。