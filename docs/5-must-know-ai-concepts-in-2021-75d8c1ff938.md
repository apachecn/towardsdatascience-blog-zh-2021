# 2021 年必须知道的 5 个人工智能概念

> 原文：<https://towardsdatascience.com/5-must-know-ai-concepts-in-2021-75d8c1ff938?source=collection_archive---------16----------------------->

## 人工智能|解释

## 这是你不想错过的。

![](img/7b01fff9fb4ddc6b983766feb368f7e2.png)

道格拉斯·桑切斯在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

AI 应该通过复制我们的生物来模仿人类的智能吗？或者我们的心理生物学本质与人工智能无关，就像鸟类生物学与航空航天工程无关一样？

这是该领域的人们自其提出以来一直在思考的问题。我们想要建立智能系统，而我们人类可以说是唯一真正智能的物种。从我们身上寻找灵感难道不符合逻辑吗？然而，因为人工智能的构建模块与生物学的基本部件如此不同，我们难道不应该忘记人类，沿着我们的研究引领我们的道路前进吗？

没有人知道人工智能的未来会怎样。我们知道的是，现在的深度学习越来越接近类人认知。也许人类在智力方面并不特别，但进化给了我们一些独特的特征，我们在创建人工智能系统时最好考虑到这些特征。我们已经在这种环境中进化了几千年，慢慢适应了不变的自然法则。为什么不通过模拟我们的抛光机制来绕过这个过程呢？

在这篇文章中，我将谈论目前处于人工智能研究前沿的五个例子。每一个都至少松散地基于人类认知功能的某些方面。这些概念将是未来几年的核心，所以让我们密切关注它们。

# 变形金刚——人类的注意力

不久前，基于递归的架构主导了自然语言处理(NLP)。如果你面临一个自然语言处理问题——翻译、语音转文本、生成任务——你要么使用门控循环单元(GRU)，要么使用长短期记忆(LSTM)。这两种架构是为处理顺序输入数据而设计的。例如，该系统可以将一个英语句子和每个连续的单词翻译成西班牙语。

这些模型的主要缺点之一是[消失梯度问题](https://en.wikipedia.org/wiki/Vanishing_gradient_problem)。因为信息是按顺序处理的，所以当系统要输出第一个法语单词时，第一个英语单词只是被记住了。为了解决这一缺陷，研究人员在 2014 年引入了[注意力机制](https://arxiv.org/abs/1409.0473)。通过模仿认知注意力，神经网络可以衡量环境的影响。不再有信息丢失。

2017 年，谷歌的 AI 团队发表了开创性的论文 [*注意力是你所需要的全部*](https://papers.nips.cc/paper/2017/file/3f5ee243547dee91fbd053c1c4a845aa-Paper.pdf) 。它说:注意力机制强大到足以解决语言任务。我们不需要递归，也不需要顺序处理。他们发明了著名的变压器架构。变形金刚影响深度学习格局的方式只能与 2012 年辛顿的团队赢得 ImageNet 挑战赛时 CNN 在计算机视觉(CV)中的颠覆相媲美。

转换器的工作原理是并行处理一个句子中的所有单词(记号),并学习它们之间的上下文关系。与 LSTM 相反，变压器不按顺序处理数据。训练时间要短得多。如今，变压器是任何 NLP 任务的首选架构。甚至 CV 的科学家也开始将变形金刚应用于图像和视频问题。即使是卷积也不能幸免于关注。

从 2017 年到 2021 年，研究人员进一步开发了变压器，旨在解决各种缺点，提高性能。[transformer-XL](https://arxiv.org/pdf/1901.02860.pdf)更大，允许系统在更大的上下文中学习依赖性。GPT-3——它建立在最初的 transformer 架构上——不能越过它的上下文窗口，这使得它没有记忆。改革者解决令人望而却步的培训费用。它提高了效率，减少了培训时间，同时实现了最先进的性能。

近年来，变形金刚最引人注目的一些应用是多任务人工智能，如[谷歌的 BERT](https://blog.google/products/search/search-language-understanding-bert/) ，OpenAI 的 GPT 家族——其中 [GPT-3 是毫无争议的明星](/gpt-3-a-complete-overview-190232eb25fd)——[悟道 2.0](/gpt-3-scared-you-meet-wu-dao-2-0-a-monster-of-1-75-trillion-parameters-832cd83db484) ，它保持着最大神经网络的记录。变压器也是新一代聊天机器人——[Meena](https://ai.googleblog.com/2020/01/towards-conversational-agent-that-can.html)、 [BlenderBot 2.0](/better-than-gpt-3-meet-blenderbot-2-0-facebooks-latest-chatbot-8941f100d146) 或 [LaMDA](/googles-lamda-the-next-generation-of-chatbots-62294be58426) 背后的核心算法。它甚至涉足了生物学领域。几天前 DeepMind [宣布](https://deepmind.com/blog/article/putting-the-power-of-alphafold-into-the-worlds-hands)他们已经发布了 [AlphaFold 2](https://deepmind.com/blog/article/alphafold-a-solution-to-a-50-year-old-grand-challenge-in-biology) 的代码和数据库。一个有助于更深入理解蛋白质折叠的模型。

# 自我监督培训——人类学习

**自 2012 年以来，有监督的深度学习系统**一直主导着人工智能领域。这些系统从标记的数据中学习，以将新的实例分类到学习的类别中。我们投入大量资源对训练样本进行分类，以方便学习。然而，这些模式匹配系统不像我们一样学习。

强化学习更像我们学习的方式。这些系统生活在一个受限制的虚拟世界中，在这个世界中，它们可以做一组有限的动作来获得奖励。DeepMind 的研究人员几个月前发表了一篇论文，认为“[奖励足以](https://deepmind.com/research/publications/Reward-is-Enough)”实现通用人工智能。然而，并不是人们所做的一切都是为了优化奖励，就像增强人工智能所做的那样。更不用说我们世界的复杂性，每时每刻可能的行动数量，或者我们想要或需要的复杂性和细微差别。

出于上述原因，研究人员最近对**无监督**——或 [**自我监督**](https://bdtechtalks.com/2020/03/23/yann-lecun-self-supervised-learning/)——Yann le Cun 喜欢称之为学习——的范式产生了更多的兴趣。他认为我们的学习与这些系统相似(至少与其他范式相比)。人类通过[观察](https://en.wikipedia.org/wiki/Observational_learning#Observational_causal_learning)和感知世界学到很多东西。这就是自我监督学习的意义。

> *【自我监督学习】就是*在学习一个任务之前，先学习代表世界的思想。这是婴儿和动物做的事情*。[……]*一旦我们对世界有了很好的描述，学习一项任务就需要很少的试验和样本。”

*   监督学习系统学习在数据中寻找模式，而不关心世界。
*   强化学习系统学习优化奖励，而不关心世界。
*   自我监督学习系统需要代表世界来理解事物之间的关系。

这些系统可以从输入的可见部分中学习输入的隐藏部分。例如，如果你向一个自我监督的系统输入半个句子，它可以预测缺失的单词。要做到这一点，他们需要对事物之间的关系有更深入的了解(这并不是说他们理解世界的方式和我们一样，事实并非如此)。

对大量标记数据(监督学习)和不可计数模拟(强化学习)的需求是一个障碍。自我监督学习旨在解决这两个问题。这些系统在没有明确告诉它们必须学习什么的情况下学习。没有课。没有任务。

自我监督学习的一些重要成功都与 transformer 架构有关。例如，伯特或 GPT-3 已被证明在语言生成任务中非常成功。在许多 NLP 领域中，自我监督系统现在是最先进的。这些系统的一个显著缺点是它们不能处理连续的输入，例如图像或音频。

> "人工智能的下一场革命将不会受到监督，也不会得到纯粹的强化."
> 
> ——扬·勒昆

# 即时编程——人际交流

低代码和无代码计划出现在几十年前，是对编码领域日益扩大的技能缺口的一种反应。创建好的代码和知道如何在设计-生产管道的不同点处理任务的技术能力是昂贵的。随着软件产品变得越来越复杂，编程语言也越来越复杂。No-code 旨在为非技术业务人员解决这一差距。这是一种绕过编码让任何人都可以访问结果的方法。

几年前，知道如何编码可以说和说英语一样重要。你要么知道要么错过了很多。工作机会、书籍和文章、论文以及其他技术工作...在未来，智能房屋(domotics)的比例将会增加。技术软件技能可能和现在一样重要，比如知道如何修理水管或坏掉的灯。

在无代码计划和人工智能的未来的交叉点上，我们有即时编程。GPT 3 是最著名的使用提示的人工智能系统。OpenAI 去年发布了 API，人们很快就认识到了提示的独特性。这是不同的东西；既不是与人交谈，也不是正式意义上的编程。Gwern 称之为的提示编程(Prompt programming)，可以理解为一种新的编程形式。它不像无代码那样肤浅，因为我们用自然语言与系统交流——我们给它编程。它不像用 C 或 Python 编程那样技术性很强。

GPT-3 引起了研究人员和开发人员的注意，许多人被激励去发现它的缺点。一些人发现 GPT 3 号在应该成功的地方失败了。然而，格温证明他们错了。他认为我们应该像用英语编程一样接近 GPT 3 号。我们必须把它做好，不是每件事都顺利。他调整了提示，重复了测试，并成功地教会了 GPT-3 正确地完成任务。他说:

> "*【提示】*是使用 DL *【深度学习】*模型的一种相当不同的方式，最好把它看作一种新的编程，其中提示现在是一个“程序”，它对 GPT-3 进行编程以做新的事情。"

GPT-3 激发了用英语编写系统程序的可能性。该系统可以理解我们的意图，并以一种它可以毫无疑问地解释它们的方式将它们翻译给计算机。

一个月前，微软——去年与 OpenAI 合作的微软——发布了 GitHub Copilot。该系统由 GPT-3 的后代 Codex 驱动，是一个强大的代码自动完成系统。微软看到了 GPT-3 在创建代码方面的潜力，以及它如何理解英语并将其转化为编写良好的功能性程序。除了其他功能之外，Copilot 还可以阅读用英语描述某个功能的注释，对其进行解释，并记下该功能。

GPT-3 和 GitHub Copilot 将无代码的承诺和即时编程的潜力结合到一个新时代，这将允许非技术人员进入编码世界。

即时编程的主要优势以及它会成功的原因是，我们人类已经进化到用自然语言交流，而不是用正式语言。英语有一系列我们凭直觉知道的规则。在我们理解我们正在使用的规则之前，我们学习正确地说话。我们不会发明规则，然后遵守规则。我们发现我们已经遵循的规则。

写 Python 或者 C 就不一样了。我们称它们为语言，但它们在很多方面与英语不同。计算机需要明确的、不可解释的命令来知道该做什么。编程语言有严格的语法规则，不能被破坏，否则程序不会运行。这没有捷径可走。在没有提示编程的情况下，如果你想与计算机交流，你必须学习它的语言。甚至像 Python 这样的高级语言也需要相当程度的技术专长，而大多数人都不具备。

即时编程是编码的未来:我们将能够用自然语言编写大多数东西。将会有中间系统来处理我们不精确的、细微的、充满上下文的思想和计算机需要工作的正式指令集之间的转换。

# 多模态——人类感知

直到最近，深度学习系统还被设计用来解决单峰问题。如果您想在机器翻译方面达到最先进的性能，您可以使用英语-西班牙语文本数据对来训练您的系统。如果你想战胜 ImageNet 挑战，你的系统必须在物体识别方面是最好的，除此之外别无其他。NLP 系统和 CV 系统是截然不同且不可混合的。

现在，研究人员从神经科学中获得灵感，试图模拟我们的感知机制，专注于创建从不同类型的数据中学习的人工智能系统。与其按照专业领域来划分系统，为什么不让它们结合来自视觉和语言来源的数据呢？短信里有信息。图像中有信息。但是在两者的交汇处也有信息。这种多模态系统的新趋势就是谷歌和 BAAI 今年分别用 MUM 和 Wu Dao 2.0 T5 所做的。这是试图让人工系统类似人脑的一个进步。

我们已经进化成了一个多模态的世界。我们周围的事件和物体产生不同种类的信息:电磁的、机械的、化学的……例如，一个苹果有颜色、形状、质地、味道、气味……这就是为什么**我们的大脑是多感官的**。我们有一套感知系统，可以捕捉世界的多模态性质(其他生物有不同的感知系统，允许它们感知我们在生物学上不知道的模式)。更有趣的是，大脑将来自感知通道的信息整合到现实的单一表征中。

这就是我们可以从给人工智能灌输这种能力中找到效用的地方。如果给一个模型一对文字图像可以让它更准确地表现世界，那么它的预测或行动就会更精确，也能更好地适应环境。这就是今天对[智力](https://www.simplypsychology.org/intelligence.html)的定义:“利用遗传能力和学到的知识理解和适应环境的能力。”

一个拥有相当于眼睛、耳朵和手的人工器官以及作为大脑的 GPT-3 的机器人将比任何现有的人工智能都要强大得多。大脑是所有处理发生的地方，但处理的数据也很重要。未来的人工智能系统将拥有传感器、控制器和执行器，它们以一种快速、准确和丰富的信息处理方式相互连接。

焦点仍然在以软件为中心的虚拟系统上，但是一些研究小组已经成功地集成了文本和图像数据。这些网络应该如何结合这两种类型的信息仍然是一个谜(人类也没有完全理解)，但目前这些尝试已经成功了。 [DALL E](https://openai.com/blog/dall-e/) ， [CLIP](https://openai.com/blog/clip/) ， [MUM](/will-googles-mum-kill-seo-d283927f0fde) ， [UC](https://arxiv.org/pdf/2104.00332.pdf) ，[武道 2.0](/gpt-3-scared-you-meet-wu-dao-2-0-a-monster-of-1-75-trillion-parameters-832cd83db484) 就是活生生的证明。

# 多任务处理和任务转移——人类的多样性

监督和强化的人工智能系统是糟糕的多任务处理系统。即使是像 AlphaZero 这样被设计用来学习不同任务的系统，也必须为每个任务进行遗忘和重新学习。然而，自我监督系统在这方面更胜一筹。原因是他们接受的是任务不可知的训练。因为这些系统没有被明确告知从输入数据中学习什么，所以它们可以应用于不同的任务，而不需要改变参数。GPT 3 号就是这种情况。

GPT-3 最有力的特点之一是它能够用相同的砝码处理不同的任务。该系统不会在内部进行改变，以进行机器翻译、回答问题或生成[创意小说](https://www.gwern.net/GPT-3)。该系统是以无监督的方式从大多数互联网文本数据中训练出来的。但是它不知道如何运用它所学到的东西。在快速编程的帮助下，用户可以调节 GPT-3 来解决给定的任务。根据记录，GPT 3 号在几项未经训练的任务中达到了最先进水平。这就是**多任务处理和任务转移**的威力。

多任务系统可以将相同的输入应用于不同的任务。例如，如果我把“猫”这个词输入系统，我可以让它找到西班牙语翻译“gato”，我可以让它给我看一只猫的图像，或者我可以让它写一篇关于为什么猫如此怪异的文章。相同输入的不同任务。

这种想法经常与**的少投学习**结合在一起。有监督的深度学习系统在预先选择的一组类上进行训练和测试。如果一个 CV 系统已经学会了对汽车、飞机和船只图像进行分类，它只会在这三个类别上测试时表现良好。在少量(或零次/一次)学习设置中，系统针对新的类进行测试，而没有权重更新。

一个例子是在测试时向系统显示一辆自行车的三幅图像，然后要求它正常地对汽车、飞机、轮船和自行车图像进行分类。这很简单，因为我们已经在测试时展示了 3 个自行车的例子。一个学会了如何学习的系统(如 GPT-3)应该能够在这些极端情况下表现良好。GPT 3 号证明了这是可能的。而且它的表现也没有被监督系统羡慕的地方。

如果我们结合多任务和少镜头设置，我们可以建立一个系统，能够解决它没有训练过的任务。在这种情况下，我们不是在测试时向系统显示新的类，而是让它执行新的任务。在少数镜头设置的情况下，我们会展示几个任务是如何完成的例子。而且，在没有内部学习任何新东西的情况下，系统现在会被调整来解决新的任务。

例如，让我们以一个在巨大的文本语料库中训练的系统为例。在一次性任务转移设置中，我们可以写:“我爱你-> Te quiero。我讨厌你-> ___”我们通过向系统展示一个例子(一次性设置)，隐式地要求系统将一个句子从英语翻译成西班牙语(这是一项未经训练的任务)。

想想看，我们人类是可以做到这一点的。我们是元学习者。我们不只是学会做任务，而是知道如何学会做新的任务。如果我看到有人在打扫房间，我会马上知道怎么做。我明白扫帚的运动必须方向一致才能清洁地板，我会努力协调手和脚，使过渡平稳。我们不仅仅在有人训练我们的时候学习。我们通过观察来学习。几杆任务转移就是这样。人工智能系统开始在这方面做得更好。

## 订阅我的免费每周简讯[明日之心](https://mindsoftomorrow.ck.page/)获取更多关于人工智能的内容、新闻、见解和思考！

## 此外，欢迎在 [LinkedIn](https://www.linkedin.com/in/alberromgar/) 或 [Twitter](https://twitter.com/Alber_RomGar) 上发表评论和联系！:)

# 推荐阅读

</5-deep-learning-trends-leading-artificial-intelligence-to-the-next-stage-11f2ef60f97e>  </gpt-3-a-complete-overview-190232eb25fd> [## GPT-3 —全面概述

towardsdatascience.com](/gpt-3-a-complete-overview-190232eb25fd)