# 政府类型对新冠肺炎限制的影响

> 原文：<https://towardsdatascience.com/did-government-type-have-an-effect-on-restrictive-covid-19-measures-68fa31124b8d?source=collection_archive---------23----------------------->

## 威权政府比民主政府更有可能颁布更具限制性的新冠肺炎措施吗？

![](img/029a7cd527930ef80714ca5ea3185867.png)

乍一看，独裁政府对新冠肺炎的最初反应似乎比民主政府快得多。但这是正确的说法吗？(图片由作者提供)

新冠肺炎疫情病毒首次爆发已经一年多了。自那以后，我们看到各国以截然不同的方式处理疫情问题，许多人思考了可以用来预测各国不同反应和经历的指标。一些[学者](https://journals.sagepub.com/doi/full/10.1177/2319714520928884)认为，由于民主对人民的责任，民主政府(而不是专制政府，如中国的)是成功控制疫情的关键(Alon et al .，2020)。卡内基国际和平基金会(Carnegie Endowment for International Peace)的研究提出了一个更具批判性的观点，认为即使是韩国和意大利等民主国家也采用了近乎独裁主义的方法，如侵犯隐私的数字合同追踪应用程序或违反隔离的刑事处罚(Kleinfeld，2020)。

在这篇文章中，我考察了政府对新冠肺炎的反应和国家的民主水平之间的关系。我要问的是，正如经济学人智库(EIU)所描述的那样，政府的政权类型是否会对政府的反应产生影响。我假设专制国家对制定内部流动限制的反应更快，而民主国家反应更慢。本文旨在介绍探索性分析，调查新冠肺炎疫情最初几个月与政府类型的关系，并鼓励未来的研究。

我使用 Python 和标准数据科学包进行分析。我用`BeautifulSoup`从维基百科上抓取民主指数。我使用`pandas`来处理我的大部分数据争论、切片、合并和操作。我用`seaborn`来绘图。用于进行这些分析的 Jupyter 笔记本可在 [my GitHub](https://github.com/yenniejun/covid_government_type) 上获得。

# 数据

我使用两个来源的数据:

*   OxCOVID19 数据库:这是牛津大学编译的新冠肺炎数据数据库。它是几个数据库的广泛集合，不仅包括与 COVID 病例和死亡相关的标准流行病学统计数据，还包括关于流动模式、天气模式和政府应对指标的数据。我使用`EPIDEMIOLOGY`表按国家确定第一个新冠肺炎病例。我还使用了`GOVERNMENT_RESPONSE`表，其中包含了各国政府为应对疫情而采取的遏制和关闭政策的信息(这是[牛津新冠肺炎政府应对跟踪](https://www.bsg.ox.ac.uk/research/research-projects/covid-19-government-response-tracker) (Mahdi 等人，2020 年)的一部分)。推荐大家去查阅一下指标的完整列表，可以在[码本](https://github.com/OxCGRT/covid-policy-tracker/blob/master/documentation/codebook.md)中找到。在这篇文章中，我特别关注其中一个指标:`c7_restrictions_on_internal_movement`
*   民主指数:经济学人智库(EIU)计算出一个数值分数来衡量每个国家的民主程度，数值越高，政府越民主。这一民主分数被映射到四种政体类型之一:完全民主、有缺陷的民主、混合民主和专制。民主指数是从相应的维基百科页面收集的。

# 关于民主指数的一点信息

[EIU 2020 年民主指数](https://www.eiu.com/n/campaigns/democracy-index-2020/)用于衡量民主和政体类型(经济学人智库，2020)。民主指数吸收了每个国家的 60 个不同指标，计算出代表民主的数值分数，数值越高，政府越民主。这一民主分数被映射到四种政体类型之一:完全民主、有缺陷的民主、混合民主和专制。民主指数来自维基百科页面。虽然民主指数有其自身的批评和局限性(将在本文后面讨论)，但一些研究，[包括 Bashar 和 Tsokos (2019)](https://www.researchgate.net/publication/338816815_Statistical_Classification_of_Democracy_Index_Scores_of_Countries_of_the_World) 的研究，声称它是最全面的民主指标。

每个国家第一个新冠肺炎病例的日期是从 OxCOVID19 的流行病学表中通过确定第一个病例数超过 0 的条目来计算的。内部流动的严格性来自 OxCOVID19 的政府响应表。这一具体指标可以取下列值之一:0(无措施)、1(建议不要在区域/城市之间旅行)、2(内部流动限制到位)和空白(无数据)。这一分析侧重于二级限制，因为它旨在将最严格的政府措施与威权主义联系起来。

# 结果

乍看之下，专制国家在制定严格的内部流动规则方面似乎比民主国家反应更快。一些威权国家(如利比亚和委内瑞拉)在报告首例新冠肺炎病例前几天颁布了限制措施。

`Figure 1`按政权类型对颁布内部限制措施的反应速度进行分组。政府的政体类型越专制，对内部流动限制的严厉反应就越快。这似乎证实了一个假设，即独裁政府在制定内部限制措施方面行动更快，而民主政府则行动更慢。

![](img/5624adbb6a6a35b067cdf79e989201f7.png)

(图片由作者提供)

然而，在按照第一个新冠肺炎病例的日期来划分反应速度时，分析表明，第一次感染的日期对反应速度有很大影响。`Figure 2`显示了政府响应时间，按制度类型分开，第一个新冠肺炎病例的日期按月和按周汇总。对于后来的第一批新冠肺炎病例，政权的威权性质似乎对反应时间的影响较小。

![](img/14661a86fde866d9c77f1137c121c7ca.png)

(图片由作者提供)

在按月累计的响应时间中，与其他类型的政体相比，威权政体的平均响应时间在前两个月明显更快。到第三个月，所有制度类型的平均值似乎相等。在按周汇总的响应时间中，随着时间的推移，下降趋势变得明显。对于较早出现首例新冠肺炎病例的国家(在第 8 周之前)，红色数据点显示，独裁政权往往比其他类型的政权反应更快。对于首次新冠肺炎日期较晚(即 8 周后)的国家，由于数据点紧密聚集且变化较小，因此用药制度类型对反应时间的影响较小。

总体而言，第一例新冠肺炎病例的日期对一国政府颁布限制措施所需的天数有影响，尽管该国政府的政体类型不容忽视。对此的一种解释是，对于那些较早出现首例新冠肺炎病例的国家，独裁政权更有可能实施严格的国内运动措施。对于后来出现首批新冠肺炎病例的国家，制度类型对严格措施的影响较小。

`Figure 3`显示了政府对 2020 年 2 月 15 日前后出现首例新冠肺炎病例的国家实施内部流动限制的回应。选择 2 月 15 日作为截止日期是因为，正如在`Figure 2`中看到的，大约在第 8 周聚集行为开始出现。2020 年的第八周始于 1 月 16 日。

![](img/c6fab2956c19eb0ecbacdbee747d6c3c.png)

(图片由作者提供)

对于在 2 月 15 日之前出现首例病例的国家，威权国家的反应平均要快 20 天左右。对于 2 月 15 日之后出现首例病例的国家，所有国家都倾向于做出更快的反应，威权政权对反应时间的影响较小。对于在 2 月 15 日之后出现首例病例的国家，民主国家往往需要最长时间做出反应，而对于在 2 月 15 日之前出现首例病例的国家，这一趋势并不明显。

`Figure 4`显示了每种制度类型的响应分布。专制、混合和有缺陷的民主政权往往是单峰的，有长的右尾巴，这意味着他们的反应有一些统一，但在模式之外有一些变化。紫线所示的民主政权反应时间的分布就不那么确定了。民主政权的反应时间分布是双峰的和可变的，这表明不同民主政权的反应差异很大。

![](img/2193722bc4b066bfa19c9e98c0332f4a.png)

(图片由作者提供)

`Figure 5`针对每种制度类型，绘制响应速度最慢的前 3 个国家和响应速度最快的前 3 个国家。圆点表示第一个新冠肺炎病例的日期，箭头的末端表示第一次响应颁布内部移动限制的日期。向左箭头表示该国在他们的第一个病例之前已经作出反应。虚线上方是每个政权类型中反应最快的前 3 个国家。虚线下方是每个制度类型中反应最慢的前 3 个国家。

![](img/f693c5149453efd62e641c789210aeda.png)

(图片由作者提供)

该图证实了上述观察结果，即较晚出现新冠肺炎首例病例的国家比较早出现新冠肺炎首例病例的国家反应更快。然而，即使在这个框架内，我们可以注意到最快的民主国家的反应与其他 3 种政体类型中最快的国家的反应有很大的不同。即使是最快的民主国家也没有积极响应(即在新冠肺炎确诊病例之前)，而其他类型的政权却这样做了。

至于反应最慢的国家，各种制度类型之间似乎差异不大。无论何种政体类型，较早出现首例新冠肺炎病例的国家往往比较晚出现首例新冠肺炎病例的国家需要更长的时间做出反应。

# 讨论和限制

该项目表明，虽然在某些情况下，专制政权实施内部限制的反应更快，但许多其他因素影响了这一观察。几乎所有后来出现新冠肺炎病例的政体都迅速做出了反应，不仅仅是威权政体，也不是所有威权政体都迅速做出了反应。这与民主政府和独裁政府各有优缺点的观点相一致，它们都不擅长应对新冠肺炎的威胁(Stasavage，2020)。

有几个突出的因素没有包括在这个分析中。这一分析中未包括的因素包括国家人口、新冠肺炎严重程度和国家以往大流行的历史。鼓励未来的研究人员调查一些因素，如这些国家与病毒最初爆发的中国在地理上的接近程度。也许蒙古反应如此迅速的原因之一(在他们的第一个新冠肺炎病例前 18 天)是因为他们与中国接壤。

# 数据来源的有效性

对分析中使用的数据来源持批评态度是很重要的。EIU 的民主指数被用来代表一个国家的威权和民主水平，但该指数一直受到批评。例如，Bashar 和 Tsokos (2019)认为，EIU 的民主指数可能不太准确，因为它没有考虑到收集的数据之间的相互作用和相关性。

OxCOVID19 数据库中也有一些空白。没有以下国家的病例数数据:瓦努阿图、皮特凯恩岛、也门、福克兰群岛、所罗门群岛、香港、南苏丹、澳门、马拉维、土库曼斯坦、塔吉克斯坦和莱索托。也可能有人担心为每个国家计算的第一个新冠肺炎病例的准确性。[一项研究](https://arxiv.org/abs/2007.09566)使用统计方法表明，独裁政府很可能操纵了他们公布的新冠肺炎数据(Kapoor 等人，2020)。由于数据库中的数据可能不准确或伪造，第一个新冠肺炎病例的日期可能不准确，并且本文的分析具有误导性。

# 未来方向

这项研究只调查了国家对国内流动实施严格限制的时间。我们鼓励未来的研究结合世界价值观调查数据对其他类型的限制进行重复研究。更重视贸易的国家会不会更慢地颁布国际旅行管制的限制？更重视教育的国家在颁布关闭学校的限制方面往往更慢吗？这项研究中的分析可以用关于每个国家的额外数据来充实，如国内生产总值、卫生基础设施状况和以前大流行的历史。有许多方向可以将当前的研究扩展到对各国应对全球疫情的新理解。

# 参考

阿龙，我，法雷尔，m .，，李，S. (2020)。政体类型和新冠肺炎反应。FIIB 商业评论，9，152–160 页。

巴沙尔河和措科斯河(2019 年)。世界各国民主指数得分的统计分类。

牛津新冠肺炎政府响应跟踪码本(2020)。GitHub 仓库。2020 年 11 月 18 日检索自[https://github . com/ox cgrt/covid-policy-tracker/blob/master/documentation/code book . MD](https://github.com/OxCGRT/covid-policy-tracker/blob/master/documentation/codebook.md)。

民主指数。(2020).民主指数。2020 年 11 月 29 日，从 https://en.wikipedia.org/wiki/Democracy_Index[检索。](https://en.wikipedia.org/wiki/Democracy_Index)

经济学人信息部。(2020).民主指数 2020。于 2021 年 3 月 27 日从[https://www.eiu.com/topic/democracy-index](https://www.eiu.com/n/campaigns/democracy-index-2020/)取回。

m .卡普尔、a .马拉尼、s .拉维和 a .阿格拉瓦尔(2020 年)。独裁政府似乎操纵 COVID 数据。arXiv:普通经济学。

柯菲德河(2020)。专制国家还是民主国家更好地应对流行病？。卡内基国际和平基金会。2020 年 11 月 29 日检索，来自[https://Carnegie endowment . org/2020/03/31/do-authoritative-or-democratic-countries-handle-pandemics-better-pub-81404](https://carnegieendowment.org/2020/03/31/do-authoritarian-or-democratic-countries-handle-pandemics-better-pub-81404)。

Mahdi，a .、Blaszczyk，p .、Dlotko，p .、d .、Chan，t .、Harvey，j .、Gurnari，d .、Wu，y .、Farhat，a .、Hellmer，n .、Zarebski，a .、Hogan，b .、& Tarassenko，L. (2020)。OxCOVID19 数据库:更好理解新冠肺炎全球影响的多模态数据库。medRxiv。

斯塔萨维奇博士(2020 年)。民主、专制和紧急威胁:新冠肺炎过去一千年的教训。国际组织，1–17。doi:10.1017/S0020818320000338。