# 四年内做软件工程师、机器学习工程师、数据科学家，我学到了什么。

> 原文：<https://towardsdatascience.com/i-worked-as-a-software-engineer-machine-learning-engineer-and-data-scientist-within-four-years-a4afa19545ca?source=collection_archive---------4----------------------->

## 从角色转换和科技职业导航中学到的经验

![](img/716452e942e7382f360772f481e41a4c.png)

图片来源:MSIA 西北部。我在教室里用我的笔记本电脑做一些事情。

# 嗨，我是杰森。

我是一名会计出身的数据科学家，一名数据科学家出身的软件工程师。

# 介绍

你好。4 年前，我得到了第一份数据科学家(DS)的工作，我在 TDS 上讲述了那次[经历。两年前，我离开了数据科学家的职位，成为了一名软件工程师(SWE)。上个月，我辞去了在 GoDaddy 担任机器学习工程师(MLE)的工作。善变吗？这是一个关于我如何转入软件工程并离开数据科学的故事。这也是我在短短 4 年内拥有三个不同头衔(DS、SWE、MLE)后获得的观点。以下是我的头衔、团队、技术团队和简短的角色描述，供您参考:](/how-to-data-science-without-a-degree-79d8388a49ba)

*   **数据科学家**(市场营销、数据科学):Python、Tensorflow、PySpark、SQL →建立大量的 ML 模型，用于预测客户行为、构建特征和进行分析。
*   **软件工程师**(数据平台):Java、Beam、Spark →为其他团队构建和生产核心数据产品。
*   **机器学习工程师** (GoDaddy 机器学习):Python，AWS →在 AWS 中搭建 ML 平台，将 ML 模型部署到生产中。

当我进入一家新公司时，我想回顾一下我的经历，并谈谈这篇文章中的要点。我喜欢和不喜欢这些角色的什么？我后悔这些开关吗？如果你曾经想换工作，我希望这些课程能帮助你做出决定。

# 我在数据科学中不喜欢的是

作为数据科学家的最初几年是一段狂野的旅程。我学会了如何构建和部署模型、自动化管道、分析结果等等。虽然作为一名数据科学家，我喜欢做很多事情，但也有一些事情让我感到困扰。

首先是**杂乱、无组织、无文档记录的代码/查询**。人们通常不太关心你的代码，主要是因为这些代码通常不会投入生产。也是因为很多 DS 项目都是单人项目。当只有您和经理时，您可能不太关心变量的格式和硬编码。只要结果是好的，我们就可以继续前进，因为你不会重新访问相同的代码。

其次是**将机器学习模型部署到面向客户的生产**中的困难和无力。这在很大程度上取决于你公司的内部工具。像脸书和谷歌这样的公司拥有成熟的 ML 部署工具，科学家可以用它们来部署模型。在许多其他公司，数据科学家可能需要自己解决，或者依靠其他软件工程师来生产。作为一名数据科学家，我觉得自己拥有整个管道和部署自己的机器学习模型的能力有限。在大公司中创建一个面向客户的 ML 模型并不是一件容易的事情。您需要确保模型具有低延迟，符合公司编码标准，经过审查和测试，并有随叫随到的员工来处理故障。

# 我喜欢软件工程的什么

首先，你去**制造一个产品**。当你做了一件东西，看到其他人使用它并从中受益，这是一种很棒的感觉。它可以是数据产品、web 应用程序或 API。Lyft、Shopify 和 Instagram 等公司都是软件产品的例子。一个好的产品会持续很长时间，并在世界上产生很大的影响。虽然分析是有用的，可以引导公司的方向，但它只在特定的情况下使用一次。当你真正建造一个东西时，这是一种非常不同的感觉。

第二，**自动化**让你的生活更轻松。尽管自动化并不是软件工程的专利，但它在数据科学中并不常见。例如，像 Jenkins 这样的工具可以帮助你从 Github 自动构建、[单元测试](https://en.wikipedia.org/wiki/Unit_testing)，部署你的代码( [CICD](https://en.wikipedia.org/wiki/CI/CD) )。使用不同的工具，您可以定制如何重新格式化和测试代码。事实上，只要有意义，任何事情都可以自动化。例如，每当您对代码进行更改时，您可以让 Github 运行预定义的测试，检查未使用的导入和错误的格式，并在结束时自动发送失败或错误警报。与数据科学中的一次性分析不同，在软件工程中，您会多次重新访问相同的代码。因此，对每一个变化进行相同的测试和检查是至关重要的。我喜欢 SWE 的这个方面，因为我不喜欢重复同样的任务，喜欢事情有效率。

第三，**通过版本控制的协作(如 Github)** 让你和别人成为更好的程序员。作为一名数据科学家，我使用 Github 主要是作为一个存储和保存我的工作的地方。这很好，因为没有人真正检查我的代码。但是在软件工程项目中，多个工程师在同一个代码库上工作，你必须有一个清晰的版本控制系统。看到代码库在每个人的贡献下成长和发展是很有趣的。我还发现通过[拉动请求](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)提供和接收反馈是非常有建设性的。审查别人的代码和了解自己的代码一样重要。Git 允许您查看代码是如何随时间变化的，如果在最近的变化中有问题，可以恢复到以前的版本。

# 我不喜欢软件工程的地方(作为一名数据科学家)

第一，**随叫随到烂**，通常。如果你是一名数据科学家，很少会随叫随到。随叫随到类似于医生随叫随到，以及在紧急情况下他们需要如何待命。例如，Github 在上周感恩节期间宕机了。我的第一个想法是，“撕掉随叫随到的人”，因为他们必须尽快解决这个问题。我曾经遇到过每隔一周待命的情况，也曾遇到过每两个月待命一周的情况。所以这真的取决于你团队的文化和产品。不管怎样，你需要根据随叫随到的时间表来安排你的生活，你可能会在凌晨 12 点或 5 点接到电话。这是不可避免的，因为构建和维护软件产品就像在汽车行驶时修理汽车一样。你能想象一个网站只从早上 9 点到下午 5 点在线吗？这对于不同时区的人来说会很烦人。因为大多数软件工程产品需要全天候可用，所以随叫随到是必要的。

第二，如果你来自数据科学，一个僵化的 [**scrum 框架**](https://www.atlassian.com/agile/scrum) 会令人窒息。虽然有些过于简化，但 scrum 是敏捷开发过程的一部分，该过程使用两周的时间间隔来计划、跟踪和组织工作，其中工作被分成详细的项目。你为每两周设定目标，并确保完成所有任务。在每个 sprint 结束时，你会召开一个回顾会议，回顾 sprint 的进展并继续下一个 sprint。这种类型的计划需要非常严格的结构、详细的监控和频繁的会议。这可以被视为一种令人敬畏的组织方法或极端的微观管理。

作为一名数据科学家，我不习惯这样，因为数据科学的问题往往很模糊。你可能会遇到一个开放式的问题，比如“我们如何增加产品 X 中的度量 Y？”你也可能有几周或几个月的时间通过一些签到来解决这个问题。不仅如此，给定的问题可以用不同的方法解决，如详细分析、ML 建模或实验。你也可能找不到答案，然后转向一个新的问题。很多不确定性。所以像软件工程中那样提前几周计划好工作是很困难的。

第三，**细节决定一切**。作为一名数据科学家，您可能习惯于使用已经设置好并随时可用的工具和环境。但是当你自己构建一个产品时，你需要自己设置和维护这些环境。这可能是旋转集群，设置服务器，确保您的代码符合公司的安全标准，等等。不仅如此，你还需要关注一些小细节，比如格式化(比如在每个文件的末尾添加新的一行)，或者选择正确的变量名(比如 *describe_var* ？ *var_describe* ？ *VAR* ？ *var* ？).我在这里夸大其词，并不是说这些不重要，因为说到底，这就是工程。细节至关重要。当你有 10 个人在同一个代码库上工作时，拥有一个清晰的编码格式和清晰的风格是很重要的。

# 我希望在转换之前知道的事情

尽管我很兴奋，但当我换成 SWE 时，我很沮丧。作为一名数据科学家，我对自己的能力和表现充满信心。我很擅长我的工作。但是在我换了之后，我又成了一个菜鸟，比其他人都慢。这很令人沮丧，因为我想做得更好，但这在身体上是不可能的，因为我有很多事情要做。我被迫对自己的新角色抱有可控的期望。这是一个很大的变化，除非你以前是瑞典人。不要以为从第一天就可以开始表演。这需要时间。**但是** **要谦虚，虚心接受反馈，向你的队友学习，感谢他们的帮助和时间**。

其次，因为我在相对较短的时间内切换到不同的角色和团队，**我没有晋升的那么快**。我的一些同事留在同一个角色和团队，成为经理或更高级别的个人贡献者(ICs)。如果你的目标是收入最大化和尽快升迁，这可能是不好的。如果我的目标是尽快升职，然后退役，我应该以 DS 的身份加入方，留在那里。不是说这是一条容易的路，但它会更有效地利用我的时间。这是否意味着我后悔我的决定？不，这取决于你在优化什么。

第三，从工作中你能学到的东西是有限的。**你要边学东西**。我将链接几个对你学习入门很重要的概念:

*   面向对象编程(OOP): [科里·斯查费的 YouTube 教程](https://www.youtube.com/watch?v=ZDa-Z5JzLYM&list=PL-osiE80TeTsqhIuOqKhwlXsIBIdSeYtc)。
*   单元测试:[科里斯查费的 YouTube 教程](https://www.youtube.com/watch?v=6tNS--WetLI&t=1273s)。

您将会学到许多其他的概念和工具。但是放心，所有的资源在网上都是免费的。SWE 的一生是不断学习和适应新技术和工具的一生。

# 结论

应该选择什么角色？你可以猜到，两者都有利弊。SWE 侧重于构建，而 DS 侧重于发现。我在这里没有过多地谈论 MLE，因为正如我在本文中所解释的，MLE 可以是 DS 或 SWE。我作为 MLE 的经历是一个在 ML 空间工作的 SWE。90%是软件工程，10%是数据科学。

我从这次经历中得出的最后一点:世上没有完美的工作！如果你不确定该选择哪个方向，我建议你使用著名的**后悔最小化框架** : *在临终前，你会因为尝试而更后悔还是因为没有尝试而更后悔？*当我切换的时候，我不知道该期待什么。但是我知道如果我不去尝试，我会后悔的。虽然有时很痛苦，但我很高兴我尝试了。下周，我将在 Shopify 开始新的工作。我祝你在未来的努力中好运，并在这个职业丛林中找到自己的路。祝我在新的岗位上好运！

如果你有任何问题，请在下面评论或联系我[这里](https://salary.ninja/feedback/)。