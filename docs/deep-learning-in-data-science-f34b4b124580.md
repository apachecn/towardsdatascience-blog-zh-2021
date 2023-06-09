# 数据科学中的深度学习

> 原文：<https://towardsdatascience.com/deep-learning-in-data-science-f34b4b124580?source=collection_archive---------10----------------------->

## 它是什么，为什么使用它？

![](img/e98eadafbc68899c7f00b288d95d2912.png)

Solen Feyissa 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

在我的上一篇文章中，我提到了想要重新研究机器学习。最初，我第一次尝试是在一个 24 小时的黑客马拉松上。我的团队使用监督机器学习模型。起初，尝试另一种监督模式听起来是个好主意，但有了一个项目，灵感就来了。如果你没有阅读我的上一篇文章，随着十月的临近，该项目将使用机器学习来生成简短的恐怖故事。但这意味着分类或预测不会发生。代代做。所以，我们需要使用深度学习模型，而不是监督/非监督/强化学习模型。

在我的《[数据科学常用词](/commonly-used-words-in-data-science-ea06a8f17577?source=your_stories_page-------------------------------------)》一文中，我们简要描述了什么是深度学习。我们也提到了神经网络的使用，但仅仅简单的定义并不总是能清楚地描述它们是什么以及它们是如何工作的。因此，在本文中，我们将更多地了解什么是深度学习，它是如何工作的，什么是神经网络，以及深度学习的目标/结果。

# **什么是深度学习？**

深度学习是一种更接近人脑决策方式的机器学习训练模型。我说的大脑是指创建的算法更深入。不是只有一个层，而是多个复杂的层被用于处理。神经网络是一个允许层间通信的系统。这个过程更接近于无监督学习，因为它也是自动化的。

因为这种类型的学习充当了一个强大的大脑，所以需要大量的数据进行训练。需要如此多的数据，以至于在大数据和云计算出现之前，数据量和处理能力都不容易获得。但是仅仅因为需要大量的数据，并不意味着数据必须是结构化的。深度学习可以处理无标签和非结构化数据。这种学习方法还会创建更复杂的统计模型。随着每一个新数据的出现，模型变得更加复杂，但也变得更加准确。

# **深度学习模型**

深度学习的一种方法是迁移学习。与其他训练模型相比，它需要更少的计算时间。它也不需要那么多的数据。迁移学习从一个预先存在的网络开始。这个网络还必须有一个接口。然后，该网络被输入新的数据，这些数据带有它尚未面对的场景，以获得反应并从数据中学习。随着时间的推移，可以进行调整以适应新数据和旧数据。然后，新的任务可以根据网络所学到的东西来执行，甚至可以利用其新发现的适应性获得更具体的分类能力。本质上，它采用现有的接口，为其提供新的场景，这些新的条件使网络在接受数据方面更加广泛，但在分类方面更加精确和具体。

深度学习的另一种方法是辍学法。特别是在监督学习中，可以创建类别来容纳不需要制作的数据。简单地说，过度匹配是指类别过于具体，以至于钻得太深。为了对抗过拟合，dropout 方法选择神经网络中的随机节点/单元来“退出”。通过去除那些随机节点，它努力消除钻得太深的分类。这发生在训练期间。

我们接下来要看的深度学习方法是从零开始训练。这种方法听起来一模一样，因为用户从零开始创建和训练网络。网络体系结构是根据需要构建的，需要一个带标签的数据集来配置该网络。与其他方法相比，这种方法有点像保姆，如果数据没有被标记，那么它就不能包含在训练集中，至少在训练的早期阶段是这样。为了捕捉所有场景或至少大部分场景，需要大量数据进行测试。它也比许多其他方法需要更长的时间，所以它不是一种常见的方法。

我们今天要讨论的最后一种深度学习方法是学习率衰减法，也称为自适应学习率法。一旦测量了误差率，学习率决定了发生多少变化。通过监控学习率，您可以调整模型以提高性能并减少训练时间。随着时间的推移，目标是降低学习率，以便在通过模型发送数据时不需要做太多的更改。如果速率太高，那么网络中的变化太多，并且在训练期间可能不稳定。但是，如果速率太小，那么性能可能会受到影响，甚至数据可能会在训练期间停滞不前。通过学习来平衡学习速率，可以提高准确性，并且可以显著提高训练性能。

# **什么是神经网络？**

神经网络之所以重要，是因为通信源是节点，节点包含算法层，可以评估原始数据，并找到隐藏的模式。像无监督学习一样，深度学习会随着时间的推移而改变并适应数据，这使得它可以随着时间的推移而改进。神经网络也用于更复杂的问题，甚至解决现实生活中的场景。

但是节点到底应该是什么呢？一个节点应该代表必须做出决定的输入，然后连接到隐藏层。这些隐藏层是决策网络的一部分。一旦做出决定，它将连接到输出层，显示该决定的结果。就像大脑中的神经元一样，输入可以在隐藏的网络层周围反弹，像神经元触发大脑中的反应一样触发节点。这有助于做出更准确、更具描述性的决策。

# **深度学习的目标**

深度学习的第一个也是主要的目标是随着每一个新的数据而改进。这包括能够调整其底层结构以准确评估数据。一旦使用测试数据完全构建了网络，就可以使用客户分析实现更大的个性化。就像一个流媒体服务建议你接下来应该看什么，你看什么节目/电影的数据被处理，并做出决定建议你可能也喜欢什么。

深度学习模型试图专注于认知计算，并模仿类似人类的思维结构。正因为如此，深度学习在 AI(人工智能)中被大量使用。无论是你最喜欢的游戏中不可玩的敌人角色学习如何更好地攻击，还是聊天机器人回答你的问题，深度学习都允许人工智能以表达认知能力的方式思考，这与我们以前创造的任何东西都不同。这个 AI 和深度学习以后只能越来越准，越来越快。

# **结论**

今天，我们深入探讨了深度学习。作为机器学习的一个子集，深度学习与神经网络合作，模仿大脑如何对输入做出反应以及如何做出决定。神经网络具有从输入连接到隐藏网络层，然后连接到输出的节点。模型运行的时间越长，深度学习试图改善决策过程，并随着模型的运行变得更加准确和更具描述性。随着时间的推移，AI 已经采用深度学习来改善其决策过程。因此，随着突破性进展，人工智能可以在准确性和速度方面变得更加智能。随着深度学习驱动我们的未来，大数据使得使用这种模式变得更加容易。请随意对您如何创建深度学习模型发表评论。下次见，干杯！

***用我的*** [***每周简讯***](https://crafty-leader-2062.ck.page/8f8bcfb181) ***免费阅读我的所有文章，谢谢！***

***想阅读介质上的所有文章？成为中等*** [***成员***](https://miketechgame.medium.com/membership) ***今天！***

看看我最近的一些文章:

<https://python.plainenglish.io/web-scraping-with-beautiful-soup-1d524e8ef32>  <https://python.plainenglish.io/something-i-learned-this-week-paramikos-remote-file-management-f13af69baf4>  </all-about-big-data-ae01afacc081>  <https://python.plainenglish.io/i-suck-at-coding-cb9bc7ef6c06>  <https://python.plainenglish.io/arrays-vs-list-vs-dictionaries-47058fa19d4e>  

参考资料:

<https://www.sas.com/en_us/insights/analytics/deep-learning.html>  <https://www.sas.com/en_us/insights/analytics/neural-networks.html>  <https://searchenterpriseai.techtarget.com/definition/deep-learning-deep-neural-network> 