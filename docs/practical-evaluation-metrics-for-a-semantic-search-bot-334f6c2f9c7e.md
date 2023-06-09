# 语义搜索机器人的实用评估指标

> 原文：<https://towardsdatascience.com/practical-evaluation-metrics-for-a-semantic-search-bot-334f6c2f9c7e?source=collection_archive---------20----------------------->

![](img/47b73e7bac0faf996e04654e2a91e036.png)

作者图片

## 人工智能中的产品度量指南

每一个在企业人工智能领域工作的数据科学家都必须或者将要与智能聊天机器人打交道。随着自然语言处理模型的激增，如伯特家族、GPT 家族和其他重量级模型，语义问答变得非常容易。

再加上像 Elasticsearch 这样的知识库提供商，它们允许定制搜索功能，机器人也变得高效了。

然而，当你建造一个智能机器人时，你需要量化它的性能。这对于弄清楚继续使用机器人是否是个好主意非常重要。因此，为你的机器人设计性能指标是非常重要的。

在这篇文章中，我将谈论一个基于知识库训练的问答机器人。这意味着有一个文档包含一组属于一个或多个主题的唯一问答对。

属于前语言模型时代的聊天机器人致力于词对相似性。这意味着给定两个句子，计算向量形式的组成单词之间的相似性(使用余弦相似性分数)。

然而，闪光的不都是金子。并非所有出现在最佳匹配列表顶部的答案都不一定是最佳答案。

这些模型的问题不在于衡量相似性的方式，而在于单词在句子中的表达方式。例如,“公园”这个词在句子“我需要把车停在某个地方”中可能有不同的意思，在“我们去公园散散步”中也可能有不同的意思。这种意义上的差异对机器人如何找到相似性产生了巨大的影响。旧的模型只寻找单词的相似性，而不是上下文。

输入语言模型！这些模型代表单词和句子。这有助于模型捕捉句子中单词的上下文。这就是语言模型对自然语言理解的附加值。

仍然使用每个句子的矢量形式的余弦相似度来计算单词相似度。

# 现在，我们如何比较两个聊天机器人模型的性能？

实际上，我们如何比较我们的聊天机器人模型和另一个模型的性能呢？

在聊天机器人框架内比较一个问题的两个候选答案似乎更容易——余弦相似度对！

但是就模型本身而言，比较一个模型与另一个模型的余弦相似性是没有意义的。例如，假设我们有两个候选模型 CB1 和 CB2。我们想比较一下这两种型号的性能。在我们的问答测试集中，我们可能会有一个问题“如何设置我的智能电视?”？’，聊天机器人候选人 A 可能返回以下前 2 名答案:

1.  按照以下方式设置您的 Samsung X50(相似性得分:0.87)
2.  按照以下方式设置您的银行账户(相似性得分:0.77)

候选 B 给出了以下相似性:

1.  按照以下方式设置您的银行账户(相似性得分:0.91)
2.  按照以下方式设置您的 Samsung X50(相似性得分:0.8)

候选人 B 在两个模型的顶部答案中得分最高。

但是我们当然可以看到候选人 A 给出了一个更准确的答案。因此，我们知道余弦相似性可能不是一个很好的性能指标。

那我们能做什么？

我们能做的一件事是:

1.  从测试集中抽取一个问题样本
2.  考虑每个问题的最佳答案池
3.  考虑以下方案的元评分系统:如果最佳答案是正确答案，则给它 1，如果最佳答案不正确但正确答案存在于模型返回的最佳答案集中，则给它 0.5，如果答案不在答案集中的任何地方，则给它 0
4.  对样本中的所有问题执行此操作将会给出两个聊天机器人中每个问题的分数
5.  合计每个聊天机器人的所有分数，然后用样本中的问题总数除以它们

如果样本中有更多的 1，那么计算出的分数将会很高。如果 0.5s 或者 0 多了，那么分数就低了。这意味着，一个模型给出正确答案的次数越多，它的表现就越好，而它给出错误答案的次数越多，分数就越低，模型的表现就越差。

然而，这种系统的一个非常明显的缺点是不容易实现自动化。然而，这并不难。我们需要为样本中的每个问题标记一组正确答案，当该组中的最佳答案与相似性分数为 1 的答案标记匹配时，该问题的分数为 1，如果它与该组中分数为 1 的答案之一匹配，该问题的分数为 0.5，如果没有答案匹配，则该问题的分数为 0。

现在你有了！一个简单实用的评分系统来评估你的聊天机器人的表现！