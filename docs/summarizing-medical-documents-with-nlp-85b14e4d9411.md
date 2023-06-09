# 用自然语言处理技术概括医学文献

> 原文：<https://towardsdatascience.com/summarizing-medical-documents-with-nlp-85b14e4d9411?source=collection_archive---------10----------------------->

![](img/794ae560f103ebe4707216e7ffb614b1.png)

图片由 [funforyou7](https://www.vecteezy.com/members/funforyou7) 来自 [Vecteezy](https://www.vecteezy.com/vector-art/130802-prescription-pad-medical-vector)

*如果你想建立自动总结长文本的工具，自然语言处理肯定是一条可行之路。然而，由于许多原因，医疗文件可能很难处理。这里有一些关于如何应用文档摘要而不犯任何错误的考虑。*

# 什么是文档摘要？

文本摘要是一项自然语言处理(NLP)任务，我们试图从文本输入(如书籍、文章、新闻)开始创建摘要。

当来源是一个文档时(在我们的例子中是一个*临床文档*，像出院信和护理报告)，我们称之为**文档摘要**。

根据输出类型，文档摘要可以是:

*   **提取**:摘要是从输入的文本中提取的**。输出通常是原文中最重要的句子的连接。**
*   **摘要**:摘要由**生成**。这意味着我们使用原始文本来学习内部表征，然后我们使用这样的表征来生成新的文本。输出是*原*，而不是输入句子的组合/串联。
*   **混合**:在识别出一个**提取中间状态**后产生一个**抽象概要**或者他们可以根据文本的细节选择使用哪种方法(例如:指针模型)。

![](img/0b635297a67ab7c5731fbb91c41f1ae9.png)

摘录总结示例。通过保留输入中信息最丰富的句子，原始文档被压缩成一个单句文档。(图片由作者提供)

## 临床文档摘要的问题

尽管 NLP 有很大的承诺，但并非所有闪光的东西都是金子。当处理生物医学文本时，问题总是迫在眉睫。

在这种情况下，问题就出在我们试图传达的**类型的信息**上，这种信息可以是难以置信的**精确和具体**。在临床文件中，**词汇选择很重要**，**数字和单位很重要**，解释和改写的余地很小。

这对抽象的摘要模型来说是个坏消息。到今天为止，你的超级骗子 GPT 怪物，经过数万亿次的训练，将无法重新表述"*心电图显示向心 LVH，EF 为 62%。出院用药:诺和灵 70/30，每日两次 15 单位*“不要弄乱了。
不幸的是，这里没有诠释和创造的空间。

然而，我们必须考虑到**并不是每一篇生物医学文章都是临床文档**。散漫的、写得好的医学论文传达不同种类的信息，可以讲述不同的故事，更适合文本生成。然而，生物医学文本是复杂的，抽象模型有时仍然会犯事实错误。但在恢复摘要时犯事实错误的影响比打包解雇信要轻松得多。

获得事实上正确的生成摘要的一个重要的方法——但仍然相对未被探索——涉及混合模型。**指针生成器网络** ( [参见 et al .，2017](https://research.google/pubs/pub46111/) )尤其似乎能够产生更流畅的摘要，同时解决了再现事实细节不准确的缺点( [Dang et al .，2019](https://www.researchgate.net/publication/338093789_Abstractive_Text_Summarization_Using_Pointer-Generator_Networks_With_Pre-trained_Word_Embedding) )。这是通过将**提取约束**(即指针)添加到抽象过程中来实现的:一些不能弄乱的单词是从源文本中复制的**，其余的是生成的。**

![](img/1c8e3e074de383ecf98dd0446a3e9902.png)

图片来自 [Vecteezy](https://www.vecteezy.com/vector-art/122533-prescription-pad-workspace-vector)

# 总结方法和实现

今天我们有很多有前途的摘要算法。然而，评估哪一个是最好的是一个长镜头。首先，**对于使用哪些指标来评估这些系统还没有明确的共识**(我希望在下一篇博文中回到这个问题上)。此外，最好的摘要技术是**高度依赖于你感兴趣的领域和文本类型**。

鉴于上面讨论的前提，这里我们将实现两种不同的临床文档摘要策略，即**可靠**、**快速**和**提取**。

这两种方法都是**无监督的**:我们不依赖于将每个文档与人工生成的摘要相关联的标记数据集，因为它们创建起来很昂贵，并且需要领域专家的贡献。我也不知道有任何公开可用的临床报告评估数据集(如果有，请在评论中告诉我！).

我们将使用的输入数据取自 mtsamples.com<https://www.mtsamples.com/>*，这是一个庞大的匿名转录医疗报告集合，可以免费获得。*

*我们将使用一封[心脏评估信](https://www.mtsamples.com/site/pages/sample.asp?Type=86-Letters&Sample=39-Cardiovascular%20-%20Letter)，但是您可以随意探索该集合并尝试使用其他文档。*

## *传统方法:基于频率的句子评分*

*这是最简单、最直接的方法。这里，我们使用信息论为输入的每个句子分配一个基于相对频率的分数。一个句子的高值意味着它的内容可能是信息性的。
在 [SpaCy](https://spacy.io/) 的帮助下，我们可以用几行代码实现这一点，SpaCy 是一个非常棒的库，旨在快速流畅地实现标准的 NLP 管道。*

*初始化*

*这里我们使用 SpaCy NLP 管道来处理英语，这非常方便，因为它返回一个 Doc 对象，该对象包含已经标记化和预处理的文本，被分成单词和句子。*

*首先，我们遍历 doc 对象中的标记化文本，用每个唯一的单词(没有停用词，没有标点符号)及其出现的相对频率创建一个字典。*

*词频计算*

*我们已经提到了摘要是如何基于**句子评分**的。因此，我们需要找到一种方法，给每个句子一个**重要性分数**，这样我们就可以在摘要中包含最重要的句子。为了给每个句子打分，我们**对每个句子中的** **相对词频**求和，然后我们创建一个字典，将句子和它们的分数配对。*

*相对频率总和的问题在于它对短句不利。这是一件坏事吗？嗯，看情况。
确实存在这样的情况，即在一个繁琐的句子中找到有用信息的概率要高于较短的句子。然而，事实可能并非如此:虽然临床记录中的病历部分可能会很冗长，但药物处方或诊断通常会被浓缩成由几个词组成的短句。为了解决这种潜在的不希望的**长度偏差**，我们可以**通过将相对频率和除以每个句子中的字数来归一化**。*

*句子评分*

***最终摘要**由 *heapq* 模块中的 *nlargest* 函数生成，该函数高效地返回得分最高的 ***k* 个句子**。*

*汇总生成*

*我们检查的文件是一封关于一名患者的[信](https://www.mtsamples.com/site/pages/sample.asp?Type=86-Letters&Sample=39-Cardiovascular%20-%20Letter)，该患者有治疗控制的高血压、临界糖尿病和肥胖症的病史。
输出摘要如下所示:*

*   *NON _ REL:“*他否认有任何冠心病的症状，但他可能有某种程度的冠状动脉粥样硬化，功能测试可能影响下壁[S1]。他有冠心病家族史，但否认有任何心绞痛或不耐努力的症状[S2]。我担心这位先生可能患有糖尿病和代谢综合征，包括躯干肥胖、高血压、可能的胰岛素抵抗、一定程度的空腹高血糖以及轻微的甘油三酯升高[S3]。总之，我们有一位 67 岁的男性患者，他有冠心病的危险因素[S4]。他进行了踏车心脏复律，仅进行到第 2 阶段，当患者达到预测最大心率的 90%时，监督医生终止了该试验[S5]。”**
*   *REL:“*众所周知，他的母亲患有冠心病[S1]。心脏检查正常[S2]。静脉压正常[S3]。这个病人对阿司匹林[S4]过敏。肾功能正常[S5]。”**

*正如我们所料，**的第一个输出显示了冗长且内容丰富的句子**，而第二个输出则简洁得多。第二个总结也倾向于更多地关注病人的进展，忽略了医生担心的重要信息。*

*考虑到这一点，我们可以说摘要#1 在质量上优于这种类型的笔记。*

*尽管这个玩具示例很简单，但是这些模型现在仍然非常流行，并且经过一些改进，输出摘要的质量可能已经很高了。例如，学术文献中一种非常常见的方法( [Widyassar 等人，2019](https://www.semanticscholar.org/author/Adhika-Pramita-Widyassari/2079753366) )不是依赖*内部*频率(只对长文本有效)，而是使用 **TF-IDF** 计算整个临床样本集合上的词频。当文档显示可用于获得关于内容的额外信息的循环结构时，还可以设计额外的加权方案，如**位置惩罚** ( [Sarker 等人，2020](https://www.frontiersin.org/articles/10.3389/fdgth.2020.585559/full) )。*

*![](img/f0fe5f72d748a6f0c38185add6445a11.png)*

*图片由 [Reno Devissandy](https://www.vecteezy.com/members/justdevissandy) 提供，来自 [Vecteezy](https://www.vecteezy.com/vector-art/1270246-pink-and-white-battle-robot)*

## *现代方法:基于变压器的总结*

*可以根据不同的标准选择句子。第二种方法不是使用术语频率，而是围绕着 **BERT** ( [Delvin 等人，2018](https://arxiv.org/abs/1810.04805) )，这是**Transformer**([vas Wani 等人，2017](https://arxiv.org/abs/1706.03762) )家族最受欢迎的模型之一。*

*讨论 BERT 的细节超出了这里的范围。我们只需要知道这一大堆注意力驱动的编码器是迄今为止学习上下文嵌入最有效和最流行的技术之一。*

*这种方法背后的主要思想是通过对预训练深度学习模型的输出嵌入进行聚类来执行**提取摘要，如 [Miller，2019](https://arxiv.org/abs/1906.04165) 中所述。这项工作旨在创建讲座摘要，利用文本嵌入的 BERT 模型和 K-means 聚类来识别靠近质心的句子以进行摘要选择。***

*此处可用的[汇总器管道遵循以下 4 个步骤:](https://github.com/dmmiller612/bert-extractive-summarizer)*

1.  *传入的文本经过预处理，并标记为干净的句子。*
2.  *将标记化的句子输入到 BERT 模型以获得句子嵌入。BERT 产生 N×W×E 个嵌入，其中 W 等于标记化的单词。为了得到句子级的嵌入，嵌入可以被平均或最大化以产生一个 N×E 矩阵。*
3.  *使用 K-means 对句子嵌入进行聚类。*
4.  *通过挑选更接近其质心的句子来选择候选摘要句子。因此，聚类的数量 K 定义了概要的输出句子的数量。*

*结果如下:*

**“感谢您推荐样本患者先生进行心脏评估【S1】。这是一名 67 岁的肥胖男性，有治疗控制的高血压、临界糖尿病和肥胖史[S2]。体检显示一名中年男子体重 283 磅，身高 5 英尺 11 英寸[S3]。
我担心这位先生可能患有糖尿病和代谢综合征
，这位先生患有躯干肥胖、高血压、可能存在胰岛素抵抗和一定程度的空腹高血糖，以及轻微的甘油三酯升高【S4】。鉴于没有症状，目前需要进行药物治疗，并对危险因素进行非常积极的调整[S5]。在没有症状的情况下，我目前没有发现进行任何进一步检查的迹象，如冠状动脉造影[S6]。”**

*这份总结几乎包含了我们需要的一切。第一句解释了临床记录的目的(心脏评估)。然后，下面的[S2] [S3]句子揭示了病人情况的细节(年龄、病史、医疗条件等。)，而最新的句子围绕着医生的担忧(即为什么他需要心脏评估，在[S4]中解释)和他的适应症/意图([S5]和[S6])。*

*![](img/f19e4dbb98be278d9e34a0b43e1b9dd2.png)*

*图片由 [imajin noasking](https://www.vecteezy.com/members/imajin-noasking) 来自 [Vecteezy](https://www.vecteezy.com/vector-art/2127142-medicine-and-healthcare-concept-vector-illustration-health-examination-patient-consultation-can-use-for-web-homepage-mobile-apps-web-banner-character-cartoon-illustration-flat-style)*

# *结论*

*在本文中，我们探讨了两种不同的策略来解决总结临床文档的问题。在这种情况下，文档摘要可能会很棘手，原因有很多:医生的词汇选择、简洁的信息密集型句子加上冗长的句子、缩写、拼写错误等。
**在这种情况下，应不惜一切代价避免事实错误**。这也是我们从一开始就放弃抽象概括的主要原因。*

*但是，有一个重要的工具我们没有在这里讨论。一个在未来几年可能变得非常有用的工具，它可以克服像临床领域这样的棘手领域中的文档摘要的局限性:**知识库**。在最近 30 年里，科学家们付出了非凡的努力，将生物医学概念和关系映射到复杂的**本体**，实现了医学知识的共享和形式化。因此，**用特定领域的本体信息增强现代摘要技术**可能是克服当前在报告准确事实信息方面的限制的关键。*

*我希望尽快找到时间，在一篇新文章中讨论**总结评估策略**和**指针生成器网络**。与此同时，请在评论区留下你的想法，如果你觉得这有帮助，请分享！如果你喜欢我的工作，现在你也可以给我买瓶啤酒！🍺*

*<https://www.linkedin.com/in/tbuonocore/> *