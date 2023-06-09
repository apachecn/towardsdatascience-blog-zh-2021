# SQL 排序终极指南

> 原文：<https://towardsdatascience.com/the-ultimate-guide-to-sorting-in-sql-d856a15e4315?source=collection_archive---------43----------------------->

## *这本终极指南概述了 SQL 排名函数、它们的语法以及来自 StrataScratch 面试问题的真实面试示例*

![](img/46e1f12bf3085908e4b8865693e8cb93.png)

作者在 [Canva](https://canva.com/) 上创建的图片

数据科学家使用 SQL 来查询和操作数据集，根据业务需求对结果进行排序在现实应用中无处不在。除了现实世界的应用程序，SQL 排序问题也经常出现在面试中，这刺激了初出茅庐和经验丰富的数据科学家去掌握它们。

例如，在一个业务场景中，数据科学家可能需要为年同比订单量下降最多的 20 个客户编写查询脚本。在确定当年不太活跃的公司后，企业领导人可以为每个公司制定适当的战略，提高企业绩效。

在数据分析或数据科学面试中，你可能会被要求按降序排列最繁忙的一天。熟悉 SQL 排序原则将有助于您编写高效准确的查询。

在本文中，我们使用来自 StrataScratch 专有数据库的真实采访示例来研究 SQL 排序问题。我们将回顾正确回答 SQL 排序问题所需的方法和技能的最佳实践。

# SQL 排序问题

SQL 中的排序问题通常需要数据科学家争论相关数据，并对前 N 名或后 N 名结果进行排序。虽然参数和业务案例可能会有所不同，但排序查询的语法是相当一致的，通过实践，您可以提高在这些重要和常见问题上的性能。排序面试问题往往需要数据科学考生了解如何识别合适的数据，并根据某个属性进行排序。

在本文中，我们将介绍如何对预处理数据进行排序，以及如何对数据进行排序以准确得出结果。更具体地说，我们帮助您开发必要的技术框架，以了解分组观察、按列按特定顺序排序、添加排除不相关行的标准，以及如何确定最终结果中包含的行数。我们将通过复习三个面试问题来完成这一任务。这些问题的难度从相对简单的问题到更复杂的问题不等，但基本原理是相同的。

*   首先，查看您的表，并确保您理解您的数据集。如果可能的话，查看列名和每列中的一些值。如果只有一个表，这将是 FROM 命令引用的表。如果有多个表，您可能需要连接这些表。
*   接下来，确定你的问题所涉及的属性。例如，如果您的问题涉及“公司”或“卖方”，这些很可能包含在您的选择函数中。
*   对于我们的第三步，确定是否有任何额外的标准，如“包括在亚洲发生的结果”或“在过去 6 个月”。如果是这样，使用 WHERE 解决这些问题，并通过排除不符合我们标准的数据来减少我们的数据大小。
*   接下来，确定是否有提到的类别可以组合在一起。GROUP BY 将值转换为符合条件的记录的摘要。例如，可能会要求您按财政月对订单进行排序。在这种情况下，您需要根据财政月属性进行分组。
*   最后，我们指定对结果进行排序的属性。这可以以上升或下降的方式进行，意思是从最小到最大或从最大到最小。如果我们被要求找出 2021 年 MLB 赛季打出最多本垒打的前 5 支棒球队，我们对“本垒打”感兴趣，并将降序排列(从大到小)，限制为 5 支。极限是用极限来完成的，后面跟着数值。

虽然在排序问题中可以找到其他命令，但是理解 SELECT、FROM、WHERE、ORDER BY、GROUP BY 和 LIMIT 将有助于您解决这些常见问题。我们开始吧。

# 示例 1——福布斯面试问题

![](img/bc527860849f8915078d346965ef95e4.png)

作者在 [Canva](https://canva.com/) 上创建的图像

在《福布斯》最近的一次采访中，一名候选人被要求找出最赚钱的金融公司，并返回其名称和所在的洲。

![](img/e5ced7bd195ca1f068ffb43f04c510bf.png)

截图来自 [StrataScratch](https://platform.stratascratch.com/coding/9663-find-the-most-profitable-company-in-the-financial-sector-of-the-entire-world-along-with-its-continent?python=&utm_source=blog&utm_medium=click&utm_campaign=medium)

问题链接:[https://platform . stratascratch . com/coding/9663-寻找全球金融领域最赚钱的公司](https://platform.stratascratch.com/coding/9663-find-the-most-profitable-company-in-the-financial-sector-of-the-entire-world-along-with-its-continent?python=&utm_source=blog&utm_medium=click&utm_campaign=medium)

一个可能的解决方案是如下处理这个问题——使用 SELECT、FROM、WHERE、ORDER BY 和 LIMIT。

```
SELECT company, continent
FROM forbes_global_2010_2014
WHERE sector = 'Financials'
ORDER BY profits DESC LIMIT 1;
```

首先，我们以一种相当简单的方式使用 SELECT 命令，因为请求只需要公司的名称及其关联的洲。虽然更复杂的例子可能需要您在查询的早期完成聚合函数或定义变量，但这个例子只需要返回适当字段的名称。

一定不要错过这里的点。仔细检查问题并确认相关属性。对于电话面试，你可以与面试官跟进，以确保你了解感兴趣的属性。在工作或现实世界中，在运行查询之前，一定要提问以了解问题。对于使用云服务的公司来说，浪费的查询可能会导致更高的服务成本。

接下来，我们以一种简单的方式使用 FROM 语句来指定我们应该用来运行查询的表。在更复杂的查询中，您可能需要执行连接，这里我们只需要指定所需的表。查看我们关于 [SQL JOIN 面试问题](https://www.stratascratch.com/blog/sql-join-interview-questions/?utm_source=blog&utm_medium=click&utm_campaign=medium)的帖子，其中涵盖了最常见的 JOIN 面试问题。

即使在更复杂的查询中，一般的方法也是一样的。FROM 指示表上的 SQL 执行所需的查询。

下一步，让我们记住，我们被要求在结果中只包括金融公司。使用 WHERE，我们可以通过设置一个标准来包含“部门”列的值等于“财务”的属性，从而轻松实现这一点。通过只选择只有金融公司的行，我们从结果中删除了不相关的行。还值得注意的是，您可以通过编写相同的查询来显式排除条件，但是在等号(！idspnonenote)前包含一个感叹号。=).这仅仅意味着“不等于”。

ORDER BY 对于查询的成功完成尤为重要。“排序”的机械方面是通过 ORDER BY 来完成的，因为它提供了对哪一列结果进行“排序”的指令。对于这个问题，我们最感兴趣的是利润列。

ORDER BY 是一个灵活的函数，可以以“升序”或“降序”的方式执行。升序从序列中的最小值开始，向上计数到更大的值。默认情况下，SQL 按升序排序。降序从列中的最大值开始，并按“从大到小”的顺序对系列进行排序。

最后，LIMIT 设置要包含的最大结果数。如果我们在没有 LIMIT 命令的情况下运行上面的查询，我们的结果将包括表中的每一行，而不仅仅是利润最高的公司。通过设置一个限制，我们的查询只返回第一个结果。如果要求您包含更多结果，请相应地调整这个数字。

现在我们已经完成了整个查询，让我们快速回顾一下问题的逻辑。

从“forbes_global_2010_2014”表中，我们选择公司名称和相关的洲值。我们过滤掉金融行业的所有实例，然后根据利润值从最大值开始对剩余结果进行排序。然后我们设置一个限制，只包括最高的结果。这一过程充分回答了我们最初的问题，并且很容易被跟随您的任何其他数据科学家或分析师阅读。

# 示例 2 — Airbnb 面试问题

接下来，我们有一个 Airbnb 问题，要求候选人找到 2017 年夏天评论最积极的十大酒店，但只包括 6 月至 8 月之间的结果。

![](img/1f5aebbea44a86f156d2299bf1f0da17.png)

截图来自 [StrataScratch](https://platform.stratascratch.com/coding/9877-find-the-top-ten-hotels-with-the-most-positive-reviews-in-summer-june-aug?python=&utm_source=blog&utm_medium=click&utm_campaign=medium)

问题链接:[https://platform . stratascratch . com/coding/9877-查找夏季六月至八月评价最高的十大酒店](https://platform.stratascratch.com/coding/9877-find-the-top-ten-hotels-with-the-most-positive-reviews-in-summer-june-aug?python=&utm_source=blog&utm_medium=click&utm_campaign=medium)

然后，我们将输出酒店名称以及相应的正面评论数量。这些结果将根据正面评价的数量按降序排列。

一个机构群体提交的解决方案采用了以下方法。您是否注意到大多数函数在我们之前的示例中也是如何使用的？让我们看一下这个解决方案，了解一下如何解决稍微复杂一点的 SQL 排序问题。

```
select hotel_name,count(positive_review) as n_positive_reviews
from hotel_reviews
where review_date BETWEEN '6/1/17' and '8/31/17' and positive_review !=
    'No Positive'
group by hotel_name
order by n_positive_reviews desc
limit 10;
```

SELECT 再次用于从我们的表中选择相关字段，但是在这个例子中，我们还需要计算正面评论的数量。为了统计正面评论的数量，我们使用聚合函数“count ”,并使用 as 定义一个别名。我们称我们的别名为‘正面评论’。我们的别名是一个临时存储的变量，我们手动定义，并允许计算值有可识别的名称。

FROM 再次标识包含我们的数据的适当的表。与上一个问题类似，所有数据都存储在一个表中。

WHERE 函数用于定义日期范围的参数，并且只包含积极的结果。这是通过 BETWEEN 函数和定义日期来完成的。请注意，查询中的日期格式与表中的格式相匹配。通过指定 6 月 1 日和 8 月最后一天之间的日期，这确保了我们的结果表只包括相关的日期—6 月、7 月和 8 月。此外，AND 还用于引用“positive_review”列，并排除值为“No Positive”的观察值。的！查询中的“=”最终意味着“排除值等于下列 __”的结果。更简洁地说，它用来表示‘不等于’，起源于数学。

此处的 GROUP BY 语句指示查询根据“hotel_name”列中的值聚合结果。请记住，我们的问题要求我们找出 6 月至 8 月间评价最高的前十家酒店。酒店的名称存储在“hotel_name”中，因此请确保在搜索结果中包含这些信息。

接下来，我们使用 ORDER BY 函数对结果进行排序。通过引用之前启动的变量(n_positive_reviews ),查询将使用此列基于正面评论的计数进行排序。基于降序执行排序可以确保我们的最大值位于表的顶部。

最后，我们将我们的结果限制为包括十个结果，并且由于我们之前的 ORDER BY 语句，我们的前十个最大值。

# 示例 3 — Yelp 面试问题

![](img/5fe23cd2d8e5debb729125ef9b0eb5d7.png)

作者在 [Canva](https://canva.com/) 上创建的图像

在最后一个例子中，我们的任务是找出拥有最多五星级企业的 5 个州。

![](img/e13d5191c6301e41ef1d9987be98a10e.png)

截图来自 [StrataScratch](https://platform.stratascratch.com/coding/10046-top-5-states-with-5-star-businesses?python=&utm_source=blog&utm_medium=click&utm_campaign=medium)

问题链接:[https://platform . stratascratch . com/coding/10046-排名前 5 位的五星级企业](https://platform.stratascratch.com/coding/10046-top-5-states-with-5-star-businesses?python=&utm_source=blog&utm_medium=click&utm_campaign=medium)

一种可能的方法是如下看待问题，使用 SELECT、FROM、聚合函数 COUNT、GROUP BY、ORDER BY 和 LIMIT 来处理请求。

```
select state, five_stars
from (select state, count(stars) as five_stars from yelp_business
where stars=5
group by state) a
order by five_stars desc
limit 5;
```

首先，我们使用 SELECT 来包含两个感兴趣的变量——state 和一个我们稍后将定义的变量“five_stars”。由于问题指定了“stars”列的重要性，我们的变量“five_stars”在计算中引用了“stars”。

接下来，FROM 在这里比在其他例子中更活跃一些。FROM 不是简单地指定我们想要引用的表的名称，而是用来完成一个更复杂的任务。为了更好地理解正在发生的事情，让我们从第 2 行的末尾向后看。首先，我们明确定义了我们所引用的表——“yelp _ business”。这实际上和我们其他的练习题是一样的。接下来，我们从选择函数中定义名为“five_stars”的变量。“Five_stars”是包含“state”并执行“stars”计数的表的别名。接下来，代码指示只包含“stars”列等于 5 的行，并使用 GROUP BY 对 state 进行分组。

让我们花点时间看看我们到目前为止做了什么。我们在 yelp_business 表中查询了自己的“state”列和一个通过别名(five_stars)创建的附加列。变量“five_stars”包含“state ”,并将其与一个附加列配对，该列计算“stars”列等于 5 的实例的数量。我们最初的请求是找到拥有最多五星级餐厅的五个州，通过按州统计五星级餐厅，我们很好地完成了这个问题。

现在我们有了一个计算五星级餐馆数量的结果，剩下的就是将结果从大到小排序并包括前 5 名。

接下来，我们使用 ORDER BY 通过调用我们的“five_stars”表来准备排序，并指示降序排序。记住，这意味着返回表顶部的最大值。

最后，根据我们问题的参数，我们设置我们的极限函数只包括前 5 个结果。

*此外，请查看我们的*[*SQL 窗口函数终极指南*](https://www.stratascratch.com/blog/the-ultimate-guide-to-sql-window-functions/?utm_source=blog&utm_medium=click&utm_campaign=medium) *，了解 SQL 窗口函数的类型、语法以及实际使用示例。*

# 结论

无论什么行业，掌握 SQL 中的排序对业余和高级程序员都很有用。数据科学家可能会遇到许多排序的用例，完善你的技术可以提高你对团队产生影响的能力。SQL 中排序的一般原理是一致的，效率是通过重复发展起来的。StrataScratch 提供了数千个练习题，让你为下一次面试做好准备，或者提高你在数据科学领域工作的数据技能。

*最初发表于*[*【https://www.stratascratch.com】*](https://www.stratascratch.com/blog/the-ultimate-guide-to-sorting-in-sql/?utm_source=blog&utm_medium=click&utm_campaign=medium)*。*