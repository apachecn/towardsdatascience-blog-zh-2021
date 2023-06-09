# 作为开源机器学习框架创建者，我学到的 5 件事

> 原文：<https://towardsdatascience.com/5-things-ive-learned-as-an-open-source-machine-learning-framework-creator-10ca2a577a55?source=collection_archive---------35----------------------->

## [行业笔记](https://towardsdatascience.com/tagged/notes-from-industry)

## 如果你是一个有抱负的开源机器学习框架的创建者或维护者，你可能会发现这些提示很有帮助。

![](img/39335965b22b359ef0f925f7e7dab6c6.png)

作者拍摄的照片(布莱斯峡谷 UT 在我的 2021 年公路之旅)

创建一个成功的开源项目非常困难，尤其是在数据科学/机器学习/深度学习领域。大量开源项目从来不用，很快就被放弃了。作为[流量预测(Flow Forecast)的创建者，这是一个针对时间序列预测框架](https://github.com/AIStream-Peelout/flow-forecast)的开源深度学习，我分享了我的成功和陷阱。以下是我为有抱负的开源机器学习框架的创建者/维护者提供的技巧汇编。

1.  **文档，文档，文档**

拥有好的文档、教程和入门指南可能是任何开源框架最重要的方面之一。虽然在工作环境中，代码库的知识通常在会议、辅导和结对编程会议上共享，但对于开源项目，主要的学习方法是通过文档、教程和示例。此外，数据科学家通常非常忙碌，如果您的文档/入门指南不清楚，他们通常会转向更易于使用的框架。不管模型的承诺性能如何，这通常是正确的。

为了帮助人们容易地开始使用你的框架，我推荐一个简单的入门教程。除了入门教程之外，你还需要一个地方来存放方法和类的更详细的文档。这对贡献者和高级用户都很有用。我发现 [ReadTheDocs](https://flow-forecast.readthedocs.io/en/latest/) 很适合这个目的。对于数据科学项目(尤其是 ML 繁重的项目)，您可能还需要一个包含概念信息和模型性能信息的站点。特别是对于 FF，我们决定使用 Atlassian 的 Confluence。这为更多的概念性信息和模型结果提供了完美的位置，而不会弄乱代码文档。

当然，文档的编写和维护是相当耗时的。所以你应该在这上面投入充足的时间。我发现的一个诀窍(如果你可以这样称呼它的话)是，在编写代码的同时编写文档是最容易的。时间越久，你对代码的记忆就越模糊。最终，您和您的其他维护人员甚至不会记得某个特性存在于代码库中。所以马上写你的文档吧！

我发现的另一件有用的事情是，在做任何设计改变之前，开始一个设计文档。然后，设计文档就成了对项目的变更和变更原因的生动记忆。另一个技巧是在 VSCode 中使用类似 Python DocString Generator 的扩展。这些将自动生成适当格式的文档字符串，用于呈现您的在线文档站点。

2.**“如果你建造了它，他们就不会来了”**

不幸的是，创建一个好的开源数据科学框架不会自动让人们使用它。此外，很多时候，成为最流行的框架不一定是最好的，而是营销、品牌和关键字优化最多的框架。虽然许多 ML 开发者更喜欢只关注事物的技术方面，但营销和推广是必要的。

这是我们在流量预测早期努力解决的问题。尽管是第一个支持变形金刚的时序框架，但我们并没有做什么推广。其他框架很快出现，并在社交媒体上获得了更多的关注。我们面临的另一个挑战是我们框架的名字。尽管 FF 向存储库的根源致敬，但它有时会让人们困惑，让人们认为我们只是一个预测河流流量的框架，而不是一个通用的时间序列预测框架。因此，我建议从一开始就选择一个相当通用的名字。

为了更好地营销你的知识库，我建议定期在媒体上写文章，并发布教程视频。这有助于提高你的框架的流量，并建立星级。你也可以(偶尔)在适当的 Reddit 子编辑上发布主要版本。在本地聚会上发言是在 DS 社区中传播您的框架意识的好方法。大多数聚会总是在寻找新的演讲者，并且非常支持开源项目。最后，在流行的 Kaggle 数据集和竞赛上使用你的框架的教程笔记本也能有所帮助。

虽然星星真的不应该意味着太多(我认为 watchers 和 forks 是一个更好的指标)，但它们在 GitHub 的推荐算法和其他人如何看待你的回购中起着核心作用。因此，随着时间的推移，尝试在存储库上建立星星是很重要的。如果你能在短时间内获得足够多的明星，你的知识库也将开始形成趋势，这将导致更多的明星。记得在 GitHub 上给你的库添加合适的标签，这样会给你的库排名(根据标签上的星星)。

举办定期活动也可以让更多的人参与到你的知识库中来。2020 年，我们举办了 FF sprint，作为 PyData 全球活动的一部分。今年在 FF，我们计划举办一场黑客节冲刺赛(点击查看[细节](https://github.com/AIStream-Peelout/flow-forecast/discussions/419))。在这些活动中，迅速响应 PRs 并准备好回答开发人员可能提出的问题非常重要。像 t 恤这样的激励也可以激励参与者贡献更多相关的功能。

**3。测试**

测试是具有挑战性的，尤其是在机器学习领域，因为大多数 ML 模型显然是不确定的。最好从简单开始，利用标准类型的单元测试(例如，测试是否返回正确的形状，测试训练循环是否端到端运行)。确保包含单元测试和集成测试。测试应该用 CircleCI 或 Travis-CI 这样的工具来运行。您可以使用 CodeCov 或其他工具来自动跟踪您的代码覆盖率。一旦你有了基本的代码覆盖，并确保这些测试通过，你现在可以开始更棘手的测试了。

为了测试诸如测试的有效性和评估循环之类的东西，你可能需要创建一个虚拟的确定性模型。然后，您可以使用虚拟模型和小型数据集运行这些函数，并检查计算是否准确。对于模型，您可以编写相对便宜的收敛“测试”来确保模型在几个时期后收敛。有了这些测试，你就可以安心了，你的代码运行正常。

也许最棘手和最耗时的测试形式之一是确保你移植到你的框架中的模型与论文中提到的原始结果相匹配。这通常需要使用精确的超参数进行实验，并对论文进行预处理。这些测试不能作为 CI 的正常部分运行，因为它们会花费太长时间。相反，它们应该只是偶尔运行一次，以确保模型性能不会随着主要框架修订而改变。

**4。良好的依赖性管理和向后兼容性是必不可少的**

当维护一个开源项目时，依赖关系是一个经常要处理的问题。我的首要建议是在 requirements.txt 文件中设置依赖项的版本。否则，每当一个依赖项被更新时，它可能会破坏您的代码，您将会收到一串来自用户的消息，他们想知道为什么他们的代码突然不能工作了。Dependabot 擅长打开 PRs 来自动增加依赖项，然后您可以很容易地看到它们是否会通过 CI。查看我的另一篇[文章](/how-to-make-your-deep-learning-experiments-reproducible-and-your-code-extendible-7ef56767dddb)了解更多信息。

另一件需要跟踪的事情是你的框架在 PyPi 上的版本和你的发布周期。有一个易于使用的 GH 工作流，可以在发布时自动推送至 PyPi。我通常尝试在每个月初发布(或者如果我每隔一个月就发布一次)。

**5。选择系统以确定问题/新功能的优先级**

这就引出了我们的下一点，创建一个系统来区分问题的优先级。对于许多开源维护者来说，时间是极其稀缺的。然而，bug 和所请求的特性的数量继续呈指数级增长。因此，跟踪进度和管理未决问题非常重要。在 FF，我们尝试了各种项目管理工具(如 JIRA)，但最终发现简单的 GH 问题和项目委员会效果最好。

开源维护者面临的另一个困难是委派工作。开发人员经常会出于好意自愿实现某个特性，但是却陷入了其他工作的泥沼，无法完成指定的问题。你应该试着定期与开发人员联系，尤其是在重要问题上。如果有必要，你应该尽可能礼貌地将问题重新分配给其他人来完成，如果是关键问题。

我希望你觉得这个指南有用！请随意留下任何问题或评论。也请检查我的其他文章！