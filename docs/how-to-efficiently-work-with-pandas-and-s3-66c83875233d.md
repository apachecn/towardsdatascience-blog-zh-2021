# 如何有效地与熊猫和 S3 一起工作

> 原文：<https://towardsdatascience.com/how-to-efficiently-work-with-pandas-and-s3-66c83875233d?source=collection_archive---------18----------------------->

## 关于如何使用 python 和 S3 进行内存操作以及如何测试这些代码的教程。

![](img/59c01956f87254851a3751b7f50486ef.png)

埃里克·麦克林在 [Unsplash](https://unsplash.com/s/photos/cloud-pandas?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

对于我们这些数据科学家来说，至少有两件重要的事情；**数据**和**科学**。太惊喜了:)。从这两个方面来看，科学无疑是更令人兴奋也不那么混乱的部分。然而，没有数据，科学只是一个干巴巴的理论，没有把它变成现实的激情。那太无聊了。

![](img/1fbec96d156d75ffb353043f95899af6.png)

照片由 [Cris Saur](https://unsplash.com/@crisaur?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

当存储或加载数据时，我们应该考虑性能。没有人愿意等很久，直到数据可供处理。当使用云存储时，我们可以通过直接从-写入数据或者将数据加载到内存而不是使用中间文件来提高性能。对于运行在 AWS Fargate 或 Lambda 上的应用程序，这甚至可能是一个强烈的需求，因为本地磁盘存储很低或者根本不可用。

最后，由于我们不仅是伟大的数据科学家，也是出色的开发人员，我们希望测试我们的应用程序代码。当您的代码访问 S3 时，您不希望在测试中访问真正的 S3 桶。您更喜欢将数据保存在本地，甚至在内存中生成数据。否则，您的测试会变得很慢，并且依赖于网络连接。这当然是我们应该避免的。

那么我们应该做什么来运行测试访问 S3 的代码呢？

> **模拟**对 S3 的读写连接

在这篇文章中，我将向你展示如何在内存中从/向 S3 读写熊猫数据帧。为了测试这些函数，我还展示了如何使用库 [moto](http://docs.getmoto.org/en/latest/#) 模拟 S3 连接。作为一个好孩子，我指导你如何让你的测试变得枯燥，写起来更有趣。

说够了。我们开始吧！

# 熊猫数据框和 S3

在下面，我们想开发两个功能；一个是 ***写*** 一个熊猫数据帧给一个***【S3】***桶，另一个是 ***从那里读*** 数据回来。为了确保这些函数做它们应该做的事情，我们还编写了一些测试。

在深入研究之前，我们首先需要设置一些基础知识。

## 基础知识

当使用 Python 处理 AWS 服务时，有三个库是你必须知道的。

1.  [**boto core**](https://botocore.amazonaws.com/)**:**boto core 是越来越多的 AWS 服务的底层接口。从描述中你已经得到了最重要的部分；是*低级*。由于是低级的，用起来比较繁琐。幸运的是，围绕 botocore 有一个更高层次的抽象。
2.  [**boto**](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html)**3:**boto 3 是配合各种 AWS 服务工作的 Python SDK。它是围绕 botocore 构建的，但提供了更高级、更方便的 API。它是您应该在代码中用来创建、配置和管理 AWS 服务的库。
3.  [**Moto**](http://docs.getmoto.org/en/latest/#)**:**Moto 模拟出各种 AWS 服务的连接。这对于测试与 AWS 基础设施对话的应用程序代码是必要的。在您的测试中，您不应该访问真实的基础设施，因为这会使您的测试变慢，并且依赖于连接性。

如果要运行下面的例子，需要安装 boto3 和 moto。你不必明确地安装 botocore，因为它是 boto3 自带的。我使用 [pytest](https://docs.pytest.org/) 作为测试框架。最后，你需要熊猫，因为我们正在处理数据帧。

一如既往，我推荐使用[poems](https://python-poetry.org/)来管理您的 Python 项目和依赖项。如果你对此感兴趣，你可能想看看这篇文章。当然，你也可以使用普通的 pip 来安装所有的东西，最好是在虚拟环境中。

一切就绪。让我们继续前进！

## 将数据帧读写到内存中

在开始测试之前，我们需要测试一些东西。正如简介中所承诺的，我们希望从/向 S3 读取/写入数据都完全在内存中完成。让我们从给 S3 写信开始，直接进入代码。

所以这很简单。首先，您需要序列化您的数据帧。对于序列化，我使用 parquet，因为它是一种高效的文件格式，并且开箱即用。但是，您也可以使用 CSV、JSONL 或 feather。接下来，我写入一个类似文件的对象，而不是写入或序列化到磁盘上的文件中。该对象保存在内存中。为此，我使用了 python 标准库中的[字节序](https://docs.python.org/3/library/io.html)。最后，我创建了一个 boto3 S3 客户端，并使用方法`upload_fileobj`来运行上传。

数据帧在云中！

我们怎么把数据帧拿回来？同样，让我们从看一下代码开始。

我们在这里所做的只是颠倒我们之前所做的。我们从使用 boto3 创建 S3 客户端开始。接下来，我们使用`get_object`下载对象，并将其放入一个类似文件的对象中。最后，我们使用 pandas 和 parquet 反序列化对象。我们的数据框架回来了！

![](img/2f2b2c13f05a9c168ee683d6928bbb7f.png)

杰弗里·F·林在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

现在，这些代码真的有用吗？你可以盲目地信任我，但我不会这么建议。因此，让我们添加一些测试，我们甚至可以运行没有 S3 帐户，甚至没有互联网连接。

## 测试在没有 S3 的情况下与 S3 对话的代码

为了测试我们的 S3 IO 代码，我们需要一种方法来欺骗 boto3，使其不真正与 S3 对话，而是与它的内存版本对话。这就是 moto 为我们做的。重要的是，它不仅模拟了连接，而且几乎完全复制了内存中的 S3 服务。有了它，我们就可以创建存储桶，把文件放在那里，然后读回来。听起来不错，不是吗？真正好的一点是，我们不需要做太多就能得到它。让我们深入到测试这两个函数的基本测试代码中。

最重要的部分是`mock_s3`装饰。当您将它添加到您的测试函数中时，所有的 boto3 交互都将与内存中的 S3 版本对话。顺便提一下，如果您想模仿其他 AWS 服务，您只需添加 moto 提供的相应装饰器，您的测试就可以开始了。

我们要做的下一件事是创建一个我们想要定位的桶。从代码中可以看出，我们只是使用了 boto3，就像创建一个真正的 S3 桶一样。

最后，我们调用我们想要测试的函数，并做一些断言。为了给 S3 写信，我们检查是否能在桶中找到文件。我们再次使用普通的 boto3。对于读取，我们检查我们得到的数据帧是否与我们上传的数据帧相同。

就是这样。看起来我们的内存读/写操作像承诺的那样工作。

快乐你好 GIF 摘自 [Giphy](https://giphy.com/gifs/happy-good-job-RgfGmnVvt8Pfy)

我不喜欢测试代码的地方是它显示了相当多的重复。例如，创建存储桶总是相同的操作。此外，对于编写测试的人来说，用测试数据填充桶的代码看起来可以简化。

因为我们不仅是伟大的数据科学家，也是出色的软件开发人员，所以让我们努力让代码[干燥](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)并可重用。

## 让测试代码变干

如前一节所述，我们*不想在我们编写的每个测试中重复桶创建*代码。这只会让测试变得不必要的冗长，而且需要输入的内容太多。可选地，我希望有可能*容易地上传一组数据帧*到测试桶。为了简单起见，我将这里的上传限制为数据帧，但是代码可以进一步扩展以更加通用。

让我们从利用一些高级 python 概念来实现我们目标的代码开始。但别担心，我们之后会解剖它。

我在这里添加的是一个类固醇上的 mock_s3 装饰器。我已经将装饰器编写为一个可调用的类，在这里我可以使用神奇的方法`__call__`来实现神奇的效果:-)。

使用可调用类，您可以使用括号调用类的创建实例*，并可能传递参数。用代码解释你可以做`x = SomeCallableClass(); y = x(1, 2)`。这里要执行的是在`__call__`方法中定义的。*

为什么我们需要一个可调用的？我们可以用它来创建一个基于类的装饰器。这允许我们*参数化我们的装饰器*并*保持状态*。后者使我们能够在稍后的测试中使用可调用的实例，例如获取创建的 bucket 的名称。

简单地说，`__call__`方法包含实际的装饰逻辑。我想我们实际上可以说，是装修工。在那里，内部函数使用`mock_s3`装饰器来模拟 S3 连接。这里有这么多装修工人。新的和枯燥的部分是，在执行测试函数之前，我们创建了 bucket，并可选地向它上传一些数据帧。现在，实际的测试函数运行了，带有一个模拟的 S3 连接、一个新模拟的桶和一些数据。任务完成！

最后，让我们看看如何在测试中使用 pimped mocker。

重要的一点是，您首先必须创建的实例，然后使用该实例来修饰您的测试函数。这样，您就可以在测试中访问桶名，而不必使用更多的常量。总的来说，测试代码看起来更干净，更专注于需要测试的东西。

顺便说一下，您看到我已经从[功能工具](https://docs.python.org/3/library/functools.html)内置模块中添加了另一个装饰器`wraps`。这实际上非常重要。没有这一点，失败的断言不会直接指向失败的函数，而是指向装饰器本身。当然没有帮助。此外，如果您在实际的测试函数中使用 pytest fights，那么只有当包装装潢师就位时，它们才能与装潢师一起工作。

# 包裹

最后，我简要总结了本文的主要观点

1.  当处理存储在 AWS S3 中的数据时，请尝试直接在内存中执行所有 IO 操作，而不要遍历中间文件。如果你还没有这样做，我向你展示了如何使用熊猫数据帧的代码。
2.  测试您的代码，并使用 moto 测试与 AWS 服务交互的功能。它很容易使用，可以帮助您学习如何使用 boto3。
3.  保持代码干燥！*也是您的测试代码*。它让写作测试更有趣。作为一个 Kickstarter，我给你看了一个干的和丘疹版本的摩托模拟 AWS S3。

谢谢你关注这篇文章。和往常一样，如果有问题、评论或建议，请随时与我联系。期待您的回音！