# 数据科学的难点在于

> 原文：<https://towardsdatascience.com/the-hard-part-of-data-science-fa9cad734319?source=collection_archive---------22----------------------->

## 那些闯入这一领域的人往往会遗漏什么

![](img/bab2c5ba7ec221737282490206845dfc.png)

马库斯·斯皮斯克在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

第一次看数据科学实习生候选人简历的时候，我得了冒名顶替综合症。这些应届毕业生拥有我所有的技术技能(在很多情况下，甚至更多)。如果所有这些直接从大学毕业的人都知道我所做的一切，我如何证明我作为“高级”数据科学家的工作是正确的？

我对他们的第一次采访也没有帮助——许多人可以回答所有的技术问题，并且在数学上更容易。许多人有更令人印象深刻的编码经验。那我到底有什么用？

直到我开始与实习生和初级数据科学家密切合作，我才真正意识到，那些简历和技术面试并不能告诉你全貌。

# 缺失的技能

大多数候选人最大的缺失不是技能。它能够在目标和算法之间进行转换。如果你不知道什么时候该用锤子，什么时候该用螺丝刀，那么你的工具箱里有多少工具都没用。

商业问题很复杂。它们很少被定义得如此之好，以至于与一个技术解决方案是同构的。相反，你需要足够好地理解一个业务问题(和技术工具),以知道哪些部分可以被抽象掉或者近似。

# 一个例证

一个例子将使这一点更加具体。当我在医疗保健行业工作时，预测分析的圣杯是预测哪些病人会住院。如果我们能够识别这些患者，我们就有可能避免住院，这将是一个巨大的胜利(对患者和公司的底线而言)。听起来像是一个简单的分类问题，对吗？

![](img/697a64f5beb7d1488728c8e124123db3.png)

比尔·牛津在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

但事实并非如此。这里有一堆隐藏的问题。给出一个简短的、非详尽的清单:

*   我们想在住院前多长时间发现它？
*   鉴于我们正在努力防止住院，我们如何看待基于我们实际上无能为力的高风险因素(如年龄)的预测？
*   考虑预测可预防的住院是不是更好？
*   考虑预测我们认为最有可能预防的住院是不是更好？
*   假阳性(预测某人将不住院)与假阴性(未发现将住院的人)的成本是多少？
*   如果我们认为这在经济上是值得的，我们是否有无限的资源，或者我们是否试图在我们能接触到的病人的特定限制下最大限度地进行预防？
*   一个模型需要多精确才能提供价值？

这些问题很多都没有明确的答案。有些人只是需要做出判断。有些需要对问题进行艰难的重构。有些需要业务目标和技术方法之间的折衷。

根据我的经验，商业利益相关者很适合回答这些问题，但是需要技术专家来识别正确的问题。

# 第二次看简历

建立判断和商业意识以知道如何在商业问题和技术解决方案之间进行转换需要一些经验和常识。这也是很难在简历中发现的东西，尽管很容易看出一个人何时可能缺乏这些技能。

除了 Kaggle 项目，或者上过一些 Coursera 课程，或者跟随一个在线教程，所有这些都指向技术技能，而没有将它们应用于商业问题的经验。并不是说这些都是学习技能的坏方法。只是他们不能教你所有你需要的技能。在一个真实的数据项目中，有各种各样的妥协要做，有各种各样的环境要考虑，有各种各样的假设要质疑。

现在我已经有了看简历的经历，当某人的技术技能和项目不具备在现实世界中应用这些技能的适当能力时，这变得有点明显。这就是为什么 Kaggle 的玩具项目往往不成功，正如我在另一篇文章中深入讨论的那样，我经常建议有抱负的数据科学家通过从事具有真实应用程序的项目来获得真实世界的经验——通过志愿服务、实习或与小型初创公司合作。