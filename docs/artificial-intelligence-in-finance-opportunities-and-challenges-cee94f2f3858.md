# 金融中的人工智能:机遇与挑战

> 原文：<https://towardsdatascience.com/artificial-intelligence-in-finance-opportunities-and-challenges-cee94f2f3858?source=collection_archive---------3----------------------->

![](img/fb50fc40a14077e60e3717ea2150d501.png)

杰弗里·布鲁姆在 [Unsplash](https://unsplash.com/s/photos/finance?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

人工智能(AI)不再是一个新生事物，这个领域正在以不断加快的速度发展。几乎每天都有某种新的发展，无论是宣布新的或改进的机器学习算法的研究论文，还是最流行的编程语言之一(Python/R/Julia)的新库，等等。

在过去，这些进步中有许多没能进入主流媒体。但这种情况也在迅速改变。最近的一些例子包括 AlphaGo 击败了 18 次世界冠军[1]，使用深度学习生成从未存在过的人类的逼真面孔[2]，或者深度假像的传播——图像或视频将人们置于从未实际发生的情况中。

除了这些有新闻价值的成就，在过去的几十年里，人工智能已经被广泛应用于几乎每个行业。我们可以在周围看到它。我们在网飞得到的推荐，我们收到的关于我们最近没有使用的网上商店额外折扣的电子邮件，仅举几例。

企业采用人工智能来获得竞争优势:

*   他们可以做出更好的、数据驱动的决策，
*   通过有效的定位或准确的推荐直接增加他们的利润，
*   通过尽早识别“犹豫不决”的客户来减少客户流失，
*   自动化一些重复的任务，人工智能可以比人类员工做得更快，
*   还有很多。

考虑到以上所有因素，难怪《哈佛商业评论》将数据科学家评为“21 世纪最性感的工作”[3]。

同样的“人工智能革命”正在影响金融行业。《福布斯》报道称，已经有“70%的金融服务公司正在使用机器学习来预测现金流事件、微调信用评分和检测欺诈”[4]。

在本文中，我们展示了人工智能在金融领域中影响最大的领域，以及使用了哪些技术来实现这一点。此外，我们还讨论了在金融领域进行数据科学研究时需要考虑的最重要的挑战。

# 人工智能在金融中的应用

我们首先提到金融行业中的一些关键领域，在这些领域中，人工智能产生了最大的影响，并提供了超过传统方法的附加价值。

## **信用评分**

机器学习在金融行业的一个重要应用是信用评分。许多金融机构，无论是大型银行还是较小的金融科技公司，都在从事放贷业务。为此，他们需要准确评估个人或另一家公司的信誉。

传统上，这种决定是由分析师在与个人进行面谈并收集相关数据点后做出的。然而，与过去的评分系统相比，人工智能可以使用更复杂的方法来更快更准确地评估潜在的借款人。为此，高级分类算法使用各种解释变量(例如，人口统计数据、收入、储蓄、过去的信用历史、在同一机构的交易历史等等)来得出最终分数，该分数决定了该人是否会获得贷款。

基于人工智能的评分系统的另一个优势是做出公正决策的潜力——没有人为因素，如银行员工在某一天的情绪或其他一些影响决策的因素。此外，它可能有利于没有广泛信用历史的人，让他们证明自己的可信度和偿还贷款的能力。

## **欺诈防范**

机器学习可以产生巨大影响的另一个关键领域是欺诈预防。对于欺诈，我们理解为任何欺诈活动，如信用卡欺诈、洗钱等。由于电子商务的日益普及、在线交易的数量以及第三方集成，前者近年来一直呈指数级增长。

尼尔森[5]的一份报告揭示了这种影响的潜在规模——“2019 年，全球基于卡的支付系统产生了 286.5 亿美元的总欺诈损失，相当于每 100 美元的总交易量中有 6.8 美元”。

过去，组织使用领域专家设计的硬编码规则来打击欺诈。然而，潜在的危险在于欺诈者发现了规则，然后能够利用该系统。基于人工智能的解决方案则不是这样，它可以随着时间的推移而进化，并适应数据中发现的新模式。

有许多机器学习算法专门从事异常检测，擅长发现欺诈性交易。这种算法可以筛选数以千计的交易相关特征(客户过去的行为、位置、消费模式等)。)并在出现故障时触发警告。

虽然许多传统的机器学习技术(如逻辑回归、支持向量机或决策树)已经可以达到合理的性能，但行业仍在不断推动改进。这是可能的，因为更复杂的算法可以更好地处理大量数据(包括观察数据和潜在特征)。除了 XGBoost 或 LightGBM 等 Kaggle 竞赛获胜者之外，欺诈检测是深度神经网络擅长的一个领域，因为它们能够处理非结构化数据并识别模式，而无需太多的特征工程。

![](img/11cfd653023728952ea519fef935c4c3.png)

[行政长官](https://unsplash.com/@executium?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在[广场](https://unsplash.com/s/photos/trading?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)拍照

## **算法交易**

“时间就是金钱”这句话在交易中最有意义，因为更快的分析意味着更快的模式识别，从而带来更好的决策和交易。当某种模式被发现，市场做出反应时，采取行动已经太晚，机会已经错过。

这就是为什么如此多的精力和金钱被投入到算法交易中，也就是说，复杂的系统在瞬间做出决定，并根据确定的模式自动执行交易。这样的系统可以大大超过人类交易者，也考虑到他们不受情绪的影响。Mordor Intelligence 的一份报告[6]指出，2020 年美国股票交易总量的大约 60%到 73%是由某种人工智能支持的系统处理的。

算法交易系统结合了机器和来自各个领域的深度学习的最新发展。虽然这些系统的某些部分可以专注于尝试预测资产回报(在合理的程度上)，但其他组件可能会使用基于计量经济学和资产配置理论的更传统的方法。

最近获得大量关注的是使用替代数据源来获得对竞争对手的优势。对象识别的进步有助于分析卫星图像，而自然语言处理(NLP)的最新技术允许从新闻文章、Twitter、Reddit 等来源进行准确的情感识别。

算法交易在数据科学的个体从业者中也越来越受欢迎，他们试图在本地机器或云中建立自己的交易系统。随着最近开始交易的难易程度的变化以及各种经纪人 API 的可用性越来越多，愿意尝试的人越来越多。

或者，数据科学家可以参加 numeri[7]—一项类似 Kaggle 的数据科学挑战，目标是根据提供的数据(匿名)和潜在的外部替代数据来预测股市回报。该公司可以被描述为人工智能主导的对冲基金，它汇总了参与个人做出的预测，并允许他们以计价单位(该基金自己的加密货币)赚取他们的收益份额。

## **机器人顾问**

鉴于通货膨胀对我们储蓄的影响，以及把钱存在储蓄账户中不再有利可图的事实，越来越多的人对被动投资感兴趣。这正是机器人顾问发挥作用的地方。它们是财富管理服务，AI 根据投资者的个人目标(包括短期和长期目标)、风险偏好和可支配收入，提出投资组合建议。投资者只需每月存入资金(或自动转账)，其他一切都由他们来处理——从选择投资的资产、实际购买资产，然后可能在一段时间后重新平衡投资组合。所有这些都是为了确保客户能够以最佳方式实现他们的预期目标。

这种系统的主要优点是，它们对客户来说非常容易使用，并且不需要任何金融知识。自然，成本也起着重要作用——机器人顾问往往比人力资产管理公司的服务更便宜。

## **个性化银行体验**

银行业试图利用人工智能的力量为每个人提供个性化的银行体验。一个例子可能是聊天机器人，它们越来越难以从真正的人类顾问中辨别出来。使用先进的自然语言处理技术，他们可以理解客户的意图，并试图为他们指出正确的方向。例如，他们可以帮助用户更改密码、检查当前余额、安排交易等。此外，这种聊天机器人通常可以识别客户的情绪，并在此基础上调整他们的反应。如果他们检测到消费者非常生气，可能有必要将他们与人类顾问联系起来，以尽快解决问题，避免进一步的挫折。智能聊天机器人不断增强的能力还可以通过减少呼叫中心的工作量来节省成本。

但聊天机器人并不是金融领域唯一的个性化体验。许多机构利用他们拥有的大量数据来分析消费者的消费行为，并提供量身定制的金融建议，帮助他们实现目标。这种服务可以包括如何减少每月开支的技巧，或者以简单和用户友好的方式向客户展示这些开支，例如，本月你花费最多的三个地方。这些机构也可以让你知道，一些经常性的转移将很快发生，你的帐户上没有足够的资金。所有这些只是现代金融公司能够为客户提供的服务的冰山一角。

## **过程自动化**

最后，当谈到自动化时，人工智能提供了很多。使用高级光学字符识别(OCR)可以显著提高通常由员工处理的普通且耗时的任务的效率。例如，数字化文档、处理表单或从文档中提取相关信息。

许多金融机构要么使用专用软件，要么为 KYC(了解您的客户)流程构建内部解决方案。在金融领域，通常需要提供某种形式的 ID 以避免欺诈。许多新经纪人和金融科技公司让这个过程变得非常简单——你用手机扫描你的 ID，然后自拍以验证与 ID 匹配。在后台，一个基于人工智能的解决方案验证是否有匹配，但同时检查 ID 是否不是假的，以及图片是否没有什么值得警惕的。处理图像是深度学习和卷积神经网络(CNN)等架构显示出非常有前途的结果的领域。

# 人工智能在金融领域的挑战

描述了人工智能在金融领域产生影响的关键领域后，讨论与之相关的潜在挑战才是有意义的。

## **数据质量**

数据科学领域有一句格言——“垃圾进，垃圾出”。虽然适用于任何与数据相关的工作，但它在金融行业中至关重要。一天的损坏数据，甚至是输入到交易算法中的几个错误的观察值，都会对整个系统产生可怕的后果，导致糟糕的交易和财务损失。

这就是为什么在金融领域的这些关键领域，拥有干净、有条理、维护良好的数据源作为机器学习模型的输入非常重要。如果数据发生了任何不希望的事情，或者引入了不合适的东西，必须有一种方法在整个管道中快速跟踪它，确定问题并修复它。一些公司基于这一概念开展业务，并为数据提供类似 git 的版本控制。

![](img/0caa3141cefc25befc38b8991ddb998c.png)

弗兰基·查马基在 [Unsplash](https://unsplash.com/s/photos/data?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

## **有偏差的数据**

人工智能做出的决策会对金融机构的客户产生重大影响。一个被拒绝的贷款申请可以改变一个人的一生。这就是为什么需要特别注意消除数据中的任何偏差来源。凯茜·奥尼尔(Cathy O'Neil)的《数学毁灭的武器》(Weapons of Math Destruction)【8】(*免责声明*:参考链接)详细阐述了数据偏差的几个例子及其有形的后果。

## **降维**

金融机构坐拥大量数据，因为一笔交易可能有数千个数据点。这也是为什么行业中的信噪比非常低，这使得数据科学家的工作同时非常具有挑战性和趣味性。

许多机器学习技术随着观察的数量而很好地扩展，但是当特征的数量爆炸时，它们会受到影响。也就是说，分析师必须要么执行某种特征选择(基于领域知识或自动进行)，要么尝试降低数据的维度。对于后者，他们可以使用成熟的技术，如主成分分析(PCA)、线性判别分析(LDA)或更现代的技术，如 t 分布随机邻居嵌入(t-SNE)或均匀流形逼近和投影(UMAP)。

## **黑匣子**

在许多行业中，数据科学家非常渴望使用最新、最先进的技术，这些技术可以在幕后执行大量复杂的计算，并提供非常准确的预测。尽管在许多情况下，这可能是一件合理的事情，但在金融领域，事情远不止如此。

金融行业受到严格监管(这是有充分理由的)，算法做出的许多决定必须被该机构完全理解。想象一下，一个人的信用评分很低，贷款申请被拒绝了。然后，这样的人可以提出索赔，并要求详细解释导致这一决定的所有因素。

这就是为什么模型可解释性在金融行业中起着至关重要的作用。虽然使用最新和最棒的神经网络架构可能很有吸引力，并提供额外的几个百分点的准确性(或用于评估的其他性能指标)，但它通常不是适合工作的正确工具，而是选择更简单的模型(如逻辑回归或决策树)。这是因为有了这样的模型，分析师总能解释是什么因素塑造了决策。

此外，可解释的人工智能领域发展非常迅速，研究人员致力于模型不可知的方法，允许解释相对简单和非常复杂的模型的决定。这种技术的例子包括 LIME(局部可解释模型不可知解释)或一种基于博弈论的方法，称为 SHAP (SHapley 加法解释)。

# **结论**

在本文中，我们描述了金融行业中广泛理解的人工智能可以为公司及其客户提供大量增值的领域。我们还讨论了在实现这些技术时需要解决的一些关键挑战。这些列表绝不是详尽的，因为人工智能和金融领域都在不断变化，并适应每天的进步。可以肯定的一点是，我们生活在一场基于人工智能的革命的尖端，这场革命对企业和个人都产生了影响。

喜欢这篇文章吗？成为一个媒介成员，通过无限制的阅读继续学习。如果你使用[这个链接](https://eryk-lewinson.medium.com/membership)成为会员，你将支持我，不需要额外的费用。提前感谢，再见！

您可能还会对以下内容感兴趣:

</introduction-to-backtesting-trading-strategies-7afae611a35e>  </mplfinance-matplolibs-relatively-unknown-library-for-plotting-financial-data-62c1c23177fd>  </learn-what-a-depth-chart-is-and-how-to-create-it-in-python-323d065e6f86>  

***来自《走向数据科学》编辑的提示:*** *虽然我们允许独立作者根据我们的* [*规则和指导方针*](/questions-96667b06af5) *发表文章，但我们并不认可每个作者的贡献。你不应该在没有寻求专业建议的情况下依赖一个作者的作品。详见我们的* [*读者术语*](/readers-terms-b5d780a700a4) *。*

# 参考

[1][https://deep mind . com/research/case-studies/alpha go-the-story-迄今为止](https://deepmind.com/research/case-studies/alphago-the-story-so-far)

[2]https://thispersondoesnotexist.com/

[3][https://HBR . org/2012/10/data-科学家-21 世纪最性感的工作](https://hbr.org/2012/10/data-scientist-the-sexiest-job-of-the-21st-century)

[4]AI 在金融服务中的采用状况—[https://www . Forbes . com/sites/louiscolumbus/2020/10/31/The-State-Of-AI-Adoption-In-Financial-Services/？sh=42c39ad12aac](https://www.forbes.com/sites/louiscolumbus/2020/10/31/the-state-of-ai-adoption-in-financial-services/?sh=42c39ad12aac)

[5]卡及移动支付行业统计|尼尔森报告图表存档—[https://Nilson Report . com/publication _ chart _ and _ Graphs _ Archive . PHP？1=1 &年=2020](https://nilsonreport.com/publication_chart_and_graphs_archive.php?1=1&year=2020)

[6]算法交易市场趋势、规模| 2021 年至 2026 年行业预测与 COVID 影响—Mordor Intelligence—[https://www . Mordor Intelligence . com/Industry-reports/Algorithmic-Trading-Market](https://www.mordorintelligence.com/industry-reports/algorithmic-trading-market)

[7]数字—[https://numer.ai/](https://numer.ai/)

[8]奥尼尔，凯茜。*数学毁灭武器:大数据如何增加不平等并威胁民主*。皇冠，2016。