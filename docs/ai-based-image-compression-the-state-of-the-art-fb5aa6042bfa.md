# 基于人工智能的图像压缩技术现状

> 原文：<https://towardsdatascience.com/ai-based-image-compression-the-state-of-the-art-fb5aa6042bfa?source=collection_archive---------9----------------------->

## 一些领先的库和框架的概述

![](img/baad95559b073124e99124e7eb072119.png)

图片来源: [Pixabay](https://pixabay.com/illustrations/web-network-information-technology-4869856/)

# 什么是图像压缩？

图像压缩包括减少图像的像素、尺寸或颜色成分，以减小其文件大小。这减轻了它们的存储和处理负担(对于 web 性能而言)。先进的[图像优化技术](https://cloudinary.com/blog/image_optimization_for_websites_beautiful_pages_that_load_quickly)可以识别更重要的图像成分，并丢弃不太重要的成分。

图像压缩是[数据压缩](https://www.sciencedirect.com/topics/computer-science/data-compression)的一种形式，因为它减少了编码图像所需的数据位，但保留了图像细节。

图像压缩的应用包括:

*   **存储** —压缩后的数据占用更少的磁盘空间，这对于归档详细图像(如医学图像)特别有用。
*   **主成分分析(PCA)** —提取图像最重要成分的图像压缩方法用于提取或总结特征和分析数据。
*   **标准化** —在某些情况下，图像集必须符合标准的大小和格式，要求将所有图像压缩成相同的大小、形状和分辨率。例如，安全和政府机构维护的记录需要标准化的图像。

# 深度学习的图像压缩

深度学习(DL)自 20 世纪 80 年代以来一直用于图像压缩，并已发展到包括多层感知器、随机神经网络、卷积神经网络和生成对抗网络等技术。

## 多层感知器

多层感知器(MLPs)具有夹在输入神经元层和输出神经元层之间的隐藏层(或多层)或神经元。理论上，具有多个隐藏层的多层线性规划对于降维和数据压缩是有用的。使用 MLPs 的图像压缩涉及整个空间数据的单位变换。

用于图像压缩的初始 MLP 算法在 1988 年公开，并且将诸如空间域变换、二进制编码和量化的传统图像压缩机制合并到集成的优化任务中。该算法依靠分解神经网络来识别压缩比特流输出中的最佳二进制码组合，但是它不能将神经网络的参数固定为可变压缩比。

该算法进一步发展了预测技术，根据周围的像素来估计每个像素的值。然后，MLP 算法使用反向传播来最小化预测像素和原始像素之间的均方误差。

## 卷积神经网络

[卷积神经网络(CNN)](https://www.run.ai/guides/deep-learning-for-computer-vision/deep-convolutional-neural-networks/)与传统的计算机视觉模型相比，卷积神经网络提供了增强的压缩伪像减少和超分辨率性能。细胞神经网络的卷积运算允许它们确定相邻像素如何相关。级联卷积运算反映了复杂图像的特性。

然而，在整个图像压缩过程中结合 CNN 模型是具有挑战性的，因为它需要梯度下降算法和反向传播，这在端到端图像压缩中是具有挑战性的。

CNN 第一次实现图像压缩是在 2016 年，算法由分析模块和合成模块组成。分析模块由卷积、除法和子采样归一化阶段组成。每个阶段以仿射卷积开始，产生下采样输出，然后使用广义除法归一化(GDN)来计算下采样信号。

基于 CNN 的图像压缩改进了 [JPEG2000](https://cloudinary.com/blog/the_great_jpeg_2000_debate_analyzing_the_pros_and_cons_to_widespread_adoption) 指标，如峰值信噪比(PSNR)和结构相似性(SSIM)。该算法进一步发展了熵估计，使用称为超先验的尺度。这导致图像压缩性能水平接近诸如高效视频编码(HEVC)的标准。

## 生成对抗网络

生成对抗网络(GAN)是由两个对立的生成网络模型组成的深度神经网络。首个基于 GAN 的图像压缩算法于 2017 年推出。它产生的压缩文件只有 WebP 的一半大小，比 JPEG 或 JPEG200 小 2.5 倍，比 BPG 小 1.7 倍。该算法还利用并行计算 GPU 核心实时运行。

GAN 图像压缩涉及基于来自输入图像的特征，在微小的特征空间中重建压缩图像。在图像压缩方面，GANs 相对于 CNN 的主要优势是对抗损失，这提高了输出图像的质量。相对的网络被一起训练，彼此相对，增强了图像生成模型的性能。

# 基于人工智能的图像压缩框架和库

理论上，自己编写整个图像处理应用程序是可能的，但更现实的做法是利用他人开发的内容，根据自己的需要简单地调整或扩展现有软件。许多现有的框架和库提供了用于图像处理的模型，其中许多是在大型数据集上预先训练的。

## OpenCV

开源计算机视觉( [OpenCV](https://opencv.org/) )库提供了数百种机器学习和计算机视觉算法，有数千个函数支持这些算法。这是一个受欢迎的选择，因为它支持所有领先的移动和桌面操作系统，具有 Java、Python 和 C++接口。

OpenCV 包含许多用于图像压缩功能的模块，包括图像处理、对象检测和机器学习模块。您可以使用该库来获取图像数据，并对其进行提取、增强和压缩。

## 张量流

[TensorFlow](https://www.tensorflow.org/) 是谷歌支持机器学习和深度学习的开源框架。TensorFlow 允许您定制和训练深度学习模型。它提供了几个库，其中一些对于计算机视觉应用和图像处理项目非常有用。TensorFlow 压缩(TFC)库提供数据压缩工具。

您可以使用 TFC 库来创建内置优化数据压缩的机器学习模型。您还可以使用它来识别存储高效的数据表示，例如对模型性能影响极小的影像和要素。你可以把浮点张量压缩成更小的比特序列。

## MATLAB 图像处理工具箱

矩阵实验室，或 [MATLAB](https://www.mathworks.com/products/image.html) ，既指一种编程语言，也指一个流行的数学和科学问题解决平台。该平台提供了一个图像处理工具箱(IPT)，其中包含各种工作流应用程序和算法，用于处理、分析和可视化图像，并可用于开发算法。

MATLAB IPT 实现了图像处理工作流程的自动化，应用范围从降噪和图像增强到图像分割和 3D 图像处理。IPT 函数通常支持生成 C/C++代码，对于部署嵌入式视觉系统或桌面原型开发非常有用。

虽然 MATLAB IPT 不是开源的，但它提供免费试用。

## 高保真生成图像压缩

这种高保真的生成式图像压缩是一个 Github 项目，它利用学习到的压缩和 GAN 模型来创建一个有损压缩系统。这对编码爱好者来说很有吸引力，他们可以在 Github 上试验 HiFiC 代码。该模型对于重建压缩图像中的细节纹理非常有效。

# 结论

在这篇文章中，我讨论了基于深度学习的图像压缩算法的现状，包括多层感知器、卷积神经网络和生成对抗网络。我还展示了可以用来构建基于人工智能的图像压缩应用程序的现成工具:

*   **OpenCV** —包括数百个机器学习模型，包括几个执行图像压缩的模块。
*   **TensorFlow** —允许您构建和精细定制图像处理和压缩模型。
*   **MATLAB 图像处理工具箱** —让您构建图像处理工作流程和算法，包括图像分割和 3D 图像处理。
*   **高保真生成式图像压缩** —一个使用 GAN 模型执行有损压缩的开源项目。

我希望这将有助于您评估深度学习在图像压缩和优化项目中的使用。