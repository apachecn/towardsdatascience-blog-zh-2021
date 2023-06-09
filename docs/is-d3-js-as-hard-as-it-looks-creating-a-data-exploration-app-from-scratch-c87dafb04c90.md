# D3.js 有看起来那么难吗？从头开始创建数据探索应用程序

> 原文：<https://towardsdatascience.com/is-d3-js-as-hard-as-it-looks-creating-a-data-exploration-app-from-scratch-c87dafb04c90?source=collection_archive---------25----------------------->

## 比较电影平台——TMDb 与 IMDb

![](img/3a0038a7ae4e0442842a716aa3468e3a.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上由 [Myke Simon](https://unsplash.com/@myke_simon?utm_source=medium&utm_medium=referral) 拍摄的照片

JavaScript 的 D3 库以其创建交互式和/或动画可视化的灵活性和功能以及陡峭的学习曲线而闻名。

这个库是由 Mike Bostock 开发的，他也提供了大量高质量的可视化及其代码。这些例子可以在官方网站[这里](https://d3js.org/)找到。我发现这些可视化示例是很好的资源，甚至可以用来集思广益，决定哪种类型的可视化更适合您的目的，不过，主要的力量来自所提供的代码，这些代码在理解了一些 D3 基础知识后可以很容易地进行修改。

# 真的有看起来那么难吗？

事实上，与其他数据可视化工具相比，初始投资成本更高，尽管我认为这个库的难度被夸大了。当我开始学习 d3(通过直接开始一个可视化项目)时，我甚至没有任何 JavaScript 方面的经验。我想说的是，在学习了一些概念(如数据连接、进入、更新、退出循环)后，事情变得非常清楚，甚至非常复杂的动画/交互式可视化也变得非常容易实现。

# 那这个项目是什么？

这是一个数据探索和可视化项目，是不久前作为作业完成的。这是关于创建一个数据可视化工具来比较电影和电影数据库。

我们都熟悉 [IMDb](https://www.imdb.com/) 这是一个盈利组织，另一方面， [TMDb](https://www.themoviedb.org/) 是另一个众包平台。我最初想调查他们的用户的电影口味之间是否有任何显著的差异。因此，我开发了这个应用程序。

> 我在下面添加了可视化的链接，你可以去发现什么类型的电影受到社会的喜爱，或者为他们幸运的制片人带来更多的利润。

<http://anilgurbuz.com/visualisation/Page2.html>  

PS:我知道网页的设计违背了所有的启发法，但是当时唯一的担心是可视化的设计。

在下一部分中，我将尝试解释我在项目中使用的 D3 的一些方面，并希望它能对一些在网上寻找什么是进入-更新-退出循环的初学者有所帮助——我们都经历过。

# 如何使用 D3 创建交互式/动画可视化？

显然，这是一个非常宽泛的问题，可能有很多答案，但所有这些答案都需要首先学习 D3 如何将数据绑定到 DOM 元素。因此，我们会研究一下。

如果你问自己什么是 DOM 元素，这个[链接](https://stackoverflow.com/questions/1122437/what-is-dom-element#:~:text=The%20DOM%20is%20the%20way,interact%20with%20them%20using%20JS.)可能有助于理解 DOM 的概念。简而言之，DOM 元素是一个存储网页中对象的容器，是的，D3 将数据分配给这些容器，因此我们可以使用该数据的任何维度对网页/容器/DOM 元素的相应部分进行更改。

# D3 里如何控制数据绑定？—进入、更新、退出循环

我们通过一个 3 步的过程控制数据绑定到 DOM 元素；
进入-更新-退出循环。

1.  在 Enter 步骤中，我们选择没有匹配 DOM 元素的数据，并创建新的 DOM 元素来分配所选数据。
2.  在 Update 步骤中，我们选择被绑定的 DOM 元素和数据，并由于 DOM 元素的现有绑定数据的任何变化而更新所选 DOM 元素的属性。这一步要求 DOM 元素和匹配数据都存在。
3.  退出是我们选择没有匹配数据的 DOM 元素并删除这些 DOM 元素的步骤。

# 进入-更新-退出循环

在这个可视化中，我们将创建 DOM 元素来渲染散点图中的圆圈，绑定数据将是关于电影的，因为图中的每个点将代表 IMDb 或 TMDb 中的一部电影。

让我们看看应用程序的一些用户动作和相应的反应，以了解数据绑定如何控制所有这些动作-反应循环，然后我们将查看代码。

在此处再添加一次链接以访问应用程序。

<http://anilgurbuz.com/visualisation/Page2.html>  

## 用户使用滑块或按钮过滤数据

1.  **当用户使用 gif 中的滑块过滤数据时应用程序的反应:**

*   反应 1.1:重新缩放 x 轴，以在 x 轴上为新点集获得更合适的值范围。
*   反应 1.2:移除(点的下落)和增加点(从顶部落入可视化)。

## 用户悬停点

**2。当用户悬停在 gif:** 中的& off 点时应用程序的反应

*   Reaction2.1:发出一个 API 请求，构造响应，并呈现由悬停点表示的电影的海报和元数据。
*   反应 2.2:增加悬停点的不透明度。
*   反应 2.3:当用户悬停时，回滚到可视化的初始状态。

# 密码

下面的代码显示了“render”函数，每次用户通过过滤数据进行更改时都会调用该函数。此代码包括散点图圆圈的整个进入-更新-退出循环。

**代码中的一些变量:
d:** 将要呈现的数据。它存储电影的利润、评级、投票数信息。海报图像不包括在这个加载的数据集中，因为这些图像是通过 API 请求与用户动作同时获得的。
**xScale:** D3 缩放对象。从技术上讲，是输入数据值到轴值的映射器。

## 重新缩放 x 轴

我们首先通过改变映射器的域来重新调整 x 轴(反应 1.1)，以便我们的 x 轴将只包括过滤用户后保留的值。比如用户想和 Min 一起看电影。利润 6 亿美元，那么，借助代码第 5–7 行的修改，x 轴将从 6 亿美元开始。

但还有一点，我们不希望我们的轴只是消失，并重新出现一个新的值看起来平滑。因此，`transition.duration(1000)` part 使 DOM 元素的变化在一秒钟内发生，而不是立即发生。—在这种情况下，DOM 元素是“xAxis”。d3.select()选择的元素。

## 进入阶段

这个阶段从这个代码的`selectAll("circle").data(d)`开始，我们选择现有圆圈的所有 DOM 元素，然后给每个圆圈分配一行数据。使用`enter()`之后的命令，我们为没有任何绑定 DOM 元素的数据创建一个新的圆圈。例如，如果我们在图中有 100 个圆，我们改变了过滤器，使其为 150，这意味着我们的数据点比 DOM 元素多。这是在进入步骤中通过创建 50 个额外的 DOM 元素(“圆圈”)来处理的，以便与手边的数据匹配。

如上所述，enter 是我们为没有有界 DOM 元素的数据创建新 DOM 元素的步骤。`append("circle")`是创建这些新元素的命令，然后我们指定这些圆的属性。例如，`attr("cx",d=> xScale(d.Profit))`指定圆的“cx”属性，这是数据“d”的“利润”属性。xScale 将原始利润值转换为绘图中的坐标。

`.on("mouseover"...`可以被认为是这些圆圈的另一个属性，它描述了用户悬停时 DOM 元素的反应。我们已经提到了反应 2.1 和反应 2.2。因此，通过为“mouseover”属性定义一个函数来实现这些反应。

> 使用 d3.json()函数，我们发出一个 API 请求，并获取电影海报下呈现的海报图像和信息。这样，我们就不用在服务器上保存海报图像，当用户悬停在一个圆圈上时，就可以立即从 API 中获取。

showPoster 是我实现的一个函数，用来调整海报图像的大小并渲染它。这个函数也在`.on("mouseout"...`中使用，当用户把鼠标从圆圈中拿出来时，不渲染任何东西。另外，`.on("mouseover"...)`中的`d3.select(this)`和`.on("mouse out"...`选择用户悬停的 DOM 元素。

## 更新阶段

这是更新现有 DOM 元素属性的步骤。如果在 d3.select 中选择了一个 DOM 元素，这个步骤将数据的变化反映到 DOM 元素的属性中。更新步骤没有关键字，可以在输入步骤之后通过选择已经与数据绑定的现有 DOM 元素来启动。只有当数据和 DOM 元素都存在，并且数据发生变化时，这一步才会发生变化。

## 退出阶段

如果 DOM 元素没有附加数据，我们将在这里删除它们。当我们通过向右移动奥斯卡雕像来应用滤镜时，这种情况就会发生。我们过滤数据，所以一些 DOM 元素的数据被过滤了。因此，这些 DOM 元素在这一步被删除。

`Mycircle.exit()`选择过滤了数据的圆，使用`attr("cy",...`，我们在`remove()`命令前改变这些圆的位置。我们还使用了`transition().duration(1000)`，所以这些点的 y 轴值不会立即改变，尽管这些点会在 1 秒钟内转换到新的位置。这样，我们可以使点像反应 1.2 中描述的那样下落，而不是消失。

# 结论

进入-更新-退出阶段只是代表了我们选择没有 DOM 的数据，数据和 DOM 都有对方，或者没有数据的 DOM 元素的步骤。通过这种方式，我们可以控制数据— DOM 元素绑定并操纵 DOM 元素的属性。这个概念在开始的时候可能有点混乱，但是一旦你明白了，它看起来就很直观了。