# 通过可视化 YouTube 上的社区和联系获得的见解

> 原文：<https://towardsdatascience.com/insights-from-visualizing-communities-and-connections-on-youtube-30141f31bb20?source=collection_archive---------14----------------------->

## 流行文化的视觉图谱

![](img/bd15299edebf7d067b567befc1857b83.png)

YouTube 图集[作者]

YouTube 一直以其难以置信的庞大内容库吸引着我。点击缩略图，发现单片频道，并找到丢失的文物感觉很像探索。

这种探索启发了我，让我尝试将内容生态系统作为一个整体来缩小和可视化。YouTube 的地图集会是什么样的？这种类型的可视化有什么见解？

看到大范围的社区和联系也可能是理解在线行为的有力工具。随着危险的互联网泡沫和新社区的崛起，有必要了解这些群体是如何形成、成长和变化的。

大约一年前，我创建了热门直播网站 Twitch 的地图。这个项目向我展示了社交媒体关系的视觉表现可以引起平台、创作者和观众的共鸣。我在这里写了一篇关于我的观察的文章。

为 YouTube，一个*大得多的*平台，复制这个过程不是一件容易的事情*。*我需要一种方法，通过可公开访问的数据将频道相互连接起来。我通过查看每个视频下谁留下评论找到了我的答案。通过收集这些评论，并在多个渠道中进行比较，我可以构建一个渠道关系图。这可以被可视化成一个地图集。

经过几个月的 AWS 学习，大量的 Python，平衡了一学期的课业，我达到了我的目标。该地图集的一个可搜索、可交互的版本位于 https://youtubeatlas.com<https://youtubeatlas.com.>****。去探索吧！**对任何可用性怪癖表示抱歉。我不是一个有经验的 web 开发人员，这个实现的大部分使用了一个我不太了解的库和框架。下面是地图的静态图像，供那些对交互式版本有疑问的人使用。**

**![](img/74c4db41eae0d6055bdb342eef438441.png)**

**按地区[按作者]标记的 YouTube 图集**

> **互动地图可在[https://youtubeatlas.com](https://youtubeatlas.com)获得**

# **如何阅读地图集**

*   **每个泡泡都是一个 YouTube 频道。**
*   **每个气泡的大小由该频道的用户数决定(2021 年 8 月)**
*   **两个泡泡之间的一条线显示，这两个频道在收集的 20，000 条评论中至少分享了 350 条评论。**
*   **气泡的颜色表示所有共享评论者的 YouTube 频道社区。这是由检测图簇的[模块算法](https://neo4j.com/docs/graph-data-science/current/algorithms/modularity-optimization/)决定的。**

## **谁在地图上？**

**该图集显示了按用户数量排名的前 5700 个 YouTube 频道。 [SocialBlade](https://socialblade.com/) 非常好心地提供了这个列表，如果没有他们的帮助，这个项目是不可能完成的！**

**地图集不包括针对儿童的频道，因为这些频道不允许评论(例如 [Cocomelon](https://www.youtube.com/channel/UCbCmjCuTUZos6Inko4u57UQ) 是 YouTube 上第四大频道，但属于此类)。**

**如果你想知道更多关于我的方法和过程的细节，这个项目的所有代码都是公开的[在这里](https://github.com/KiranGershenfeld/YoutubeCommunities)。**

# **地图集告诉了我们什么？**

**虽然一开始可能会有很多东西需要接受，但一些事情可能会立即凸显出来。以下是从可视化如此庞大的内容生态系统中可以发现的一些见解。**

## **彩虹簇**

**t 系列是 YouTube 上最大的频道，拥有 2 亿订户。宝莱坞音乐集团在 2019 年的比赛中超过了 PewDiePie，达到 1 亿，并继续以越来越快的速度增长。**

**该频道也是代表印度 YouTube 社区的色彩鲜艳的集群的一员。这个星团和巴西星团(都在下图中)看起来与地图的其他部分非常不同——它们的密度令人难以置信，并且具有许多不同的颜色。**

**![](img/e8a07bd246d36a81d1e4333a2c329acf.png)**

**巴西和印度集群[作者]**

**为什么印度和巴西群集看起来与其他语言区域如此不同？**

**像 T8 T 系列和 T10 Canal KondZilla 这样的频道每天会上传很多次音乐视频，大部分都是很低的收视率。由于这些国家人口众多，视频数量庞大，大多数评论者在我的数据中只出现过一次。这就是为什么计算机在这些集群中分配了如此多的颜色，并揭示了这些频道正在向大量人口中的大量不同观众广播。**

**这些星团的第二个定义特征是它们与地图上其他区域相比的密度。这是因为将这些频道链接在一起的评论者通常会将所有的*频道链接在一起。这些狂热的粉丝导致这些音乐/电影频道非常紧密地聚集在一起。***

**许多 YouTube 用户不知道这些社区在这个平台上有如此巨大的影响力。即使看看 YouTube 热门频道的列表和它们的页面，也不能清楚地表明这些频道的表现与大多数其他地区不同。通过像这样可视化社区和连接，这种独特的受众行为就凸显出来了。**

## **中间的斗争**

**地图集上广阔的英语区占据了图像中心的大部分。四个社区在这个区域的中心发生冲突，颜色分别为橙色、浅蓝色、绿色和紫色(如下图所示)。总的来说，这四个地区包含了大多数人认为的现代英语 YouTube 景观。分开来看，这些地区都有独特的文化，根据我的经验，推荐源通常都在这些界限之内。**

**![](img/8528e76cad9b2aba8628c1b47b257d43.png)**

**英语社区的冲突在中心[作者]**

**Orange 包含好莱坞脱口秀和许多高预算、适合家庭的创作者。浅蓝色以视频游戏和游戏相关内容为中心，但已经发展到包括许多其他形式的互联网娱乐。Magenta 是 YouTube 广泛教育的一面，这是一个随着最近“教育娱乐”内容的繁荣而爆炸的部分。我在这部分的大部分时间都在看像 [3Blue1Brown](https://www.youtube.com/channel/UCYO_jab_esuFRV4b17AJtAw) 、 [CGPGrey](https://www.youtube.com/greymatter) 和[马克斯·布朗利](https://www.youtube.com/c/mkbhd)这样的频道。深绿色给了我们嘻哈明星和吸引粉丝的大范围的影响者。**

**这些地区已经相对独立，随着 YouTube 的发展，它们之间的距离越来越远。我在紫色区域的生活实际上从未让我接触到橙色或绿色通道，尽管我确实倾向于浅蓝色边界。考虑到这种日益严重的两极分化，将这些有色人种社区联系在一起的渠道变得越来越重要。**

**以[马克罗伯](https://www.youtube.com/c/MarkRober/videos)为例。这位前美国国家航空和宇宙航行局科学家创造了主要用于娱乐目的的野生工程装置(例如[病毒闪光炸弹](https://www.youtube.com/watch?v=3c584TGG7jQ)系列)。这个频道是淡蓝色的，而不是像大多数其他工程或科学频道那样是紫色的。这是因为马克专注于娱乐，并与流行游戏创作者有着非常紧密的联系，如 MrBeast。**

**马克和其他几个娱乐科学频道通过合作和深思熟虑的内容创作赢得了两个受众。我认为这个职位的渠道将对整个英语集群的发展产生重大影响，Mark 是社区之间桥梁的一个很好的例子。**

## **区域桥梁**

**地图集各区域之间的许多链接可以很好地展现社区之间是如何相互作用(或不相互作用)的。**

**![](img/1e859e79c1a87d139e411bcbe85a4b2e.png)**

**西班牙语和英语语言群集的边界[按作者]**

**看看地图上英语和西班牙语地区之间的桥梁，就可以看到夏奇拉、路易斯·丰西和皮特保罗等频道。正如所料，这些艺术家在拉丁美洲和美国观众中都很受欢迎。事实上，有很容易识别的渠道将美国音乐与西班牙、巴西、阿拉伯和东亚音乐文化联系起来。尽管有大量的印度音乐频道，但印度和英语集群之间似乎没有音乐联系。也许是一个等待被填补的空缺。**

**音乐只是这些双重文化渠道形成的一个维度。我鼓励你在地图上找到不同的社区，并寻找将它们联系在一起的渠道。我认为这些空间代表了 YouTube 作为一个平台和内容创作者的一些最大的增长机会。**

## **开放式问题**

**探索地图集不可避免地会带来疑问和好奇。以下是一些我仍然没有答案的问题:**

**为什么印度尼西亚和菲律宾集群在地理上彼此接近，却位于地图的两极对立的两侧？**

**为什么俄语集群与其他外语集群相比如此明显地孤立？**

**为什么许多粉红色的英国音乐艺术家被排挤在英国音乐圈之外？为什么他们各自的 VEVO 频道通常更靠近中心？**

# **最后的想法**

**我相信，能够以这种方式将互联网文化形象化，对于创作者、消费者和平台来说都是非常有价值的。**

**它可以帮助创作者了解他们的观众不仅在一维指标，而且在文化，社区和联系。这种理解可以指导新的内容方法，并激发新的利基形成。**

**它可以帮助消费者对他们消费的内容做出明智的选择，并更好地理解吸引我们注意力的算法。它还可以提供一种途径，在平台上完全不同的地方找到新的创作者，或者在他们非常熟悉的社区中找到隐藏的宝石。**

**它可以帮助 YouTube 微调算法旋钮，以增加观看时间和参与度等北极星指标。研究这些社区和它们之间的联系也可以洞察在线毒性、积极性和适度性。**

**作为一个 20 岁的大学生，我在这些网络社区中度过了很长一段时间，我知道它们对社区居民有多重要。理解它们是如何成长、变化和相互作用的是令人着迷的，我希望成为其中的一员。**

**如果你喜欢图集，请分享给大家！**

**你可以在 Twitter 上找到我，或者在 Github 上找到 T2。**

**感谢阅读！**