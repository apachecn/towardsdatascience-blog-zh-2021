# 轻松下载用于 AWS Lambda 图层的 Python 包

> 原文：<https://towardsdatascience.com/easily-download-any-python-package-for-aws-lambda-layers-b8ffd43a26ee?source=collection_archive---------10----------------------->

## 两分钟内即可上传 AWS Lambda 图层包。使用 Lambda 为我们的 Lambda 创建图层

![](img/a8e9ba40407941b3a1583db10893cc3f.png)

图片由 Pixabay 提供

AWS 云服务，如 AWS Lambda，是一种快速部署数据解决方案的灵活方式。但是，在部署复杂的 Lambda 基础设施时，处理包和相关的依赖关系可能会令人沮丧，即使您使用的是 Lambda 层。

AWS 使用他们自己风格的 Linux 操作系统。这意味着我们不能只是在本地 pip 安装 Python 包，然后直接部署到 AWS Lambda。通常，在上传到 Lambda 之前，我们需要使用 Docker 或 EC2 来准备 Python 包层。

**事实证明，我们可以使用 AWS Lambda 来自动化 AWS Lambda 层准备..**

# 如何:

## 1.在 S3 创建一个着陆桶

*   在 S3 创建一个存储桶。我们将所有的 Python 包放入这个新的桶中。*注意:我们将创建的 Lambda 将自动按照版本组织我们下载的 Python 包。*

## 2.创造一个新的λ

*   创建一个新的 Lambda，确保添加一个内联策略，以允许该 Lambda 将对象放入和删除到 S3 的目标着陆桶中。
*   一定要调整 Lambda 的最大内存和超时，以适应更大的包/依赖项。(例如熊猫用了 280MB，用了 15.153 秒)
*   将以下代码粘贴到您的 Lambda 中:

*   确保将参数与您想要下载的 Python 包、其版本以及您的目标 S3 桶进行交换。

## 4.享受

花一便士(或者更少)来编译你的 Lambda 层绝对值得节省时间。

在 Lambda 运行之后，您可以检查您的 S3 桶中是否有 Lambda 准备的 Python 包。

![](img/532807f296ba38143c7eb2f68a621995.png)

按包装分类的 S3 时段组织示例。图片作者。

您请求的每个包都会自动根据其版本进行组织。所以你可以下载同一个包的不同版本(如果需要的话)，在 S3 很容易找到。

![](img/dfd4fd0bfbaf5f7216419e139688fda8.png)![](img/7bd8ab914413d738dc1ee0b6deb297dc.png)

Pandas 包版本可以作为 Lambda 层上传。图片作者。

现在，您可以轻松地从 S3 Bucket 下载 zip 文件，并将其作为一个层上传到 AWS Lambda。

感谢阅读~。