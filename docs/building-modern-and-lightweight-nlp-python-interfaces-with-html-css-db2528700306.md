# 用 HTML 构建现代轻量级 NLP Python 接口

> 原文：<https://towardsdatascience.com/building-modern-and-lightweight-nlp-python-interfaces-with-html-css-db2528700306?source=collection_archive---------11----------------------->

![](img/cb7f32625e8a0986b14025ca02de0af1.png)

为什么是鳗鱼？继续读！(戴维·克洛德博士讲解 [Unsplash](https://unsplash.com/s/photos/eel?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## 如何将 Python 和 Web 设计结合起来，立即创建漂亮而强大的数据科学图形用户界面

# 为什么？

众所周知， **Python 是当今实现自然语言处理管道的流行编程语言**。虽然用 Python 编写一个简单的 GUI 框架并不是一件很困难的任务，但是**构建一个现代而漂亮的界面却是一个真正的噩梦**，涉及到外部库、繁重的设计工具和陡峭的学习曲线。

例如，像 [**Tkinter**](https://docs.python.org/3/library/tkinter.html) 这样的框架，唯一一个内置到 Python 标准库中的框架，提供了创建 GUI 应用程序的快速而简单的方法，但涉及大量的样板代码，并且根本不是为了呈现好看的现代界面而设计的。

![](img/cf3ca19b0240acef0565d362e3a8b405.png)

真的吗？这是 1995 年吗？(图片由作者提供)

也就是说，Tkinter 可以用于管理开发的早期阶段，并创建简单的仪表板来监控或调整我们的模型参数。对于其他一切，人们可能应该去别处看看。

然而，在这种情况下寻找其他地方意味着登陆**软件，这些软件通常是专有的，并且总是难以消化**。最流行的 Tkinter 替代品之一是 [**Qt**](https://www.qt.io/) ，这是一个用于创建生产质量图形界面和跨平台应用程序的小部件工具包。使用这个框架**可以开启** **无限的机会，但也有代价**:你需要安装一个全新的环境，学习如何使用 [Python 绑定](https://www.qt.io/qt-for-python)，掌握复杂的设计接口等等。结果会很棒，但是……**值得吗？** 如果你对这个问题的回答是*否*，那么这篇文章就是给你的。

![](img/fabf7496039798b94cb10a85eb4af426.png)

是的，我们需要找到一种方法来提供漂亮的图形用户界面，但是整个 3 GB 的设计套件看起来有点大材小用。(图片作者提供)

这篇博文旨在提供一个**简单且易于管理的环境，通过**现代且设计良好的用户界面**在本地展示数据科学模型**。通过**将 Python 与 HTML、CSS 绑定，将 Javascript** **与** [**Eel**](https://github.com/ChrisKnott/Eel) (一个用于制作简单电子类应用程序的小 Python 库)，熟悉 web 设计的人可以轻松扩展这个环境**，在几个小时内**构建出令人惊叹的 web 应用程序，几乎不需要额外的努力。

带着这个目标，我决定实现一个问答(QA)机器人，名为“**问我任何事情(AMA)机器人**”，基于 [Deepset 的 RoBERTa 实现](https://huggingface.co/deepset/roberta-base-squad2)，托管在 Huggingface 上，并在 SQuAD 2.0 上接受训练以进行提取 QA。使用 NLP，我设计了这个项目来托管和显示 Huggingface 的模型，但是完全相同的环境可以扩展到任何 Python 管道来满足您的需求。

# 怎么会？

最酷的部分来了。用 Eel 构建一个基于 web 的 python GUI 是很容易的事情。Eel 是一个轻量级 Python 库，用于制作简单的离线 web 应用程序，可以完全访问 Python 功能和库。它托管本地 web 服务器，然后让您用 Python 注释函数，以便可以从 Javascript 调用它们，反之亦然。
**换句话说，如果你知道 Python 并且熟悉前端 web 开发，你就可以开始了**。

![](img/ce738f97349ba706f795e935a7065e4f.png)

Eel 提供了 Python 和 Javascript 之间的双向绑定。(图片由作者提供)

## **构建应用**

除了安装 Python 之外，构建这些应用程序没有特别的先决条件。它们**只依赖于 Eel 模块**，它可以像任何其他 Python 模块一样通过 pip -install 加载到您的虚拟环境中。当然，同一个环境应该包括项目所需的所有其他依赖项。在我的例子中，我也需要 Transformer 库。

一旦你的环境准备好了，像往常一样编写你的 Python 代码，用 *@eel.expose* 修饰你想要公开给 Javascript 端的函数。这里有一个 AMA 机器人 python 代码的例子:

从 Javascript 方面来说，现在可以通过 Eel 对象访问 Python 功能。

对于 web 应用程序的外观，规则与任何其他 web 应用程序相同:创建 HTML 文件，用 CSS 样式化它们，使之与 Javascript 交互。为了使它更容易，你可以使用 Bootstrap 或者任何你喜欢的框架。

以下是最终结果:

![](img/1ed50ace8c385393c537b941281bf897.png)

来自 AMA 机器人网络应用的屏幕截图。(图片由作者提供)

如果您需要关于如何实现 Eel 应用程序的更多细节，请查看作者资源库中的[文档](https://github.com/ChrisKnott/Eel)。

# 结论

Eel 是数据科学家和机器学习研究人员的游戏规则改变者，他们需要立即用干净和现代的仪表板显示他们的结果。这个轻量级的绑定器**填补了玩具级图形用户界面和产品级图形用户界面**之间的空白，提供了一种巧妙的方式来获得兼顾 Python 和 HTML/CSS/JS 的中级图形用户界面。

作为一个在医学信息学领域工作的人，每当我需要向临床医生和同事展示 ML 演示时，我发现这特别有用。在不损失太多时间的情况下，我们可以**交付真实且引人注目的应用程序，帮助利益相关者理解我们工作的潜力**。

在这里你可以找到这个项目的 GitHub 库。请随意使用 eel 来创建令人惊奇的 NLP 应用程序和更多！

<https://github.com/detsutut/ama-bot>  

我希望这篇文章对你有用！如果你喜欢我的工作，现在你也可以给我买一瓶啤酒！🍺

<https://www.linkedin.com/in/tbuonocore> 