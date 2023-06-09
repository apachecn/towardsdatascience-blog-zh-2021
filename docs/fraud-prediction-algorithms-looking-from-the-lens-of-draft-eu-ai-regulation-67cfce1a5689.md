# 欺诈预测算法:从欧盟人工智能法规草案的角度看

> 原文：<https://towardsdatascience.com/fraud-prediction-algorithms-looking-from-the-lens-of-draft-eu-ai-regulation-67cfce1a5689?source=collection_archive---------25----------------------->

## 欧盟人工智能条例草案可能会对欺诈预测算法产生影响，可能需要审查和完善

![](img/6b2723680ccfe75b1dc965a545ee3364.png)

来源:vectorjuice 创建的人向量[(通过 Freepik)](https://www.freepik.com/free-vector/controller-reading-regulations-robot-artificial-intelligence-regulations-limitations-ai-development-global-tech-regulations-concept_11669237.htm#page=1&query=vectorjuice%20robot&position=26)

欺诈预测模型在金融服务和新兴技术行业(包括电子商务)中已经存在了十年或更长时间，它在多个其他行业中针对各种使用案例(例如保修欺诈预测)发展缓慢

欺诈或网络安全预测模型是一种典型的预测模型，其特定目的是在给定特定输入参数的情况下识别欺诈或网络安全威胁的指标。这些模型可以是统计模型或机器学习模型(这里称为“算法”)。这些算法中的许多主要是基于预先识别的模式和/或历史数据来识别潜在的不一致或不适当的交易；以及它的概率值。例如，金融服务试图识别在贷款时寻求信贷的潜在欺诈性申请，或者电子商务试图基于客户的一组数字足迹/动作来消除潜在的欺诈性交易。

更常见的是，这些算法将 3 个方面的信息作为输入(a)交易数据，(b)客户身份相关数据(即一种客户评分形式)和人口统计数据。算法会检查这些数据方面，以查看是否存在与代表欺诈或网络安全问题的预先识别/历史交易相似的模式。

在某些情况下，欺诈行为通常可以直接从交易中识别出来，而在某些情况下，它们可以从交易中推断出来或在交易中假设出来。推断或假设是指在这些情况下，数据所显示的内容并不能得出欺诈的结论，但却有可能导致欺诈。这些推论和假设是经过一段时间建立起来的。例如，来自过去欺诈案例比例较高的地区的个人申请的信贷；可能有被算法归类为欺诈的风险。训练数据集对于开发预测欺诈行为的平衡算法至关重要。不平衡的数据集或有偏差的数据集可能会导致本质上具有歧视性的不良结果。

考虑到确定欺诈交易的性质和复杂性，组织注入人在回路算法来验证预测的结果，从而消除误报。只有概率(比如说 60-70%)高于某个阈值的预测才会被考虑用于人在回路的评审。然而，这并不是一致的行业惯例，因为在许多流程中，交易是基于预测而被归类为欺诈的，而没有人工验证(“自动算法”)。值得注意的是，在某些情况下，例如，在线支付欺诈的预测模型，在某些情况下可能没有验证机制来消除误报(限于推断)，而不管是否存在人在回路中的审查或其他情况。

最近，算法经常因歧视和对种族、性别和/或其他因素的偏见而受到批评。这对于欺诈预测算法来说没有什么不同。在各个地区，监管机构正试图引入与管理算法相关的政策和框架。

欧盟(EU)也在考虑可以帮助管理算法的法律。拟议法规的草案强调了拟采取的措施和罚款。欧盟法规打算对违规公司处以 3000 万欧元或全球总营业额的 6%的罚款，以较高者为准。

除其他外，拟议的法规提到，如果算法预测犯罪或预测某人提供的信息的可信度，影响该人的人身自由，则应被列为高风险人工智能。高风险人工智能应进行符合性评估(即人工智能系统的审计),以确定采取了足够的措施来避免潜在的伤害或可预见的意外后果。此外，该规定提出，禁止任何让用户形成意见或做出不利于他们的决定的算法。对用户进行分类的社会评分也是禁止的，这反过来会对他们产生不利影响。

该条例还提出了一项义务，即在意识到事件发生后 15 天内向当局报告任何违规或违法行为。虽然全球的技术治理专业人士都在对拟议法规的充分性/不足性发表评论，但有必要了解此类法规对欺诈预测或广泛应用于各行各业的网络安全算法的潜在影响。

这些法规目前分别适用于欧盟的提供商(直接或通过第三方开发和部署算法的人)和用户，无论他们来自哪个国家或国籍。根据该法规，欺诈预测模型需要具备以下条件:

1.高质量数据集，用于在部署前对上述数据进行沙盒培训或测试。

2.清楚地阐明算法的预期用途，并评估可预见的意外后果。

3.展示为防止伤害所做努力的符合性声明，包括可能的误解或假设情景。

4.适当的用户界面，不会影响用户采取不利于他们的行动或决定。

虽然上述原则看似规范，但也存在与之相关的内在挑战。它们是:

1.历史欺诈数据集通常不完整且不完整，在描述欺诈的性质、证据以及与被归类为欺诈的交易相关的触发因素方面存在差距。因此，它们包含几个部分记录的推论和假设，从而暴露了缺乏欺诈的高质量数据集和嵌入在这种算法中的固有社会评分。

2.在没有指导方针或框架的情况下，定义和识别意外后果将是主观的。

3.符合性声明或评估要求组织详细说明在确定结果时的假设和推论，因此需要重新考虑预先存在的算法。

尽管上述原则显示出与提议的法规相关的复杂性，但是组织可以采取某些明确的步骤。它们是:

1.重新审视预先存在的欺诈预测或网络安全算法，以理解和评估培训数据、绩效指标(以特定的准确度)、假设和推论。

2.进行算法风险分析，以确定由此产生的潜在意外后果。记录风险，让风险承担者达成共识。

3.制定风险缓解计划，包括定义适当的风险处理和控制实施。

当务之急是，随着全球对人工智能危害的关注，这些法规将迅速成熟。在这种情况下，缺乏管理欺诈预测算法的结构化方法可能会对组织的声誉产生严重的不利影响。因此，重新访问-修订-恢复值得信赖和合规的欺诈预测或网络安全算法。

原文发表于 Linkedin Pulse [此处](https://www.linkedin.com/pulse/fraud-prediction-algorithms-looking-from-lens-draft-eu-narayanan/?trackingId=XwIVOXjQQnqglA%2FNz3wH5Q%3D%3D)