# 业内成功数据科学项目的 7 个技巧

> 原文：<https://towardsdatascience.com/7-tips-for-a-successful-data-science-project-in-the-industry-1aa4166708?source=collection_archive---------21----------------------->

## [办公时间](https://towardsdatascience.com/tagged/office-hours)

## 你参加的任何课程都没有给出的建议

![](img/15534696d6e44945f483f0d067a2861b.png)

[Racool_studio](https://www.freepik.com/free-photo/toy-bricks-table-with-word-tips_10051082.htm#page=1&query=tip&position=39) 在 [freepik](https://www.freepik.com/) 上拍摄的照片

# **简介**

我决定写这篇文章，因为它包含了课程中通常不会涉及的主题，或者任何其他与数据科学相关的材料。大多数资料包括你应该学习的工具、你应该知道的算法解释、数据科学项目的生命周期等等。

这篇文章不一样。它包括了我根据自己的经验收集的一些技巧，这些技巧相当普遍。不管你在哪个领域工作，它都是相关的。也许这与那些在创业环境中工作的人更有关系，但不是唯一的关系。而且，坦白地说，我把这篇文章看作是自己不时回顾的参考，以确保我在正确的轨道上:)

**业内认为什么是成功的项目？**

简单来说，如果你的项目给你的公司带来了价值，那就是成功的！但是，除了您的解决方案的准确性(或使用的任何其他指标)，一个关键因素是定制解决方案的速度。DS 项目通常需要时间，但理想情况下，我们希望它们越短越好。有些情况下，项目进行到一半时发现了一个错误，迫使我们(几乎)重新开始。这是我们想要避免的情况。这些技巧的目的是创建更好的解决方案，并在尽可能短的时间内集成它们。

那么如何才能让我们给公司带来的价值最大化？

# **1。定义问题和目标**

> 经理:“我需要你建立一个模型，识别系统中流动的坏数据。”
> 
> 我:“嗯，当然，没问题。只要让我知道数据在哪个数据库中，我就能马上找到它。”

但究竟什么是“坏数据”？为什么我们要过滤掉呢？这个项目的商业价值是什么？重要的是要明确问题是什么，我们的目标是什么。在这种情况下，假阳性的代价是什么？是否等同于假阴性？**询问所有需要的问题，以便达到一个明确的目标**，并且**为您的项目创建一个明确的指标**，最好是一个单一的值。如果你执行了构建模型的整个周期，却发现你没有完全理解问题到底是什么，这是一种耻辱。你可能不会完全回到起点，但这是在错误的方向上花费了很多努力。

有些情况下，你需要依赖公司的其他人员来完全理解项目。不要拖延，向前迈进，明确定义你的项目需要什么。

由于我们正在讨论项目的开始，我将添加另一个与项目的这个阶段相关的注释。你的经理不一定理解手头问题的难度。反映项目的初步结果(你将达到什么样的准确度，等等)是很重要的。).你可能会有点偏离，但是当你带着结果回来时，你不希望得到“哦…”的反应。从一开始就保持一致。

# **2。充分理解数据**

> 经理:“标签列中缺少值。这表明注释者没有在图像中找到任何东西。

这听起来合乎逻辑。但是结果表明，缺少的值也表明注释者无法确定 6 个可能的标签中哪一个是最准确的，所以他将其留空。这两种情况是完全不同的，但是如果两种类型的缺失值被相同地对待，这将损害您的训练模型。

确保你很好地理解你的数据是至关重要的。您可能设计了一些功能，但后来发现设计错误(例如，您获取了一个“邮政编码”列并将其存储到某个国家的不同地区，但结果发现并非所有的邮政编码都属于同一个特定国家)。

无论是标签列，还是您将用作功能的列，**确保您对数据的理解与您希望的模型一样准确**。您甚至可以咨询注释者自己或他们的经理。不惜一切代价。

# **3。生产中会是什么情况？**

> 经理:“相关数据在表一、表二、表三、表四。一个简单的连接就能得到所有的数据。”

太好了，你需要的都有了。您继续开发您的模型，获得了很好的结果，并且您已经准备好将它部署到生产中了。你只需要做最后的调整。

> 我:“说，哪一个来源提供字段 A？”
> 
> 经理:“A 场？一旦数据完成了系统中的全部流程，我们就会对其进行一些充实。”

哎呀，这可不好。事实证明，这甚至是一个不会给模型的准确性增加太多的功能。但是你的模型已经用它训练过了。**确保您了解您的模型将投入生产时的情况，这样您的模型将拥有所需的所有数据，并且适合生产中的特定设置**。

# **4。保持简单**

> 我:“我想我会先试试超级酷的型号。你怎么看？”
> 
> 经理:“你是有知识的人。去吧！”

如前所述，通常你的目标是相对快速地带来结果。你的经理并不总是知道可能的解决方案是什么。**通常，考虑到投入的时间，简单的解决方案更有价值**。而且，不管投入多少时间，它们的表现往往比你认为很酷的超级复杂的解决方案还要好。当然，情况并不总是这样，但至少在转向“酷”的解决方案之前，先尝试更“简单”的解决方案。

此外，通常有可能用一个简单的解决方案至少部分地解决问题。这样做的时候，你已经在创造价值了。一旦完成，如果还需要的话，你就可以前进到更复杂的解决方案。

# **5。咨询他人**

> 我:“是啊，我试过算法 a，这里看起来是个不错的解决方案。”
> 
> 同事:“有意思，在这里可能行得通。不过我想我会在这里尝试算法 B。”
> 
> 我:“嗯……没有想到。好主意！”

希望你不是公司里唯一的数据科学家。如果是这样，这是一个向他人学习的好机会，听听他们会如何解决你的问题。不要觉得不舒服。**没有人能想出所有可能的解决方案，也没有人什么都知道**。此外，通常情况下，一起头脑风暴的结果是，你自己会想到一个想法，如果没有这个咨询，你是不会想到的。

关于这个话题，我还想补充一下**规划你的项目和将工作分成任务**的重要性。集体讨论的结果应该就是这样。这将使你能够保持专注，而不是过多地研究一个潜在解决方案的特定算法。

# **6。误差分析**

> 经理:“我想知道为什么模型在情景 A 和 B 中表现良好，而在情景 c 中表现不佳。”
> 
> 我:“我觉得另一个算法会更好。此外，对更多数据的训练可能会奏效。”

是啊，这可能不是你得到这份工作时的梦想。但这非常重要。手动查看几个(或许多)错误可以给你一个很好的直觉，知道哪里错了。不要觉得这“不是我应该做的事情”。这可能比仅仅向你的模型扔更多的数据更有效。

# **7。文件**

> 我:“我从数据中过滤掉那些行是有原因的。我不记得我为什么那样做了……”

这有时是一个被忽视的步骤，或者只是做了一部分。你正在做的当前项目中有一些元素，当你下个月继续下一个项目时，你会忘记它们。记录您在整个项目中采取了哪些步骤，选择了哪些数据及其原因，您在 DB 上运行的查询(当然还有您的代码！).**越多越好**。当您可能需要修改项目并改进您的解决方案时，或者当您将要处理与此项目相关的另一个项目时，这将非常有用。你甚至可以在仍然进行项目的时候从文档中获益(“为什么我又决定走路线 A 而不是路线 B..?").

# **结论**

如果我不得不用几句话来总结一个人为了在行业中部署一个成功的项目需要做什么，我会说**务实**和**与你的同事和经理良好沟通**很重要。不要被动，要主动，确保你拥有所有你需要的信息。并且**把你的注意力集中在你的目标上**。我希望你觉得这很有见地:)祝你好运！