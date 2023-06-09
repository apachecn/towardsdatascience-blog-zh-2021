# 根据 OpenStreetMap 估算出行成本

> 原文：<https://towardsdatascience.com/estimating-travel-cost-from-openstreetmap-49138ff81289?source=collection_archive---------17----------------------->

## 可以使用建筑物/道路和 LULC 图层模拟子区域通勤的路面成本

![](img/8d6f71c4ee4df4d634932e64335a6dff.png)

OSM 大楼/里斯本高速公路覆盖在谷歌地图上。来源:谷歌地图和 OSM

交通数据以其产生的强度存储是不可行的，甚至按月存储也是不可行的，它更适用于实时用例，正如我们所知的大多数日常通勤应用程序使用它的情况一样。

然而，有些情况下，我们需要对一些研究或商业项目进行静态分析，这时我们才意识到并没有这样的数据来源。很少有公司提供这种服务，但首先，它仅限于某些地区/城市，而且，这当然会让我们付出代价。

这篇简短的文章解释了如何将开源数据用作替代资源，以及如何从中构建有意义的东西。

# OSM 倡议

众所周知，OSM 是一个众包平台，为社区提供和构建开源地图。多年来，它提供了巨大的价值，因为现在大多数商业应用程序都使用 OSM 来提供大部分底图和与路线相关的服务。

有多种平台/API 可用于接收数据，下面列出了其中一些:

1.  [https://download.geofabrik.de/](https://download.geofabrik.de/)
2.  【https://overpass-turbo.eu/ 号
3.  ArcGIS OSM 编辑器
4.  QGIS QuickOSM 插件

有多种类别的键/值对或数据集被分为多个类，对于这个练习，我们只需要**建筑物和高速公路。**

以葡萄牙里斯本为例，这里有几张 2015 年**和 2021 年**的矢量多边形快照

![](img/e299e34bed11b2d9d778d473a702e8fa.png)![](img/0bc4e701c7111d84abd0f94399e87760.png)![](img/f4a28a16163bb4dd604654a01496160b.png)![](img/d60e0f47d32ecd80321d7e687135908a.png)

左边是 2015 年的建筑/道路，右边是 2021 年的地图。来源:OSM 的地图和矢量数据

从视觉上，我们可以推断出两件主要的事情:

1.  在过去的 6 年里，建筑物的数量增加了
2.  道路网络也有所改变

这也可能是因为 OSM 储存库中没有 2015 年的数据。

# ESRI 2020 LULC 地图

另一个有用的来源是 2020 年发布的 ESRI LULC 地图。使用分辨率为 10m 的全球地图范围，我们可以推断出小区域级别的类别，并尝试估计预定义子区域的**表面成本。**

方法很简单，我们可以执行以下步骤:

![](img/97dae42d61f172da3051b17a614b7952.png)

里斯本的谷歌地图图像上覆盖的网格。来源:谷歌图片

通过创建更小的子区域来数字化里斯本，这也可以在一个教区(官方子区域)级别完成。

然而，对于这个实验，我们将实现简单的基于网格的分离。这些多边形的形状会影响我们推断最终结果的方式，通常建议使用**六边形**而不是正方形，因为它们更有可能代表真实的地理位置。

这些图像显示了基于正方形的栅格线的示例，但是在下一步中使用了六边形栅格。

![](img/b3941c8b11cefa8b1a1a70669ba261c8.png)

建筑多边形上覆盖的网格。来源:OSM 矢量多边形

叠加 OSM 的建筑多边形会得到这样的结果。

现在，我们可以简单地计算每个方块中建筑物的平均数。这可以通过交叉或分区统计来实现。不同的工具有自己的方式来定义不同算法的名称。

在运行统计数据时，我们可能有两种选择:

1.  每个多边形中建筑物的平均数量
2.  每个多边形中建筑物的平均面积

获得*的平均面积更有意义，因为*较大的建筑可能意味着较高的人口密度，而相比之下，有几栋住宅建筑可能人口密度较低。一旦我们运行这个，我们得到类似下图的东西。

![](img/75560511a7e73a3af522eac1204ae9a4.png)

生成的每个多边形中建筑物平均面积的地图。来源:ESRI 底图

现在我们有了一个基础设施的一般概念，城市中的大多数人将聚集在这里，因此交通也将主要集中在这些地区。然而，这并没有告诉我们从**六角形 A 到六角形 x**有多困难

这可以从 2020 年 ESRI 提供的一张 LULC 地图中推断出来。我们可以将 LULC 地图重新分类为成本表面地图。例如，这意味着，水的数字较高，因为它是理想世界中最不喜欢的出行方式，同样，建筑面积类的数字最低，因为我们假设该类还包括可行驶的道路。

最后，我们可以建立一个这样的表。

![](img/63071a1f15f609301157a855f8346f8b.png)

每个类别的地面通勤复杂性权重。

这是我们得到的 ESRI 地图样本。由于地图的分辨率较低，目视判读最多只能识别 3-4 个类别，因此地图用处不大。

![](img/f25477a88725fddff98f1271ee0a6d3d.png)

来自 ESRI 2020 的原始 LULC 地图。资料来源:ESRI

重新分类后，我们得到了以下描述通勤表面韧性的图像

![](img/361e088a870a86db960a69e29bf3f90e.png)

重新分类的 LULC 栅格。地图现在减少到只有 8 个类。NODATA 已被添加到被视为不可替换的类中。来源:ESRI 底图/ArcGIS Pro

为了最终为我们的道路创建成本表面模型，我们将开发一个简单的公式，为两个数据源分别赋予不同的权重。LULC 地图的权重较低，因为信息质量不如我们从建筑物图层获得的信息精确。

![](img/08f4c1cdd2bc250c1989ca9a6040e133.png)

以下地图是 LULC 和建筑物数量的混合栅格。一个地区可能有较低的建筑数量，但更难穿越的地表地形或看起来更像土路的糟糕道路，因此，在这些地方成本会更高。

![](img/297fa4de65761953637d5ebb749bda12.png)

加权栅格输出。来源:ESRI ArcGIS Pro

在 ArcGIS Pro 中运行**路径距离分配**工具后，我们提供道路网络作为输入源，道路最终被栅格化，每条道路线显示了通过该区域的出行成本。

![](img/c6167d8f1c39ee7131d8a8318a44863b.png)

道路网络及其相关成本的最终结果。来源:ESRI ArcGIS Pro

## 这是一个覆盖了道路网络的放大版本

![](img/41b3d0291912979371e20c55ba9b3d66.png)

最终地图的放大视图。来源:ESRI ArcGIS Pro

在哪些数据变量可用于提供更好的估计方面仍有很大的改进空间，但这可以作为数据不容易获得的交通相关应用的开端。

> 请随时联系:jaskaranpuri@gmail.com