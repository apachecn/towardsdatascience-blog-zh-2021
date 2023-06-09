# 5 个我最喜欢的 sci kit-用于增强数据分析的学习工具

> 原文：<https://towardsdatascience.com/5-of-my-favorite-scikit-learn-tools-for-enhanced-data-analysis-694a1f1c69ba?source=collection_archive---------58----------------------->

## 使用 SkLearn 中的一些分析方法来更好地理解你的数据

![](img/6ea45690a6c324691858593c0296b020.png)

(图片由作者提供)

# 介绍

如果您长期从事 Python 中的数据科学工作，您可能会对 Scikit-Learn 或 SkLearn 模块很熟悉。该模块提供了一系列有用的模块，这些模块被设置用于衡量某些问题，并且实际上非常常用于解决遵循分类或连续准则的问题。

也就是说，虽然这可能是 SkLearn 模块的主要吸引力，但也有许多非常酷的扩展类和功能。这些不仅很棒，而且为 Python 中的机器学习建立了一整套语法体系，现在几乎所有其他建模包都在遵循这一体系。如果你想了解这方面的更多信息，我写了一篇关于 SkLearn 如何用标准化的函数和类改变 Python 中机器学习模型的适当编程的许多方面的文章，请查看:

</how-scikit-learn-changed-machine-learning-forever-90c1eebe3484>  

我认为这个包对整个行业的影响是令人印象深刻的，而且非常酷！不用说，这个包在将 Python 和机器学习带到这个领域的前沿方面做了很多工作。然而，我们很容易沉迷于其中的一些工具，而忽略许多其他非常棒的工具，只喜欢少数几个，因为这个模块非常全面，实际上相当大。

这肯定是真的，其中一个方法就是分析。SkLearn 有各种不同的方法来处理和试验经常被忽略的数据，如果模块是一个依赖项，这些方法已经可用了——所以只要有可能，它们当然值得使用。此外，许多这些技术对于数据科学和数据分析的某些方面来说是真正非常有价值的资产。

SkLearn 中不仅有专门为分析构建的工具，还有可以与无监督学习模型一起使用的分析方法，这些方法通常可以教授许多有关您可能正在处理的数据的信息。记住这一点，这里是我最喜欢的 10 个工具，我从 SkLearn 中最常用来进行数据和模型分析！

## №1:线性判别分析

SkLearn 有一个我非常喜欢但并不突出的特性，那就是线性判别分析的能力。这些话听起来比实际意思可怕得多。线性当然意味着直线，我希望任何数据科学家都能自然地理解这一部分。数学中的判别式是一个基于多项式系数的非任意值。这些系数当然可以用多种方法计算，所有这些方法都会显著影响结果。

记住这个新的措辞，我们现在可以考虑这个模型实际上会对我们的数据做什么。我们将对系数进行线性比较，以便分析某组多项式连续数据。在处理连续特征但目标明确的情况下，该模型也是一个很好的选择。当然，这是模型；不是一个分析工具，但是该模型也有能力将多项式组转换成系数。任何时候涉及到系数，它们都可以被可视化。这是因为系数只是一些非任意的单位，是要乘以一个多项式。

也就是说，SkLearn 实现相当深入，将允许使用几个不同的参数，这些参数可以完全改变分类器和多项式转换器的有效性。我想关注的第一个论点是解算器论点。此参数可用于更改计算系数所依据的线性模型。这样做的好处是，一些数值应用可能需要不同的方法来拟合这条线。可用的值及其匹配描述如下:

*   奇异值分解；SVD 是奇异值分解的缩写。虽然这是转换器的默认设置，但我想说，在许多情况下，真正的默认设置应该是线性最小二乘法，因为它通常最适合应用于大多数情况下的连续问题。也就是说，使用 lsqr 求解器的一个特殊困难和缺点是，它已经是一个处理高维数据的模型。奇异值分解也不会计算协方差矩阵，因此建议将此求解器用于包含大量要素的数据。
*   lsqr 线性最小二乘法对于这个模型的大多数用例来说都是一个很好的应用，我想说我认为这真的应该是这个模型求解器的默认选项。为什么？因为这个模型是简单的，数学的，并且当它不使用成本时通常用典型的斜率公式计算。也就是说，成本仍然用于确定斜率值和 y 截距，因此该模型是我们都熟悉的典型线性模型之一。
*   eigen 提供本征解算器将为我们提供本征分解——这基本上只是一个花哨的术语，表示我们将把向量转换成本征向量，将值转换成本征值。这是什么意思？在不深入研究的情况下，特征分解将通过重构来分解我们的数据，直到它成为规范形式。这在计算机科学中很常见，基本上就是说，我们把一个向量减少到它在数学中可以表示的最小可能的公式。虽然我认为这些都是有趣的概念，但关于这个模型和其他模型还有很多要讨论的，所以我现在将放下数学，但如果你想了解更多关于规范形式的知识，我写了一篇文章，你可能会感兴趣！：

另一个我认为对调整这个模型/变压器至关重要的参数是收缩参数。如果您正在处理大量稀疏数据，并且似乎找不到合适的数据，则此参数肯定很有用。也就是说，这些只能与协方差矩阵一起使用，因此 SVD 求解器在处理参数时是不可用的。该参数可以采用三种不同的选项:

*   none:No shrink，这也是缺省值，很大程度上意味着要使用 SVD 求解器，尽管我不会说在处理一些紧密的低方差连续数据时不使用 shrink 是完全不可能的。
*   在 0 和 1 之间浮动:这将给你一个固定的收缩参数。这样做的好处是收缩是手动的，程序员可以很容易地控制。然而，话虽如此，不允许统计学发挥作用也有一些不利之处——尤其是在多变量分析方面。
*   ' auto ':使用 Ledoit-Wolf 引理的自动收缩。这个收缩估计器真的很酷，所以我坚持认为，如果你想了解更多，你可以查看这个完全集成的 PDF(非常酷的媒介),它是最初由 Oliver Ledoit 和 Michael Wolf 发表的论文:

## №2:主成分分析

不经过主成分分析(PCA)就很难谈论分析建模方法。PCA 是另一种形式的分解。主成分分析和其他类似的分解方法的最大区别是主成分分析只使用奇异值分解方法。

该模型的输入数据也是集中的，但是在应用 SVD 分解方法之前，不对每个特征进行缩放。很可能大多数数据科学家都熟悉这个模型，因为它是分析行业的一个主要部分。这是因为降低数据的维度确实有助于更好地理解数据，以及特征之间的差异和它们各自的方差水平。我认为对于这种无监督学习方法来说，唯一至关重要的参数是 svd_solver 参数。该参数为算法提供了一个基础，使用了 SkLearn 中已经提供的一整套奇异值分解方法。

## №3:排列重要性

虽然置换重要性可能不是 SkLearn 库中的一个众所周知的工具，但我确实认为它们是解决复杂分类问题的一个绝对重要的工具。通常，每当讨论排列重要性时，我们都在谈论基尼系数不纯。吉尼杂质只是随机森林分类器使用的排列测量的一个花哨名称。

此模型中要素的重要性可以告诉您许多关于您正在处理的数据和要素的信息。它不仅可以给出删除一些不重要特性的可靠提示，而且还可以从您的模型中提供重要的反馈，说明是什么使它变得更准确或更不准确！不用说，这肯定是我们大多数人想要了解和利用的来自 SkLearn 的东西。

您可以通过从 Scikit-learn 的检查模块导入此方法来使用排列重要性:

```
**from** **sklearn.inspection** **import** permutation_importance
r = permutation_importance(model, x_val, y_val)
```

## №4:随机投影

一个非常酷的概念是随机投影，我们可以把它作为一个整体来看待，我认为这个概念被低估了，并且已经完全应用到 SkLearn 中。随机投影是一种计算非常简单的技术，用于计算分解和降低数据的维数。

这种分解方法是不同的，因为它以更高的精度换取更好的性能。如果您的数据中有很多需要缩减的内容，这将非常有用。然而，我认为随机投影不如 SVD 使用得好的部分原因是因为 SVD 实际上是一种非常高效和可伸缩的分解方法。然而，我确实看到了许多应用，其中一些非常高维的数据，可能具有许多非常重要的特征，可以真正利用这样的分解方法。

## №5:功能集聚

你听说过数据争论，但你听说过数据聚集吗？好消息是，我刚才提供的上下文线索应该已经给了你一个凝聚这个词的确切定义。我必须承认，在我的一生中，我从来没有听到这个词被大声地说出来，我仍然不确定如何发音，但它肯定可以毫无问题地被书写和阅读——所以

> 不要大声读出来。

这也是你大声朗读的一个非常奇怪的选择。无论如何，使用我们刚刚学到的这个奇怪词汇的定义，如果不是数学，我们不会接触到它，我们可以假设这意味着功能的集合-这将是一个正确的假设！这一过程与凝聚聚类非常相似，但它合并的是特征而不是样本。当然，这只是 SkLearn 提供的庞大武器库中做降维的又一个选择。然而，当涉及到数据科学时，学习如何利用 SkLearn 中提供的大量工具肯定会非常有用。

# 结论

作为一名数据科学家，这篇文章包含了很多我觉得非常令人兴奋的东西。这当然不仅适用于排列和系数，甚至更进一步；我也很喜欢分解这个话题。我认为很多在幕后工作的非常酷的线性代数，实际上在数学上相对简单，是非常了不起的——很难想象如果没有这些算法，我们会在哪里。

特别是 SVD 可能是现实世界机器学习中最好的数学概念之一。这是因为实际上经常需要对真实数据进行分解。在现实世界中，特性并不总是默认的特性，所以利用这篇关于分解的文章中提出的概念将会非常有用——我认为这些工具既没有被充分利用，又非常有用。