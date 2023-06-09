# 随着大数据的出现，了解正确背景变得越来越重要

> 原文：<https://towardsdatascience.com/with-big-data-comes-the-importance-of-knowing-the-right-context-af5b3ec6f981?source=collection_archive---------32----------------------->

## 在开发算法之前，理解 3 个关键问题中的业务目标

![](img/6f76bf38a233882ef5db0585b54a7c39.png)

布雷特·乔丹在 [Unsplash](https://unsplash.com) 上的照片

上下文，语境，语境。在数据科学领域，背景就是一切。我认为数据科学家犯的最大错误是不理解他们的工作背景和业务目标。相反，他们非常注重了解人工智能/人工智能技术。复杂算法用在正确的地方是很棒的。理解那个地方应该在何时何地是困难的。

从理解你的商业目标开始。从我的目标开始，这是我在过去两个月里更加关注的事情。当我在解决一个问题时，我不想马上找到解决方案。相反，我需要与 [SME 的](/stop-wasting-your-time-and-consult-a-subject-matter-expert-f6ee9bffd0fe)合作，了解情况的背景以及他们如何看待数据。自从开始做顾问以来，我理解商业目标的策略已经改变了。我们来看一些问题，以及回答这些问题时需要考虑的事项。

为了做好准备，让我们挑选一个精简版的 [Kaggle](https://www.kaggle.com/c/competitive-data-science-predict-future-sales/data) 竞争问题，并假设这是我们给定的业务目标:

> 预测每个商店销售的产品总量。

## **这个目标要求什么？**

着眼于你的目标，确保你理解企业提出的问题。在本例中，数据是由俄罗斯最大的软件公司之一 1C 公司提供的。了解您的目标的一个方法是与您的主要利益相关者进行演示，并浏览目标和期望的结果。讨论你所知道的，以及你需要澄清或弥补的地方。

乍一看，这个目标似乎很简单——你需要预测每家商店销售的产品总量——但是深入挖掘会发现更多的问题。

## **回答这个问题需要哪些数据？**

经过初步的数据分析，您可以了解您的数据集中有什么和没有什么。有了这些信息，您应该与您的利益相关者讨论如何利用他们当前的数据。同样，你可以讨论什么不是。如果你的目标因为缺少数据而无法实现，这就是你需要让大家知道的时候了。

对于我们的例子，让我们看看数据本身。即使为您提供了每日历史销售数据，这些数据也可能逐月发生变化。商店和产品的列表会发生变化，这意味着创建一个能够处理给定数据的模型会更具挑战性。同样重要的是要注意，我们在这些数据中有唯一的标识符。我们有`shop_id`、`item_id`和`item_category_id`，给你一个独特的商店、产品和物品类别。

这里要注意的另一件事是文本列。给定的目标不会询问这些字段。因此，此分析不需要它们。重要信息包括售出产品的数量、每件商品的当前价格和日期。所有这些都可以在数据集中找到。到目前为止，看起来我们理解了主要目标，并且有可用的数据来实现它，但是最终用户会用这些信息做什么呢？

## 用户希望用这些数据做什么或实现什么？您的数据能做到这一点吗？

您的用户可能是业务分析师、SME 或其他人。当您为您的目标开发方法时，您需要确定他们将如何利用输出。坐下来与用户交流。分析完成后，他们想用这些数据达到什么目的？当我进行这些对话时，我发现有时候最初的目标并没有涵盖真正想要的东西。这意味着我可能必须返回并确定是否需要任何额外的数据来获得期望的输出。

我们知道我们的示例目标是预测每家商店销售的产品总量，但是如何使用它呢？假设我们正在与利益相关方进行对话，可能会出现以下情况:

*   了解特定商店将订购多少商品有助于确定下个月需要准备多少商品才能发货。我们可以根据已提供的信息来确定该输出。
*   知道有多少不同的项目被购买显示哪些项目是高利润与低利润。了解了这一点，企业就可以决定停止销售什么。如果你同意这种说法，你可能需要更多的数据来了解每个项目的利润率。
*   希望创建一个仪表板，根据一周中的某一天来查看销售项目的趋势。特定商品是否比其他商品更有可能在不同的日子卖出？如果你更深入地挖掘你最初的目标，你可能会发现不同的目标从中浮现出来。如果是这种情况，你需要重新组织你的工作，并确保你有数据。在这个数据集中，我们的数据是按天给出的，因此这种类型的分析可以根据一周中的某一天来分析商品的销售趋势。

我们可以继续，但我想你明白了。当你开始分析你的业务目标时，你可能会发现最初的目标发生了变化或增长。这是完全正常的。我发现如果你允许的话，这些对话可以持续很长时间。我喜欢把这种讨论的开始时间限制在最多一个小时。有了在那次会议中学到的信息，我就可以去修改我的方法，并根据更新寻求反馈。通过这项工作，您和利益相关者都将更好地理解您的数据、您修改的方法以及什么是可能的。

## 概括起来

业务目标在开始时可能看起来非常简单，直到它们不再简单。这就是为什么在我开始写代码和构建模型之前，我开始问自己三个问题。这些问题有助于确定问题的框架，了解是否有解决问题的数据，并计算出结果。通常，你会发现用户想要的结果并不总是他们最初所说的那样。相反，当你开始深入讨论他们在寻找什么以及数据能告诉他们什么时，他们的愿景会发生变化。这些问题是:

1.  这个目标要求什么？
2.  回答这个问题需要哪些数据？
3.  最终用户希望用这些数据做什么或实现什么？您的数据能做到这一点吗？

在接近业务目标时，你还有其他想问的问题吗？如果是，它们是什么？它们如何帮助您构建解决方案？

如果你想阅读更多，看看我下面的其他文章吧！

</a-quick-and-easy-morning-routine-to-jumpstart-a-productive-week-6f35dc28f739>  </top-3-reasons-public-speaking-can-help-you-in-data-science-18cdbf4bb2f2>  </top-3-lessons-learned-from-leaving-a-job-i-loved-6c71a76cae7> 