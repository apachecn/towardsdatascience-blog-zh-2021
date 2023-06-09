# 如何使用 Python 向 Google BigQuery 上传数据:3 个步骤

> 原文：<https://towardsdatascience.com/how-to-upload-data-to-google-bigquery-using-python-in-3-steps-7138ae625fe3?source=collection_archive---------2----------------------->

## 在 Google 的云数据仓库中自动更新 API 数据

![](img/78fda73e4e955afa8aa00587018297e1.png)

图片由[像素](https://www.pexels.com/)上的 [Anete Lusina](https://www.pexels.com/@anete-lusina) 拍摄

Google BigQuery 是一个快速、可扩展的数据存储解决方案，可以轻松地与 Power BI 和 Tableau 等一些顶级数据科学应用程序集成。如果你以前用过 BigQuery，你可能知道它有很多特性。比如，很多功能。这对于新用户来说肯定是令人生畏的，但是如果你坚持下去，你会从这个平台中得到很多有用的东西！

我经常使用 BigQuery 的一个功能是上传数据，以便与其他应用程序共享和集成。与反复编辑和上传 CSV 文件相比，您会发现将一个功能链接到所有应用程序要容易得多！在本文中，我将向您展示如何从 API 中获取数据，并使其易于在各种平台和应用程序之间共享和访问。这应该适用于任何 API，只要您能够输出 pandas 数据帧。

**第一步:创建云函数**

登录您的帐户后，您要做的第一件事就是转到右上角的“控制台”部分。如果你还没有一个项目，那就按照你的喜好来设置吧。进入控制台后，进入右上角的导航菜单，向下滚动到“云功能”

![](img/b488db3fe05263ef503b699b724b3b70.png)

作者[谷歌大查询](https://cloud.google.com/bigquery)截图

您需要启用计费来使用此功能，但根据您需要的数据量，此功能不会很贵。云函数可以使用各种语言来做几乎任何事情，从简单的 API 调用到机器学习，所以非常值得！

一旦你进入云函数，点击“创建函数”按钮。名称和区域可以是您喜欢的任何名称，对于触发器类型，我通常将它保存在 HTTP。然后，对于运行时设置，我更喜欢将我的超时设置为最大值 540 秒，内存分配和最大实例数由您决定，但这是我通常使用的:

![](img/a375f0a42dfd526540fcd2c4c3fb0230.png)

作者 [Google BigQuery](https://cloud.google.com/bigquery) 截图

然后点击“保存”和“下一步”，你就可以添加你的自定义 API 了。在您将代码复制并粘贴到 Google 的 IDE 之前，您必须添加一些特定于 BigQuery 的函数。幸运的是，我已经得到了你在第二步中需要的一切！

**第二步:添加 BigQuery 特定函数**

这些 BigQuery 函数的结构看起来有点复杂，但简单来说，它看起来像这样:

*   功能 1:验证 HTTP 响应
*   功能 2:您的自定义 API 拉
*   功能 3:将数据帧加载到 BigQuery 表中

那么在 python 中这看起来像什么呢？大概是这样的:

如果您已经编写了一个 API 拉脚本，那么您可以将它粘贴到 get_all_data()函数中，然后将整个脚本复制并粘贴到您的 BigQuery 云函数中。就这么简单！在尝试在云中运行 API 调用之前，只需确保它在本地运行即可。

在部署函数之前，要做的最后几件事是确保“入口点”是第一个函数 validate_http，并确保您拥有正在使用的任何库的所有正确的依赖项。这个例子看起来是这样的:

![](img/8564e666a1bfc0912cdd4e58a5190dc1.png)

作者提供的[谷歌大查询](https://cloud.google.com/bigquery)截图

最后，您可以部署您的功能！在您点击部署后，它将运行几秒钟，如果您看到一个绿色的勾号，这意味着您做得对。

**第三步:测试并刷新你的表**

有很多方法可以让你的新表显示数据，我认为最简单的方法是点击你的云函数，点击“测试”，然后“测试函数”。这将创建一个 BigQuery 表，其中应该包含来自 API pull 的所有数据！要查看该表，只需进入左上角的主菜单，向下滚动到“BigQuery”

![](img/b1f3d3999fa2ff1068d434f7d508a017.png)

作者提供的[谷歌大查询](https://cloud.google.com/bigquery)截图

在这里，您可以查看数据的模式，查看数据的更新时间，并预览数据集的外观。就这样，您将数据存储在 BigQuery 中！现在你可以将这些数据链接到 Tableau、Google Data Studio、Power BI 或任何最适合你的应用程序。能够从任何地方访问这些数据并将其链接到多个应用程序是非常值得的，您甚至可以通过使用 BigQuery 的“云调度程序”来自动化这个过程。这也可以在主菜单中找到，向下滚动直到看到以下内容:

![](img/de7322de22f7a205ab89396a21b0e3fa.png)

作者[谷歌大查询](https://cloud.google.com/bigquery)截图

在这里，您可以决定您希望数据刷新的频率，BigQuery 将自动处理测试过程。这就让你少担心一步了！

**最终想法**

如果你曾经考虑过使用云数据存储解决方案，我肯定会推荐你使用 Google BigQuery！一开始可能会有很多，但是我认为如果你按照本文中的步骤去做，你应该能够适应它的一些特性。我希望这篇文章能够帮助您更好地理解 BigQuery 以及如何将您的数据上传到云中。非常感谢你的阅读，我希望你有一个伟大的一天！

跟我来！——【https://bench-5.medium.com/】T2

通过使用此链接升级您的中级会员来支持我:[https://bench-5.medium.com/membership](https://bench-5.medium.com/membership)