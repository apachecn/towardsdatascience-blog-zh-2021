# 为什么非营利组织应该关注合成数据

> 原文：<https://towardsdatascience.com/why-nonprofits-should-care-about-synthetic-data-ab1d327908dc?source=collection_archive---------15----------------------->

## 合成数据如何帮助非营利组织改善其业务运营及其对服务对象的影响

![](img/6066bf05954e5ecb4dec23329a6aac4d.png)

版权所有 2021 Gretel.ai

# TL；速度三角形定位法(dead reckoning)

我是 Gretel 公司的机器学习研究员，这是一家为开发者开发隐私工程工具的公司。11 月，我参加了一个小组，讨论为什么合成数据对非营利组织很重要，以及他们如何使用它。用例是无止境的，跨越医疗保健、教育、经济发展等行业。很多创新取决于正在成熟的技术创新以及这些创新如何解决非营利组织的各种痛点。非常感谢 [DataKind](https://www.datakind.org/) 邀请 Gretel 在 [NetHope 峰会](https://www.nethopeglobalsummit.org/)上与 [Medic](https://medic.org/) 谈论这些问题。

# 介绍

合成数据被认为是[最重要、最激动人心的新兴技术创新之一](https://blogs.gartner.com/andrew_white/2021/07/24/by-2024-60-of-the-data-used-for-the-development-of-ai-and-analytics-projects-will-be-synthetically-generated/)。它将使营利性公司能够共享数据，特别是在使用有差异的私人合成数据时，因为它消除了隐私相关许可问题的摩擦，并允许在预生产管道中进行更快速的技术开发。此外，合成数据可用于支持太小或数据集严重失衡的数据集。这将帮助组织建立更复杂的机器学习能力，这些能力通常非常渴求数据。然而，这些好处不仅有助于营利性部门，也能极大地影响公共部门。

我很高兴受到 DataKind 的邀请，在 NetHope 峰会上与 Medic 一起在一个关于合成数据的小组上发言。这是一个完美的机会来展示合成数据的力量，以及为什么非营利组织也开始思考它是重要的。营利性组织经历的每一个痛点都会被非营利性组织放大。以下是三个主要挑战以及合成数据如何应对这些挑战:

# (1)保护数据隐私

许多非营利组织和非政府组织与弱势群体打交道，[在这些群体中，隐私风险更高](https://www.fastcompany.com/90317495/another-tax-on-the-poor-surrendering-privacy-for-survival)。这些人口面临着技术滥用，如[监控系统](https://urbanomnibus.net/2020/01/caught-in-the-spotlight/)、[累犯算法](https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing)和[政府福利系统](https://www.nytimes.com/2018/05/04/books/review/automating-inequality-virginia-eubanks.html)。非营利组织明白，这种滥用可能发生在他们服务的人群身上，因此必须对他们收集的任何数据加以保护。 [‍](/common-misconceptions-about-differential-privacy-5f2c37953cdd)

[有区别的私人合成数据](/common-misconceptions-about-differential-privacy-5f2c37953cdd)是非营利组织可以减轻这种风险的一种方式，释放了一些以前被认为风险太大的创新和实践，例如合作[打击人口贩运](https://www.iom.int/news/iom-microsoft-collaboration-enables-release-largest-public-dataset-bolster-fight-against-human-trafficking)(在我们的小组讨论中，一名观众分享了一个用例！).尽管这不一定能防止模型开发中数据的不完美使用，但它确实能保护弱势群体的信息不被泄露和用于其他邪恶目的。 **‍**

# (2)收集和利用有限的数据集

但是，即使我们能够共享数据来改进分析、洞察和模型构建，公共部门也不从事收集数据的工作。致力于加强公民社区纽带的研究团体公民社会法律家庭委员会(Law Family Commission on Civil Society)于 2021 年 10 月发布了一份报告，描述了公共部门如何因糟糕的数据做法而落后于私营部门，例如使用 pdf 等“不可读格式”来存储数据。 [‍](https://www.communityforce.com/nonprofits-are-faring-poorly-with-data-collection-and-use/)

[收集数据既费钱又辛苦](https://www.communityforce.com/nonprofits-are-faring-poorly-with-data-collection-and-use/)，做对更是难上加难。定义收集的信息的粒度、节奏和类型本身就是一项全职工作。很少有非营利组织有预算或员工带宽来致力于强大的内部数据收集和管理系统。不可避免的是，更接近非营利组织核心使命的其他活动几乎总是优先于这些困难的任务，尤其是当投资回报难以计算的时候。

这就是合成数据大放异彩的地方。如果一个非营利组织已经收集了足够的数据(数量未知，但少于一次完整的数据收集)，那么他们可能能够训练一个合成模型来增加一个相对较小的样本。因为如果有足够的真实数据来源，那么即使只有一点点也可以转化为无限量的合成数据！随着数据集的扩大，非营利组织对其战略计划和每个计划的绩效有了更全面的了解，他们可以做出更明智的选择，将稀缺资源分配到哪里，从而最大限度地提高效益。

我在会上讨论的一个真实世界的例子是与 [Microcred](https://www.datakind.org/projects/advancing-financial-inclusion-in-senegal-using-predictive-modeling) 合作建立的模型 DataKind。这种模式本可以帮助 Microcred 在贷款方面做出更好的决策，因此它变得更加高效和包容。然而，Microcred 只收集获得贷款的人的数据。因此，该模型只能用于那些获得贷款的人，而不能用于那些被拒绝的人。这限制了该模式的效力和影响。收集这些被拒贷款的数据需要几个月甚至几年时间。但如果 Microcred 在未来利用合成数据，他们将能够在更短的时间跨度内收集数据，并在更好的隐私保证下构建其数据集的其余部分。

# (3)共享数据

隐私保护数据带来的最大好处之一是能够安全地共享数据集。将孤立的私人信息转化为团队可以合作的匿名工件可以引发新的讨论和发现，从而为所服务的弱势群体带来更好的结果。

英国的一些公务员已经开始倡导使用合成数据来改善政府对数据的使用。例如，在最近由几个公共机构主办的[公务员竞赛](https://www.datachallenge.uk/)期间提出的 200 多个想法中，合成数据被评为最佳之一，作为一种工具，它可以在公共部门中用于，除其他外，“通过工作和养老金部、英国税务海关总署以及英国签证和移民局之间更丰富的数据交换，提高对福利和税务欺诈的检测。”通过赋予公共部门团体与数据合作的权力，可以发现新的见解，弥合差距，并为所服务的人群建立更好的系统。

# 结论

非营利部门对任何健康社会的运作都至关重要。它有助于确保贫困的弱势群体得到照顾，并改善全世界数百万人的生活质量。为了继续向个人提供这些基本服务，并在更大范围内成为一股向善的力量，非营利组织必须有效地利用数据。通过使用像[格雷特](https://gretel.ai/)这样的合成数据工具，他们可以打破隐私瓶颈，开启以前似乎难以置信的创新。

现在的关键是确保各地的非营利组织都知道这些高效、廉价(在某些情况下甚至免费)的工具已经可以为他们所用。我希望你能和我一起传播这个好消息！

你可以[免费开始](https://gretel.ai/signup)合成数据。