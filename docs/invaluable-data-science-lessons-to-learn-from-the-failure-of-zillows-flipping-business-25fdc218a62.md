# 从 Zillow 翻转业务的失败中吸取宝贵的数据科学经验

> 原文：<https://towardsdatascience.com/invaluable-data-science-lessons-to-learn-from-the-failure-of-zillows-flipping-business-25fdc218a62?source=collection_archive---------3----------------------->

## 哪里出了问题？

![](img/675860299c7ceb59a8be145cf3b92fb8.png)

丹尼尔·陶西斯在 [Unsplash](https://unsplash.com/s/photos/burning--house?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

# 介绍

Zillow 是一家成立于 2006 年的在线房地产公司。它在 2019 年创造了 27 亿美元的收入。很长一段时间以来，他们在很多方面都做得更好。这篇文章不是关于进展顺利的事情。我们会关注最近的错误。这导致该公司停止其翻转业务，并削减了 25%的员工。

一、什么是房地产的翻转业务？当某人购买一处房产，并打算在将来转售获利时。该公司通常以相对较低的价格购买房产。花钱进行翻新和其他改进。然后以更高的价格出售房产。这是一种用来赚快钱的流行技术。

如你所知，这里最重要的因素是准确预测房地产价格。这样房产就能以较低的价格买进，卖出获利。

根据[的文章](https://www.zdnet.com/article/zillow-machine-learning-and-data-in-real-estate/)，2006 年 Zillow 的数据库中有大约 4300 万套房屋，他们能够以 14%的中位绝对百分比误差预测房产价格。到 2017 年，他们的数据库中约有 1.1 亿套住房。误差率已经降低到 5%。用于预测房价的模型，拥有数千个复杂的统计模型和海量数据。

# 哪里出了问题？

由于许多原因，他们模型的精度开始下降。这导致人们以远高于售价的价格购买房产。根据这里的[消息](https://www.npr.org/2021/11/03/1051941654/zillow-will-stop-buying-and-renovating-homes-and-cut-25-of-its-workforce)，Zillow 在 2021 年第三季度因其翻转业务亏损超过 3 亿美元。根据这篇《彭博》文章，Zillow 现在期待出售大约 7000 套房屋，价值 28 亿美元。

下面是一些显示损失有多大的推文，

[这是另一篇文章](https://vip.graphics/zillow-opendoor-housing-bubble-2021/?ref=twitter)，其中有许多 Zillow 试图以低于购买价格的价格出售房产的例子。

基于这些数据，很明显失败的主要原因是无法准确预测价格。数据科学家可以从这次失败中吸取很多教训。我将根据公共领域中可用的内容来阐述可能的原因。

# 1.数据质量

机器学习模型表现良好的首要因素是高质量的数据。当机器学习算法的输入是垃圾时，你不能指望它有多好。

<https://www.investopedia.com/articles/personal-finance/111115/zillow-estimates-not-accurate-you-think.asp>  

根据上面的文章，肯定存在数据质量问题的可能性。Zillow 一直依赖于用户共享的数据和公开的数据集。如果说 Zillow 的数据质量是垃圾，那就太苛刻了。尤其是因为他们的模型在很多情况下都做得很好。但是这里误差的影响是巨大的。让我用一个例子来解释一下，

Zillow 正在考虑购买一处名为“ABC”的房产，然后计划投资一些资金进行改造，并在几周内出售以获取利润。假设 Zillow 的 Zestimate 对房产“ABC”的估价为 50 万美元。如果模型有 10%的误差，这意味着实际价格应该是 45 万美元。现在，Zillow 以 5 万美元的溢价买下了这处房产。Zillow 将很难在这块地产上获利。

如上例所述，对于每一个百分比，模型都偏离准确预测。附在预测上的价值正在偏离一个很大的值。价值百万美元的房产 10%的误差就是 10 万美元。仅仅几个这样的财产就可能造成超过一百万的损失。此外，预测郊区房地产价格的错误会影响附近其他房地产的价格，并在总体上影响该地区本身的房地产价值。

数据中的一个简单错误，如房产中房间的数量、离最近学校的距离，以及其他与关键属性有关的问题，都很容易导致预测错误。这很容易产生滚雪球效应。

**第三课**:在任何数据科学问题中，都应该关注数据的质量。有适当的指标来衡量数据的质量是很好的。在像 Zillow 这样的场景中，小错误可能导致大错误，应该有一种方法至少部分地验证数据质量。这有助于在质量问题造成巨大影响之前发现它。

# 2.算法依赖性

算法不错。他们很有见地。这对决策有很大帮助。他们容易出错和出问题，这也是事实。不建议完全依赖算法。尤其是当你在解决一个有很多不确定性的问题时。

房价取决于很多因素。有太多的外部因素会对房价产生影响。不可能监控这些外部因素并将其纳入模型。因为每一个改变在投入使用之前都需要经过测试。

当用例没有巨大的货币影响时。预测出现一些误差是可以的。例如，假设我们想要预测客户的终身价值。客户终身价值 10%的误差不会严重影响财务状况。但与房价类似，也有小误差不可接受的情况。

第七课:在我们无法承受预测偏差的情况下。模型输出应该作为一种补充，帮助业务用户做出决策。例如，在为保险公司承保的情况下。承销过程有巨大的财务影响。模型输出应该补充信息，但不应该做出决策。这个决定还是应该由承销商来做。因为承保人是领域专家，他可以发现算法可能遗漏的东西。

下次当你在解决数据科学问题时。总是询问关于重要性和影响的问题。如果风险很高，那么应该有一个专家小组来监督模型输出并做出决定。

# 3.玩弄系统

当涉及到金钱时，用户总是有可能试图欺骗系统。

<https://www.theguardian.com/business/2021/nov/04/zillow-homes-buying-selling-flip-flop>  

上述文章清楚地阐述了系统被利用的可能性。很明显，郊区的房价很少能带动郊区的房价上涨或下跌。明白这一点的人可以人为地提高郊区房价。

想知道怎么做吗？假设有一个代理人，在郊区持有多套房产。起初，代理人会以人为抬高的价格向一个已知的内部联系人出售部分房产。一旦影响波及到郊区的其他房产。他们以更高的利润出售其他财产。

**教训**:确保系统不被利用的唯一方法是建立一个防欺诈团队。反欺诈团队将会获得所有以高于或低于市场价格出售的资产。以确保这些影响不会传递到模型上。

# 4.选择性聚焦

很明显，在 Zillow 的案例中，人们对房产及其价格预测有着太多的关注。对买家的关注还不够。最终是投资房产的人。没有很好地了解买家可能会有问题。

对于房地产公司来说，了解买家行为非常重要。不了解买家，就无法准确衡量需求。因此价格本身无法准确预测。

**第一课**:任何数据科学问题都要从所有可能的角度去分析。应该以整体的方式研究它们。此外，如果你在模型投入使用前就学习是不够的。即使在模型投入使用后，也应继续进行整体数据分析。情况可能会有变化。

为了简单地解释这一点，假设我们想要预测正在搅动的客户。有一个内部焦点来理解客户为什么会有各种各样的原因是一回事。这将告诉你很多关于导致客户流失的问题的信息。但是，可能有其他因素，如竞争提供更好的折扣。因此，如果不从不同的角度处理这个问题，就不可能做出有把握的决定。在这个例子中，如果只关注客户和提供的服务是不够的。它还需要对互动、社交媒体上的情绪、竞争策略等进行分析。

# 5.外部因素

外部因素在任何问题中都起着巨大的作用。在房价预测的情况下，也有很多外部因素会影响房地产的价格。

例如，假设 Zillow 计划以 500，000 美元的价格购买一处房产“ABC ”,计划投资 50，000 美元进行装修，并计划以 600，000 美元的价格出售该房产。

为了简单起见，让我们假设 500，000 美元的购买价格是准确的，并且反映了当前的市场价格。现在，翻新的计划预算为 50，000 美元，但由于外部因素，劳动力需求增加，因此翻新成本也增加了 25，000 美元。最重要的是，由于像 Covid 这样前所未有的事件，对房子的需求减少了。这导致了房产价格的下降。因此迫使 Zillow 亏本出售房产。此外，长期持有该物业并不理想，因为这将吸引额外的维护成本。

Zillow 拥有的许多房产现在正在亏本出售。有许多外部因素在起着巨大的作用。不可能总是识别所有的外部因素。但是应该努力将这些事件纳入模型中。此外，应该努力分散风险。

在 Zillow 的案例中，很明显，根据这里的[文章](https://www.bloomberg.com/news/articles/2021-11-01/zillow-selling-7-000-homes-for-2-8-billion-after-flipping-halt)，他们在投资组合中增加了太多的房产，而不是正在出售的房产。增加如此多的房产增加了对装修所需劳动力的需求。对劳动力需求的增加增加了劳动力成本。从而使局势进一步恶化。

# 最后一个音符

有如此多的数据科学应用为企业增加了巨大的价值。他们中的一些人帮助企业赚钱。其中一些有助于解决问题。其中一些有助于改善体验。但确实也有一些人失败了。其中一些失败并没有造成很大的损失，而另一些却造成了巨大的损失，比如 Zillow。

心智模型对于正确分析商业问题非常有帮助。它也有助于构建思维过程，从而得出最佳解决方案。这是一篇关于使用思维的基本原则来解决数据科学问题的文章

</how-to-use-first-principle-thinking-to-solve-data-science-problems-db94bc5af21> [## 如何用第一性原理思维解决数据科学问题？

towardsdatascience.com](/how-to-use-first-principle-thinking-to-solve-data-science-problems-db94bc5af21) 

# 其他参考文献

<https://www.theguardian.com/business/2021/nov/04/zillow-homes-buying-selling-flip-flop>  

# 保持联系

*   如果你喜欢这篇文章，并对类似的文章感兴趣，[在 Medium](https://rsharankumar.medium.com/) 上关注我。成为[的中级会员](https://rsharankumar.medium.com/membership)，访问数千篇与职业、金钱等相关的文章。
*   我在我的 YouTube 频道上教授和谈论各种数据科学主题。在这里订阅我的频道。
*   在此注册[我的电子邮件列表，获取更多数据科学技巧，并与我的工作保持联系](https://chipper-leader-6081.ck.page/50934fd077)