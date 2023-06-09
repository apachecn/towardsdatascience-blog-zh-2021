# 如何用第一性原理思维解决数据科学问题？

> 原文：<https://towardsdatascience.com/how-to-use-first-principle-thinking-to-solve-data-science-problems-db94bc5af21?source=collection_archive---------11----------------------->

## 埃隆·马斯克解决问题的方式

![](img/253f1923b8e43bf3b1e36007a3872456.png)

莫尔·蒂亚姆在 [Unsplash](https://unsplash.com/s/photos/structured-problem-solving?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

大约 2000 年前，亚里斯多德将*【第一原理】*定义为*【认识事物的第一基础】*。这个概念仍然非常相关，可以帮助您为复杂的数据科学问题提出创新的解决方案。第一原理思维背后的思想是将一个复杂的问题分解成它的基本部分，然后使用自下而上的方法来构建一个以前没有概念化的独特解决方案。

在本文中，我将向您解释如何应用第一原理思维来解决数据科学问题。为了简单明了，让我们考虑一下*“客户流失问题”*。为了帮助你理解第一原理思维的好处，我将首先展示如何使用传统方法解决这个问题，然后使用第一原理思维方法。

> **问题陈述:零售能源领域的客户流失**
> 
> **让我们假设“XYZ”是一家试图解决客户流失问题的零售能源公司。每年大约有 10%的客户流失,“XYZ”公司正在寻找减少客户流失的方法。**

# 传统方法

解决问题的传统方法或最常用的方法是主观思维。也就是说，我们大多受已有假设或观点的影响。这种方法涉及的一般步骤是，

1.  从现有的假设开始
2.  根据假设确定需要逐步改进的领域
3.  探索选项并选择最佳解决方案

现在，让我们考虑一下能源零售行业的客户流失情况，看看如何使用传统方法解决这个问题。如前所述，传统方法的第一步是从假设开始，

**假设:**

*   与客户代理的糟糕经历会导致客户流失
*   可以通过折扣/优惠来防止流失

基于上述假设，我们现在提出了可以帮助我们解决问题的解决方案。

*   向不满意的客户提供折扣—我们可以通过检查投诉登记簿来识别不满意的客户
*   专注于获得更多客户
*   确定导致最多投诉的投诉类别，并使用表现最佳的代理来处理这些问题——这有助于避免给客户带来不好的体验
*   确定高能耗消费者，并主动向他们提供折扣

以上是一些基于假设的解决方案。这里的优点是，

*   这里确定的解决方案易于实现，不需要太多的努力。
*   增量改进可以很快实现

但另一方面，缺点是，

*   客户流失的主要原因没有得到解决
*   无法作为长期战略持续下去

# 第一原理思维方法

现在，我将向您展示如何通过使用第一原理方法来解决客户流失问题。这种方法背后的主要思想是花尽可能多的时间去理解问题，然后试图解决它。就像爱因斯坦说的，

> “如果我有一个小时来解决一个问题，我会花 55 分钟思考问题，花 5 分钟思考解决方案。”——阿尔伯特·爱因斯坦

## 理解问题

更好地理解问题的一个最好方法是尽可能多地提问。不要认为任何假设都是理所当然的。一直问问题，直到没有进一步的问题！

有助于更好地理解问题的一些问题是，

*   每月有多少客户流失？
*   客户流失的行业平均水平是多少？
*   你的客户是什么样的？
*   搅动的客户是什么样的？
*   不同配置文件给客户带来的收入/利润是多少？
*   客户流失的原因都是什么？
*   客户什么时候会流失？有什么趋势吗？

所有这些问题有助于更好地理解问题，量化问题，也有助于确定当前的重点领域。如果你试图解决一个不同的问题，试着用下面的问题来理解它，

*   有什么问题？
*   问题有多大？(可以用美元或受影响的客户来量化)
*   为什么会发生？
*   谁面临这个问题？
*   它什么时候发生？

## 将它分解

一旦对问题有了很好的理解，下一步就是开始分解问题。对于客户流失这个问题，我们先根据客户流失的原因来分解一下。这有助于区分可解段和不可解段。假设客户流失可以分为以下几类:

1.  客户离开了我们不提供能源零售商服务的国家/州？
2.  因业务关闭而流失
3.  前 3 个月内的流失
4.  成为常客超过 3 个月，然后流失的客户

以上原因，很少是可解的，其他都是不可解的。第 1 类和第 2 类是无法解决的，因为在第一类中，客户正在转移到能源零售商不提供服务的地方，而在第二类中，客户由于他们的业务关闭而搅动，从能源零售商的角度来看，没有什么可以做的。

第三类是客户在 3 个月内流失，这是一个问题，但这应被视为入职问题，而不是流失问题。由于这些客户没有花足够的时间来正式成为客户，他们几乎没有花任何时间。

所以，现在我们只剩下第四类了。这一类别的客户可以进一步划分成组，

*   根据客户的终身价值、在平台上的年龄等将客户进一步细分。

这种细分实际上有助于识别需要立即关注的细分市场和可以忽略的细分市场。继续细分类别，直到单个组/类别变得更小

## 数据怎么说？

根据上述细分，确定需要立即关注的细分市场/类别。对于所有这些客户，探索他们跨不同业务部门的数据。就像在我们的客户流失问题中，需要做的分析是，

*   客户的能源使用模式是怎样的？
*   这些顾客抱怨过吗？解决这些投诉需要多长时间？谁处理这些投诉？
*   最近 2 个月内是否与客户有过互动？
*   是否有客户的能源账单出现峰值？
*   这些客户中有谁收到过营销信息吗？

## 使用自下而上的方法求解

根据上述数据分析，找出导致客户流失的前 10-15 个场景。深入研究这些已确定的场景，假设我们有这样一个场景，客户就账单问题联系支持中心时，大多数情况下都是不了了之。我们需要确切了解导致这些客户流失的原因。原因可能是，

*   这些类别的合规性需要更长的时间来解决？为什么它们需要更长的时间来解决？
*   修改账单所需的时间要长得多。为什么他们需要更多的时间？

像上面一样，问尽可能多的问题，直到没有进一步的问题。这样，问题就一清二楚了，因此可以主动解决。

# 是什么阻止了许多数据科学家使用第一原理思维？

而我们可以清楚地看到，第一原理思维才是解决问题的方法。但是为什么数据科学家不在他们解决的所有用例中使用它们呢？

原因是时间。是的，“时间”是一项非常重要的资源，数据科学团队通常会处理具有不同重要程度的多项任务，因此可能会有一些问题不值得使用绝对没问题的第一原理思维方法来解决。

但是，当有一个对业务有更大影响的业务问题时，最好使用第一原则思维方法来解决，而不是采用增量增强。

# 结束语

有许多数据科学项目时不时会失败。虽然技术挑战仍然是许多失败的关键因素，但也有失败是由于缺乏对业务问题的理解。没有很好地理解问题的首要原因是因为组织试图关注太多的问题，并且经常面临过快交付结果的压力。在这个视频中，我分享了一些使用第一原理思维解决数据科学问题的技巧

# 保持联系

*   如果你喜欢这篇文章，并对类似的文章感兴趣，[在 Medium 上关注我](https://medium.com/@rsharankumar)
*   我在我的 YouTube 频道上教授和谈论各种数据科学主题。[在这里订阅我的频道](https://www.youtube.com/c/DataSciencewithSharan)。
*   点击[我的电子邮件列表](https://chipper-leader-6081.ck.page/50934fd077)获取更多数据科学技巧，并与我的工作保持联系