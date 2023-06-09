# R 的 expand.grid()函数的本质

> 原文：<https://towardsdatascience.com/the-essence-of-rs-expand-grid-function-a-love-letter-to-a-function-that-say-it-all-3f0ebba649c?source=collection_archive---------13----------------------->

## *写给一个函数的情书，它说明了一切*

![](img/a73a1b2e0c23542d1380d184c54a98b2.png)

照片由[詹姆斯·哈里逊](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

当审查某人的代码时，有什么迹象告诉你这是一段好代码吗？它可以是代码结构、风格、注释文档、[制表符或空格](https://www.youtube.com/watch?v=SsoOG6ZeyUI)，或者任何让你说“这一切都有意义”的东西

对我来说，要给人留下这样的印象，所需要做的就是使用 expand.grid()函数开始编写代码！

# expand.grid()函数是什么？

它是 R 的基础系统中的一个功能，意味着当你第一次安装 R 时它就已经存在了，甚至不需要安装任何额外的包。

根据[函数的文档](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/expand.grid)，它“从因子变量的所有组合中创建一个数据框”。

这里有一个例子:

```
expand.grid(height = seq(1, 10, 3), 
               sex = c("Male","Female"))
#>     height    sex
#> 1      1      Male
#> 2      4      Male
#> 3      7      Male
#> 4     10      Male
#> 5      1     Female
#> 6      4     Female
#> 7      7     Female
#> 8     10     Female
```

还有一个最近的版本，它被改编成了一个 [tidyr::expand_grid()](https://tidyr.tidyverse.org/reference/expand_grid.html) 版本，该版本处理了一些烦人的副作用，并且还允许扩展 data.frames. *(不要将:base::expand.grid 与"."混淆)，vs tidyr::expand_grid()带“_”.*

# 幕后发生了什么？

基本版本:

```
> expand.grid
function (..., KEEP.OUT.ATTRS = TRUE, stringsAsFactors = TRUE) 
{
    nargs <- length(args <- list(...))
    if (!nargs) 
        return(as.data.frame(list()))
    if (nargs == 1L && is.list(a1 <- args[[1L]])) 
        nargs <- length(args <- a1)
    if (nargs == 0L) 
        return(as.data.frame(list()))
    cargs <- vector("list", nargs)
    iArgs <- seq_len(nargs)
    nmc <- paste0("Var", iArgs)
    nm <- names(args)
    if (is.null(nm)) 
        nm <- nmc
    else if (any(ng0 <- nzchar(nm))) 
        nmc[ng0] <- nm[ng0]
    names(cargs) <- nmc
    rep.fac <- 1L
    d <- lengths(args)
    if (KEEP.OUT.ATTRS) {
        dn <- vector("list", nargs)
        names(dn) <- nmc
    }
    orep <- prod(d)
    if (orep == 0L) {
        for (i in iArgs) cargs[[i]] <- args[[i]][FALSE]
    }
    else {
        for (i in iArgs) {
            x <- args[[i]]
            if (KEEP.OUT.ATTRS) 
                dn[[i]] <- paste0(nmc[i], "=", if (is.numeric(x)) 
                  format(x)
                else x)
            nx <- length(x)
            orep <- orep/nx
            x <- x[rep.int(rep.int(seq_len(nx), rep.int(rep.fac, 
                nx)), orep)]
            if (stringsAsFactors && is.character(x) && !is.factor(x)) 
                x <- factor(x, levels = unique(x))
            cargs[[i]] <- x
            rep.fac <- rep.fac * nx
        }
    }
    if (KEEP.OUT.ATTRS) 
        attr(cargs, "out.attrs") <- list(dim = d, dimnames = dn)
    rn <- .set_row_names(as.integer(prod(d)))
    structure(cargs, class = "data.frame", row.names = rn)
}
<bytecode: 0x000001dee40a0128>
<environment: namespace:base>
```

tidyr 版本:

```
> expand_grid
function (..., .name_repair = "check_unique") 
{
    dots <- dots_cols(...)
    ns <- map_int(dots, vec_size)
    n <- prod(ns)
    if (n == 0) {
        out <- map(dots, vec_slice, integer())
    }
    else {
        times <- n/cumprod(ns)
        out <- map2(dots, times, vec_rep_each)
        times <- n/times/ns
        out <- map2(out, times, vec_rep)
    }
    out <- as_tibble(out, .name_repair = .name_repair)
    flatten_nested(out, attr(dots, "named"), .name_repair)
}
<bytecode: 0x000001deeb1c15c8>
<environment: namespace:tidyr>
```

# 这有什么大不了的？

人们可以简单地认为这只是两个嵌套的循环。这里真的需要一个指定的函数吗？我的回答:要看用途！如果您在日常编码中不止一次地使用它，那么当然可以。为什么不呢？

在接下来的段落中，我将试图论证为什么它不仅仅是嵌套循环，以及为什么它与统计编程原则和需求产生共鸣。

# 为什么重要？

作为一名统计学家，这两个关键术语在我的日常工作中至关重要:

> 假设和实验设计

对我来说，这些是**什么**和**如何。** **我们回答的解析题是什么**？我们要测量/收集什么 T21？我们要怎么做呢？

下面是**如何…** 我们将在多个组中比较一个指标:病例/对照组，治疗 A 与治疗 B 与治疗 C，等等。通过定义这些组，我们考虑了以下几点:这些组有什么共同点？它们有什么不同？我们期望测量哪种类型的效果？说明了什么？什么是随机的，什么是固定的？最后，我们如何提出一个比偶然更有可能成立的论点？

当我们引入更复杂的实验设计，让我们有一个更好的答案，同时解决可能的混淆，最小化偏差，并在理想情况下，暗示合理的因果关系时，乐趣就开始了。

# 回到编码…

要为回答一个假设(或商业问题)做出令人信服的论证，你需要列出他们收集的证据，以及考虑的可能解释的范围。类似地，在数据科学和统计编程的背景下，代码应该尽可能早地反映我们测量什么，以及跨哪些组。expand.grid()允许我们列出问题的范围(使用的因子水平及其组合)，然后遍历我们的实验/分析中考虑的不同组合。理想情况下，该表应包含可能组合的广泛可行范围，涵盖可能与该措施相关的所有内容。即使太细也不用担心。我们总是可以根据需要向下钻取并消除(折叠、聚集)更多的粒度级别。

# 表格格式的 Tidyverse 和嵌套对象

对于像我这样的统计学家来说，“整洁”的概念完全有意义。简单说:行是观察值，列是变量(字段/协变量)。

我喜欢 [tidyverse](https://www.tidyverse.org/) 的地方在于，表格中的单元格不一定只有数字字符。相反，它可以是(整个)对象。例如:嵌套表，任何类/对象，列表，列表列表，列表列表列表，…好了，你明白了。

因此，剩下要做的就是从该对象中提取所需的信息，将其填充到所需的实验单元/级别，根据需要进行汇总/总结，并得出结论。用 Tidyverse 的术语来说，这就是[巢/不巢](https://tidyr.tidyverse.org/reference/nest.html)。一开始肯定会让人不知所措，但是一旦你习惯了，它(可能)实际上是有意义的。

# 没有循环了！真的！

所以我们列出了实验因素，并把细胞内的数据打包。那么应该如何遍历所有可能的组合呢？嗯，就像以前的 excel 一样，对第一行(或任何其他感兴趣的因素级别组合)进行操作，然后将其拖到其他行上。使用一些“整洁”的技巧，您可以定义(变异)按行工作的新列，而不是使用嵌套的 for 循环和索引。这里至少有两种方法可以做到:1。**DP lyr**::[row wise()](https://www.tidyverse.org/blog/2020/04/dplyr-1-0-0-rowwise/)2。 [**purrr** ::map_()](https://purrr.tidyverse.org/index.html) 家庭功能。

不服气？再看一下前面出现的 **tidyr** ::expand_grid()的代码。用 map()不是看起来优雅多了吗？

# 当范围增加时…

好吧，我知道，生活是会发生的，有时我们不得不在实验中引入额外的因素，然后呢？嗯，有了这个框架，添加另一个因素回到我们最初的 expand.grid()父函数不应该[违反范围](/how-to-choose-the-software-package-with-the-widest-scope-a8851f29d8b7)，即不应该破坏我们已经创建的一切！原始数据现在被拆分成更多的子组，但是我们变化后的新列保持不变！

# 弊端？

好吧，我对这篇文章有偏见，毕竟这是一封情书，所以请让我知道你不喜欢这种方式的什么。也许是可扩展性？我不知道。

# expand.grid()用其他语言怎么说？

每种语言都有自己的文化、方言、社区和用例。您是否找到了一个与上面类似的很好的实现？或许 R 还有向别人学习的提升空间？

# 真诚地…

现在你知道了如何打动我的秘密，你所要做的就是给我看一些以 grid.expand()开头的代码