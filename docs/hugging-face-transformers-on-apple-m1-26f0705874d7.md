# 在苹果 M1 上安装拥抱脸变形金刚

> 原文：<https://towardsdatascience.com/hugging-face-transformers-on-apple-m1-26f0705874d7?source=collection_archive---------4----------------------->

## 以及 Tensorflow 和 Tokenizers 包

![](img/1b02cbd596b2e5f3986b7958c4ba7c49.png)

由[大卫·拉托雷·罗梅罗](https://unsplash.com/@latorware?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

不是所有的事情都来得容易。向苹果 M1 公司的过渡也有类似的故事要讲。尽管我喜欢这种速度，但我讨厌不得不寻找非传统的方法来安装传统的库，否则在命令提示符下只有一行代码。

如果你是苹果 M1 用户，并与 NLP 密切合作，有可能你以前遇到过这种情况，甚至找到了解决方案，但如果没有，或者你最近加入了 M1 党，这篇文章提供了一种方法，你可以在你的 MacBook 上安装 M1 芯片拥抱脸变压器。而且不，不是`pip install transformers`。

启动和运行变压器有三个步骤。

1.  安装 Tensorflow
2.  安装 Tokenizers 包(带 Rust 编译器)
3.  安装变压器包

虽然它的工作，请考虑研究更可靠的方法来安装变压器-写于 2021.10.25

## 1.张量流

安装 tensorflow 很容易，你只需指向你现有的虚拟 env，或者你可以创建一个新的来玩，或者如果你不想创建一个新的，它会为你创建一个。

1.  *创建并启用* *虚拟环境*

如果您还没有 virtualenv 软件包，请安装它

```
pip install virtualenv
```

通过键入以下命令创建 virtualenv

```
python virtualenv venv --python=python3
```

要启用虚拟环境

```
source venv/bin/activate
```

2.*下载*

点击从[下载最新版本。确保下载包含安装脚本的**tar.gz**文件。在撰写本文时，最新的版本是 tensorflow-macos 0.1 alpha 3。没错，是 *tensorflow-macos，*而不是 tensorflow。](https://github.com/apple/tensorflow_macos/releases)

3.*安装*

一旦有了脚本，转到下载目录并运行下面的命令`./install_venv.sh --prompt`。它会询问您虚拟环境文件夹的路径，请提供我们创建的路径。您也可以让它创建另一个，但在我看来，创建我们打算使用的或我们已经拥有的总是更好。

![](img/c81111310029e089cce9fc008a3160e3.png)

输入虚拟环境的路径

![](img/9f3b87eb7049913b8718b70dbad1c63d.png)

已成功安装 tensorflow-macos

*注意*——你可以通过 [tensorflow-metal](https://developer.apple.com/metal/tensorflow-plugin/) 利用 M1 加速训练你的机器学习模型。如果你是这种情况，请点击了解更多信息[。](https://makeoptim.com/en/deep-learning/tensorflow-metal)

## 2.标记化者

我们将从源代码中构建标记化器以避免任何中断，我确信如果我们决定不这样做，它将会出现。这里有几个步骤，所以当你跟着做的时候要精确。

*2.1 安装防锈语言*

我们需要安装 Rust 来从源代码安装令牌化器。您可以通过键入以下命令来做到这一点

```
curl --proto '=https' --tlsv1.2 -sSf [https://sh.rustup.rs](https://sh.rustup.rs) | sh
```

您可以在安装后按照命令提示符下的说明配置当前的 shell，或者您可以打开另一个会话来查看它的效果。

*2.2 安装令牌化器*

一旦我们有了 Rust，我们就可以下载令牌化器的源代码

```
git clone [https://github.com/huggingface/tokenizers](https://github.com/huggingface/tokenizers)
```

转到 python 绑定文件夹`cd tokenizers/bindings/python`

确保您已经安装并激活了虚拟环境，然后键入以下命令来编译令牌化器

```
pip install setuptools_rust
```

最后，安装令牌化器

```
python setup.py install
```

## 3.变形金刚(电影名)

现在终于，你可以安装变压器了

```
pip install git+https://github.com/huggingface/transformers
```

![](img/e86093d5a58480361567198e583bb1a0.png)

瞧，变压器安装成功

## 结束注释

最近我一直在试图弄清楚如何在苹果 M1 上安装许多东西，当我弄清楚的时候，我试图记下它，以方便其他可能有同样问题的人。希望这对你有所帮助，如果你有任何反馈或正在为任何其他安装而挣扎，请随时联系[联系](https://twitter.com/dhrumilcse)，也许我有一个解决方案，但没有机会写下来。快乐学习。