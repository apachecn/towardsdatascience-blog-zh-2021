# 使用生成性对抗网络的机器艺术

> 原文：<https://towardsdatascience.com/machine-made-art-using-generative-adversarial-networks-35faa41a4feb?source=collection_archive---------26----------------------->

## 以数据为中心的绘画方法

![](img/d0931cc3acc913d162309f23f634344b.png)

算法还是艺术家——有区别吗？(本文所有图片均为作者)

**简介**

在我看来，过去几年机器学习社区所做的大部分研究工作都过于狭隘。研究人员采用已知的样本数据集，花数年时间在这些数据集上训练模型，并发表论文，对每个项目中最先进的基准进行边际改进。对于那些来自机器学习社区的读者来说，想想你多久会看到一次对 CIFAR、MNIST、LibriVox、ImageNet、IMDB 评论或维基百科语料库的提及；这些数据集用得太频繁了。我们没有看到对原始数据进行足够的研究。

背后有一个很好的理由:在比较新的机器学习模型时，我们需要一些共同的数据来与现有的模型进行比较。基准数据集使之变得简单。没有它们，这就像拿苹果和橘子做比较。但是在相同的旧数据集上加入超越最先进性能的竞赛只是**无聊的**。我总是喜欢把时间花在更具原创性的工作上。

最近在机器学习领域变得日益突出的一个主题是以数据为中心的人工智能。与上面详述的方法相反，在该方法中，我们努力在同一数据集上创建更好的模型，我们用更好的数据训练现有模型，以增加它们的推理或生成能力。教学中的类比是，假设大多数人有相似的学习能力，更好的例子和更好的解释会导致对问题陈述以及如何解决它的更好理解。

以数据为中心的人工智能非常适合生成模型。当训练模型以在输出领域(例如，音频、视频、图像……)中创建新样本时，训练数据对推理期间的结果输出有显著影响。一旦研究人员发布了一个新的模型，我们就可以将相同的设计初始化为一张白纸(或者做一些迁移学习，对于那些熟悉这个过程的人来说)，并用我们自己的数据训练它，以获得我们自己的结果。

在我环游世界期间，我有时间拍了许多照片。看着它们让我想到也许可以画出一些和它们相似的画。浏览技术文献，我发现[最近的一篇研究论文](https://arxiv.org/pdf/1902.09631.pdf) (2019)可能胜任这项工作。这篇题为“通过变换向量学习进行图像到图像的翻译”的论文描述了一种实现这一点的方法。使用论文中提出的模型，我希望以数据为中心的方法可以用来训练他们的模型根据我在日本旅行时拍摄的照片绘制水彩画。

**行程**

那么，到底什么是变换向量学习(简称 TraVeL)？2014 年，一位名为 Ian Goodfellow 的研究人员开创了一项名为生成对抗网络(GANs)的技术。当时，机器学习模型在分类任务上取得了稳步的进步，但在生成内容方面仍然非常有限。GANs 从一个新的角度处理内容生成问题:我们不是训练单个神经网络来生成内容，而是一起训练两个网络来解决问题。

第一个网络被称为“生成器”，它被训练为基于来自明确定义的输入域的样本(例如，弗兰克·辛纳特拉(Frank Sinatra)的录音、浣熊的照片、随机初始化的噪声向量等)来创建所需的内容。第二个网络称为“鉴别器”，作为来自输出域的样本的分类器，并试图确定给定的输入是否是输出域的真正成员。这两个网络并肩训练，互相促进。更好的鉴别器可以更好地区分输出域中的真实样本和生成器生成的人工样本。这反过来迫使生成器输出与输出域中的真实样本更相似的内容，以成功欺骗鉴别器。

为了提取由鉴别器学习的知识并使用它来改进生成器，我们从鉴别器损失函数反向传播并更新生成器中存在的权重张量。这导致两个网络竞争的反馈回路:较低的鉴频器损耗导致较高的发电机损耗，反之亦然。我们让它们相互竞争，以便它们可以达到一种平衡，根据它们的竞争性质将它们命名为“敌对网络”。

![](img/cc408a0c520cde9cbb28e40fcaa7a196.png)

风格转移 GAN 的基本设计:黑色箭头表示哪个样品被输送到哪里；彩色箭头表示反向传播。

给定来自输入空间的样本，可以训练生成器在输出空间中创建样本。然而，即使给定随机噪声作为输入，它们也可以被训练成产生真实的样本。为了执行风格转换(如将照片转换为绘画)，我们希望在输出样本中保留输入样本的一些内容。使用像素差分损失函数(均方误差)的天真尝试已经产生了一些初始增益，但是当输入和输出域彼此更加不同时，这些尝试无法推广。

让我们问问自己为什么会发生这种情况:请注意，最小化图像之间的像素差异与最小化像素之间的欧几里德距离是相同的，就索引而言。将逐像素损失形式化，设 x 为输入空间 x ∈ **ℝ** MxNx3 中的样本。我们希望生成器学习一个函数 g，在相同维数的输出空间中产生样本:G(x) ∈ **ℝ** MxNx3。将每个像素视为向量 p ∈ ℝ，我们在输入和输出图像中迭代相同的索引。对于每个索引[m，n] | 1≤m≤M，1≤n≤N，我们比较两幅图像中该索引处的像素。设 p₁ = x[m，n]，设 p₂ = G(x)[m，n]。像素之间的平方差是 L(p₁，p₂) =(p₁-p₂) = (p₁-p₂) ⊗ (p₁-p₂)，其中⊗是两个向量之间的元素乘积，l 是度量函数 L:ℝ xℝ ⟶ℝ.像素方面的损失只是所有平方差的平均值。

![](img/3ea512a60e8966665bceec9db9dad34b.png)

当源图像和生成的图像相同时，均方误差(MSE)被最小化。这导致了一些问题:具有完美 MSE 分数的输出样本将很容易被鉴别器归类为人工样本，仅仅因为它不属于输出域。MSE 对平移、旋转、倾斜和变换也非常敏感；即使具有低 MSE 损失的样本，简单的水平翻转也会显著增加其 MSE 值，这仅仅是因为该度量被计算为图像之间的像素分数。最后，MSE 对输入和输出样本的像素进行平均，以计算损失。平均技术通常不能获得高质量的样品。在某种程度上，这也是有意义的:我们不想优化网络以收敛到从训练集平均的样本，而是基于训练集中样本中存在的变化来创建许多独特的样本。

TraVeL 通过训练生成器学习使不同损失函数最小化的函数 G 来解决图像风格转移的问题。我们不是最小化图像空间 RMxNx3 中像素之间的距离，而是要检查输出空间中保留的更高级别特征，并最小化与输入空间中相同特征的差异。然而，我们不知道如何跟踪图像空间中的高级特征，更不用说一旦它们被生成函数 g 变换，我们如何处理这个问题？

从研究人员的角度来看，他们必须试验和尝试一些东西。他们试图保持一个合适的**不变量**:不变量是物体的一个属性，即使对它们施加一个函数，它也不会改变。形式上，设 v 和 w 是某种空间，设 f: V⟶W 是从 v 到 w 的函数映射，一个度量 l 是 f 的不变量如果对每个 x ∈ V，f(x) ∈ W，L(x) = L(f(x))。

![](img/62044b37d59693af46760b4bed6a4ef6.png)

角度是比例的不变量。在这个例子中，两个向量 v1、v2 按恒定量缩放，但是角度θ保持不变

他们希望通过教导生成器网络保持函数 G 的适当不变量，该函数将在输出空间内保留来自输入空间的一些高级特征。然而，将距离或角度等较低级别的度量保持为不变量无助于解决该任务，因为就像 MSE 度量的情况一样，只有当 g 是恒等式变换(即，x = G(x) ∀x ∈ V ⇔ L(x，G(x)) = 0 ∀x ∈ V)时，才能实现来自生成器模型的完美损失值。知道了这一点，我们训练生成器网络保持哪个不变度量？

幸运的是，他们想起了一种首先在自然语言处理领域使用的技术，叫做潜在空间编码。当把 v 看作向量空间时，任何子空间 V* ⊂ V 都可以看作 v 的潜在空间。潜在空间对我们有用有两个原因:由于 v 和 V*之间的映射函数的性质，以及由于它们内部向量之间的关系。

相同大小的图像可以被视为称为图像空间的向量空间内的向量。设 v 是一个向量空间，使得 V ~ **ℝ** MxNx3。v 可以由 NxMx3 个标准基向量跨越，每个基向量表示空间中存在的图像向量内的单个子像素。这意味着每个图像是跨越图像空间 V 的子像素的线性组合，但也意味着它们是线性独立的:每个基向量只编码一个子像素，在同一图像的子像素之间没有任何关系。

如果我们可以“压缩”这种表示，我们就可以在每幅图像的组成部分之间建立一种关系。我们可以使用映射 S: V ⟶ V*将图像映射到 v 的任何子空间，允许我们在该子空间内使用较小的基跨越相同的图像，在潜在空间中的每个基向量和原始空间中的图像之间建立一对多关系。这种映射也可以看作是“丢弃”,因为根据定义，任何到更小维度的子空间的映射都会丢失嵌入在该子空间内的向量的信息。

寻找这种转换的方法已经知道几十年了，其中最著名的是[主成分分析](/principal-component-analysis-now-explained-in-your-own-terms-6f7a4af1da8)。在认识到可以使用基于梯度的方法(如神经网络)对潜在空间进行编码之后，自然语言处理领域的最新研究应运而生。不要苦干多年试图找到一个直接的映射来最小化一个任意的度量，而是使用一个由神经网络学习的非线性函数，在相同的度量上进行优化。

因为我们可以学习优化任何度量的映射，所以我们可以明确地学习在潜在空间内优化度量的映射。例如，选择两幅图像 x₁，x₂ ∈ V，x₁ - x₂之间的差异只是图像之间的像素差异。但是因为映射 s 丢弃了关于图像的信息，差异 S(x₁) - S(x₂)意味着完全不同的东西。潜在空间 V*的维度越小，我们丢弃的信息越多，保留的信息越有意义。当然，丢弃大部分或所有信息会产生无意义的潜在空间编码，我们永远无法提前知道哪些特征将被学习(因为神经网络通常是不可解释的，我们无法提前计划它将向哪个最小值收敛)。但是根据经验，我们丢弃的信息越多，我们在潜在空间中保留的特征水平就越高。

有了这些知识，我们可以训练发电机网络来优化 g，同时添加一个**第三个网络**来优化 s。我们训练 g 保持的不变量是 l(s(x₁)-s(x₂))=l(s∘g(x₁)-s∘g(x₂)).向量 S(x₁) - S(x₂)被命名为 S(x₁)和 S(x₂)之间的变换向量，因此有术语变换向量学习。度量 L 同样被称为行程度量。

![](img/ad0ca45576191ee2e7f9eaed5663e1ad.png)

TraVeLGAN 在标准设计中增加了第三个网络，用于将行程度量保持为不变量

**型号**

我承认在编写这个模型的代码时偏离了最初的设计。论文中的规范要求一个三部分模型，每一部分都试图优化一个不同的损失函数。一台发电机，试图画出这些画；一个鉴别器，试图区分真实的绘画和人工的绘画，以及一个编码器网络，试图将行程度量保持为生成器函数的不变量。

对模型内部的深入研究可能值得在某一天发表一篇文章，但从鸟瞰的角度来看，它可以描述如下:鉴别器网络是由五个卷积层组成的完全卷积网络，每层都有两倍于前一层的滤波器。然后，输出被展平并通过完全连接的层，产生单个 logit，基于我们将进一步描述的损失函数来决定样本是原始的还是人造的。编码器网络具有相同的设计，除了全连接层输出图像在潜在空间内的嵌入(矢量，而不是鉴别器的单个 logit)。该生成器使用一种众所周知的设计，称为 U-Net，本质上是一种美化的卷积自动编码器，图像通过连续的卷积和池层向下传递，然后以相反的顺序通过相同的因子进行放大。该设计非常擅长学习卷积核的较低级和较高级特征图，并使用剩余链接来防止在产生输出图像时“忘记”在模型中较早提取的特征。

以上是您可能称之为 GAN 的“标准设计”(另外还有编码器网络)，但如果您是 GANs 新手，想要更好地理解，有许多很好的资料可以详细解释其内部工作原理。然而，我确实希望更详细地讨论设计的两个方面:损失函数和反向传播。

**损失**

TraVeLGAN 尝试优化三种不同的损失项。第一个是用于 GAN 鉴别器的“标准损失”:二元交叉熵损失(在本文中也称为最小最大损失)。设 G: RMxNx3 ⟶RMxNx3 是发生器学习的函数，D: RMxNx3 ⟶R 是鉴别器学习的函数。我们将极大极小损失表示为 L(adv)，定义如下:

![](img/87188a83b53aeae4360e5a48a61dbc36.png)

根据研究论文中的设计和调整，该模型针对不同的数据集进行了校准。当我开始训练我自己的实现时，模型不会收敛。为了解决这个问题，我决定将对抗性损失函数改为沃瑟斯坦损失函数。Wasserstein loss 计算一个称为 Wasserstein distance 的度量，它可以被视为测量两个概率分布之间的“最小”距离。它被定义为:

![](img/5b7307fdcdab3e9c696073c0fd15d9f4.png)

该公式本质上规定，我们迭代向量 x∈ **ℙ** ᵣ和向量 y∈ **ℙ** *g* 的所有组合，并将它们视为来自乘积分布π的随机样本(或者等价地，将每个视为来自其自身分布的随机样本)。然后，我们选择一个参数向量γ，当对 x 和 y 的所有组合求和时，它使距离||x — y||之和最小。Wasserstein 度量本身是包含最小γ的所有标量权重的总和。

虽然概率分布之间的距离度量比样本之间的距离度量更稳健，并且优化分布之间的距离的 GANs 在历史上比优化样本之间的距离的 GANs 达到了更好的结果，但是以上面所示的形式计算 Wasserstein 距离是一个棘手的计算。即使当用从输入空间中选择的离散样本训练模型时，置换每个小批量运行中的 **ℙ** ᵣ和**ℙ**g 的所有可能样本也是多项式时间复杂度的——对参数化γ的每个选择重复进行。

然而，一个被称为 Kantorovich-Rubinstein 对偶的相当晦涩的定理可以用来更可行地计算 Wasserstein 距离。该定理将 Wasserstein 距离视为优化问题的解决方案。最优化问题可以表述为两种形式:要么最小化一个约束，要么最大化它的逆。将优化问题公式化为最小化问题称为问题的素形式，而将优化问题公式化为最大化问题称为问题的对偶形式。Kantorovich-Rubinstein 对偶建立并解决了 Wasserstein 距离的对偶形式，提供了一个更简单的方程来测量它。在对偶形式中，它可以表示为:

![](img/d23ff4d9812f3942ba12122e26d893cd.png)

在我们问题的上下文中， **ℙ** ᵣ被表示为 D(x)而**ℙ**g 被表示为 D∘G(x).假设梯度下降过程使 D 收敛到最优函数 f，我们可以将 Wasserstein 损失改写为:

![](img/3f8c0f2241c89e1ec388f0aaefca0ce5.png)

这个解决方案带有一个警告:为了保持结果，生成 **ℙ** ᵣ和 **ℙ** *g* 的函数必须满足一个称为李普希茨连续性的约束(具体来说，就是 1-李普希茨连续性)。因为**ℙ**t20】g 中的图像是由 g 生成并由 d 分类的，所以 g 和 d 都必须是 Lipschitz 连续的。根据 Lipschitz 连续性的公式，如果存在某个常数 k，则函数 f: ℝ⟶ℝ是 K-Lipschitz 连续的，该常数满足:

![](img/1b0016003b6933ad45bbdda658a52508.png)

率先使用 Wasserstein 距离作为 GANs 损失度量的研究人员努力在他们的模型上实施 Lipschitz 约束，尝试梯度裁剪等方法，这些方法严重限制了他们模型的学习能力。然而，最近关于归一化方法的见解提出了一种解决方案，即使用一种称为频谱归一化的技术。谱范数是非标准矩阵范数，可与给定矩阵的所有标量项上的元素式 L₂范数相比。可以证明，对于任何矩阵 W，W 的谱范数等于 W 的最大奇异值，表示σ(w):

![](img/e3a2e28b3759bcdeb04632267200bf33.png)

频谱归一化就是使用矩阵的频谱范数对矩阵进行归一化的操作:

![](img/365a750adbdc111868b84fbc4de56a78.png)

根据该见解，可以通过对 G 和 d 层中的所有权重矩阵进行频谱归一化来建立 Lipschitz 连续性。此外，可以使用一种称为“幂迭代”的技术来计算频谱范数的快速近似。该技术利用了 W 的特征向量的特性，确保收敛到谱范数本身(即，在训练时段上逼近真实范数)。通过在每个小批量训练后对模型的权重执行光谱归一化，Lipschitz 连续性得到加强，允许我们使用其对偶形式来计算 Wasserstein 度量。

第二个损失项在机器学习文献中被称为裕度对比损失，并与潜在空间编码器一起使用，以确保它们不会退化到学习零函数(即，f(x) = 0 ∀x).)我们选择常数δ代表潜在空间中向量之间的最小距离，对于每一对向量 S(x₁、S(x₂，我们计算以下损失项:

![](img/341a1168a9538d0c787595b027dc0fe6.png)

注意术语 S(x₁) - S(x₂)是 S(x₁)和 S(x₂).)之间的转换向量将向量表示为 v，我们可以将上面的项重写为:

![](img/173fe10a200cb8a7d544d235612a5a40.png)

如果距离大于或等于δ，则 S(x1)的损耗，S(x2)等于 0。否则，边际对比损失将增加附加值(对于每对向量高达δ)，在此过程中不利于编码器网络。这个损失函数也被称为连体损失，因为它在来自小批量的向量对上迭代。我们将暹罗损失表示为 L *s* ，并将其公式化为:

![](img/696e126458fe3c8fc7b143a5ac0fe345.png)

第三个也是最后一个损耗项称为行程损耗，与我们在上一节中讨论的不变度量相同。表示为 LTraVeL，原始公式允许使用任何距离度量。我选择了余弦距离和欧几里德距离的组合，学习保持角度和长度。与暹罗损失一样，我们对每对向量的损失项求和，公式如下:

![](img/c5c09ffd6288ec013c93fa7eb0c9d785.png)

**繁殖**

在标准 GAN 设计中，损耗函数由发生器和鉴频器共享。当对来自输出域的样本进行分类时，鉴别器试图最小化其损失函数，而生成器试图最大化相同的损失(或者等效地，最小化否定的损失)。

在 GAN 中执行反向传播时，两个网络相互连接，这意味着鉴频器的梯度会反向传播到发生器。在形式上，我们可以把 G 看作是各个层函数的组合。设 G *L* 为发电机组成的层数，设 Gᵢ为 g 内的 I 层(1≤i≤ G *L* )。g 可以改写为:

![](img/1a21c2d837700b80fe5b956d35915191.png)

以类似的方式看 d，我们可以把 D∘G 改写为:

![](img/a8089fd82f68b2dc47e86bd1427cb58b.png)

利用鉴频器损耗，通过标准程序完成通过鉴频器层的反向传播。当通过发生器传播时，我们必须首先计算鉴别器的梯度，但是是相对于负损耗。表示鉴别器损耗 L *D* 和发电机损耗 L *G* ，我们可以使用导数的链式法则来计算给定发电机层 Gᵢ:的损耗

![](img/27efe8c6f9bd7efa924db5967cd5ec4a.png)

然后，我们跳过鉴别器层的梯度(我们应用 w.r.t. L *D* ，而不是 w . r . t . L*G*)，只对生成器权重矩阵应用生成器层梯度。

![](img/c07d83649c6aa23aa070d79cacd72275.png)

发生器(黄色)和鉴别器(蓝色)层的渐变更新细节。虚线箭头显示如何计算每个渐变，以及何时应用每个渐变。

编码器网络经历类似于鉴别器的过程。然而，因为生成器需要根据编码器函数 S 计算的损失来优化 G，所以我们需要在每个时期对生成器权重执行第二次更新。类似地表示这些术语，我们得到:

![](img/deeb65f9f0b6aefd62f0603058cad638.png)![](img/a6464a0492ea82fec967d44fb8255154.png)

渐变更新的完整方案，也包括编码器渐变(绿色)。

因此，我们对每个小批量的生成器应用两个梯度更新。从几何角度可视化梯度向量，梯度下降过程采用朝向分类梯度的最小值的下降和不变性梯度的最小值之间的平均路径。为了坚持梯度下降过程的学习速率，通常将梯度除以 2(即，计算平均梯度)，这也是深度学习编码框架(TensorFlow、PyTorch 等)的默认行为。

![](img/fd73902a528528b1074d7b8e7b5d06cd.png)

表示为矢量相加的生成器层的梯度: **∂Gi** 是应用于层 Gi 的两个梯度的总和。

**数据**

使用监督学习来训练对抗网络。也就是说，我们需要提供源域和目标域的数据以及标签来计算分类损失。因为我们使用的是 GAN 架构，所以标签是由模型本身提供的(我们知道将哪些图像提供给鉴别器，因此我们可以提供匹配的标签)。然而，图像必须事先收集。

因为我想把我的照片转换成水彩画，所以我必须收集风景照片和油画。为此，我构建了两个网络爬虫，扫描选定的网站寻找匹配的图片。第一个网络爬虫扫描了一个名为 Flickr 的网站，该网站有许多高分辨率的风景照片可供下载。第二个网络爬虫扫描了一个名为浮世绘数据库的网站，该网站保存了过去三个世纪中超过 20 万张日本木刻版画的扫描图。在对两个爬虫进行了一些优化之后，我从每个域收集了 10k 个图像，并将其保存到我的云存储中。

每个图像都被归一化到(-1，1)范围。由于水彩印刷品的扫描问题(其中许多都有注释、边框、伪像、网格线和其他不需要的元素)，我确定每个图像的中心将出现最少的干扰(根据经验)。因此，我裁剪了每张图像，在中心保留 256x256 像素，并丢弃其余的像素。然后将这些图像分组，每组 32 张。

**训练**

使用 Google Collaboratory 在可用的 GPU 上部署了该模型的四个不同实例(我通常被分配到特斯拉 P100 GPU)。冗余部署背后的原因是，初始实验表明，基于初始权重的随机选择，模型倾向于收敛于随机局部最小值。这些最小值在它们所代表的调色板中是稳定的，但是大多数调色板是完全关闭的，导致输出域图像的非自然颜色。在 30 个时期之后，当调色板稳定时，仅保留两个最佳模型，并训练总共 100 个时期。

经过训练后，从我的私人相册中收集了一个小测试集的图像，用于判断生成器输出的绘画质量。每张图片都被切成 256x256 像素的正方形。这些方块被一起分批，并作为生成器的输入。输出被重新组合，在输出域中产生新的连续图像。

![](img/0e6c9fbbfa208f7696fc1e792bdb9cce.png)

样本绘画，由生成器制作

在最初的测试中，在正方形小块之间的边界周围出现了许多伪像，导致小块之间出现可见的网格分割。使用两种方法来校正该效果:围绕中心裁剪训练集图像，以及对发生器进行小的修改。作为输入提供给生成器的每个图像被分成四个小块，并且输出小块在被馈送给鉴别器之前以相同的顺序连接。鉴别器学会了将这些图像归类为人工样本，从而教会生成器在某种程度上纠正补片之间的不连续性。

**结果**

这两个网络可以比作不同的艺术家，每一个都有略微不同的风格。“最佳”网络(最忠实于输入域的颜色方案)最终绘制出非常精确的图像。“第二好的”是画出同样精确的画，但是调色板更强调红色和粉色。

![](img/6b4f0772c04213f9e92df02826826c51.png)

**左**:第一次网络输出，“标准”调色板。**右**:第二网络输出，“红色”调色板。

当从与输入域相匹配的分布中获取照片时，两个网络都能生成非常精确的水彩画。那就是——风景图片和静态自然图片(远景、植物、树木等等)。当输入来自不同分布(动物、人、建筑物等)的照片时，结果不太准确，并且网络不能消除图像块之间的边界伪影。这种行为是意料之中的，因为网络是在风景图像的数据集上训练的，主题与目标领域的水彩画相似。从某种意义上来说，这就像让伦勃朗再造杰森·布拉克的艺术一样——可以做出一幅画，但很可能没有人会喜欢它。

最终，我选择了新京桥的照片。它横跨流经日本北部日光镇的河流，被认为是日本已建桥梁的最佳范例之一。红色的桥、蓝色的河和周围绿色的森林之间的鲜明对比被模型漂亮地捕捉到了；用简单的笔触描绘，仍然保留了原画中许多复杂的细节。

![](img/6d050a0ce8cc29e65a62b65919dbe3c7.png)

Shinkyo 桥，输出覆盖在原始输入之上。请注意对原始配色方案的保真度，以及为模拟输出域的样式所做的更改。

这张照片印在尺寸为 188x110 厘米的日本 Washi 纸上，看起来像是将木刻压在一张传统日本纸上的艺术。俗话说，情人眼里出西施。但如果我可以自夸的话，这是我迄今为止制作的最好的艺术品之一。

![](img/3e19088215d782b17abc69bedf721c47.png)

自豪地展示！

**代号**

用于训练网络的代码和数据可从以下链接获得:[https://drive . Google . com/drive/folders/1 smqebd 7 huzooxb 5k xmhtf 1 ldajwofwnb](https://drive.google.com/drive/folders/1SMQEbd7HUzoOxb5kxMhtF1lDajwoFWNB)