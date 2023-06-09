# 利用因果关系改进自然语言处理

> 原文：<https://towardsdatascience.com/improving-nlp-with-causality-2dec1fa90b74?source=collection_archive---------10----------------------->

## 因果推理在提高自然语言处理模型的健壮性、公平性和可解释性方面的潜在用途

![](img/3cc331b960d9c3b0f418370e5a1c3830.png)

克里斯·劳顿在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

两年前，[谷歌宣布正在使用一种人工智能语言模型，命名为 BERT，以改进谷歌搜索](https://blog.google/products/search/search-language-understanding-bert/)；当时大约有 10%的搜索使用了这个词。一年后，在一篇题为“[人工智能如何为更有帮助的谷歌](https://blog.google/products/search/search-on/)提供动力”的文章中，该公司报告称，100%的搜索查询都在使用 BERT。然而，这些公告并没有包括模型中编码的性别和种族偏见的信息。自从 BERT 公开发布以来，许多研究人员已经注意到模型中存在的偏差( [Kurita 等人 2019](https://aclanthology.org/W19-3823/) ， [Bhardwaj 等人 2020](https://arxiv.org/abs/2009.05021) ， [Bender 等人 2021](https://dl.acm.org/doi/abs/10.1145/3442188.3445922) )。然而，谷歌尚未解决围绕这一如今无处不在的模式的许多紧迫的伦理问题。抛开令人失望的问责缺失，我们可以选择专注于解决方案；因此，本文主要讨论如何使用因果关系来改进像 BERT 这样的 NLP 模型。

在[之前的一篇文章](/causal-inference-using-natural-language-processing-da0e222b84b)中，我提到了最近的一篇计算语言学调查论文([费德等人，2021a](https://arxiv.org/abs/2109.00725) )，该论文着眼于因果关系和 NLP 模型之间的关系。我的[前一篇文章](/causal-inference-using-natural-language-processing-da0e222b84b)关注的是如何将 NLP 方法用于文本变量进行因果推理，而本文关注的是反向连接。在这里，我探索因果推理如何帮助改进传统的 NLP 任务，如文本分类、情感分析或文本生成。我首先简要介绍像 BERT 这样的 NLP 模型，强调其固有的弱点，并提出因果关系可以解决现有缺点的广泛方法。接下来，我将讨论伪相关性，并介绍一个实际的案例研究，该研究将在本文的剩余部分中使用。接下来，我将重点关注健壮性和敏感性——特别是因果驱动的数据增强和分布标准可以克服挑战的方式。这导致了对 NLP 模型中的公平性和偏见的讨论，以及如何使用因果关系来解决提高公平性和减少偏见的目标。最后一节讨论了因果关系在提高 NLP 模型的可解释性和可解释性中的应用。最后，我对未来的工作提出了一些想法，这些工作将进一步探索因果关系和 NLP 之间的关系。

## **相关预测模型**

[BERT](https://en.wikipedia.org/wiki/BERT_(language_model)) 代表了 NLP 的一个突破时刻， [Transformer 架构](https://arxiv.org/abs/1706.03762)的使用和[上下文嵌入的双向特性](https://arxiv.org/abs/1810.04805)已经被许多研究人员采用，衍生出了诸如 [RoBERTa](https://arxiv.org/abs/1907.11692) 、 [M-BERT](https://arxiv.org/abs/1906.01502) 、 [ALBERT](https://arxiv.org/abs/1909.11942) 和 [ERNIE](https://arxiv.org/abs/1905.07129) 等模型。然而，这些架构不区分原因、结果和混杂因素。[费德在阿尔。(2021a)](https://arxiv.org/abs/2109.00725) 解释这些模型并不试图确定因果关系。因此，“一个特征可能是一个强大的预测器，即使它与期望的输出没有直接的因果关系”( [Feder et al .，2021a](https://arxiv.org/abs/2109.00725) )。为了更好地介绍这些以芝麻街角色命名的模特，我推荐这本由 Jay Alammar 撰写的[视觉入门。](https://jalammar.github.io/illustrated-bert/)

根据 [Feder et al. (2021a)](https://arxiv.org/abs/2109.00725) ，当前的 NLP 模型可以被描述为“相关性预测模型*”*，其中预测是由于相关性(可能是虚假相关性)而不是因果关系。因此，尽管取得了最先进的结果，这些相关性预测模型可能是不可信的，并可能导致分布外设置的错误([费德等人，2021a](https://arxiv.org/abs/2109.00725) )。关于信任， [Jacovi 等人(2021)](https://arxiv.org/abs/2010.07487) 探索了人工智能模型的可信度——他们讨论了“有保证的”信任意味着什么，以及如何通过内在推理和外在行为来实现信任。他们提出了设计可信人工智能的方法，一个关键的发现是信任和可解释人工智能(XAI)之间关系的重要性——这是使用因果关系来提高人工智能可解释性的进一步理由。此外， [McCoy et al. (2019)](https://aclanthology.org/P19-1334/) 展示了人工智能语言模型如何在错误的原因下往往是正确的，并且会由于依赖易错的语法试探法(虚假的“快捷方式”)而在非分布设置中出错。显而易见，缺乏因果关系会导致难以解释的模型，而这些模型的概括能力很差。

相关性预测模型还存在另外两个问题:“用户组之间不可接受的性能差异，以及他们的行为太难以理解而无法纳入高风险决策的问题”( [Feder 等人，2021a](https://arxiv.org/abs/2109.00725) )。例如，一项名为“[男性也喜欢购物](https://arxiv.org/abs/1707.09457)”的电子商务研究讨论了性别偏见放大，并展示了这些人工智能模型如何在不同用户群之间表现出不同的表现([赵等人，2017](https://arxiv.org/abs/1707.09457) )。此外，如上所述，像 BERT 这样的黑盒模型的一个常见问题是，它们缺乏用于高风险决策的透明度( [Guidotti 等人，2018](https://arxiv.org/abs/1802.01933) )。在处理人的生命或生计受到威胁的场景时，依赖内部逻辑被隐藏的 AI 模型是不道德的。

解决相关预测模型的这四个已知缺点的解决方案是将因果观点应用于模型开发和验证。最近的研究表明，可以“利用观察值和标签之间的因果关系知识，将虚假相关性形式化，并减轻预测者对这些相关性的依赖”( [Feder 等人，2021a](https://arxiv.org/abs/2109.00725) )。换句话说，理解数据生成过程(DGP)的因果结构可以帮助识别潜在的混杂因素。例如， [Veitch 等人(2021)](https://arxiv.org/abs/2106.00545) 建议使用压力测试作为一种形式化要求的方式，即改变输入的不相关部分不应改变模型的预测(反事实不变性)。这项工作还表明，反事实不变性的意义和含义取决于数据的真正潜在因果结构。因此，不同的因果结构需要不同的正则化方案来诱导反事实不变性([维奇等人，2021)](https://arxiv.org/abs/2106.00545) 。

因果关系的另一个优点是，它提供了一种语言来说明和推理公平条件。 [Kilbertus 等人(2017)](https://arxiv.org/abs/1706.02744) 探索了如何使用因果推理来避免歧视，他们通过用因果推理的语言来构建歧视问题来做到这一点。他们声称这是必要的，因为观察标准有内在的局限性，阻止他们决定性地解决公平问题。这意味着，与其关注什么是正确的公平标准，不如关注应该对因果 DGP 做出什么样的假设。

此外，当涉及到测试时，解释预测的任务可以通过用反事实的术语来表述预测来完成。Feder 等人(2021b) 在 BERT 上测试了这种方法，在最近的一篇论文中，他们概述了通过反事实语言模型进行因果模型解释的框架。他们的方法是微调像 BERT 这样的深度情境化嵌入模型，使用从预测问题的因果图中导出的辅助对抗性任务。他们表明，有可能选择辅助对抗性训练前任务，使伯特有效地学习一个感兴趣的概念的反事实表征。然后，这种反事实表示可以用来估计概念对模型性能的真正因果影响。本质上，“一个反事实的语言表示模型被创建，它不受测试概念的影响，这使得它有助于减轻训练数据中存在的偏见”[(费德等人，2021b)](https://arxiv.org/abs/2005.13407) 。

虽然最近的因果动机研究给了我们有希望的结果，但由于当前 NLP 模型带来的鲁棒性和可解释性挑战，“有必要开发新的标准来学习超越利用相关性的模型”([费德等人，2021a](https://arxiv.org/abs/2109.00725) )。下一节通过一个实际例子强调了这些挑战，并更详细地讨论了伪相关性。

## **虚假相关性&案例研究**

随后的章节讨论了关于稳健性的伪相关性问题，以及处理公平性和可解释性问题的因果方法。为了有助于下面几节中的解释，我们需要一个实际的例子来说明这些挑战。因此，我依赖一个取自之前提到的调查论文的例子( [Feder 等人，2021a](https://arxiv.org/abs/2109.00725) )。考虑这样一个场景，我们希望构建一个分类器来预测诊断/医疗状况，给定一个书面的临床叙述，并使用来自多家医院的带标签的训练集。下图显示了此示例，其中 Z 代表医院，Y 是医生指定的诊断标签，W 是书面的临床叙述，Y_hat 是来自分类器的预测。

![](img/ede2ae61ceb4b8651b740130ed4f5550.png)

分类问题，其中预测(Y_hat)取决于临床叙述(W)，临床叙述本身受诊断标签(Y)和医院(Z)的影响，这两者恰好相关。来源:[费德等人，2021a](https://arxiv.org/abs/2109.00725) 。

分类器 Y_hat(W)将临床叙述(W)的文本作为输入，并输出诊断预测。然而，叙述是基于医生的诊断(Y ),也受医院 Z 使用的写作风格的影响。在这种情况下，根据[费德等人的说法(2021a](https://arxiv.org/abs/2109.00725) ),我们希望在保持标签(Y)不变的情况下对医院 Z 进行干预。反事实地，我们将医院设置为( *z* )，这给了我们反事实叙事 W( *z* )，而 Y 是固定的。给定反事实叙事 W( *z* )的输入，分类器 Y_hat(W)的输出是反事实预测 Y_hat(W( *z* ))。

因为训练数据具有来自多个医院的记录，所以可能存在这样的医院，在该医院中，患者更有可能被诊断为具有特定状况。也可能是由于特定医院的惯例，该医院的医生倾向于使用独特的文本特征。如果我们要使用 BERT 建立一个相关性预测模型，该预测器将使用携带医院信息(Z)的文本特征(X)，这些特征对于预测任何特定医院内的诊断都是无用的( [Feder 等人，2021a](https://arxiv.org/abs/2109.00725) )。因此，挑战在于较差的分发外性能。由于写作风格和医疗诊断之间的虚假相关性，预测对于训练数据之外的医院将无效。

[Feder 等人(2021a)](https://arxiv.org/abs/2109.00725) 指出，出现伪相关性必须满足两个条件:首先，在训练数据中，需要有一个因子(Z)来提供关于特征(X)和标签(Y)的信息，其次，Y 和 Z 必须以某种方式依赖于训练数据，而这种方式一般不能保证成立。在这个医疗诊断分类器示例中，如下图所示，Z 与 y 相关。

![](img/ede2ae61ceb4b8651b740130ed4f5550.png)

医疗诊断分类器示例，其中诊断标签(Y)与医院(Z)相关。资料来源:[费德等人，2021a](https://arxiv.org/abs/2109.00725) 。

医院 Z 和标签 Y 之间的这种虚假关联存在于训练数据中；因此，预测器将学习 X 中提供医院 z 信息的部分。然而，该预测器并不稳健，因为特征 X 和标签 Y 之间的学习关系在部署期间将不会成立( [Feder 等人，2021a)](https://arxiv.org/abs/2109.00725) 。下面的章节描述了如何利用因果关系来解决这类问题。

## **灵敏度和鲁棒性**

当处理像 BERT 这样依赖相关性进行预测的人工智能语言模型时，确保预测不会因为错误的原因而变得正确是至关重要的。有两种类型的评估可用于这项任务:不变性测试和敏感性测试。不变性测试“评估预测是否受到与标签没有因果关系的扰动的影响” [(Feder 等人，2021a)](https://arxiv.org/abs/2109.00725) 。另一方面，敏感性测试“应用的扰动在某种意义上应该是转换真实标签所需的最小变化”( [Feder 等人，2021a](https://arxiv.org/abs/2109.00725) )。因果动机不变性测试的目的是观察当给定反事实输入时，预测者是否表现不同。如果 Z 是文本中应该与标签 Y 因果无关的原因的标签，那么反事实输入将是 X(Z = *~z* )。根据 [Veitch 等人(2021)](https://arxiv.org/abs/2106.00545) 的说法，在某些情况下，一个其预测在这些反事实中不变的模型在 Y 和 z 之间具有不同关系的测试分布中表现更好。

敏感性测试类似于不变性测试，因为它们也是对反事实的评估；但不同的是，标签 Y 被改变了，但所有其他对 X 的因果影响保持不变( [Kaushik et al .，2020](https://arxiv.org/abs/2010.02114) )。敏感性测试的反事实可以表示为 X(Y = ~y)。敏感性和不变性测试是测试稳健性的一种方式，并且有几种学习预测器的方法可以通过这种测试。这些方法是将数据因果结构的领域知识结合到学习目标中的一种方式，这意味着它们是因果驱动的方法。在这篇文章中，我介绍了[费德等人(2021a)](https://arxiv.org/abs/2109.00725) 描述的两种方法:反事实数据扩充和因果驱动的分布标准。

数据扩充是指构建反事实实例并将其纳入训练数据。这种方法对不变性和敏感性都有效。例如，利用不变性，可以向学习目标添加一项，该项惩罚反事实对的预测中的不一致(例如，X(Z = *z* 和 X(Z = *~z* ))。如果我们测试敏感性，干预将在标签 Y 上，我们将用标签反事实 X(Y = ~y)来增加训练数据。这将“降低对噪声的敏感性，提高域外泛化能力”( [Feder 等人，2021a](https://arxiv.org/abs/2109.00725) )。

有几种方法可以生成反事实的例子，如手动后期编辑、关键字的启发式替换或自动文本重写( [Feder et al .，2021a](https://arxiv.org/abs/2109.00725) )。手动编辑的第一种选择通常是准确的，但是昂贵的。使用关键字的第二种选择只在某些场景下有效；例如，当反事实可以通过像代词这样的词的局部替换来获得时。然而，这种关键字方法不能“保证流畅性或覆盖所有感兴趣的标签和协变量，并且难以跨语言推广”( [Feder 等人，2021a](https://arxiv.org/abs/2109.00725) )。最后一个选项是完全生成的方法，其目标是“将手动编辑的准确性和覆盖范围与词法试探法的便利性结合起来”( [Feder 等人，2021a](https://arxiv.org/abs/2109.00725) )。

对于所有这三种选择，都存在引入虚假相关性的风险。例如，如果关键字词典不完整，关键字替换方法可能会引入新的虚假相关性( [Feder 等人，2021a](https://arxiv.org/abs/2109.00725) )。手动编辑和自动文本生成的其他两个选项具有相同的问题，即反事实的生成也会引入新的虚假关联。反事实的例子可能是“强有力的，因为它们直接解决了因果推断固有的缺失数据问题”([费德等人，2021a](https://arxiv.org/abs/2109.00725) )，但是反事实的数据增强容易受到虚假相关性的影响。因此，另一种选择是“直接对观察数据进行操作的因果动机分布标准”([费德等人，2021a](https://arxiv.org/abs/2109.00725) )。

根据定义，反事实不变预测器将满足可从 DGP 的因果结构中导出的独立性标准( [Veitch 等人，2021)](https://arxiv.org/abs/2106.00545) 。通过推导不变预测器的分布特性，我们可以确保这些特性被训练的模型所满足。对于我们的医疗示例，我们希望确保改变医院书写风格 Z 不会改变诊断 Y，因为这是一个虚假的相关性。根据 [Feder et al. (2021a)](https://arxiv.org/abs/2109.00725) 这种对 Z 的反事实不变性，给定一个预测因子 *f* 和文本特征 X，可以形式化为*f*(X(*Z*)=*f*(X(*Z’*))对于所有*Z；*。这里，Z 和 Y 都是 X 的原因，因此反事实不变预测器将给出独立于协变量 Z 的预测 *f* (X ),条件是真实标签 Y。也就是说，“标签不是文本的影响”( [Feder 等人，2021a)](https://arxiv.org/abs/2109.00725) 。

除了为不应该影响预测的文本原因设置明确的标签 Z(这是我们的医学示例的情况)之外，还有两种其他的方法来获得分布标准。第一种选择是将训练数据视为“源自一组有限的环境，其中每个环境在原因上具有唯一的分布，但是 X 和 Y 之间的因果关系在环境之间是不变的”( [Feder 等人，2021a)](https://arxiv.org/abs/2109.00725) 。环境不变性标准的目的是确保我们有一个表示，其中相同的预测值在每个环境中都是最佳的。这可以被认为是领域泛化。另一个选择是控制混杂；如果 Z 是一个混杂因素，根据[费德等人(2021a)](https://arxiv.org/abs/2109.00725) 的说法，一个与将观察概率转换为干预概率的“后门调整”相关的因子分解可用于控制 Z 的混杂特征([珀尔，2000](https://en.wikipedia.org/wiki/Causality_(book)) )。

与数据扩充相比，分布式标准需要“比监督学习问题通常可用的数据更丰富的训练数据”( [Feder 等人，2021a](https://arxiv.org/abs/2109.00725) )。因此，方法的选择应取决于是否更容易获得分布标准所需的观察数据，或者是否更容易创建反事实实例来扩充训练集( [Feder 等人，2021a](https://arxiv.org/abs/2109.00725) )。下一节讨论公平和偏见，这是可以通过数据扩充或分配标准解决的问题。

# **公平和偏见**

当谈到确保模型公平和无偏见时，“因果关系提供了一种语言，用于指定跨种族和性别等人口统计属性的期望公平条件”( [Feder 等人，2021a](https://arxiv.org/abs/2109.00725) )。例如，[哈特等人(2016)](https://arxiv.org/abs/1610.02413) 表明，需要进行因果分析，以确定观察到的数据分布和预测是否会引起公平性问题。他们讨论了反歧视法如何要求人工智能模型不会延续现有的不平等，这项工作通常专注于“受保护”的属性，如性别、种族和宗教等。“通过无意识的公平”的想法表明，人工智能模型只需要忽略这些受保护的属性；然而， [Hardt 等人(2016)](https://arxiv.org/abs/1610.02413) 声称这是无效的，因为冗余编码使得从其他特征预测受保护的属性成为可能。他们测试各种“不经意”的方法，发现它们无效；因此，他们得出结论，因果关系是必要的，以确定公平的关注。

如前一节所述， [Kilbertus 等人(2017)](https://arxiv.org/abs/1706.02744) 表明，DGP 的因果解释可以激发公平性度量。与 [Hardt 等人(2016)](https://arxiv.org/abs/1610.02413) 类似，他们提出这种方法是因为观察数据在正确解决公平性问题方面存在固有的局限性。 [Kusner 等人(2017)](https://arxiv.org/abs/1703.06856) 定义了“反事实公平”的概念，其中，如果对于每个个体，预测对于通过改变受保护属性而创建的个体的反事实版本保持相同，则预测器是公平的。他们声称这是必要的，因为历史数据可能包含偏见，人工智能模型必须考虑这一点，以避免歧视。

使用因果推理 [Kusner 等人(2017)](https://arxiv.org/abs/1703.06856) 开发了一个模型公平的框架，该框架捕捉了一个直觉，即一个决定对一个人是公平的，如果它在真实世界中与在反事实世界中是相同的，其中该个人属于不同的人口统计组。也就是说，改变一个受保护的属性，比如种族，在预测上应该具有反事实不变性。[费德等人(2021a](https://arxiv.org/abs/2109.00725) )解释说，将受保护的属性视为服从反事实推理或干预的变量的合法性存在问题。作为一个解决方案， [Kilbertus et al. (2017)](https://arxiv.org/abs/1706.02744) 提出可以用名字等可观察的代理来测试不变性。

根据 [Feder 等人(2021a)](https://arxiv.org/abs/2109.00725) 的说法，有几种方法可以使用反事实数据增强来减少偏差。例如，可以通过交换“身份术语”列表来构建反事实，目的是减少文本分类中的偏差 [(Garg 等人，2019)](https://arxiv.org/abs/1809.10610) 。另一项研究将代词等性别标记物用于指代消解，指代消解是指文本中的同一实体[(赵等，2018)](https://aclanthology.org/N18-2003/) 。反事实数据扩充也已经被用于减少像 BERT 这样的模型的预训练中的偏差；然而，这种预训练模型中的偏差会在多大程度上传播到下游应用，目前尚不清楚( [Feder 等人，(2021a](https://arxiv.org/abs/2109.00725) )。迄今为止，分配标准还没有经常被用来提高公平性。由 [Feder 等人(2021a)](https://arxiv.org/abs/2109.00725) 提到的一项值得注意的研究使用不变风险最小化来减少对毒性检测数据集的虚假种族相关性的使用 [(Adragna 等人，2020)](https://arxiv.org/abs/2011.06485) 。

回到我们的医疗诊断示例，假设训练数据包含患者和医生的受保护属性，也许这些方法中的一些可能有助于提高公平性。然而，一个值得关注的问题应该是书面叙述中潜在的偏见；例如，[批判种族理论](https://en.wikipedia.org/wiki/Critical_race_theory)认为用来描述有色人种的语言可以不同于用来描述白人的语言。从历史上看，人口统计受贫困等社会问题的影响，这意味着某些医院服务区可能有更高比例的 BIPOC 患者，同时获得的资金和财政捐赠也较少。此外，还有大量关于有色人种和女性面临的医疗保健不平等的研究。例如，引用[美国律师协会](https://www.americanbar.org/groups/crsj/publications/human_rights_magazine_home/the-state-of-healthcare-in-the-united-states/racial-disparities-in-health-care/)的话，“黑人根本得不到与白人同等质量的医疗保健，这种二流的医疗保健缩短了他们的寿命。”。

所有这些因素都可能对用于构建诊断预测因子的书面临床叙述产生影响，并且偏倚可能被硬编码到医生诊断标签本身中。因果关系可以帮助确定预测是否公平和公正，例如，因果数据扩充可以测试预测的不变性。然而，同样重要的是，这种决策的透明度，这需要可解释和可说明的人工智能模型。下一节将讨论这个问题。

## **因果模型的可解释性&可解释性**

虽然像 BERT 这样的 NLP 模型目前是“难以理解的黑匣子，难以解释，但有必要诊断错误并与决策者建立信任”( [Feder 等人，(2021a](https://arxiv.org/abs/2109.00725) )。目前，[费德在艾尔。(2021a)](https://arxiv.org/abs/2109.00725) 陈述了一种常见的方法是利用网络工件，例如注意力权重，来生成解释。理由是注意力权重是在生成预测的路径上计算的([王等，2016](https://aclanthology.org/D16-1058/) )。另一种方法是试图通过使用测试实例或其隐藏表示的扰动来估计更简单和更可解释的模型( [Kim 等人，2017](https://arxiv.org/abs/1711.11279) )。这两种基于注意力和干扰的方法都有重要的局限性，会使它们产生误导。例如，“基于注意力的解释通常只可能用于单个标记，因此不能用抽象的语言概念来解释预测”( [Feder 等人，(2021a](https://arxiv.org/abs/2109.00725) )。此外，基于扰动的方法“不允许估计句子级估计的影响，并且经常会产生不可信的反事实”( [Feder 等人，(2021a](https://arxiv.org/abs/2109.00725) )。

鉴于现有可解释性度量的问题，有应用因果观点的空间。根据[费德在阿尔。(2021a)](https://arxiv.org/abs/2109.00725) ，一种方法是使用数据扩充生成反事实示例，然后将每个示例的预测与来自生成的反事实的预测进行比较。反事实数据增强使得计算观察到的文本和如果文本中不存在特定概念时的文本之间的差异成为可能。在这种情况下，生成反事实文本似乎是合理的，这就有可能估计基于文本的模型的因果效应( [Feder 等人，(2021a](https://arxiv.org/abs/2109.00725) )。

例如， [Ross 等人(2021)](https://arxiv.org/abs/2107.07150) ，为了促进数据扩充，创建了一个任务不可知的生成系统，它以语义受控的方式干扰文本。这个系统被他们命名为 Tailor，它使用了不相似性训练和一个生成器，该生成器遵循一系列来自语义角色的控制代码，这些控制代码的修改允许细粒度的扰动。使用 Tailor 生成反事实，减少了通常与特定任务扰动生成器相关的开销，并具有提高模型可解释性的优势。 [Gardner et al. (2020)](https://aclanthology.org/2020.findings-emnlp.117/) 试图通过使用“对比集”来评估模型的决策边界，从而提高模型的可解释性。他们建议，在构建数据集后，作者应该以小而有意义的方式手动扰动测试实例，以创建对比集。这些对比集应该“提供模型决策边界的局部视图，然后可以用来更准确地评估模型的真实语言能力”( [Gardner 等人，2020)](https://aclanthology.org/2020.findings-emnlp.117/) 。

尽管在生成自然语言反事实方面取得了进展，但对于风格、主题或情感等抽象语言概念来说，通常不可能“自动生成有意义的反事实，手动生成成本太高”( [Feder 等人，(2021a](https://arxiv.org/abs/2109.00725) )。鉴于这一问题，提出了一种替代方法，其中文本本身被搁置，而文本的表示被操纵。这种方法的一个例子是前面提到的 Feder 等人(2021b) 关于反事实语言表征模型的工作。他们通过预先训练分类器使用的语言表示模型(BERT)的附加实例来计算反事实表示，并使用对抗性辅助任务来控制混淆概念。另一个例子是 [Ravfogel 等人(2020)](https://arxiv.org/abs/2004.07667) 的工作，其中提出了一种使用迭代零空间投影从模型中移除信息的方法，以保留受保护的属性。

到目前为止，所讨论的可解释性方法使用反事实来确定不变性，一种“补充方法是生成具有最小变化的反事实，以获得不同的模型预测”( [Feder 等人，(2021a](https://arxiv.org/abs/2109.00725) )。这种敏感性方法提高了可解释性，因为它强调了改变模型预测所需的变化。例如，[莫西拉尔等人(2020)](https://arxiv.org/abs/1905.07697) 开发了一个框架，用于生成和评估一组不同的反事实解释，作为提高模型可解释性的一种方式。本质上，将不变性和敏感性测试合并到模型开发过程中，是一种使用因果关系来提高可解释性和可解释性的方法。

# **最后的想法**

因果关系可以通过增加鲁棒性、公平性和可解释性来改进 NLP 模型。做出这些改进应该有助于解决当前最先进的人工智能语言模型(如 BERT)中存在的一些问题。我相信因果推理在伦理人工智能的发展中有一定的作用。事实上，我最近描述了[神经科学和批判理论如何能够启发基于突触可塑性的道德人工智能系统，这些系统使用因果推理](/mindful-machines-neuroscience-critical-theory-for-ethical-ai-4162ebdcc334)。最近的研究加强了这一观点，即因果关系可以提供一种识别和减轻偏见的方法。然而，最终还是要靠公司和从业者来利用我在本文中描述的一些因果方法。我希望这些因果驱动的技术能够成为标准实践。

目前，我主要关注的是使用 NLP 进行因果推理的潜力。然而，在没有首先解决鲁棒性、公平性和可解释性问题的情况下，追求将 NLP 模型用于因果社会科学研究是不负责任的。完成我的尽职调查后，我打算回到我的第一篇文章[中关于因果推理和 NLP 的观点。由于这一领域的研究刚刚开始获得牵引力，因此缺乏实用教程来帮助数据科学家将这些想法融入他们自己的工作中。因此，我的下一篇文章将是如何使用 NLP 估计因果关系的实际 Python 代码演练。](/causal-inference-using-natural-language-processing-da0e222b84b)

我欢迎反馈和问题，请随时通过 [Linkedin](https://www.linkedin.com/in/haaya-naushan-a4b5b61a5/) 与我联系。