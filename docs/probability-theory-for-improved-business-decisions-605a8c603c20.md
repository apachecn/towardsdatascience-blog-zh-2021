# 改进商业决策的概率论

> 原文：<https://towardsdatascience.com/probability-theory-for-improved-business-decisions-605a8c603c20?source=collection_archive---------7----------------------->

![](img/791a96d9de7e3bbc0a6e20c7c107a790.png)

安迪·汉德森在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

## 商业中概率的概念和应用

让我们从简单的开始。你已经调查了 50 位顾客，了解他们对你的产品/服务是否满意。其中，35%的人说他们很快乐。

仅仅基于这些信息，你能预测一个随机的顾客的态度吗？你可以用概率做出这样的预测:

*35/50 = 0.7*

这意味着，有 70%的机会，一个样本外的客户会有一个积极的看法的产品。用最简单的术语来说，那就是*概率*——某事发生的可能性。

上面的例子只有一个结果——客户的*积极*态度。然而，一些客户可能会表现出其他偏好，如*消极*或*中立*态度。对于诸如此类的多重结果，计算概率略有不同。下面结合实例探讨两种方法。

# **加法规则**

在 50 名客户中，35 名持正面观点，10 名持负面观点，5 名持中立观点。现在，您需要预测客户对产品持*正面*或*中立*观点的概率。

解决方案听起来很简单——增加两个概率。

*P(正)= 35/50*

*P(中性)= 5/50*

因此，客户持正面或中性观点的概率为 35/50 + 5/50 = 80%。

加法规则的一般公式如下:

**P(A 或 B) = P(A) + P(B) — P(A 和 B)**

通过使用集合论中的形式符号:

**p(a⋃b)= p(a)+p(b)—p(a⋂b)**

# 乘法法则

加法规则适用于两个互斥的事件。在上面的例子中，顾客不能同时持有正面的*和负面的*观点，因为它们是互斥的。

然而，存在两个事件*不*互斥的情况，因此，两种结果都有可能同时发生。比方说，一个学生要参加两个科目的考试——物理和文学。学生通过每次考试的概率是:

*P(物理)= 0.4
P(文学)= 0.3*

基于这些信息，你能预测学生通过物理*和*文学考试的概率吗？

从数据来看，这个学生似乎很难通过任何一门考试。所以通过*两个*考试的概率肯定极低。这就是*乘法规则*在计算联合概率时派上用场的地方:

***P(物理与文学)= P(物理)* P(文学)***

答案当然是 0.4*0.3 = 12%。

将此类问题推广到两个不互斥的事件 **A** 和 **B** :

**P(A⋂B) = P(A)。P(B)**

# 条件概率

条件概率是在满足另一个条件的情况下，某事发生的可能性/机会。

作为例子，让我们考虑两个相关的事件。

如果一家新的创业公司熬过了第五年，它最终成为十亿美元公司的概率有多大？

因此，对于一家有朝一日成为十亿美元公司的初创公司来说，它必须熬过 5 年。在所有创建的创业公司中，如果 20%存活下来，存活下来的公司中有 5%成为十亿美元公司，那么新公司最终成为十亿美元公司的概率是:0.2* 0.05 = 1%。

条件概率的一种形式表示是: **P(B|A) = P(A 和 B)/P(A)**

# 概率的商业应用

概率的关键作用是在面对不确定性时改善决策。它有助于决策的客观和数据驱动，而不是基于本能。

比方说，海滨商店的冰淇淋销售取决于两个因素——好天气和大量的游客。

因此，一周后，如果好天气的概率为 90%，预期游客率为 30%，那么预期销售额的概率为:

*P(天气)* P(预期访客)= 0.90 * 0.30 = 27%。*

这个数字本身就可以帮助老板决定当天安排多少员工。

商业应用的几个其他例子:

*   根据风险调整后的投资回报(ROI)选择投资选项，尤其是在投资选项为:a)高风险高回报，b)高风险低回报，或 c)低风险低回报的情况下。
*   财产保险公司使用概率来计算一部分客户的保险索赔几率，并决定收取的保费。同样，人寿保险公司使用概率来估计客户的预期寿命，以设定保费。

# 一锤定音

企业——无论大小——经常根据直觉、本能和经验主观地做出重要决定。但是，随着数据量、工具和技术的增加，许多组织在面临不确定性的情况下正在转向数据驱动的决策。这篇短文介绍了概率的一些基本概念及其应用。关于概率的相关文章，请查看文章:[概率分布:数据科学家的直觉](/probability-distribution-an-intuition-for-data-scientists-72d68a8feb4)。

如果你有评论和想法，请随意写下来，或者通过[媒体](https://mab-datasc.medium.com/)、[推特](https://twitter.com/DataEnthus)或 [LinkedIn](https://www.linkedin.com/in/mab-alam/) 与我联系。