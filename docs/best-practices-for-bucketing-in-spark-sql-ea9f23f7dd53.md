# Spark SQL 中存储桶的最佳实践

> 原文：<https://towardsdatascience.com/best-practices-for-bucketing-in-spark-sql-ea9f23f7dd53?source=collection_archive---------0----------------------->

## Spark 斗气终极指南。

Spark 从 2.0 版开始支持分桶功能。这是一种如何在文件系统中组织数据并在后续查询中利用它的方法。

有许多资料解释了分桶的基本思想，在本文中，我们将更进一步，更详细地描述分桶，我们将看到它可能具有的各种不同方面，并解释它如何在幕后工作，它如何随着时间的推移而发展，以及最重要的是，如何有效地使用它。

我们将从两个不同的角度来看分桶—一个是数据分析师的角度，他是数据的典型用户；另一个是数据工程师的角度，他负责准备数据并将其展示给数据用户。

在本报告中，我们将讨论 Spark 3.1.1 中对 bucketing 的最新增强，这是撰写本文时的最新版本，对于代码，我们将使用 PySpark API。

# 什么是 bucketing？

让我们从这个简单的问题开始。Spark 中的分桶是一种如何以特定的方式组织存储系统中的数据的方式，以便可以在后续的查询中利用它，从而变得更加高效。如果存储桶设计得很好，这种效率的提高与避免查询中的连接和聚合混乱特别相关。

具有排序-合并联接或混排-散列联接以及聚合或窗口函数的查询要求数据按联接/分组键重新分区。更具体地说，具有相同联接/分组键值的所有行必须在同一个分区中。为了满足这一要求，Spark 必须对数据进行重新分区，为了实现这一点，Spark 必须将数据从一个执行器物理地移动到另一个执行器——Spark 必须进行所谓的洗牌(有关 Spark 用来确定是否需要洗牌的逻辑的更多详细信息，请参见我的另一篇与该主题密切相关的文章。

有了 bucketing，我们可以提前洗牌，并以这种洗牌前的状态保存数据。在从存储系统读回数据后，Spark 将会意识到这种分布，并且不需要重新洗牌。

## 如何使数据分桶

在 Spark API 中，有一个函数 *bucketBy* 可用于此目的:

```
(
  df.write
  .mode(saving_mode)  # append/overwrite
  .bucketBy(n, field1, field2, ...)
  .sortBy(field1, field2, ...)
  .option("path", output_path)
  .saveAsTable(table_name)
)
```

这里有四点值得一提:

*   我们需要将数据保存为表格(一个简单的*保存*函数是不够的)，因为关于分桶的信息需要保存在某个地方。调用 *saveAsTable* 将确保元数据保存在 metastore 中(如果配置单元 metastore 设置正确的话), Spark 可以在访问表时从那里获取信息。
*   与 *bucketBy、*一起，我们也可以调用 *sortBy* ，这将按照指定的字段对每个桶进行排序。调用 *sortBy* 是可选的，分桶也可以在没有排序的情况下工作。反过来也不行——如果不调用 *bucketBy* ，就不能调用 *sortBy* 。
*   *bucketBy* 的第一个参数是应该创建的桶的数量。选择正确的数量可能很棘手，最好考虑数据集的整体大小以及所创建文件的数量和大小(参见下面更详细的讨论)。
*   不小心使用 *bucketBy* 函数可能会导致创建过多的文件，并且在实际写入之前可能需要对数据帧进行自定义重新分区——参见下面关于此问题的更多信息(在*从数据工程师的角度进行分桶*部分)。

## 数据是如何在存储桶之间分布的？

因此，我们知道分桶会将数据分发到一些桶/组中。您现在可能想知道这些桶是如何确定的。有了一个特定的行，我们知道它将在哪个桶中结束吗？嗯，是的！粗略地说，Spark 使用一个应用于 bucketing 字段的散列函数，然后计算这个散列值*模*应该创建的桶数(hash(x) mod n)。这个*模*操作确保创建的存储桶不超过指定的数量。为了简单起见，让我们首先假设在应用散列函数之后我们得到这些值:(1，2，3，4，5，6)并且我们想要创建 4 个桶，所以我们将计算*模* 4。模函数返回整数除法运算后的余数:

```
1 mod 4 = 1  # remainder after the integer division
2 mod 4 = 2
3 mod 4 = 3
4 mod 4 = 0
5 mod 4 = 1
6 mod 4 = 2
```

计算出的数字就是最终的桶。如您所见，我们只是将这六个值分配到四个桶中

```
(1, 2, 3, 4, 5, 6 ) -> (1, 2, 3, 0, 1, 2)
```

更确切地说，Spark 不是使用简单的模函数，而是所谓的正模，它确保最终的桶值是一个正数，定义如下:

```
b = value mod nif b < 0:
  b = (b + n) mod n
```

因此，如果桶值为负，我们将添加 *n* (桶数)并再次计算*对*取模，这将不再是负的。让我们假设这个例子，其中散列函数返回负数-9，我们想要计算它属于哪个桶(仍然假设我们使用四个桶):

```
n = 4
value = -9b = value mod n = -9 mod 4 = -1# be is negative so we continue:
b = (b + n) mod n = (-1 + 4) mod 4 = 3 mod 4 = 3
```

因此值-9 将属于第 3 个存储桶。

Spark 使用的哈希函数是通过 MurMur3 哈希算法实现的，该函数实际上是在 DataFrame API 中公开的(参见[文档](https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.functions.hash.html#pyspark.sql.functions.hash))，因此如果我们需要，我们可以使用它来计算相应的桶:

```
from pyspark.sql.functions import hash, col, expr(
  spark.range(100) # this will create a DataFrame with one column id
  .withColumn("hash", hash(col("id")))
  .withColumn("bucket", expr("pmod(hash, 8)"))
)
```

在这里，我们可以看到，如果我们使用带有 8 个存储桶的列 *id* 的存储桶，数据将如何分布到存储桶中。注意， [*pmod*](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) 函数是在 *expr* 内部调用的，因为该函数在 PySpark API 中不直接可用，但在 SQL 中可用(要查看关于如何将 *expr* 函数与 SQL 函数一起使用的更多信息，可以查看我最近的关于 DataFrame 转换的[文章](/a-decent-guide-to-dataframes-in-spark-3-0-for-beginners-dcc2903345a5))。

# 桶装的优势

分桶的主要目的是加快查询速度，提高性能。分桶主要在两个方面有所帮助，第一个方面是避免在使用连接和聚合的查询中出现混乱，第二个方面是通过称为分桶修剪的特性来减少 I/O。让我们在下面的小节中更详细地了解这两种优化机会。

## 无洗牌连接

如果您要连接两个表，并且这两个表都不是特别小，Spark 将必须确保这两个表以相同的方式分布在集群上(根据连接键),因此将对数据进行混洗(这两个表都将被混洗)。在查询计划中，您将在连接的两个分支中看到一个*交换*操作符。让我们看一个例子:

```
tableA.join(tableB, 'user_id') 
```

如果计划使用排序合并连接，则执行计划将如下所示:

![](img/a34a013a3e50b9e3acebd12bed8985bc.png)

作者图片

正如您所看到的，连接的每个分支都包含一个代表 shuffle 的*交换*操作符(注意 Spark 并不总是使用排序-合并连接来连接两个表——要查看 Spark 选择连接算法所使用的逻辑的更多细节，请参阅我的另一篇关于 Spark 3.0 中的连接的文章)。

但是，如果两个表都被连接键存储到相同数量的存储桶中，Spark 将读取具有这种特定分布的集群上的数据，因此不需要额外的重新分区和洗牌——计划中将不再出现*交换*操作符:

![](img/c72acf79a18c6ab47d72f19a09667ceb.png)

作者图片

## 单向无洗牌加入

一个有趣的问题是，如果只有一个表被分桶，而另一个没有，会发生什么情况。答案实际上取决于桶的数量和洗牌分区的数量。如果存储桶的数量大于或等于洗牌分区的数量，Spark 将只洗牌连接的一边——没有被存储桶的表。但是，如果桶的数量少于混洗分区的数量，Spark 将混洗两个表，并且不会利用其中一个表已经被很好地分布的事实。随机分区的默认数量是 200，可以通过以下配置设置进行控制:

```
spark.conf.set("spark.sql.shuffle.partitions", n)
```

因此，如果我们使用默认设置(200 个分区)，其中一个表(比如说 *tableA* )被分成 50 个桶，而另一个表( *tableB* )根本没有被分成桶，那么 Spark 会将两个表进行混洗，并将这些表重新分成 200 个分区。

为了确保利用*表 A* 的分桶，我们有两个选择，或者我们将洗牌分区的数量设置为桶的数量(或者更小)，在我们的例子中是 50，

```
# if tableA is bucketed into 50 buckets and tableB is not bucketedspark.conf.set("spark.sql.shuffle.partitions", 50)tableA.join(tableB, joining_key)
```

或者，我们通过显式调用 repartition 将*表 B* 重新分区为 50 个分区，如下所示:

```
(
  tableA
  .join(tableB.repartition(50, joining_key), joining_key)
)
```

这两种技术都将导致单向无洗牌连接，这也可以从查询计划中看出，因为*交换*操作符将只出现在连接的一个分支中，因此只有一个表将被洗牌。

## 具有不同存储桶编号的表

这里还有一种情况我们可以考虑。如果两个表都分桶，但是分入不同数量的桶中，会怎么样呢？将会发生什么取决于 Spark 版本，因为在 3.1.1 中对这种情况进行了增强。

在 3.1 之前，情况实际上类似于前面的情况，其中只有一个表被分桶，而另一个没有，换句话说，两个表都将被混洗，除非满足混洗分区和桶数量的特定条件，在这种情况下，只有一个表将被混洗，我们将获得一个单边无混洗连接。这里的条件与前面类似—洗牌分区的数量必须等于或小于较大表的桶的数量。让我们在一个简单的例子上更清楚地看到这一点:如果 *tableA* 有 50 个桶， *tableB* 有 100 个，洗牌分区的数量是 200(默认)，在这种情况下，两个表都将被洗牌为 200 个分区。然而，如果混洗分区的数量被设置为 100 或更少，则只有*表 A* 将被混洗到 100 个分区中。类似地，我们也可以将其中一个表重新划分为另一个表的桶数，在这种情况下，在执行过程中也只会发生一次洗牌。

在 Spark 3.1.1 中，实现了一个新特性，如果桶数是彼此的倍数，它可以将较大数量的桶合并成较小数量的桶。这个特性默认是关闭的，可以用这个配置设置*spark . SQL . bucketing . coalescebucketsinjoin . enabled*来控制。因此，如果我们打开它，再次将*表 A* 存储到 50 个桶中，*表 B* 存储到 100 个桶中，那么连接将是无洗牌的，因为 Spark 将把*表 B* 合并到 50 个桶中，所以两个表将具有相同的编号，这将与洗牌分区的数量无关。

## 那种呢？

我们已经看到，通过分桶，我们可以从排序-合并连接计划中消除*交换*。该计划还包含*排序*操作符，就在*交换*之后，因为必须对数据进行排序才能正确合并。我们能不能也取消*排序*？您可能想说是，因为分桶也支持排序，我们可以在 *bucketBy* 之后调用 *sortBy* 并对每个桶进行排序，这样在连接期间就可以利用这一点。然而，sort 的情况更加复杂。

在 Spark 3.0 之前，如果每个存储桶恰好由一个文件组成，那么可以从连接计划中删除*排序*操作符。在这种情况下，Spark 确信在集群上读取数据后对数据进行了排序，实际上最终的计划是 *Sort-* free。然而，如果每个桶有更多的文件，Spark 不能保证数据是全局排序的，因此在计划中保留了 *Sort* 操作符——数据必须在连接执行期间排序。(参见下面的*从数据工程师的角度分桶*一节，了解如何实现每个桶一个文件。)

在 Spark 3.0 中，这种情况发生了变化，默认情况下，即使每个存储桶只有一个文件，也会出现*排序*。这种变化的原因是列出所有文件来检查每个存储桶是否只有一个文件太昂贵(如果有太多文件)，所以决定关闭这种检查，并在计划中一直使用*排序*(用于排序-合并连接)。如你所见，这是一种权衡，一种优化对另一种优化。还引入了一个新的配置设置*spark . SQL . legacy . bucket edtablescan . output ordering*，您可以将它设置为 *True* 以强制执行 3.0 之前的行为，并且仍然利用一个文件的排序桶。

## 无洗牌聚合

与联接类似，聚合也要求数据在集群上正确分布，通常 Spark 将不得不对数据进行洗牌，以便进行以下查询:

```
# this requires partial shuffle if tableA is not bucketed:
(
  tableA
  .groupBy('user_id')
  .agg(count('*'))
) # this requires full shuffle if tableA is not bucketed :
(
  tableA
  .withColumn('n', count('*').over(Window().partitionBy('user_id')))
)
```

然而，如果字段 *user_id* 对 *tableA* 进行分桶，那么两个查询都将是无洗牌的。

## 桶形修剪

Bucket pruning 是 Spark 2.4 中发布的一个特性，它的目的是减少 I/O，如果我们在表被分桶的字段上使用过滤器的话。让我们假设以下查询:

```
spark.table('tableA').filter(col('user_id') == 123)
```

如果表不是分桶的，Spark 将不得不扫描整个表来查找这个记录，如果表很大，它可能需要启动和执行许多任务。另一方面，如果表是分桶的，Spark 将立即知道这一行属于哪个桶(Spark 用模计算散列函数以直接看到桶号),并且将只从相应的桶中扫描文件。而 Spark 又是如何知道哪些文件属于哪个桶的呢？每个文件名都有一个特定的结构，不仅包含它所属的存储桶的信息，还包含哪个任务生成了该文件，如图所示:

![](img/05bc5345711a58cd52eded13fb713121.png)

作者图片

如果表非常大，桶形修剪可以大大加快速度。

# 桶装的缺点

我们刚刚描述了 bucketing 可以提供的优势。你可能想知道是否也有一些缺点，或者只是一些最好避免它的情况。实际上，分桶的一个结果是值得记住的，那就是执行过程中的并行化。如果一个表被分成 *n* 个桶，并且您将查询它，那么结果作业的第一阶段将正好有 *n* 个任务。另一方面，如果表没有分桶或者分桶被关闭，许多任务可能会非常不同，因为 Spark 会尝试将数据划分到分区中，每个分区大约有 128 MB(这由配置设置*Spark . SQL . files . maxpartitionbytes*控制)，因此任务具有合理的大小，不会遇到内存问题。

如果一个表被分桶，并且随着时间的推移它的大小增加，桶变大，那么关闭分桶以允许 Spark 创建更多的分区并避免数据溢出问题可能会更有效。这非常有用，尤其是当查询不执行任何可能直接利用 bucketing 提供的分布的操作时。

在 Spark 3.1.1 中，实现了一个新特性，它可以根据查询计划(没有连接或聚合)识别分桶没有用的情况，并将关闭分桶，因为它将丢弃分布，并以与未分桶相同的方式扫描数据。该功能默认开启，可由*spark . SQL . sources . bucket ing . autobucketedscan . enabled*配置设置控制。

# 从数据分析师的角度来看

数据分析师想要查询数据，而在理想情况下，他/她不想关心表如何存储在数据湖中的细节。嗯，我们并不是生活在一个理想的世界中，有时了解一些关于表的细节仍然是有用的，以便利用更快的执行和实现更好的性能。重要的是至少能够检查查询中是否利用了分桶，或者是否可以利用分桶，换句话说，是否有一种方法可以轻松地提高查询的性能。

## 桌子是桶装的吗？

要查看一个表是否被分桶以及如何分桶，我们只需通过调用 SQL 语句来检查关于该表的详细信息

```
spark.sql("DESCRIBE EXTENDED table_name").show(n=100)
```

![](img/c2ad57bf92e5e9a2150a231e9bf5c585.png)

作者图片

从这里，您可以看到该表是否分桶，哪些字段用于分桶，以及该表有多少个桶。注意，我们在这里调用了 *show(n=100)* ，因为默认情况下 *show* 函数只显示 20 行，但是如果表的模式很大，关于分桶的信息将不会出现在前 20 行中，所以请注意，根据表的不同，可能需要显示更多的行来查看分桶信息。

## 我的查询中是否利用了分桶？

首先，必须启用分桶，这是默认的，但是如果您不确定，可以按如下方式进行检查

```
spark.conf.get("spark.sql.sources.bucketing.enabled")
```

并且它应该返回*真值*。此配置设置可用于控制存储是打开还是关闭。

如果一个表被分桶，关于它的信息将保存在 metastore 中。如果我们希望 Spark 使用它，我们需要以表的形式访问数据(这将确保 Spark 从 metastore 获得信息):

```
# Spark will use the information about bucketing from metastore:
df = spark.table(table_name)# Spark will not use the information about bucketing:
df = spark.read.parquet(path_to_data)
```

请注意，在第二种情况下，我们直接从路径访问数据，Spark 将不会与 Hive metastore 通信，也不会获得有关分桶的信息—分桶将不会被使用。

最后但同样重要的是，我们可以检查查询计划，看看在计划中我们想要避免的地方是否有*交换*操作符。

## 我能帮火花吗？

通常，如果表存储在相同数量的存储桶中，存储桶将开箱即用。但在某些情况下，Spark 将无法利用分桶，我们实际上可以帮助它工作。为了有个概念，让我们来看看这些情况。

在 Spark 3.0 之前，如果分桶列在我们想要连接的两个表中具有不同的名称，并且我们将数据帧中的列重命名为具有相同的名称，则分桶将停止工作。例如， *tableA* 由 *user_id、*分桶， *tableB* 由 *userId* 分桶，列的含义相同(我们可以对其进行联接)，但名称不同(*user _ id*vs*userId*)。在以下查询中，将不会完全利用存储桶:

```
# The bucketing information is discarded because we rename the 
# bucketed column and we will get extra shuffle:
(
  tableA
  .withColumnRenamed('user_id', 'userId')
  .join(tableB, 'userId')
)
```

为了让它工作，我们需要保留原来的名字:

```
# Here bucketing will work:
(
  tableA
  .join(tableB, tableA['user_id'] == tableB['userId'])
)
```

Spark 3.0 修复了这个问题，因此重命名列不再是问题。

另一件需要注意的事情是连接列的数据类型——它们需要相同。让我们假设这个例子: *tableA* 被整数类型的 *user_id* 分桶， *tableB* 也被整数类型的 *user_id* 分桶，但是它是长类型的，并且两个表都被分桶到 50 个桶中。在这种情况下，每个表中连接列的数据类型都不同，因此 Spark 必须对其进行转换，丢弃存储桶信息，并且两个表都将被打乱:

```
# both tables will be shuffled if user_id has different data type 
# in both tables:tableA.join(tableB, user_id)
```

非常不幸的是，这两个表是用不同的数据类型为一个具有相同含义的列创建的。然而，我们可以帮助 Spark 实现至少一方的无洗牌连接，如下所示:

```
(
  tableA
  .withColumn('user_id', col('user_id').cast('long'))
  .repartition(50, 'user_id')
  .join(tableB, 'user_id')
)
```

如您所见，我们显式地将两个表中的数据类型转换为相同，然后将更改后的表重新分区为与另一个表相同数量的分区。洗牌将只发生在我们重新分配它的这一边，另一张桌子将不洗牌。这基本上相当于只有一个表被分桶，而另一个没有。

本节中的最后一个示例与在带有连接的查询中使用用户定义的函数(UDF)有关。我们需要记住，UDF 将丢弃关于分桶的信息，所以如果我们在连接之前调用 UDF，将导致相同的情况，就好像只有一个表被分桶。要么两个表都将被混洗，要么如果我们对表进行重新分区，或者如果我们将混洗分区的数量设置为存储桶的数量，我们将得到单向无混洗连接:

```
# Spark will shuffle both tables because of the UDF
(
  tableA.withColumn('x', my_udf('some_col'))
  .join(tableB, 'user_id')
)# One-side shuffle-free join:
(
  tableA.withColumn('x', my_udf('some_col'))
  .repartition(50, 'user_id') # assuming we have 50 buckets
  .join(tableB, 'user_id')
)# One-side shuffle-free join:
# set number of shuffle partitions to number of buckets (or less):spark.conf.set('spark.sql.shuffle.partitions', 50) 
(
  tableA.withColumn('x', my_udf('some_col'))
  .join(tableB, 'user_id')
)
```

如果我们想完全避免混乱，我们可以在加入后简单地调用 UDF

```
(
  tableA
  .join(tableB, 'user_id')
  .withColumn('x', my_udf('some_col'))
)
```

# 从数据工程师的角度来看

数据湖中的表通常是由数据工程师准备的。他们需要考虑如何使用数据，并准备好数据，以便为数据用户(通常是数据分析师和科学家)的典型用例服务。分桶是需要考虑的技术之一，类似于分区，分区是在文件系统中组织数据的另一种方式。现在让我们看看数据工程师通常必须面对的一些问题。

## 如何创建分桶表

我们已经看到上面使用函数 *bucketBy* 的查询。实际上的问题是控制创建文件的数量。我们需要记住，Spark 作业最后阶段的每个任务都将为它携带数据的每个存储桶创建一个文件。让我们假设这个例子，其中我们处理一个 20 GB 的数据集，我们在最后一个阶段将数据分布到 200 个任务中(每个任务处理大约 100 MB)，我们希望创建一个有 200 个存储桶的表。如果集群上的数据是随机分布的(这是一般情况)，这 200 个任务中的每一个都将携带这 200 个存储桶中的每一个的数据，因此每个任务将创建 200 个文件，导致 200 x 200 = 40 000 个文件，其中所有最终文件都将非常小。您可以看到，结果文件的数量是任务数量与请求的最终存储桶数量的乘积。

我们可以通过在群集上实现我们希望在文件系统(存储)中实现的相同分布来解决这个问题。如果每个任务只有一个存储桶的数据，在这种情况下，每个任务将只写一个文件。这可以通过写入前的自定义重新分区来实现

```
(
  df.repartition(expr("pmod(hash(user_id), 200)"))
  .write
  .mode(saving_mode)  # append/overwrite
  .bucketBy(200, 'user_id')
  .option("path", output_path)
  .saveAsTable(table_name)
)
```

这将为每个存储桶创建一个文件。如您所见，我们通过 Spark 使用的相同表达式对数据进行重新分区，以便在存储桶之间分配数据(有关如何工作的更多详细信息，请参见上面的相关部分)。实际上，您可以在这里使用更简单的 *df.repartition(200，' user_id')* 来获得相同的结果，但是上述方法的优点是，如果您希望同时按照如下所示的另一个字段对文件系统中的数据进行分区，它也可以工作

```
(
  df
  .repartition(200, "created_year",expr("pmod(hash(user_id), 200)"))
  .write
  .mode(saving_mode)
  .partitionBy("created_year")
  .bucketBy(200, "user_id")
  .option("path", output_path)
  .saveAsTable(table_name)
)
```

这里，每个文件系统分区将正好有 200 个文件(每个存储桶一个文件)，因此文件总数将是存储桶的数量乘以文件系统分区的数量。请注意，如果您只调用 *df.repartition(200，“created_year”，“user_id”)，这是行不通的。*

## 如何确定合理的桶数

这可能很棘手，取决于更多的情况。考虑最终存储桶的大小很重要——请记住，当您读回数据时，一个存储桶将由一个任务处理，如果存储桶的大小很大，任务将遇到内存问题，Spark 将不得不在执行期间将数据溢出到磁盘上，这将导致性能下降。根据您将对数据运行的查询，每个存储桶 150-200 MB 可能是一个合理的选择，如果您知道数据集的总大小，您可以据此计算要创建多少个存储桶。

实际上，情况更加复杂，人们必须面对以下挑战:

*   该表不断被追加，其大小随着时间的推移而增长，桶的大小也是如此。在某些情况下，如果数据集也按某个日期维度(例如年和月)进行分区，并且存储桶均匀地分布在这些分区上，这可能仍然没有问题。如果典型的查询总是只要求最近的数据，例如最近 6 个月，我们可以设计存储桶，使合理的大小对应于 6 个月的数据。存储桶的总大小会增长，但这没有关系，因为我们永远不会请求整个存储桶。
*   数据是不对称的，如果存储关键字的某个特定值的记录比该关键字的其他值多得多，就会出现这种情况。例如，如果表按 *user_id* 分桶，则可能有一个特定的用户有更多的交互/活动/购买或数据集表示的任何内容，这将导致数据倾斜——处理这个更大桶的任务将比其他任务花费更长的时间。

# 存储功能的演变

Spark 本身也在随着每个新版本不断发展和改进。此外，分桶功能在最近几个版本中也有所改进，所以让我们在这里提一下其中的一些改进:

## Spark 2.4 的改进

*   桶形修剪(参见[吉拉](https://issues.apache.org/jira/browse/SPARK-12850) )—在桶形字段上使用过滤器减少 I/O。

## Spark 3.0 的改进

*   丢弃关于排序的信息(参见[吉拉](https://issues.apache.org/jira/browse/SPARK-28595))——这并不是对分桶的真正改进，而是相反。更改后，排序-合并连接总是需要排序，不管存储桶是否已经排序。这样做是为了有一个更快的解释命令，该命令需要做文件列表来验证每个桶是否只有一个文件。有一个配置设置可以恢复原来的行为(*spark . SQL . legacy . bucketedtablescan . output ordering*，默认情况下它是 *False* ，所以如果您想在连接期间利用排序的存储桶，您需要将其设置为 *True* )。另外，请参见上面相关部分中关于排序的讨论。
*   尊重输出分区中的别名(参见[吉拉](https://issues.apache.org/jira/browse/SPARK-30298) ) —它确保排序-合并连接对于分桶表是无混乱的，即使我们重命名了分桶列。

## Spark 3.1 的改进

*   合并用于连接的分桶表(参见[吉拉](https://issues.apache.org/jira/browse/SPARK-31350) ) —如果两个表具有不同数量的桶，则启用无洗牌连接。请参见上面相关章节中关于该功能的讨论。
*   通过规则启用/禁用分桶(参见[吉拉](https://issues.apache.org/jira/browse/SPARK-32859) ) —如果不能在查询中利用，该规则将关闭分桶。

## 未来的改进

这里列出了一些在撰写本文时(2021 年 4 月)尚未实现的特性:

*   添加存储桶扫描信息进行解释(参见[吉拉](https://issues.apache.org/jira/browse/SPARK-32986) ) —如果在查询计划中使用存储桶，请查看该信息
*   读取多个排序桶文件(见[吉拉](https://issues.apache.org/jira/browse/SPARK-24528) ) —即使每个桶有更多文件，也要利用排序桶进行排序合并连接
*   配置单元分桶写支持(见[吉拉](https://issues.apache.org/jira/browse/SPARK-19256) ) —启用与配置单元分桶的兼容性(因此 Presto 也可以利用它)

# 与存储桶相关的配置设置

在整篇文章中，我们已经看到了其中的一些，但是让我们在这里列出它们，把它们放在一个地方:

*   spark . SQL . sources . bucket ing . enabled—控制分桶是否打开/关闭，默认为 *True* 。
*   spark . SQL . sources . bucket ing . max buckets-可用于表的最大存储桶数。默认情况下，它是 100 000。
*   spark . SQL . sources . bucketing . autobucketedscan . enabled-如果存储信息没有用，它会将其丢弃(基于查询计划)。默认情况下*为真*。
*   spark . SQL . bucketing . coalescebucketsinjoin . enabled-如果两个表的存储桶数量不同，它会将编号较大的表的存储桶与另一个表的存储桶合并在一起。只有当两个数字互为倍数时才有效。它还受到下一个配置设置的约束。默认情况下，*为假*。
*   spark . SQL . bucket ing . coalescebucketsinjoin . maxbuckertratio-两个存储桶编号进行合并工作的最大比率。默认情况下，它是 4。换句话说，如果一个表的存储桶数量是另一个表的 4 倍以上，合并将不会发生。
*   Spark . SQL . legacy . bucketedtablescan . output ordering—使用 Spark 3.0 之前的行为来利用分桶中的排序信息(如果每个桶有一个文件，这可能会很有用)。默认情况下，*为假*。
*   spark.sql.shuffle.partitions —控制随机分区的数量，默认情况下为 200。

# 最终讨论

在本报告中，我们从不同的角度描述了分桶操作。我们已经看到了数据工程师在创建分桶表时需要处理的一些问题，比如选择合理数量的桶和控制创建的文件的数量。我们还讨论了 data analyst 视图—分桶表提供了优化机会。在许多情况下，这些机会被 Spark out of the box 所利用，但是在某些情况下，需要特别注意利用挖掘潜力。这种情况发生在存储桶细节不同的表的连接中，例如，表具有不同数量的存储桶，存储桶列具有不同的名称或数据类型，这里我们已经看到，通过使用数据帧的显式重新分区或改变混洗分区的数量以满足存储桶的数量的简单技巧，至少可以实现单侧无混洗连接。