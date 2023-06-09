# 101 Dalmations 和机器学习有什么共同点？

> 原文：<https://towardsdatascience.com/what-do-101-dalmations-and-machine-learning-have-in-common-9e389b899df3?source=collection_archive---------24----------------------->

## [提示和技巧](https://towardsdatascience.com/tagged/tips-and-tricks)

## **科学家可以使用至少 101 个机器学习数据的例子来创造有价值的见解。他们来了。**

![](img/6d427c9bd6b67eeb43a9a2407befde4f.png)

少年——一个非常好的 boi，由 Jim Ozminkowski 提供

最近，我被要求帮助一个组织为预期增加的需要人工智能的业务做准备。该公司的人工智能将专注于机器学习(ML)和深度学习，这是一种在人类指导下使用计算机的技术，可以在数据中找到模式，用于为工业和公共政策应用创造见解。

这个组织非常精通统计学、计量经济学和可视化。他们的实证工作与其他任何人不相上下，甚至更好，50 年来出色的公共政策研究、评估和咨询经验证明了这一点，特别是在联邦和州政府领域。为了帮助拓宽视野和扩展能力，我搜索并记录了许多可以增加他们工作的实证方法的例子。这些方法中的许多被计算机科学家使用，但是通常不与经济学或其他社会科学相关联，因此政策分析者和政策制定者可能不太熟悉。

没有免费的午餐(NFL)定理说明了为什么考虑许多分析方法是有价值的。Goodfellow 等人(2015)在他们关于*深度学习*的教科书中解释了这个定理的意义。他们引用了 WOL pert(1996)对 NFL 的定义，即“平均所有可能的数据生成分布，当对未观察点进行分类时，每个分类算法都具有相同的错误率。换句话说，在某种意义上，没有任何机器学习算法比其他算法更好”(第 113 页)。

然而，这种平等只存在于有限的范围内。事实上，有许多地方例外。在任何给定的情况下，Goodfellow 等人说，可能有一种或多种最大似然算法产生比其他算法更好的预测。此外，一组更好的预测指标可能会因研究而异。在我看来，这是最重要的一点，也是从他们对 NFL 的讨论中获得的教训:这意味着数据科学家和其他政策分析师应该寻找最佳的预测算法来解决他们的每个预测挑战。例如，它意味着对每个分类或回归问题使用某种形式的逻辑或线性回归可能并不理想，即使这些方法是分析家和决策者最熟悉的。即使对于推理工作来说也是如此，在推理工作中，关联或因果归因，而不仅仅是预测，是目标，并且潜在的因果机制是非线性的。

如果我们必须寻找最佳方法，并且如果我们对每种潜在的有价值的方法的熟练程度不一样，那么有一个指向许多有用的分析方法的快速和实用的参考将是有用的。本帖提供了这样一个参考。

**几篇机器学习文章的注释列表**

下面你会发现一个注释列表，里面有很多关于 ML 的文章链接。这些大多是博客或教程，所以不发表在同行评议的期刊上。然而，很多时候评论跟在文章后面，错误、疑问或问题经常由知识渊博的读者发布。许多作者都是各自领域的佼佼者，他们经常在 GitHub 或其他地方回答这些问题，或者提供他们方法的理由和细节。

这些文章阅读起来简单快捷，通常不到 15 分钟。有时读者会发现方程看起来很紧张，但它们通常描述得很好，潜在的直觉通常很清楚。许多作者使用可视化来阐明主要观点。

大多数策略分析师都使用受监督的模型，因此有许多链接指向关于这些模型的信息。还提供了一些集合模型讨论的链接，因为这些提供了监督方法的很大扩展。

然后我提供无监督模型的链接。这些文章中描述的聚类、可视化和数据简化技术可以帮助数据科学家使用大量不同的数据集来指定模型，以说明底层数据中的更多变化。还提供了一些因果推理模型的链接，因为近年来人们对从预测到评估因果关系的兴趣越来越大。注意到了局限性，以及将这些文章与其他来源结合使用以构建更好的模型的建议。

从今天(11/30/21)起，下面的每个链接都可以访问，但我不知道它们会活跃多久。

![](img/b69fed810a295ae6888e735e4a79338a.png)

蒂姆·莫斯霍尔德在 Unsplash.com 的照片

**监督学习**

这是一种形式的**归纳学习**，它使用统计或其他模型来学习如何使用输入数据来生成对感兴趣的结果的正确预测。在经济学和其他社会科学的术语中，监督模型的输入数据被称为预测值、独立变量或解释变量。它们在计算机科学/工程/ ML 世界中被称为特征。在用于监督学习的数据中也可获得结果(即，从属)变量，允许统计包区分由 ML 模型做出的正确和不正确的预测。统计软件包还报告了 ML 模型使用几个模型性能度量来正确预测感兴趣的结果的能力。监督学习的重点通常是回归或分类问题。

在这一部分，你可以找到几篇关于各种形式的监督学习和相关主题的文章的链接。我们从描述一般方法论概念和问题的文章链接开始。然后我提供了描述几种预测方法的文章的链接。其中包括朴素贝叶斯、逻辑回归、支持向量机、线性判别分析和决策树，所有这些都可以用于对新对象进行分类或预测二元(是或否)结果。接下来是关于分位数回归、样条回归、岭和套索回归以及广义可加模型的文章链接，这些文章讨论了连续结果。然后我们转向用时间序列模型进行预测，我们用描述神经网络和深度学习方法的文章链接来结束这一长段，这些方法可用于预测二元或连续结果。

一些文章比较多种方法或描述集成应用，帮助分析师解决没有免费午餐的问题。在未来的文章中，我们将转向自动机器学习来促进这种比较。

**高层次的方法问题**:

这一部分包括几篇文章的链接，这些文章帮助数据科学家更好地理解如何使用 ML。我们从一篇关于将 ML 与人类专业知识相结合来制作更好的模型的文章开始。我读过的每一篇机器学习文本都强烈推荐 ML 的团队运动方面——人类应该指导这项工作，以确保它是相关的，并有可能产生有用的见解。这台机器旨在增强而不是取代人类的视角。

在这个链接之后，我们提供了一个描述笔记本技术在跟踪和描述我们的工作方面的实用性的链接。然后，我们将重点放在数据准备、编程语言以及其他工具和方法上，这些工具和方法有助于优化 ML 模型的使用和评估。之后，我们提供文章链接，

从哪里获取我们机器学习模型的数据，

特征(即独立变量)选择过程，

选择和解释模型时必须考虑的偏差-方差权衡，

如何使用莱姆、SHAP 和其他方法评估每个模型预测值的重要性，以及

如何创建仪表板来帮助不是专家的人解释 ML 模型的结果？

开始了…

1.J. Langston，机器教学:人们的专业知识如何让人工智能更强大(2019)，在 https://blogs.microsoft.com/ai/machine-teaching/上。当人类指导机器工作时，机器会产生更多有用的结果。即使是自动化的 ML 方法也是如此，我将在以后的文章中再回到这一点。

2.S. Sjursen，使用 Juypter 笔记本作为数据科学工作编辑器的利弊(2020 年)，载于[https://medium . com/better-programming/Pros-and-Cons-for-jupyter-Notebooks-as-Your-Editor-for-Data-Science-Work-tip-py charm-is-possible-40e 88 f 7827 CB](https://medium.com/better-programming/pros-and-cons-for-jupyter-notebooks-as-your-editor-for-data-science-work-tip-pycharm-is-probably-40e88f7827cb)。笔记本用来存放代码，驱动机器学习的执行，并存储结果，以供将来参考。有一些竞争对手的笔记本电脑产品。Jupyter 是使用最多的一个。比较了它的替代方案。

3.主动向导，管理者的数据科学:编程语言(2019)，[https://www . kdnugges . com/2019/11/Data-Science-Managers-Programming-Languages . html](https://www.kdnuggets.com/2019/11/data-science-managers-programming-languages.html)本文介绍了几种用于监督 ml 模型的编程语言的优缺点。例子包括 Python、R、Scala、Matlab 等等。

4.五、Kashid 对于数据科学来说，Python 和 R 的主要区别是什么？(2020 年)，在[https://www . quora . com/What-is-the-major-differences of-Python-and-R-for-data-science](https://www.quora.com/What-are-the-major-differences-between-Python-and-R-for-data-science)。这是对 Python 和 R 的一个很好的高层次比较，这两种语言是工业界和学术界用于数据科学的主要编程语言。

5.C. D .，数据科学家最佳数据科学工具(2020)，在[https://towardsdatascience . com/Best-Data-Science-Tools-for-Data-Scientists-75be 64144 a88](/best-data-science-tools-for-data-scientists-75be64144a88)。描述了许多用于处理大量不同数据、构建分析数据集以及用于统计分析、机器学习、深度学习、模型部署以及报告和可视化的工具。

6.d，Johnston，一个数据科学家应该对优化技术研究到什么程度？(2019)，上[https://www . quora . com/How-deep-should-a-data-scientist-study-optimization-techniques/answer/David-Johnston-147？ch = 8&share = 64 abfe 6 f&srid = kag TN](https://www.quora.com/How-deeply-should-a-data-scientist-study-optimization-techniques/answer/David-Johnston-147?ch=8&share=64abfe6f&srid=KAgTn)。每种有监督的 ML 方法通过解决优化问题来“学习”,优化问题通常被定义为最小化在现实生活中观察到的结果的实际值与由 ML 模型生成的那些结果的预测之间的差异。理解优化是如何工作的是很有帮助的(提示:它通常是基于使用你在微积分课上学到的链式法则的迭代方法)。除了这篇文章，YouTube 上还有一些很好的视频，描述了应用链式法则的反向传播。

7.T. Waterman，谷歌刚刚在 https://link.medium.com/5Ssd71u2y3 的[发布了 2500 万个免费数据集(2020 年)。在我们开始机器学习的过程之前，我们显然需要表示感兴趣的结构、预测器和结果的数据。谷歌并没有真正发布 2500 万个数据集，他们拥有的数据中只有大约一半是免费的。然而，他们确实发布了许多数据集的可搜索元数据，这对于找到合适的数据集非常有帮助。](https://link.medium.com/5Ssd71u2y3)

8.M. Dei，《让你的模型更好工作的变量转换目录》(2019)，https://link.medium.com/PO7esQMJn4。有时需要对变量进行转换(例如，标准化、规范化、分类)，以使机器学习模型运行得更好。本文描述了如何做到这一点。

9.张，理解机器学习中的数据规范化(2019)，。这是关于在建模之前标准化变量的价值的初级读本，以减少模型训练时间并提高准确性。

10.T. Yiu，了解交叉验证(2020)，关于[https://link.medium.com/gEwvRFTE83](https://link.medium.com/gEwvRFTE83)。交叉验证是一种多次细分数据集的方法，每次都在保留一个子集的情况下训练模型，然后聚合所有模型的信息，以找到具有最佳预测能力的模型。这篇文章描述了它是如何工作的。

11.R. Agarwal，每个数据科学家都必须知道的 5 个分类评估指标(2019)，关于[https://link.medium.com/IMLmW0IrW3](https://link.medium.com/IMLmW0IrW3)。这是关于分类分析的模型性能度量的初级读本——如何判断您的模型性能是否良好。

12.S. Kochlerlakota，《偏差与方差——穿越噪音》(2019)，https://link.medium.com/XIhInRhIk3 上的[。每一个用于预测现象或解释现象的机器学习和统计程序都必须平衡偏见的概念(例如，我们得到了正确的答案吗？)和方差(我们对此有多确定？).本文讨论了这种权衡。](https://link.medium.com/XIhInRhIk3)

13.B. O. Tayo，《机器学习中的错误来源》(2020)，载于[https://medium . com/towards-artificial-intelligence/Sources-of-Error-in-Machine-Learning-33271143 B1 ab](https://medium.com/towards-artificial-intelligence/sources-of-error-in-machine-learning-33271143b1ab)。本文描述了机器学习模型中需要防范的十种错误。这些错误不是机器学习独有的；它们适用于所有类型的分析。

14.J. Zornoza，特征选择介绍(2020)，载于[https://towardsdatascience . com/An-Introduction-to-Feature-Selection-DD 72535 ecf2b](/an-introduction-to-feature-selection-dd72535ecf2b)。一旦有了数据，就该抓住有用的部分进行分析了。特征选择是为机器学习模型寻找独立变量的艺术。这可以用理论来指导，用计算机分析来辅助。

15.M. Grogan，Python 中的特征选择技术:预测酒店取消预订(2020)，载于[https://link.medium.com/H5MsJdIJn4](https://link.medium.com/H5MsJdIJn4)。这里有更多关于寻找好的预测器的内容，包括一个例子和 Python 代码。

16.W. Koehrsen，Why Automated Feature Engineering Will Change the Way You Do Machine Learning(2018)，[https://link.medium.com/L8jojOVlJ1](https://link.medium.com/L8jojOVlJ1)—[Feature Engineering](https://en.wikipedia.org/wiki/Feature_engineering)是获取数据集并构建解释变量(特征)的过程，可用于为预测问题训练机器学习模型。正如本文所描述的，这现在可以自动化了。

17.G. Hutson，feature terminator-一个从统计和机器学习模型中自动删除不重要变量的包(2021)，[在 https://www . r-bloggers . com/2021/07/feature terminator-a-Package-to-Remove-important-Variables-from-Statistical-and-Machine-Learning-Models-Automatically/](https://www.r-bloggers.com/2021/07/featureterminator-a-package-to-remove-unimportant-variables-from-statistical-and-machine-learning-models-automatically/)。本文描述了几种类型的交叉验证，可用于消除无助于改进模型预测的变量。它还提出了避免多重共线性的方法，多重共线性会导致不稳定的预测。

18.J. Brownlee，[《机器学习模型选择的温和介绍](https://t.dripemail2.com/c/eyJhY2NvdW50X2lkIjoiOTU1NjU4OCIsImRlbGl2ZXJ5X2lkIjoiN2JwNTFibjhkNTBhZHl5eG93eW0iLCJ1cmwiOiJodHRwczovL21hY2hpbmVsZWFybmluZ21hc3RlcnkuY29tL2EtZ2VudGxlLWludHJvZHVjdGlvbi10by1tb2RlbC1zZWxlY3Rpb24tZm9yLW1hY2hpbmUtbGVhcm5pbmcvP19fcz1mcDR0NWtucG5ldTVqcHZrbnJucyJ9) (2019)，在[https://machinelingmastery . com/A-Gentle-Introduction-to-Model-Selection-for-Machine-Learning/](https://machinelearningmastery.com/a-gentle-introduction-to-model-selection-for-machine-learning/)。本文描述了如何根据您想要解决的问题，在众多机器学习方法中进行选择。

19.美国马赞蒂，SHAP 在 https://towardsdatascience . com/shap-Explained-the-way-I-Wish-Someone-Explained-it-to me-ab 81 cc 69 ef 30 上解释了我希望有人向我解释的方式(2020 年)[。作者提供了一个很好的方式来理解 SHAP 如何被用来解释预测模型中各种特征(变量)的贡献。](/shap-explained-the-way-i-wish-someone-explained-it-to-me-ab81cc69ef30)

20.D. Dataman，用 https://link.medium.com/Fjo6lzakY1 上的[使用 KernelExplainer (2019)解释任何具有 SHAP 价值观的模型。机器学习模型有时看起来像是黑盒，不能显示预测变量的相对重要性。本文解释了如何通过使用一个新的 Python 实用程序来找出答案，并举例说明了许多不同类型的 ML 模型的结果。](https://link.medium.com/Fjo6lzakY1)

21.P. Dos Santos，小心你的 SHAP(2020)，[在 https://medium . com/@ pauldos Santos/Be-小心-What-You-shap-For-AEC cabf 3655 c](https://medium.com/@pauldossantos/be-careful-what-you-shap-for-aeccabf3655c)。作者指出，在结合了连续和二元预测的模型中，SHAP 会产生误导性的结果。

22.a .纳亚克，《莱姆和 SHAP 背后的想法》(2019)，《关于 https://link.medium.com/13VS0JSmD2 的 T0》。本文介绍了另一种方法来估计预测变量(石灰)的相对重要性，并比较它与 SHAP。

23.M. Dei，[每个数据科学家都应该知道的三种模型可解释性方法](/three-model-explanability-methods-every-data-scientist-should-know-c332bdfd8df) (2019)，[在 https://towardsdatascience . com/Three-Model-expolability-Methods-Every-Data-Scientist-Should-Know-c 332 BDF 8df](/three-model-explanability-methods-every-data-scientist-should-know-c332bdfd8df)。这篇文章更深入地探讨了模型的透明性和可解释性。作者介绍了排列重要性的概念，并描述了部分依赖图的效用。他引用了一个新版本的 scikit-learn 库，可以帮助应用这些技术，SHAP 也是如此。

24.马赞蒂，你的哪些特征是过度适合的？发现 ParShap:一种先进的方法来检测哪些列使您的模型不符合要求(2021)，[在 https://towardsdatascience.com/tagged/tips-and-tricks?p=c46d0762e769](https://towardsdatascience.com/tagged/tips-and-tricks?p=c46d0762e769) 。这篇文章描述了他创建的 SHAP 的扩展，以找出哪些独立变量(特征)导致模型在采样数据上表现很好，但在新数据上表现很差。

25.美国马赞蒂，黑盒模型实际上比逻辑回归更容易解释(2019)，在[https://towardsdatascience . com/Black-Box-Models-is-Actually-More-an-a-Logistic-Regression-f263c 22795d。作者很好地解释了如何从复杂的模型中推导出概率，因此它们更容易解释。](/black-box-models-are-actually-more-explainable-than-a-logistic-regression-f263c22795d.)

26.H. Sharma，机器学习模型仪表板:创建仪表板以解释机器学习模型(2021)，[在 https://towardsdatascience . com/Machine-Learning-Model-Dashboard-4544 DAA 50848](/machine-learning-model-dashboard-4544daa50848)。Sharma 展示了如何创建一个仪表板来更好地查看模型的执行情况。

**一些说明性的使用案例:**

在文献中描述了成千上万的受监控的 ML 应用，并且/或者在全世界的工业和学术界中使用。这里只是展示 ML 如何提供有用的见解的几个例子。很有可能只要在谷歌上搜索一个描述你感兴趣的问题的短语和“机器学习”就能说明 ML 如何对你的应用有用。

27.什么是好的机器学习用例？(2019)，[论 https://link.medium.com/Ja4FUL3yG2](https://link.medium.com/Ja4FUL3yG2)。我们的客户要求我们解决的大多数经验性问题可能是 ML 的良好用例。即使对于推理工作也是如此，因为我们做出的程序影响估计或其他推理可以被视为对未来结果的预测，而 ML 擅长对他们关心的结果做出可靠的预测。还有许多其他用例，其中一些解决了内部管理挑战，如降低成本、降低风险和利润最大化。本文指出了这三个管理挑战。

28.J. Wang，数据科学与公共政策交汇处的思考(2017)，[https://towardsdatascience . com/Musings-at-the-crossover-of-Data-Science-and-Public-Policy-cf 0 bb 2 fadc 01](/musings-at-the-intersection-of-data-science-and-public-policy-cf0bb2fadc01)。作者提供了一些关于数据科学在解决公共政策问题方面的效用和局限性的智慧之言。她包含了几个用例的链接。

29.J. Rowe，自然语言处理和机器学习如何帮助追踪冠状病毒(2020)，[https://www . healthcareitnews . com/ai-powered-health care/researchers-tap-ai-Track-spread-Corona Virus](https://www.healthcareitnews.com/ai-powered-healthcare/researchers-tap-ai-track-spread-coronavirus)。这篇文章是关于自然语言处理和机器学习如何帮助跟踪冠状病毒的——这是一个有趣的用例，说明了这些技术的力量。

30.来自 arXiv 的新兴技术，机器学习已经揭示了莎士比亚戏剧有多少是由其他人写的(2019 年)，[在 https://www . Technology review . com/s/614742/Machine-Learning-has-reveal-Exactly-how-do-a-a-Shakespeare-play-is-Written-by-Someone/](https://www.technologyreview.com/s/614742/machine-learning-has-revealed-exactly-how-much-of-a-shakespeare-play-was-written-by-someone/)。这个用例与我们考虑的其他用例完全不同，但是这篇文章让我们看到了这样一个事实:ML 是一个灵活的工具，可以用于各种应用程序中。

31.J. Kent，机器学习可以改善临终交流(2019)，[在 https://health analytics . com/news/Machine-Learning-can-Improve-End-of-Life-Communication？Eid = cxtel 000000199563&elqCampaignId = 12666&UTM _ source = nl&UTM _ medium = email&UTM _ campaign = newsletter&elq trackid = 891254 c 5466 e 49 b 0 be c8 c 00 BDA 09517 b&elq = c 28 e 7e 780 c 43 faac 51 db 1 f 0 FD 44882&El 本文描述了使用自然语言处理和机器学习来评估临终对话的内容，然后提出更好的方法。](https://healthitanalytics.com/news/machine-learning-could-improve-end-of-life-communication?eid=CXTEL000000199563&elqCampaignId=12666&utm_source=nl&utm_medium=email&utm_campaign=newsletter&elqTrackId=891254c5466e49b0bec8c00bda09517b&elq=c3c28e7e780c43faac51db1f0fd44882&elqaid=13294&elqat=1&elqCampaignId=12666)

32.J. Harris(与 M. Stewart 合著)，环境科学中的数据隐私和机器学习，载于[https://towards Data Science . com/Data-Privacy-and-Machine-Learning-in-Environmental-Science-490 fded 366 D5](/data-privacy-and-machine-learning-in-environmental-science-490fded366d5)。这是 Jeremie Harris 采访哈佛大学环境科学博士生 Matthew Stewart 的播客。Matthew 经常为《走向数据科学》投稿，他的博士论文是机器学习和环境科学的结合点。他和他的同事专注于气候变化模型、碳排放和其他重要问题。在这个播客中，他重点关注数据隐私、个人观察的分析价值和模型偏差等问题之间的权衡。

![](img/fda72189be88a48a82ec9603300bfbf7.png)

Alexander Schimmeck 在 Unsplash.com 拍摄的照片

**监督学习法**:

33.J. Brownlee，机器学习算法之旅(2020)，[在 https://machinelingmastery . com/A-Tour-of-Machine-Learning-Algorithms/](https://machinelearningmastery.com/a-tour-of-machine-learning-algorithms/)。我们以一位实用机器学习方法大师对许多类型的机器学习模型的精彩回顾作为开篇。

34.S. Patel，第 1 章:监督学习和朴素贝叶斯分类—第 1 部分(理论)(2017)，关于 https://link.medium.com/VZlAzZKeK2 的。当用于生成二元结果预测的变量相互独立(即天真)时，朴素贝叶斯利用贝叶斯定理来帮助生成这些预测。这很容易做到，并提供易于解释的结果，因此朴素贝叶斯通常是一种受欢迎的初始方法。这篇文章描述了它是如何工作的。

35.S. Patel，第 1 章:监督学习和朴素贝叶斯分类—第 2 部分(编码)(2017)，[关于 https://link.medium.com/87CBHgWeK2](https://link.medium.com/87CBHgWeK2)。本文描述了如何在 Python 中实现朴素贝叶斯方法。

36.T. Yiu，Understanding The Naive Bayes Classifier(2019)，on[https://link.medium.com/OpjLwR7ZF4.](https://link.medium.com/OpjLwR7ZF4.)这是关于 Naive Bayes 的另一个很好的初级读本，Naive Bayes 是一个分类器，通常概括得很好，并且易于使用。文章中的这句话概括了这一点:从高层次来说，朴素贝叶斯只是将贝叶斯定理的简化版本应用于基于其特征的每一个观察值(以及每一个潜在的类)。

37.M. Maramot Le，为什么数据科学中经常使用逻辑回归？(2019)，[在 https://www . quora . com/Why-is-logistic-regression-used-so-frequency-in-data-science/answer/Marmi-Maramot-Le？ch = 8&share = 7 E0 C7 B2 a&srid = kag TN](https://www.quora.com/Why-is-logistic-regression-used-so-often-in-data-science/answer/Marmi-Maramot-Le?ch=8&share=7e0c7b2a&srid=KAgTn)。这很好地描述了逻辑回归的优点，它可能是许多行业中最流行的分类方法。

38.H. H. Strand，当评估逻辑回归时，解释 Brier 评分和 AUROC 评分的区别是什么？你什么时候会使用其中一个而不是另一个？有没有可能一个高分一个低分？(2019)，在[https://www . quora . com/When-evaluating-a-logistic-regression-When-the-differences-interpreting-the-Brier-Score-vs-the-AUROC-When-you-use-one-vs-other-Is-possible-a-high-Score-in-one-a-low-Score-in-the/answer/H % C3 % A5kon-Hapnes-Strand？ch = 8&share = d 7361 af 6&srid = kag TN。](https://www.quora.com/When-evaluating-a-logistic-regression-what-are-the-differences-between-interpreting-the-Brier-Score-vs-the-AUROC-When-would-you-use-one-vs-the-other-Is-it-possible-to-have-a-high-score-in-one-and-a-low-score-in-the/answer/H%C3%A5kon-Hapnes-Strand?ch=8&share=d7361af6&srid=KAgTn.)这里引用作者的一句话:ROC 曲线的 AUC 是分类模型最普遍适用的度量之一，但它只评估你预测的*等级*。Brier 评分计算概率预测的准确性。如果你只关心分类，AUC 很好，但是如果你想估计某件事的概率，那么 Brier 评分是一个很好的额外指标。

39.f .乔，使用 Scikit-learn 调整逻辑回归模型-第 1 部分(2019)，关于[和](https://link.medium.com/nJf2bACEY2)本文描述了调整逻辑回归模型以提高模型性能的方法。还与随机森林进行了比较。提供了 Python 代码。

40.S. Deb，朴素贝叶斯 vs 逻辑回归(2016)，https://link.medium.com/UPGymGIfK2 的。由于朴素贝叶斯和逻辑回归是两种流行的、相对简单的、可解释的使用方法，本文描述了它们各自的优势。逻辑回归在大型数据集上占主导地位，但大多数数据集并没有那么大，很多时候朴素贝叶斯更快地生成准确的结果。描述了经验误差、概括误差和混杂误差，包括辛普森悖论。

41.M. Sanjeevi，带数学的支持向量机(2017)，上[https://medium . com/deep-Math-Machine-learning-ai/chapter-3-Support-Vector-Machine-With-Math-47d 6193 c 82 be](https://medium.com/deep-math-machine-learning-ai/chapter-3-support-vector-machine-with-math-47d6193c82be)。作者很好地描述了 SVM 是如何工作的，将图形和数学结合起来。这个应该会吸引那些有很强数学背景的人。

42.R. Pupale，支持向量机——概述(2018)，载于[https://towardsdatascience . com/https-medium-com-pupalerushikesh-SVM-f4b 42800 e989](/https-medium-com-pupalerushikesh-svm-f4b42800e989)。这是对 SVM 的一个很好的介绍，用直观的图形来描述基础理论和 Python 代码。

43.开放数据科学——在 R(2018)[https://link.medium.com/ztbUrFveK2](https://link.medium.com/ztbUrFveK2)上构建多类支持向量机。作者提供了理论，以及 SVM 在 R 中的应用，以结果变量中有多个类为例。

44.P. Nistrup，线性判别分析(LDA) 101，使用 R (2019)，[对 https://link.medium.com/WWlqD6xQN2](https://link.medium.com/WWlqD6xQN2)。LDA 是分类分析的另一种形式，从这个意义上讲，它可以替代逻辑回归、决策树、朴素贝叶斯和其他方法。它也可以被视为主成分分析的替代方法或补充方法(参见下文关于主成分分析的无监督模型)。本文中有一些很好的可视化工具来说明 LDA，并附有 R 代码来看看如何进行试验。

45.《熵:决策树如何做出决策》(2019)，https://link.medium.com/vXj620nRN2 上[。本文描述了如何使用熵(纯度的一种度量)和信息增益来创建决策树。](https://link.medium.com/vXj620nRN2)

46.P. Flom，分位数回归介绍(2018)，https://link.medium.com/hcLvE9WoK2.与普通最小二乘法相反，分位数回归对残差的分布不做任何假设。当因变量是双峰或多峰时，它也比普通最小二乘法更好。本文提供了一个用分位数方法分析出生体重数据的例子，以及 SAS 代码。

47.C. Lee，分位数回归—第一部分(2018)，https://link.medium.com/HtaBXw6oK2 的。本文描述了分位数回归的工作原理，并提供了使用 Tensorflow、Pytorch、Light GBM 和 Scikit-Learn 的示例。基于数学的理论也提供了。

48.M. Ghenis，分位数回归，从线性模型到树到深度学习(2018)，在[https://link.medium.com/arc6wSspK2.](https://link.medium.com/arc6wSspK2.)这篇文章将分位数回归与随机森林、梯度推进、普通最小二乘法和深度学习方法进行了比较。

49.S. Vyawahare，R (2019)中的样条回归，关于[https://link.medium.com/T7IGk9QpK2.](https://link.medium.com/T7IGk9QpK2.)样条回归(也称为分段回归)是一种非参数技术，可以很好地用于非线性数据。它可以替代分位数回归。

50.M.S. Mahmood，利用一般加法模型拟合非线性关系(2021)，[https://towardsdatascience . com/Fit-Non-linear-Relationship-Using-generalized-Additive-Model-53a 334201 b5d](/fit-non-linear-relationship-using-generalized-additive-model-53a334201b5d)。这是一篇很好的文章，描述了如何使用一般的可加模型来生成非线性关系的预测。结果被建模为输入变量的非线性函数的总和。提供了与样条和多项式回归的比较。

51.V. Sonone，Scikit-learn 监督学习的传统指南-稳健回归:异常值和建模误差-广义线性模型(2018)，关于[https://link.medium.com/UtGDO37BL2.](https://link.medium.com/UtGDO37BL2.)稳健回归程序在异常值或其他数据问题存在时很有价值。

52.S. Bhattacharyya，Ridge and Lasso Regression:A Complete Guide with Python sci kit-Learn(2018)，[on https://link.medium.com/RGST954ii2](https://link.medium.com/RGST954ii2)—这篇文章中的引用很好地总结了它的重点: **Ridge and Lasso regression 是一些简单的技术，用于降低模型复杂性和防止简单线性回归可能导致的过拟合**。

53.A. Singhal，机器学习:详细岭回归(2018)【https://link.medium.com/KoK0E7Oxx3 上的[。如题，这里有一个关于岭回归的更多信息。作者对过度拟合问题进行了很好的回顾，过度拟合导致模型在训练数据集上表现很好，但在用于全新数据时表现很差。他展示了如何使用岭回归来避免这个问题。](https://link.medium.com/KoK0E7Oxx3)

54.S. Gupta，各种机器学习算法的利弊(2020)上[https://towardsdatascience . com/Pros-and-Cons-of-variable-classification-ml-Algorithms-3 b5 bfb 3c 87d 6。](/pros-and-cons-of-various-classification-ml-algorithms-3b5bfb3c87d6.)本文回顾了支持向量机、逻辑回归、朴素贝叶斯、随机森林、决策树、k-最近邻和 XGBoost 在预测练习中的优缺点。

55.E. Lisowski，最佳预测技术，或如何从时间序列数据进行预测(2019)[https://link.medium.com/tR9OlYzpR1](https://link.medium.com/tR9OlYzpR1)。本文描述了如何使用时间序列数据生成良好的预测。例如，考虑如何最好地预测在全国几个州使用的全付费(即，全保险)系统下支付给医疗保健提供者的费用。这里提到的 ARIMA 模型非常适合这个问题以及类似的问题。我在这篇文章的介绍中提到的公司为此开发了一个很棒的 ARIMA 模型，极大地提高了支付给几个州的提供商的公平性和准确性。

56.J. Nikulski，AdaBoost 的时间序列预测，Random Forests 和 XGBoost (2020)在 https://link.medium.com/RX2I64fLf5.[发表](https://link.medium.com/RX2I64fLf5.)这是对三种可用于时间序列数据的最大似然技术的一个很好的回顾。作者提供了关于如何测试这些模型性能的指导。时间序列模型的性能测试技术从根本上不同于其他类型的 ML，原因在文章中提到。

57.J. D. Seo，趋势，季节性，移动平均线，自回归模型:我的交互式代码时间序列数据之旅(2018)，https://link.medium.com/n5qvZnKhY1 上的[——这篇文章回顾了更多的模型，并有一些很好的可视化。](https://link.medium.com/n5qvZnKhY1)

58.B. Etienne，Python 中的时间序列-指数平滑和 ARIMA 过程(2019)，https://link.medium.com/IwSvpfzfn2 的-这本书有更多关于检查平稳性的信息，这是从时间序列模型中做出良好预测所必需的。还提供了获得平稳性的变换。提供了 Python 代码和可视化，以及关于如何从几个选择中选择一个时间序列模型，以及如何绘制预测的思想。

59.S. Palachy，时间序列分析中的平稳性(2019)，https://link.medium.com/SLpze7QdI2 上的[。对于那些喜欢大量理论和数学的人来说，这里是在平稳性属性的背景下对这些内容的描述，平稳性属性是使用时间序列数据进行预测的可靠方法的基础。](https://link.medium.com/SLpze7QdI2)

60.R. Kompella，使用 LSTMs 预测时间序列(2018)，载于[https://towardsdatascience . com/Using-lst ms-to-forecast-time-series-4ab 688386 b1f。也可以使用神经网络方法从时间序列中进行预测。本文描述了如何用 Python 实现这一点。](/using-lstms-to-forecast-time-series-4ab688386b1f.)

61.J. Brownlee，如何用 Python 从零开始用反向传播编码一个神经网络(2021)，[在 https://machine learning mastery . com/implement-back propagation-algorithm-Scratch-Python/](https://machinelearningmastery.com/implement-backpropagation-algorithm-scratch-python/)。神经网络方法大致基于大脑中的神经元如何相互传递信息。这种生物过程激发了神经网络和深度学习模型，它们可以非常好地预测二元或连续的结果。本文解释了如何用 Python 生成神经网络模型，以及如何使用一种称为反向传播的技术来最小化模型误差。

62.答:是的，如果你不理解通用逼近定理(2020)，[在 https://medium . com/analytics-vid hya/You-dont-Understand-Neural-Networks-Until-You-Understand-the-Understand-the-Universal-Approximation-Theorem-theory-85b3e 7677126](https://medium.com/analytics-vidhya/you-dont-understand-neural-networks-until-you-understand-the-universal-approximation-theorem-85b3e7677126)这个定理指出，如果使用类似 sigmoid 的激活函数，只有一个隐藏层且其中有足够神经元的神经网络可以以合理的精度逼近任何连续(线性或非线性)函数作者提供了一个很好的描述和一些例子。

63.S. K. Dasaradh，《神经网络背后的数学的温和介绍》(2019)，https://link.medium.com/MDZLalMfI2 上的[。虽然“温柔”是情人眼里出西施，但这篇文章描述了神经网络背后的直觉和数学。](https://link.medium.com/MDZLalMfI2)

64.V. Sethi，神经网络的类型(以及每种类型的作用！)解说(2019)【https://link.medium.com/hWRnjnJEY2 上的 。神经网络可用于回归或分类问题，因此可以替代上述链接中描述的任何方法。本文对不同类型的神经网络进行了高度的描述。

65.《走向人工智能团队，神经网络的主要类型及其应用——走向人工智能团队教程》(2020)，[https://link.medium.com/rgohjQrQG8](https://link.medium.com/rgohjQrQG8)。这是对 27 种神经网络模型的简短回顾。顶部的图片很好地展示了这些方法。

66.E. Hlav，深度学习中的激活函数:从 Softmax 到 Sparsemax——数学证明(2020)，在[https://link.medium.com/sul2IG8799.](https://link.medium.com/sul2IG8799.)上本文描述了 Sparsemax，一种在神经网络中用于预测多类别结果的激活函数。

67.A. Bonner，什么是深度学习，它是如何工作的？(2019) [关于 https://link.medium.com/csFjYHHoR1](https://link.medium.com/csFjYHHoR1)—深度学习是一种基于神经网络的 ML 形式。虽然基本的神经网络只有一个位于输入数据和输出预测之间的“隐藏”层，但深度学习有两个或更多层。在复杂的成像、基因组或物理应用中，可能有数百、数千或数万个隐藏层，每个隐藏层都建立在前面的层上，以努力生成更好的预测。

68.M. Lugowska，当你用深度学习开始你的日志时的必读教程，作者 mag delna Lugowska(2019)，[在 https://blog . sky gate . io/A-必读教程-当你开始你的深度学习之旅时-5fa4da071510](https://blog.skygate.io/a-must-read-tutorial-when-you-are-starting-your-journey-with-deep-learning-5fa4da071510) 。提供深度学习的介绍。还提供了一些关于如何处理隐藏层的建议，真正的工作是在隐藏层完成的。还提供了关于如何调整这些模型的建议。

69.D. Jangir，激活函数的需求和使用(2018)，https://link.medium.com/dJYXxPbNf5.作者对神经网络中用于生成非线性数据预测的激活函数进行了很好的回顾。回顾了几种激活函数。

70.T. Folkman，如何利用深度学习即使是小数据(2019)，https://link.medium.com/f57XSYHCB2 上[。大多数人认为深度学习需要庞大的数据集，但事实并非总是如此，正如本文所解释的那样。](https://link.medium.com/f57XSYHCB2)

![](img/59465876470245191768e96f712dce22.png)

Manuel Nageli 在 Unsplash.com 拍摄的照片

**合成和集成学习:**

组合和集成学习指的是使用几种类型的机器学习来解决机器学习问题。

71.a .叶，组合学习是机器学习的未来(2020)，[上](https://link.medium.com/89fJQJGV66)。当大型任务可以被分成有意义的、不同的部分时，使用组合学习，每个部分由不同的机器学习方法进行分析。

72.J. Roca，Ensemble methods: bagging，boosting and stacking (2019)，https://link.medium.com/93kLZDWPS1—Bagging 是指同时运行许多(即 10 个、100 个或 1000 个)类似的模型。随机森林模型是装袋模型。Boosting 指的是按顺序运行模型，部分集中于利用以前模型的误差项。堆叠是指并行运行许多不同类型的模型，然后合并结果。

73.S. Glenon，决策树 vs 随机森林 vs 梯度提升机器:简单解释(2019)，载于[https://www . datascience central . com/profiles/blogs/Decision-Tree-vs-Random-Forest-vs-boosted-trees-Explained。](https://www.datasciencecentral.com/profiles/blogs/decision-tree-vs-random-forest-vs-boosted-trees-explained.)随机森林(RF)是由许多决策树在全部生成后组合而成的。梯度推进机器(GBM)方法在建造采油树时一个接一个地组合采油树。提供了 RF 和 GBM 的一些优点和缺点。

74.W. Koehrsen，Python 中的随机森林(2017)【https://link.medium.com/zJEfiDWEB2 —随机森林是最受欢迎的方法之一，也是预测二元结果的最佳监督方法之一。它经常但不总是比逻辑回归、支持向量机、梯度推进或神经网络方法更好。RF 是一种决策树方法，它将 10 个或 100 个或 1000 个独立决策树的输出组合在一起。要使用的树的数量是由用户设置的超参数——有关超参数的更多信息，请参见下文。

75.答:Ye，When and Why Tree-Based Models(经常)优于神经网络(2020)，[https://towards data science . com/When-and-Why-Tree-Based-Models-ocely-perform-Neural-Networks-ceba 9 ECD 0 FD 8](/when-and-why-tree-based-models-often-outperform-neural-networks-ceba9ecd0fd8)虽然没有免费的午餐原则保证没有特定的建模方法在每种情况下都占主导地位，但在某些情况下，随机森林和其他基于树的模型往往优于神经网络。看看里面为什么。

76.W. Koehrsen，超参数调优 Python 中的随机森林(2018)，https://link.medium.com/TFvgX1DlD2 上的。—超参数是模型用来生成预测的设置。把设置想象成电子邮件或手机的设置。分析员告诉软件使用哪个超参数。超参数选择没有很好的理论指导；使用试错法和直觉来达到最终的超参数设置，其与最小模型误差相关联。这种搜索可以是自动的。

77.P. Patidar，机器学习中的超参数(2019)，https://link.medium.com/VAVKbs6qi4 的。本文提供了关于超参数的另一个简要介绍。

78.t . S .[5 分钟 AdaBoost 的一个数学解释(2020) |走向数据科学](/a-mathematical-explanation-of-adaboost-4b0c20ce4382)上[https://Towards Data Science . com/A-Mathematical-explain-of-AdaBoost-4 b 0c 20 ce 4382。](/a-mathematical-explanation-of-adaboost-4b0c20ce4382.)这是 AdaBoost 的简短说明，AdaBoost 是一种基于自适应 boosting 树的 ML 方法。提供了一个示例。

![](img/804967fcc41d241d166e246515b10151.png)

Jan Antonin Koler 在 Unsplash.com 拍摄的照片

**无监督学习:**

这是一种学习形式，包括在数据集内搜索模式，但没有标记结果变量的优势。许多无监督的方法被用于将相似的观察结果分组为更小的群。

可视化也是一种无监督学习的形式；请参阅下面关于拓扑数据分析(TDA)的文章作为示例。TDA 是一种以更完整的方式理解我们分析的数据的方法。

最后，创建数据的低维表示的努力也是无监督学习方法的例子。很好的例子包括主成分分析、因子分析和自动编码器，它们根据用户希望如何将几百或几千个变量中的信息减少到更少(也许只是几个)的变量而变化，以便更容易在 ML 中使用。

79.J. T. Raj，机器学习降维初学者指南(2019)，在[https://link.medium.com/wWOFkXNoe3](https://link.medium.com/wWOFkXNoe3)这篇文章描述了如何将具有数百或数千个特征(即变量，或变量的函数)的数据集减少到一个更小的数量，而不会导致太多的信息损失。这使得用户可以利用庞大的数据集，同时仍然让模型收敛。

80.a .叶，《线性判别分析在四分钟内解释:概念、数学、证明和应用》(2020)，载于[https://medium . com/analytics-vid hya/Linear-discriminal-Analysis-Explained-in-Under-4-Minutes-e558e 962 c 877](https://medium.com/analytics-vidhya/linear-discriminant-analysis-explained-in-under-4-minutes-e558e962c877)。LDA 是一种可用于监督或非监督分析的技术。本文更侧重于无监督的应用程序。

81.P Nistrup，线性判别分析(LDA) 101，使用 R (2019)，在[https://towardsdatascience . com/Linear-discriminal-Analysis-LDA-101-Using-R-6a 97217 a 55 a 6](/linear-discriminant-analysis-lda-101-using-r-6a97217a55a6)。这是一个很好的应用程序，展示了如何使用 R 统计软件进行 LDA。

82.M. J. Garbade，Understanding K-means Clustering in Machine Learning(2018)，on[https://link.medium.com/YAkPCunvp1.](https://link.medium.com/YAkPCunvp1.)K-means Clustering 是一种方法，通过这种方法，用户可以决定他或她想要从源数据集(这是数字 *k* )创建多少个子集(聚类)，软件可以计算出如何构建这些聚类，以便一个聚类内的观察结果相似，但不同于其他聚类中的观察结果。

83.C. Maklin，K-means 聚类 Python 示例(2018)，https://link.medium.com/9Ro8ahOgn2 上的[——作者很好地介绍了 K-means 聚类，有很好的可视化和 Python 代码。](https://link.medium.com/9Ro8ahOgn2)

84.A. Singh，用高斯混合模型建立更好更准确的聚类(2019)，关于[https://link.medium.com/Z0Ls9KUqW3.](https://link.medium.com/Z0Ls9KUqW3.)聚类分析有助于从未标记的数据中找出意义。本文描述了如何使用 GMM 通过对相似的观察结果进行聚类来更好地理解这些数据。

85.T. Yiu，Understanding PCA (2019)，on[https://link.medium.com/ZHwhuCajK2.](https://link.medium.com/ZHwhuCajK2.)主成分分析是一种将来自许多变量的信息组合成更多变量的技术，根据作者的说法，这“有助于我们揭示隐藏在数据中的潜在驱动因素。”这篇文章简单地、高层次地描述了这是如何发生的，并带有一些漂亮的视觉效果。

86.a，Dubey，主成分分析背后的数学(2018)，关于[https://link.medium.com/xz2bMKOhK2.](https://link.medium.com/xz2bMKOhK2.)这篇文章描述了 PCA 中使用的数学，将许多变量转换成许多更少的变量，同时在这个过程中保留尽可能多的信息。

87.T. Santos，因子分析和主成分分析之间的差异(2019)，关于[https://link.medium.com/LHtYPlmjK2.](https://link.medium.com/LHtYPlmjK2.)PCA 和 FA 都是数据简化技术，但 PCA 专注于在其创建的较小变量集中保留尽可能多的变化，而 FA 专注于将来自较大变量集的信息组合成较小的潜在(隐藏)因子集，这些因子可以解释观察到的较大变量集之间的相关性。

88.T. Ciha，PCA & auto encoders:Algorithms every one Can Understand(2018)，on[https://link.medium.com/eYPIiKdiK2.](https://link.medium.com/eYPIiKdiK2.)PCA 是一种基于线性代数的方法，将变量组合成更少的变量。自动编码器是一种基于神经网络的方法，用于将来自许多变量的信息组合成更少的变量。本文描述了每种方法的属性。

89.J. Brownlee，可视化主成分分析(2021)，[https://machine learning mastery . com/Principal-Component-Analysis-for-Visualization/？UTM _ source = drip&UTM _ medium = email&UTM _ campaign = Principal+component+analysis+for+visualization&UTM _ content = Principal+component+analysis+for+visualization](https://machinelearningmastery.com/principal-component-analysis-for-visualization/?utm_source=drip&utm_medium=email&utm_campaign=Principal+component+analysis+for+visualization&utm_content=Principal+component+analysis+for+visualization)大多数人使用 PCA 进行降维，但它对可视化数据也非常有用，如本文所述。

90.Z. Singer，拓扑数据分析-解开流行词(2019)，https://link.medium.com/WKBRmTMjK2.[TDA](https://link.medium.com/WKBRmTMjK2.)是一种理解数据集中变量如何相互关联的几何方法。TDA 的应用通常可以揭示隐藏的模式，从而导致对感兴趣的结果如何产生的关键理解。TDA 提供的可视化说明了数据的“形状”，可以帮助我们生成更好的预测或解释模型。这篇文章说明了 TDA 是如何在高层次上工作的。

91.V. Deshmukh，拓扑数据分析——一个非常简短的介绍(2019)，关于 https://link.medium.com/yqlneOEjK2 的。这篇文章提供了更多关于 TDA 如何工作的信息。

**因果推断:**

介质上有很多关于因果推理的描述。一些是由经济学家和其他社会科学家，一些是由神经科学家，以及许多其他学科的代表。完全覆盖因果推理是不可能的。下面你会发现一些引起我兴趣的，从我几个月前写的一个概述开始。在 Medium 上搜索“因果关系”可以找到更多。关于经济学和其他社会科学中因果推理的三部伟大教科书已经由 Maziarz (2020)、Pearl 和 Mackenzie (2019)以及 Morgan 和 Winship (2015)编写完成。

92.什么导致了什么，我们怎么知道？(2021)，在[https://towards data science . com/what-causes-what-how-we-know-b 736 a 3d 0 eefb](/what-causes-what-and-how-would-we-know-b736a3d0eefb)。这是一个由该领域的领导者确定的五种主要因果推理方法的综述，以及它们如何帮助我们思考当今主要的社会政治经济问题。

93.A. Kelleher，因果关系技术入门(2016)，在[https://medium . com/@ akelleh/A-Technical-Primer-on-Causality-181 db 2575 e41](https://medium.com/@akelleh/a-technical-primer-on-causality-181db2575e41)。这本关于因果关系的初级读本深入到基础概念中，直观且带有一些重型数学。它应该能满足那些对因果推理感兴趣的有许多不同背景和训练的人。

94.P. Prathvikuman，通过因果影响进行因果推断(2020)，https://link.medium.com/rSFRdqmW66 上[。这是一篇关于谷歌因果影响软件的短文——基本上是关于如何找到反事实，并在随机化不可行的研究中使用这些反事实来推断因果关系。许多客户将我们生成的项目影响或其他推断估计解释为因果关系，而回归系数并不总是符合因果推断的标准。设计问题，尤其是如何处理选择偏差，是需要讨论的关键问题。](https://u2329897.ct.sendgrid.net/ls/click?upn=vmTKivNEf94zUPzY2BxJkP7AtbFqZoxYj0vgG04rCmBVR0bzEKKHce3yfdJk8wVU-r4h_coqGJLqbAbdlwK0cmJTy4WMDdZRw4DDwQ7NMsdba0Uht7jkgJD9yHV5yhQbEbLBYyC4Y6A5lhkVecPXBHy-2FejtoPHYLFHhExxDTU60BB9Dj3JDznm4eAahbXxjNWnn7vkT-2FJFi3mZMJH8C9049dPUev6h6YFER9zg-2BykqJBH06q6QYCNkjBLwng1nsMvVC0-2BmRYQXKcLHET-2F4Rx-2B2WaOvw-3D-3D)

95.P. Rajendran，使用差异中的差异、因果影响和合成控制的因果推理(2019)，[https://towardsdatascience . com/Causal-Inference-Using-Difference-Causal-Impact-and-Synthetic-Control-f 8639 c 408268](/causal-inference-using-difference-in-differences-causal-impact-and-synthetic-control-f8639c408268)。作者很好地介绍了寻找干预措施影响的三种方法，描述了每种方法的优点和缺点。

96.G. M. Duncan，[上的因果随机森林 https://econ . Washington . edu/sites/econ/files/old-site-uploads/2014/08/Causal-Random-Forests _ Duncan . pdf .](https://econ.washington.edu/sites/econ/files/old-site-uploads/2014/08/Causal-Random-Forests_Duncan.pdf.)这是一个简短的 PowerPoint 演示，描述了用于因果推理的随机森林。

97.A. Tanguy，贝叶斯分层建模(或更多 autoML 还不能取代数据科学家的原因(2020)，[在 https://towards Data science . com/Bayesian-hierarchy-Modeling-or-more-reasons-why-autoML-cannot-replace-Data-Scientists-yet-d 01 e 7d 571d 3d](/bayesian-hierarchical-modeling-or-more-reasons-why-automl-cannot-replace-data-scientists-yet-d01e7d571d3d)。作者说，“贝叶斯网络允许人们对变量之间的因果关系进行建模，弥补数据提供的信息的不足。”

98.Ctaeh，什么是贝叶斯信念网络？(第一部分)(2016)，[上 https://www . probabilistic world . com/Bayes-Belief-Networks-Part-1/](https://www.probabilisticworld.com/bayesian-belief-networks-part-1/)Bayes 信念网络通常被描述为利用条件概率和 Bayes 定理推断变量之间因果关系的努力。这里解释一下关于这些网络的直觉。

99.Ctaeh，什么是贝叶斯信念网络？(第二部分)(2016 年，[在 https://www . probabilistic world . com/Bayesian-belief-networks-Part-2/](https://www.probabilisticworld.com/bayesian-belief-networks-part-2/)在这一部分中，Cthaeh 通过展示 BBNs 背后的数学更深入一些。

100.C. Y. Wijaya，快速入门因果分析决策与 DoWhy:预测来自干预的因果效应(2021)，载于[https://medium . com/geek culture/A-quick start-for-Causal-Analysis-Decision-Making-with-DoWhy-2 ce 2d 4d 1 EFA 9](https://medium.com/geekculture/a-quickstart-for-causal-analysis-decision-making-with-dowhy-2ce2d4d1efa9)。作者描述了微软开发的基于图论和反事实分析生成因果模型的 DoWhy 包。提供了 Python 代码。这篇文章的一个很好的姊妹篇是由 DoWhy 开发人员 Amit Sharma 和 Emre Kiciman (2020)撰写的论文。

101.H. Naushan，使用自然语言处理的因果推理(2021)，载于[https://towardsdatascience . com/Causal-Inference-Using-Natural-Language-Processing-da 0 e 222 b 84 b](/causal-inference-using-natural-language-processing-da0e222b84b)。这篇文章在机器学习、因果推理和自然语言处理之间提供了一个很好的链接。在本质上，NLP 可以被看作是包含文本数据的 ML，使用它从文本中得出因果推论是一个新颖而有用的想法。

**限制:**

虽然这篇文章覆盖了很多领域，但不可能在一篇文章中探索大量重要的机器学习主题。许多其他类型的机器学习值得花费时间和精力来理解它们。示例包括强化学习(即以目标为中心的学习)和迁移学习(为一个目的训练、验证和测试模型，然后利用它实现完全不同的目的)。还有许多其他的例子。机器学习实用方法的领导者 Brownlee (2019)定义和描述了这些和其他 ML 主题。他的许多书都物有所值。

我在这里关注的只是关于媒体、数据科学和其他方面的短文。这些都是非常有用的，因为他们的务实的方法。作者提供了清晰而简要的解释，通常将理论、数学和建模技巧与 Python、R 或 SAS 代码的列表或链接以及许多更详细的参考资料相结合。许多人在 GitHub 链接或其他可以找到代码和注释的地方提供了更多的细节。

尽管如此，这仍然留下了至少五个限制。首先，要找到并描述每一篇好文章是不可能的，即使是上面包含的简短的主题列表。鼓励读者用自己的搜索来补充这个列表，以充分研究感兴趣的主题。

第二，上面包括的简要描述并不意味着包括批判性评论。没有一篇文章是完美的，但是为了简洁起见，我选择不详述任何错误，把它留给读者。

第三，我选择不提供同行评审的方法论出版物和教科书的列表，这些出版物和教科书更详细地描述了 ML 理论和应用。这个决定只是为了节省空间，我强烈推荐阅读这样的材料。如果读者用同行评议的文章和教科书材料补充上述文章，他们会发现理论、深度解释和实用方法的结合将产生理解上的收获，值得投入时间。

第四，上面的链接描述了如何进行 ML 和深度学习模型的训练、测试和验证。我特意决定不关注模型部署(即，在本地或大规模工业应用中使用这些模型需要什么)。这是一个独立的领域。关于部署的更多信息可以在 Ted Malaska 和 Shivnath Babu (2019)的优秀 O'Reilly 出版物中找到。

第五，也是最后一点，上面描述的文章集中在 ML 的机制上。近年来，出现了一个平行且非常重要的焦点，描述如何负责任地使用 ML 模型。关于这个主题的更多信息可以在我最近的一篇文章中找到(Ozminkowski，2021)，以及霍尔等人的另一篇伟大的 O'Reilly 出版物中找到(2021)。卡内基梅隆大学(2018)的数据科学和公共政策团队有一个名为 Aequitas 的优秀软件程序，该程序也促进了负责任的机器学习。Obermeyer 等人(2020)也提供了另一个关于如何避免机器学习中的偏见的很好的描述。

**结论:**

这篇文章提供了许多 ML 方法的链接，可以帮助数据科学家为他们的客户产生有用的见解。它是由没有免费的午餐定理激发的，该定理表明需要为任何分析寻找最好的学习者。这意味着测试许多不同的 ML 方法，以找到产生最佳(更准确、更敏感、更具体)预测的方法。

最近，人们对所谓的超级学习者进行了一些研究。这是一种结合来自许多不同 ML 模型的信息的方法，以产生更好的整体预测。超级学习者已经被证明能够更好地处理大量的输入 ML 方法。例如，可以使用上面链接中描述的许多方法作为超级学习者的输入。Romain Pirracchio (2016)提供了一个超级学习者如何在医疗保健分析中工作(即，预测在医院重症监护病房接受治疗的患者的死亡率)的很好的例子。介绍超级学习者的论文是由 Van der Laan 等人(2007)发表的，关于它的更多信息可以在那里找到。把超级学习者想象成应用于许多 ML 模型的 ML。

对于那些想以其他方式寻找最佳模型的人，Neo (2019)提供了许多其他关于 ML 和数据科学的网站的链接，这些网站也提供了价值。这些网站有些是免费的，有些不是。

机器学习和深度学习领域正在快速发展，跟上它的步伐是一项艰巨的任务。不可能在一篇文章中涵盖所有新的发展。我在这里的重点是许多永恒的方法，这些方法已经提供了价值，并将继续提供价值。我希望你喜欢阅读！

**参考文献:**

J.布朗利。机器学习中的 14 种学习类型(2019)，在[https://machinelementmastery . com/Types-of-Learning-in-Machine-Learning/](https://machinelearningmastery.com/types-of-learning-in-machine-learning/)

卡内基梅隆大学的数据科学和公共政策团队，Aequitas:一个用于机器学习的开源偏见审计工具包(2018 年)，在[http://www . datasciencepublicpolicy . org/our-work/tools-guides/Aequitas/](http://www.datasciencepublicpolicy.org/our-work/tools-guides/aequitas/)

I .古德费勒、y .本吉奥和 a .库维尔，《深度学习》(2016 年)，麻省剑桥:麻省理工学院出版社

页（page 的缩写）Hall，N. Gill 和 B. Cox,《负责任的机器学习》( 2021 年),塞瓦斯托波尔，CA: O'Reilly Media Inc .

T.Malaska 和 S. Babu,《通过现代工具重建可靠的数据管道》( 2019 年), Sebastopol，CA: O'Reilly Media Inc .

米（meter 的缩写））Maziarz,《经济学中的因果关系哲学》( 2020 年), Routledge-Taylor & Francis 集团，纽约

南 L. Morgan 和 C. Winship C,《反事实和因果推理:第二版》( 2015 年),剑桥大学出版社，英国剑桥

B.Neo，机器学习和数据科学 20 大网站(2019)，https://link.medium.com/zwUcGQCvz3 上的

Z.Obermeyer，R. Nissan，M. Stern 等人，《算法偏差剧本》(2020 年)，芝加哥布斯:应用人工智能中心。也在[https://www . FTC . gov/system/files/documents/public _ events/1582978/algorithm-bias-playbook . pdf](https://www.ftc.gov/system/files/documents/public_events/1582978/algorithmic-bias-playbook.pdf)

R.Ozminkowski，垃圾进垃圾出:拯救世界只是解决这个普遍问题的一个好理由(2021 年)，https://towardsdatascience . com/Garbage-in-Garbage-out-721 b5 b 299 bc1

R.Ozminkowski，什么导致什么，我们怎么知道？(2010 年)，[在 https://towards data science . com/what-causes-what-how-we-know-b 736 a 3d 0 eefb](/what-causes-what-and-how-would-we-know-b736a3d0eefb)

J.Pearl 和 D. MacKenzie,《为什么之书:因果的新科学》( 2018 年),纽约基础图书公司

R.Pirracchio，基于超级 ICU 学习者算法(SICULA)项目 MIMIC-II 结果的 ICU 死亡率预测(2016)，电子健康记录二次分析第 20 章，瑞士 Cham:麻省理工学院关键数据团队

A.Sharma 和 E. Kiciman，DoWhy:因果推理的端到端库(2020 年)，载于 arXiv:2011.04216 v1[统计。我]2020 年 11 月 9 日

米（meter 的缩写））J. Van der Laan、E.C. Polley 和 A.E. Hubbard AE,《超级学习者》( 2007 年),加州伯克利，加州大学伯克利分校生物统计工作论文系列，第 222 页