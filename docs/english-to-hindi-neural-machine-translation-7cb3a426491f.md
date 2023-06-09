# 英语到印地语的神经机器翻译

> 原文：<https://towardsdatascience.com/english-to-hindi-neural-machine-translation-7cb3a426491f?source=collection_archive---------8----------------------->

## [实践教程](https://towardsdatascience.com/tagged/hands-on-tutorials)

## 探索所有 Seq2Seq 任务中普遍存在的基本 NLP 预处理和编码器-解码器架构

![](img/2ff39889a39f9b81a08f20e5ab61021d.png)

图片经由 [Adobe Stock](https://stock.adobe.com/in/contributor/205976936/anastasibility1?load_type=author&prev_url=detail&asset_id=97687333) 授权给 Maharshi Roy

自该领域的研究开始以来，机器翻译无疑是自然语言处理中最常遇到的问题之一。通过本教程，我们将探索一个编码器-解码器 NMT 模型采用 LSTM。为了简单起见，我将在后面的文章中讨论基于注意力机制的更好的性能架构。

## 资料组

我使用了 [IIT 孟买英语-印地语语料库](https://www.cfilt.iitb.ac.in/iitb_parallel/)作为本教程的数据集，因为它是可用于执行英语-印地语翻译任务的最广泛的语料库之一。呈现的数据实际上是每种语言的两个独立文件中的句子列表，看起来像:

![](img/5ac0d9d7286b3bee60069393e61b87ea.png)![](img/3c3c5f7791e5e7860ea9bd9f8e43cdac.png)

单独文件中的英语和印地语句子对(图片由作者提供)

**预处理**

作为基本的预处理，我们需要删除标点符号，数字，多余的空格，并将其转换为小写。封装在函数中的非常标准的东西:

预处理功能

值得注意的一件重要的事情是目前的北印度语句子的恶名。除了通过上述函数运行句子之外，还需要对句子进行净化，以删除其中包含的英文字符。这实际上导致了训练中的**NaN**bug，耗费了大量的调试时间。我们可以通过使用 regex 将任何英文字符替换为空字符串来避免这个问题，如下所示:

`hindi_sentences = [re.sub(r'[a-zA-Z]','',hi) for hi in hindi_sentences`

LSTMs 通常不会执行很长的序列(虽然比 RNNs 好，但仍然无法与 Transformers 相比)。因此，我们将数据集缩减为包含长度不超过 10 个单词的句子。同样出于演示的目的，我们考虑总共 25000 个句子来保持较低的训练时间。我们可以实现以下目标:

## 准备数据

在翻译过程中，我们的模型如何知道什么时候开始和结束？为此，我们专门使用了<start>和<end>标记，我们将它们添加到目标语言中。这可以通过如下所示的一行程序来实现:</end></start>

`hi_data = ['<START> ' + hi + ' <END>’ for hi in hi_data]`

虽然这个巫毒步骤的确切用法目前可能还不清楚，但是一旦我们讨论了架构和事情是如何工作的，就很容易理解了。在这一点上，我们仍然有字符语句形式的数据，需要将其转换为数字表示，以便模型进行处理。具体来说，我们需要为英语和印地语句子创建一个单词索引表示。我们可以使用 tensorflow 的内置令牌化器来解除手动执行这一任务，如下所示:

这里需要注意的一个重要参数是 *oov_token* ，，它本质上代表词汇之外。这是专门用在我们想限制我们的词汇量，说只有前 5000 个单词。在这种情况下，任何不受欢迎的单词(基于实例计数> 5000 的单词排名)将被参数值替换，并被视为不包含在词汇表中。这样，我们可以放松我们的模型，忽略数据集中出现的模糊和罕见的单词所造成的任何影响。另一个需要注意的要点是，我们为英语和印地语单词的 vocab 大小加 1，以容纳填充数字(稍后讨论)。

## 准备解码器输入和输出

NMT 模式的运作方式可以理解为一个两阶段的过程。在第一阶段，编码器模块一次一个单词地接收输入序列。因为，我们使用的是 LSTM 层，随着每个单词的消耗，内部状态向量*【h，c】*会得到更新。在最后一个字之后，我们只关心要输入解码器的这些向量的最终值。然后，第二阶段通过摄取编码器的最终[h，c]向量并消耗目标句子的每个标记来工作，从< START >开始。为每个令牌产生的输出将与预期的相匹配，并且生成误差梯度来更新模型。在用尽目标输入后，我们期望我们的模型产生一个< END >令牌，表示这个数据样本的完成。从下图中可以更好地理解这一点。

![](img/a4b40bc9ec6ad89adaf20f6c76a14c4a.png)

训练阶段**“我会回来的”**的旅程(图片由作者提供)

我们从*《终结者》(1984)* ~《我会回来的》来演示阿诺德的著名对白的翻译。我们可以看到，解码器 LSTM 是用编码器的最终[h，c]初始化的。我们可以将这一步理解为将输入句子的思想/摘要传递给解码器 LSTM。灰色方框表示 LSTM 单位的输出，红色方框表示每个时间步长的目标令牌。当第一令牌< START >被馈送到解码器 LSTM 中时，我们期望它产生मैं，然而它产生तुम，说明了对误差梯度的贡献(用于随时间反向传播)。从上图中可以清楚地看到，我们应该按照下面的方式重新排列我们的目标句子，这可以使用下面的代码块来实现:

```
decoder-input:  <START> मैं   वापस  आऊंगा
decoder-output:   मैं   वापस आऊंगा <END>
```

将解码器输入和输出以及填充序列对齐到固定长度

LSTMs 仅适用于固定长度的序列。既然我们选择了不超过 *maxlen* 、*的句子长度，那么将所有实例填充到那个长度似乎是合乎逻辑的。*

**模型架构**

为了保持较低的训练时间，同时具有足够的维度来捕捉数据中的变化，我们选择将我们的向量维度( *d_model* )设为 256。

编码器

如上面的代码片段所示，我们关心最终的内部状态*【h，c】*，而不是编码器 LSTM 的输出。

解码器

如上所述，解码器 LSTM 由编码器内部状态初始化，并且其输出被馈送到密集层，该密集层的单元数量等于具有 softmax 激活的目标 vocab 大小( *hindi_vocab_size* )。想法是在目标词汇表的所有单词上生成概率分布。选择具有最高值的一个，意味着这个特定的令牌是最有可能的，这正是我们在这里所做的。我们使用稀疏分类交叉熵作为要优化的损失函数。

## 培训和结果

我在 95%-5%的训练测试分割上训练了上述网络大约 100 个历元，在此期间，我观察到它在 80 个历元时遭遇 **NaN** loss。因此，我使用模型检查点来保存中间解决方案，如下所示:

检查点并保存最佳验证准确性

考虑到 google colab 中有限的电源和断开连接(如果保持空闲训练)，我不得不在一个相当乏味的模型和有限的训练数据上妥协，用它我实现了 93%的训练准确率和 26%的验证准确率😢。

## 推理模型

加载保存的模型。我们需要使用 tensorflow 模型的 *get_layer* API 引入预训练层，以便在我们的推理工作流中重用。

从加载的预训练层准备推理模型:

推理模型

推理模型重用了经过训练的编码器和解码器模型。编码器部分将经过训练的嵌入层作为输入，并输出最终的*【h，c】*(实质上也引入 LSTM 层)，供解码器使用。解码器以类似的方式将第一令牌的训练目标嵌入层和编码器最终状态*【h，c】*作为输入。对于每个后续令牌，我们提供先前的解码器内部状态(本质上给出当前单词的上下文，并在此基础上预测下一个单词)。从下面的推理算法可以更好地理解这一点:

翻译步骤

在翻译步骤中，我们将英语句子输入编码器，得到输出状态*【h，c】*。主要的翻译发生在第 10–18 行，在这里我们获得当前单词的下一个单词，并更新内部状态以用于下一步。这个循环一直重复，直到我们得到一个<结束>令牌或者到达 *maxlen* 令牌*。*

## 使用谷歌翻译进行推理和 BleU 评分

为了进行推理，我使用了一些句子，并使用了谷歌翻译的其他翻译版本来计算语料库 *BleU* 的分数。我从训练集中选择样本只是因为我们的验证分数很低，我预计我们的模型在测试集上的表现也同样糟糕(不适合演示)。

*注 1:* BleU 或双语评价 Understudy Score 是评价预测句子与参考语料库相似度的度量。它在候选数据和参考数据之间的 N 元匹配上使用精确召回概念。数学解释超出了本文的范围，因此，我建议读者仔细阅读 Jason Brownlee 的一篇受欢迎的博客文章。

*注 2:* 谷歌翻译 API 不是一个免费功能，使用说明可以在相应的 GCP [文档](https://cloud.google.com/translate/docs/setup)中找到。

下面显示了执行的一些实例。很明显，鉴于我们的模型在训练数据上的出色表现和大约 0.42 的 BleU 分数(一个令人惊讶的高值)，我们的模型已经过度拟合了。一旦看到新的数据，这个模型就会彻底失败，这一点也不奇怪。

```
Input: accerciser accessibility explorer 
Prediction: एक्सेर्साइसर पहुंचनीयता अन्वेषक 
Dataset Reference: एक्सेर्साइसर पहुंचनीयता अन्वेषक
Google Translated Reference: accerciser अभिगम्यता एक्सप्लोररInput: the default plugin layout for the bottom panel 
Prediction: ऊपरी पटल के लिए डिफोल्ट प्लगइन खाका 
Dataset Reference: निचले पटल के लिए डिफोल्ट प्लगइन खाका
Google Translated Reference: निचले पैनल के लिए डिफ़ॉल्ट प्लगइन लेआउटInput: highlight duration 
Prediction: अवधि को हाइलाइट रकें
Dataset Reference:  अवधि को हाइलाइट रकें
Google Translated Reference: हाइलाइट अवधि
```

几十年来，神经机器翻译无疑一直是 NLP 的一个挑战性问题。虽然，接近完美的实现，如谷歌翻译等。今天存在，使我们的生活更容易，但我们在这个领域还有很长的路要走，特别是对于低资源语言。尝试探索这个问题对我来说是一个巨大的学习曲线，我希望这个社区的读者可以从我的分享经历中受益。完整的笔记本可在[这里](https://github.com/maharshi-roy/Machine-Learning-Experiments/blob/main/Neural_Machine_Translation_using_LSTM.ipynb)获得。