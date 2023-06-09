# 神经网络的调试提示

> 原文：<https://towardsdatascience.com/debugging-tips-for-neural-networks-f7dc699d6845?source=collection_archive---------38----------------------->

## 调试神经网络可能会非常令人沮丧。这里有一些可能有帮助的一般提示。

![](img/29b90188e3902c2fd29aebbb2a9bbe05.png)

照片由[西格蒙德](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄

通常，基于神经网络的项目中的瓶颈不是网络实现。相反，在您编写了所有代码并尝试了一大堆超参数配置之后，有时网络就是不工作。我以前去过那里。在与挑剔的网络打交道一段时间后，我收集了一些帮助我调试它们的方法。这些方法不是任何形式的保证——即使你做了我建议的所有事情，你的网络仍有可能中断。然而，我希望，从长远来看，这些提示会减少你调试神经网络所花的时间。

# **检查梯度问题:**

有时梯度是问题的原因。有几种有用的与渐变相关的调试方法:

*   **数值计算每个重量的梯度。**这通常被称为“梯度检查”,有助于确保梯度计算正确。一种方法是使用有限差分。更多细节可以在[这里](http://deeplearning.stanford.edu/tutorial/supervised/DebuggingGradientChecking/)找到。
*   **对于每个重量，将梯度的大小与重量的大小进行比较。我们想确保数量的比例是合理的。如果梯度幅度比权重幅度小得多，网络将永远需要训练。如果梯度幅度大约等于或大于权重幅度，则网络将非常不稳定，并且可能根本不训练。**
*   **检查爆炸或消失的渐变。**如果您看到梯度变为 0 或 nan/infinity，您可以确定网络不会正确训练。你需要首先弄清楚为什么爆炸/消失梯度会发生，例如，可能是因为步长太大。一旦你弄清楚为什么梯度爆炸/消失，有各种解决方案来解决这个问题，例如，添加剩余连接以更好地传播梯度或简单地使用较小的网络。
*   **激活功能也可导致爆炸/消失梯度。**例如，如果 sigmoid 激活函数的输入幅度过大，梯度将非常接近 0。随着时间的推移，检查激活函数的输入，并确保这些输入不会导致梯度始终为 0 或较大的幅度。

# **经常检查训练进度:**

经常检查你网络的训练进度会节省你的时间。例如，假设您正在训练一个网络来玩贪吃蛇游戏。不是一次训练网络几天，然后检查网络是否学到了什么，而是每十分钟用当前学到的权重运行一次游戏。几个小时后，如果你注意到代理每次都在做同样的事情，却没有得到任何回报，你就知道可能出了问题，并为自己节省了几天浪费的培训时间。

# **不要依赖定量输出:**

如果只查看定量输出，您可能会错过有用的调试信息。例如，当训练网络进行语音翻译时，请确保您阅读了翻译的语音，以确保它实际上是有意义的。不要只看评价函数是不是在递减。作为另一个例子，当训练用于图像识别的网络时，确保您手动检查网络给出的标签。你不应该依赖定量产出的原因有两个。首先，你的评估函数可能有错误。如果你只看错误的评估函数输出的数字，可能要过几周你才会意识到有问题。第二，你可能会在你的神经网络输出中发现无法定量显示的错误模式。例如，你可能意识到一个特定的单词总是被误译，或者在左上角的象限中图像识别网络总是错误的。这些观察反过来可以帮助您在代码的数据处理部分找到 bug，否则这些 bug 会被忽略。

# **试一个小数据集:**

另一种确定您的代码是否有 bug 或者数据是否难以训练的方法是首先适应一个较小的数据集。例如，不要在数据集中有 100，000 个训练示例，而是将数据集调整为只有 100 个甚至 1 个训练示例。在这些情况下，您期望神经网络能够非常好地拟合数据，尤其是在一个训练示例的情况下。如果您的网络仍然有很高的测试错误，那么您几乎可以肯定您的网络代码有问题。

# 尝试一个不太复杂的网络:

如果您的全尺寸网络在训练时遇到问题，请尝试层数较少的小型网络。这还有一个好处就是训练速度更快。如果小型网络在全尺寸网络失败的情况下成功，则表明全尺寸模型的网络架构过于复杂。如果简单网络和完整网络都失败了，那么您的代码中可能有一个 bug。

# **如果您没有使用框架，请对照框架进行检查:**

如果你是从零开始编写神经网络的代码，而不是使用机器学习框架，那么你的实现可能有问题。幸运的是，您可以通过在机器学习框架中编写相同的网络架构来检查是否是这种情况。然后将打印语句放入您的实现和框架版本中，并比较输出，直到您发现打印语句中的差异开始出现。这就是你的错误所在。例如，假设您有一个十层网络，错误在第七层。当您打印网络中第一层的输出并将其与框架实现中的第一层输出进行比较时，它们将是相同的。因此，您转而比较第二层的输出。还是老样子。然后你移动到第三层，以此类推，直到你看到第七层开始出现差异。因此你可以推断第七层是问题所在。请注意，此方法仅适用于网络的第一次迭代，因为由于第一次迭代输出的差异，第二次迭代及以后的迭代将具有不同的起点。

上面的例子假设错误发生在正向学习过程中。如果错误发生在反向传播期间，可以使用相同的思想。您可以从最后一层开始，逐层打印权重的渐变，直到您看到框架渐变和实现渐变之间的差异。