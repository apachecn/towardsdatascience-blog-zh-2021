# 人工智能可以解释任何事情——除了为什么没人听我的

> 原文：<https://towardsdatascience.com/ai-can-explain-anything-except-why-no-one-listens-to-me-33100080b56c?source=collection_archive---------51----------------------->

为什么机器学习(ML)的进步没有完全转化为更好的数据驱动决策？业务线利益相关者和数据科学家如何弥合质量分析和执行变更之间的差距？

人工智能模型不做决定——人做决定*。*因此，*之前*没有响应基本分析而执行的任何组织将*继续*基于尖端 ML 不执行。增加分析的复杂性可能会提高预测的准确性，但也会增加协调的复杂性。我们不能只获得新的工具或能力，并抱最好的希望。相反，我们需要重新想象呈现分析的最后一步，并重新思考如何将 AI/ML 输出转化为决策。

对于数据科学家来说，最终的建议或模型是漫长旅程的产物——提取利益相关者的协调、背景设置、数据争论和仔细分析。但是当该建议被提出时，利益相关者被要求相对快速地对大量新信息做出反应，因此依靠三件事来自信地采取行动。

1.  **理解建议:**
    涉众必须理解预期的结果，以及实现该结果所需的杠杆。一个有效的分析负责人将通过以一种可消费的方式交流具体的预测和支持证据，对涉众的理解负责。
2.  **信任推荐者:**
    可信的来源需要提供结果。例如，如果技术所有者有质量交付的跟踪记录，或者如果决策者已经接受了分析方法。其他时候，可信度只是一种品牌效应:这就是沃森在空闲时间玩国际象棋和危险游戏的原因。最终，这变成了一个反馈循环，因为执行变更的良好结果建立了推荐其他变更的可信度。
3.  **拥有实施建议的能力:**
    高质量的 ML 模型在面对现实世界的操作复杂性时会显得力不从心。实施任何特定建议的人力带宽和技术能力都需要到位。

随着人工智能/人工智能系统在组织中的进一步推广，它们已经:

1.  **增加了推荐的复杂度:**
    从根本上说，[很难解释](https://www.technologyreview.com/2017/04/11/5113/the-dark-secret-at-the-heart-of-ai/)AI 算法在做什么。解释 ML 结果类似于医学上的*知情同意*。受过几十年医学训练的医生需要解释一个医疗程序。但是病人在十分钟前第一次知道了他们的疾病。作为患者，做一个“知情的”决策者意味着什么？手术越复杂，病人就越难理解所有的风险和影响。面对更先进的数据科学技术，决策者变得更难“知情”。
2.  **测试现有工作模式的局限性** :
    改变底层工具，但不改变数据科学团队与决策者的互动方式，不会突然创造一种建立信任或理解的新方式。面对更复杂的过程和利益相关者更难理解的情况，建议的执行变得依赖关系资本。
3.  **实施建议时增加了操作难度** :
    零售商可能会考虑定制定价。借助新的数据管理和分析工具，分析师可以建立一个模型，为每个客户量身定制定价，根据他们所有被跟踪的网络行为创建一个预测的弹性。或者，为了降低复杂性，只需将纽约市的价格提高 2 美元。

因此，虽然 ML 帮助预测变得更加准确和容易，但是执行改变的*过程*实际上变得更加困难。随着更先进的工具被应用于更棘手的问题，组织必须积极地防止沟通复杂性以同样的速度增长。即使是完美的预测模型也需要买入；因此，不对称地发展能力，使其更能预测赢得认同的能力是没有意义的。

承担一项具有挑战性的任务的最简单的方法是把它分散到更长的时间里。在寻找答案的过程中，商业利益相关者需要更多地参与*。如果我们开始构建一个 ML 模型，非技术利益相关者不应该无所事事，想象球在他们的球场之外。相反，他们应该参与进来，审查背景设置描述性输出，表达背景知识，并了解关于正确目标变量的反馈。专家输入只能改进模型；同时，参与批判性思维有助于建立模型本身背后的直觉。*

当这种类型的合作成为惯例时，它就变成了生产化之前的快速原型制作过程。第一轮演练将触及分析的所有要点，并成为数据科学和业务线团队之间相互交换信息的框架。没有必要微调模型或浪费时间；创建端到端的 MVP 应该是轻松的，并且可以直接解决上面提到的挑战:

1.  **专注于基本分析组件降低了复杂性** :
    当利益相关者可以看到一砖一瓦构建的最终产品时，答案变得不那么完整。无论是通过快速原型制作，还是其他过程，暴露可消化的子答案有助于最终答案的可消化性。不需要理解深度学习的机制，就可以看到描述两个变量的散点图。
2.  **能够提问更小的问题消除了对整体答案的不确定性:**
    当利益相关者开始理解这种方法，并看到数据集时，不确定性或困惑可以得到解决。如果我们等到整个 ML 管道都建立起来了，混淆是非特定地指向整个产品。通过消除每一步的疑虑，最终产品也应该被认为是干净的。
3.  **通过变量工作消除了不可行性的后期发现:**
    重新设计利益相关者-分析师互动模型不会创造新的操作能力，但是可以节省大量时间来避免错误的建议。要求业务线积极地一起构建原型，可以让团队明白，在分析的前 15 分钟内，特定的目标方法是不可能的——在几天的数据争论和模型迭代之后，肯定不会在与首席运营官的会议上。

机器学习有能力利用大量数据，并为组织领导层面临的问题提供更好的答案。但是随着分析方法的复杂性增加，数据科学不能变得更加复杂难以理解。致力于更深入的合作途径将会带来更好的最终结果:更好的前期背景设置，分析团队更少的障碍和陷阱，以及决策团队更好地理解输出。

*原载于 ein blick:*[https://ein blick . ai/ai-can-explain-anything-except-why-no-one-listen-to-me](https://einblick.ai/ai-can-explain-anything-except-why-no-one-listens-to-me)

*Einblick 是全球首个可视化数据计算平台，创造了与数据最自然的交互。在 https://einblick.ai/product/*了解更多关于我们的信息