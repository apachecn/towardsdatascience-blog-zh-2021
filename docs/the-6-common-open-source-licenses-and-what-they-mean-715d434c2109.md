# 6 种常见的开源许可证及其含义

> 原文：<https://towardsdatascience.com/the-6-common-open-source-licenses-and-what-they-mean-715d434c2109?source=collection_archive---------29----------------------->

## 了解许可证，知道选择哪一个

![](img/c6aacfaf86cc6f61e205a20e9776fd88.png)

罗曼·辛克维奇在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

开源软件是计算机科学和编程史上最有影响力的创举之一。短语“开源”指的是开放给人们使用的东西。因此，开源软件是一种向公众开放的软件，在这里可以使用、修改和研究源代码。

通常，开源项目包括许多人用于各种应用程序的源代码。当一个项目是开源的，程序员将可以访问源代码来添加功能，修复损坏的部分，并在它不能正常工作时检查它。此外，因为开源代码给了人们修改代码的权力，开源许可证的创建是为了规范这个过程，让程序员清楚他们能做什么，不能做什么。

开源许可证——有时也称为 copyright left 许可证——要求任何发布开源应用程序的人发布一套规则，规定人们如何使用、更改和修改这些代码。做任何开源许可不允许的行为都会被认为是非法的，违反了许可的规定。

</getting-started-with-open-source-roadmap-35c6f76682b7>  

对于人们来说，这些许可证可能很难理解，坦率地说，需要阅读和理解它们的含义以及如何为您的应用程序选择正确的许可证。如果你需要帮助为你的项目选择许可证，试试[这个](https://choosealicense.com/)工具。

*免责声明:在本文中，我将尽力介绍 6 种最常用的开源许可证的基本规则。也就是说，如果你打算使用这些许可证中的任何一个，你应该仔细阅读它的文档，如果你还有任何问题，请咨询律师。将本文作为了解开源许可世界的入门指南。*

# №1: GNU 通用公共许可证(GPL)

当我第一次加入开源世界时，GNU 是我最熟悉的许可证；GNU 一度对我来说意味着开源。GPL 许可是我们列表中版权最多的许可。copyright left 许可证是那些要求修改后的作品与原始作品共享同一许可证的许可证。因此，如果你正在修改的作品是在 GPL 许可下，你的作品也是如此。

任何 GPL 许可都允许将许可材料用于商业用途。所以，你可以建立在 GPL 作品的基础上，并在你的工作场所使用它。如果你愿意，你也可以为你修改的作品申请专利。最后，如果你在一个更大的项目中使用一点 GPL 许可的作品，那么整个项目也必须是 GPL 许可的，这就是为什么 GPL 是开源许可中版权最多的。

</5-data-science-programming-languages-not-including-python-or-r-3ad111134771>  

# №2: Mozilla 公共许可证(MPL)

接下来我们有另一个 copyleft 许可证，它是 [Mozilla 公共许可证](https://www.mozilla.org/en-US/MPL/)。MPL 比 GPL 许可证有更弱的左版权要求。MPL 和 GPL 之间的区别在于，如果您修改最初在 MPL 许可下发布的代码，您可以选择您想要的任何许可，只要修改保存在与 MPL 许可材料分开的文件中。

使用 MPL，您可以申请专利，并且可以将修改后的材料用于商业用途，用于私人工作，或者您可以对修改进行封闭源代码，只要它与代码的 MPL 许可部分分开。

# №3: Apache 许可证

从 copyleft 许可证转移到不需要继承原始许可证的许可许可证，我们将从[Apache 许可证](https://www.apache.org/licenses/LICENSE-2.0)开始。Apache 许可证由 Apache 软件基金会(ASF)发布和修改；该许可证的第一个版本发布于 1995 年。

Apache 许可证让开发人员可以自由选择在哪个许可证下发布他们的作品，只要他们提到原始许可证并记录对许可材料所做的更改。你也可以选择对你的一些材料进行闭源，并且可以在商业上使用许可的作品或者获得专利。

</5-git-commands-that-dont-get-the-hype-they-should-d62af563acaa>  

# №4:麻省理工学院许可证

接下来是许多开发者最喜欢的许可证——包括我自己——[麻省理工学院许可证](https://opensource.org/licenses/MIT)。麻省理工许可证是一个许可许可证，最初由麻省理工学院在 80 年代末发布。许多人更喜欢这种许可证的原因是它很短，简单明了，清楚地说明了什么是允许的，什么是不允许的。

MIT 许可证是当今开源世界中使用最多的许可证之一。基本上，只要原始版权和许可证包含在您的工作文件中，本许可证允许您对许可材料做任何您想做的事情。它免除了作者的任何责任，并且没有明确包含专利授权。

# №5:增强软件许可证(Boost)

另一个简单、简短的许可证是最初为 C++ Boost 库编写的 Boost 软件许可证。为了使 Boost 许可证变得简单，已经做了大量工作，该许可证的最新版本遵循以下条件:

*   使用 Boost 授权的代码必须易于阅读和理解。
*   许可作品可以免费复制、使用、修改。
*   任何添加的作品都必须包括许可证及其所有副本，即使是再分发。

Boost 许可证是一种简单的许可许可证，在大多数情况下与 MIT 许可证非常相似，只有两个主要区别:

*   如果你要发布一个可执行文件，你需要在 MIT 许可证中包括一个版权声明，但在 Boost 许可证中不包括。
*   MIT license 对于你到底能把代码用在什么地方有一个相当广阔的视角。

# №6:无许可证

最后，我们将谈论[的无执照执照](https://choosealicense.com/licenses/unlicense/)。这个许可证很简单，对你如何使用、修改和修复任何许可材料没有任何限制。在所有其他开源许可中，非许可给了开发者绝对的自由。

如果您不想深入了解权限和条件，只想尽快发布您的作品，那么非许可通常是开源许可的选择。所以，如果你没有任何关于如何使用你的源代码的规则，但是由于法律原因必须包括一个许可，你可以不要许可。

</5-data-science-open-source-projects-you-to-contribute-to-boost-your-resume-d757697fb1e3>  

# 外卖食品

开源是一项惠及所有人的倡议，无论是技术人员还是应用程序的用户，即使他们不知道或不关心它是如何工作的。作为程序员，我们喜欢开源项目有很多原因:

1.  **控制。**开源让你对软件有很大的控制权。你可以研究它，修改它，修复它的缺陷，并在许可规则范围内随意使用它。
2.  **安全稳定。**如果不需要等待原作者的许可就可以修复问题，那么问题修复的速度会更快，效率也会更高。
3.  **社区。对于许多其他程序员和我来说，这可能是最重要的方面。开源社区是重要的事情之一；会见来自世界各地志同道合的人，并向他们学习，使得开源成为一个如此有趣的概念。**

当程序员努力构建一段代码时，他们通常会附带一个许可证。本许可证规定了代码的允许用途，并限制了原始创建者的设置。了解每个许可证的含义将保证您在构建自己的项目和使用他人的项目时选择正确的许可证。

理解每个许可证的含义是对最初的创作者和他们在构建代码中付出的辛勤劳动表示尊重的一种方式。这种尊重是开源社区有影响力的原因，也是它不断成长并在今天取得成功和繁荣的原因。