# 变形金刚

> 原文：<https://towardsdatascience.com/the-transformer-d84a06e5bc87?source=collection_archive---------24----------------------->

## 在深度学习中通过注意力工作

我已经开始浏览机器学习方面的经典论文，那些改变了艺术状态或创造了全新应用的发明。以上是我对[中介绍的**变压器**的笔记【注意力就是你需要的全部](https://arxiv.org/abs/1706.03762)。transformer 解决了自然语言处理(NLP)中递归序列建模的问题，但后来被应用于视觉、强化学习、音频和其他序列任务。

# 为什么关注？

从 RNNs、LSTMs 或 GRUs 构建的递归模型被开发来处理神经网络中的序列建模，因为它们可以包括来自相邻输入以及当前输入的信息。这对于像语言这样的数据具有明显的相关性，在语言中，单词的含义部分或全部是相对于周围的单词来定义的。

当相关单词出现在离网络的当前输入很远的地方时，问题就出现了。这些不相连的单词之间的梯度必须穿过所有的重复单元，因为模型不包含每个单词之间的直接连接。

![](img/6af6f41e65f6a2160ad86f9794039a80.png)

RNN 细胞序列

这种顺序模型还意味着计算不可并行化，因为每个单元的计算都依赖于前一个单元的结果，从而减慢了训练过程。

# 注意力

进入关注。不管距离远近，注意力都是通过衡量输入的相对重要性来发挥作用的。注意模块(也称为 head)的输入是一组查询(Q)、键(K)和值(V ),表示为通过全连接层的嵌入向量。通过将查询和键相乘，注意头确定对于特定的查询应该激活哪些键。在语言中，这意味着识别哪些单词与当前单词相关。然后，乘以价值网络，注意力头确定分配给每个查询键组合的重要性。

你可能会认为这是一把钥匙激活了锁中的插销。给定正确切割的用于制栓销的钥匙，锁将转动。与其他序列模型相比，注意力的美妙之处在于它考虑了整个序列中的相互作用。

![](img/2b327b4c85105fd5a4e61bf0427ab1fe.png)

(来源:[注意力是你所需要的全部](https://arxiv.org/abs/1706.03762))

所有这些结合成一种机制，可以允许“不考虑它们在输入或输出序列中的距离而对依赖关系建模。”[1]

# 多头注意力

然而，我们不满足于只有一个注意力头。相反，本文中开发的转换器包含多个注意力模块，称为多头注意力。通过用不同的权重矩阵初始化单独的注意头，该模型并行计算不同的注意函数，这些注意函数在通过另一个全连接层之前被组合。

![](img/abe1e2a94a0d3257d2bd9147cfb32f67.png)

(来源:[注意力是你所需要的全部](https://arxiv.org/abs/1706.03762))

您可以在下图中看到多头方法的结果，其中模型中的每个头在给定嵌入的输入单词“making”的情况下为句子的不同部分分配不同的重要性

![](img/e246be56515840aa7864a49fde39419b.png)

分配给输入单词“制作”的注意力(来源:[注意力是你所需要的全部](https://arxiv.org/abs/1706.03762)

# 位置编码

当然，使用递归模型的一个好处是基于哪个递归单元接收每个输入来编码位置信息。这些信息对于理解语法结构很有价值，比如修饰词(出现在它们所修饰的词附近的形容词)或介词短语。变压器模型将受益于该信息，因此添加位置编码层作为输入。

基于模型的深度和序列中输入的位置，使用一对具有不同波长的正弦曲线来计算位置编码。这个位置信息被添加到嵌入向量中，并且它们一起形成变换器的编码器和解码器模块的输入。

转换器上的 TensorFlow (TF)示例文档显示了根据深度和位置的位置编码图，但有点难以解释。

![](img/c4a9957b8004d2c90dfce648bfddadd9.png)

位置嵌入值的完整绘图(来源: [TF Docs](https://www.tensorflow.org/text/tutorials/transformer)

相反，考虑这个嵌入片段，它显示了不同单词位置和深度的嵌入值。单词在模型中的不同深度接收更高或更低的位置嵌入值，从而允许模型基于位置信息学习一组复杂的关系。

![](img/d828331c6657757c633a1fd36843f5f9.png)

不同模型层的位置嵌入值，其中值 *f* 是位置、 *p* 、层{1，5，15，20}和总模型深度(512)的函数。

# 变压器

转换器的目标是获取编码的输入序列及其先前的输出，通过计算两者的注意力来预测下一个输出。转换器的编码器模块从单词嵌入层和位置嵌入层获取输入，并应用前面描述的多头注意机制。解码器模块接收编码器输出作为第二多头关注块中的值和关键字，以及来自第一解码器屏蔽多头关注块的输出作为查询。

第一解码器关注块的输入被屏蔽，因此解码器看不到它试图预测的单词。每个块都包括跳跃连接。

在训练过程中，变压器根据编码器输出和训练数据中所有其他正确的*输出字学习解码正确的当前字。测试时，解码器输出*替换*正确的输出字。*

![](img/a229313ec3a4417f2cde0a19aac4e9dc.png)

完整的变压器(来源:[注意力是你所需要的全部](https://arxiv.org/abs/1706.03762))

# 肉眼观察

那么多头注意力在实践中是什么样子的呢？下面是从 TF docs 葡萄牙语到英语翻译问题的一些情节，其中每个次要情节是一个单独的注意头。在很大程度上，每一个大脑都被激活来将葡萄牙语输入翻译成英语。然而，有时在给定多个输入的情况下，转换器为单个输出计算更高的关注度，反之亦然。这是有意义的，因为有时一种语言会用两个词来表达信息，而其他语言只用一个词。

# 额外阅读和参考资料

1.  [注意力是你所需要的一切](https://arxiv.org/abs/1706.03762)
2.  [可视化神经机器翻译模型](https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/)
3.  [图示变压器](https://jalammar.github.io/illustrated-transformer/)
4.  [用于语言理解的变压器模型](https://www.tensorflow.org/text/tutorials/transformer)
5.  [我的笔记本](https://github.com/tims457/ml_notebooks/blob/main/nlp/transformers.ipynb)