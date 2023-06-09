# 人工智能的源代码数据集——为什么和如何

> 原文：<https://towardsdatascience.com/how-to-generate-code-dataset-for-machine-learning-applications-fbc1b888cc84?source=collection_archive---------32----------------------->

## 要避免的陷阱

![](img/6e8e065e071c6f2556955b6f9cb37101.png)

丹尼尔·怀尔德曼的照片来自[自由影像](https://freeimages.com)

# 为什么编码数据集

代码 AI 最近成为一个普遍的话题；无论是对一个代码[主题](https://github.blog/2017-07-31-topics/)进行分类，发现其中的[漏洞](https://arxiv.org/abs/2009.07235)，对其进行[总结](/how-to-create-data-products-that-are-magical-using-sequence-to-sequence-models-703f86a231f8)甚至是[根据前面的令牌猜测](https://www.tabnine.com/)下一个令牌。使它成为可能的是最近 NLP 的进步和丰富多样的源代码数据集的可用性提升。拥有像 Github、Gitlab 和 Bitbucket 这样的服务，生成源代码数据集可能被视为一项微不足道的任务——“抓取 Github 并开始训练模型”。事实上，这种简单性涵盖了一个相当复杂的领域，需要避免许多陷阱。下面详细解释。

# 案例研究——话题预测

让我们假设我们的任务是建立一个模型来预测一个源代码是否与服务器相关。有许多方法可以处理它，从手动收集特性(比如文件类型，它是测试代码吗，它的导入是什么，等等..)到深度神经网络，它将自动生成一组特征来查看。无论我们走哪条路，第一步都是收集相关的数据集。**一个普通(幼稚！！)建议的计划**将是使用一些相关的搜索标准(如 Node.js repositories)从公共代码托管服务(如 Github)中随机抽取存储库，并根据相关术语的存在对其进行标记(“服务器相关”与“不相关”)。沿着这条路走下去，我们很可能会发现我们的模型过度适应数据集的浅层特征。什么会出错？

# 为什么随机抽样代码不是微不足道的

我们最初计划的主要问题是源代码数据集固有的**隐含偏差**，这会影响不同语言和代码类型的模型泛化。Github 是最常见的代码托管服务之一，据报道它遭遇了[语言的长尾](https://github.blog/2019-07-02-c-or-java-typescript-or-javascript-machine-learning-based-classification-of-programming-languages/)；很少是超级常见的(像 Javascript 和 Java)，而大多数(像 C)是非常罕见的。重新审视我们的计划，随机抽样 Github 最终会得到他们长尾分布的代理。由于一些话题与语言有关，情况会变得更糟；例如，Java 比 Clojure 与服务器应用程序更相关。鉴于 Java 在我们的数据集中也更常见，可能会导致模型得出 Clojure 与服务器完全无关的结论(在我们的模型预测中总是负面的，这是不正确的)。解决方案应该是确保我们的数据集更均匀地分布在不同的语言和类中。

# 为什么分层抽样代码不简单

常见的实现均匀分布的方法是[分层抽样](https://en.wikipedia.org/wiki/Stratified_sampling')。在代码数据集上，通常在回购级别应用采样，以确保生成的训练-测试-验证分割是互斥的(以避免相同回购文件过度匹配的风险)。试图在回购级别上对语言进行抽样可能很困难，因为一些语言如 Json 和 Yaml **通常是通用的**；无论实施什么样的抽样政策，它们都可能在我们的数据集中(过于)常见。另一个问题是如何针对相关文件；为了确保数据集有足够多的服务器相关示例，我们建议使用服务器相关的术语搜索 Github(如 Java 上的“tomcat”、Python 上的“flask”和 Javascript 上的“express ”),但问题是这种搜索太过特定于技术(可能会导致过度拟合),通常很难确保每种语言都有相同数量的示例。依赖于标准化的搜索词(比如“服务器”这个词本身)会忽略许多潜在的相关例子。如何确保我们的数据集均匀分布，同时保持其丰富多样？

# 分阶段采样以调整分布

根据上面提到的代码数据集特征，我们的数据集可能会有偏差。分层抽样只能部分地解决这个问题，因为它隐含着阶级与语言的关系。解决方案应该是分阶段采样**；在正类(通常更少)上，欠采样会浪费昂贵的样本，而过采样能够记住不太常见的样本。在负类(通常更容易得到)上，分层抽样可能隐藏了类的多样性。我们的解决方案将是从对阳性类中过于常见的语言进行欠采样开始，并继续对长尾语言进行过采样。最后，我们将对负类进行欠采样，以匹配刚刚生成的正语言分布。这将产生一个数据样本，其中我们保留尽可能多的正面例子，同时确保总体人口几乎均匀分布。重要的一点是，无论我们选择应用什么样的采样策略，我们都应该**始终监控**；确保观看一般和每种语言的表演。了解潜在的隐藏偏见。**

# 主动学习填补空白

在我们建议的解决方案中，一些例子将被忽略(对太常见的正样本和通常的负样本进行采样),而一些例子将被重复(对正长尾进行过采样)。为了使采样比简单的随机采样更智能，我们可以使用弱模型来识别哪些负面例子要优先考虑(由弱模型正确识别的那些不太重要)，并且用主动瞄准感兴趣的地层来替换过采样重复。专注于数据集的“薄弱”领域将使我们能够更好地将我们的工作力量用于改进模型。

# 谨慎建造

尽管看起来很简单，但生成可靠的代码数据集可能是一项艰巨的任务，有时甚至比训练模型本身还要困难。一开始就注意训练人群特征，可以防止很多后来的头疼。