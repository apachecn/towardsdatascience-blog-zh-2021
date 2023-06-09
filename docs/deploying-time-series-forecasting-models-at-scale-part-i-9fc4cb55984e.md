# 大规模部署时间序列预测模型(第一部分)

> 原文：<https://towardsdatascience.com/deploying-time-series-forecasting-models-at-scale-part-i-9fc4cb55984e?source=collection_archive---------13----------------------->

## 如何利用 Flow-Forecast、Docker、Terraform、Airflow、Kubernetes 和 ONNX 轻松地将深度时间序列模型扩展到生产工作负载。

![](img/a4a564c03842935d1802aad23edd6c21.png)

[照片去飞溅](https://unsplash.com/photos/XLFu0PM5Qsg)

部署机器学习模型仍然是许多公司的症结所在，时间序列预测模型也不例外。据 [VentureBeat 报道，大约 90%的车型从未投入生产](/why-90-percent-of-all-machine-learning-models-never-make-it-into-production-ce7e250d5a4a)。虽然这可能有许多原因(例如，模型本质上是探索性的，最终目标不是生产，等等)，但足以说许多有前途的模型在这个阶段被搁置。对于经常有许多活动部件的深度学习模型来说尤其如此。

在本文中，我们将讨论将时间序列预测模型用于生产的一般技术。然后，我们将更具体地探讨如何使用[流量预测](https://github.com/AIStream-Peelout/flow-forecast)训练 PyTorch 模型，为部署做好准备。在本系列文章的第二部分中，我们将实际描述使用 FastAPI、Docker、Terraform 和 Kubernetes 部署示例模型。最后，在第三部分中，我们将监控它们，并展示如何定期更新它们，以及如何根据增加的工作负载进行扩展。另一个系列将处理深度学习模型的分布式训练。

## 考虑

**培训前**

正如我在之前的文章[中提到的，在你选择一个模型进行训练之前，你应该权衡你的最终目标。可解释性重要吗？我需要什么样的推理速度？我需要置信区间吗？还是只有一个预测值就好？这些考虑和分析应该告知您最初选择训练哪个模型。](/training-time-series-forecasting-models-in-pytorch-81ef9a66bd3a)

其次，在培训前规划阶段，您还应该考虑应用程序将如何与现有软件基础架构交互，以及它将接收何种类型的时态数据。例如，如果模型需要对 Kafka 数据流进行实时预测，那么您如何为部署做好准备将与模型只需要从 GCP 桶中摄取静态 CSV 文件有很大不同。这也可能导致 scaler 之类的东西中断，因为以前它们可能会缩放整个 CSV 文件并附加所有最新的数据，而现在为了便于快速推断，我们将无法重新计算 scaler 或 CSV 文件。

最后，你要考虑重新训练或者继续训练模型需要多长时间。如果你要定期获取新数据，如果你的模型每次都需要从头开始重新训练(例如由于灾难性的遗忘),这将消耗大量资源。

**选择您的总体预测长度**

预测长时间序列数据仍然是一个很大的瓶颈，因为模型只能预测与其输出预测长度一样长的值。这意味着，如果您有一个一次仅预测一个时间步长的模型，并且想要预测未来的 200 个时间步长，您将需要运行 200 次向前传递(至少对于大多数模型)加上追加操作。而如果你一次建立了 10 个时间步长预测模型，你只需要 20 个。因此，当长预测长度不会降低性能时，您应该使用它们。

**测试损失最低的模型真的是最好的模型吗？**

通常，测试损失最大的模型在全面生产环境中可能表现不佳。这主要是由于数据的分布变化和评估指标的选择不当。因此，您会希望在部署之前以严格的方式评估您的模型。为了做到这一点，我建议分析总体测试损失、最新数据的测试损失和可解释性图表。你也可以看看你的模型在极端情况下做了什么。即使预测问题很复杂，我们通常对应该发生什么或预测的大致方向有基本的直觉。例如，如果您有一个预测河流流量的模型，而该河流通常每月只有 2 英寸的降雨量，您可以尝试在一个小时内输入 20 英寸的降雨量。显然，河流流量预测应该会上升到史诗般的高度(不管正常的时间滞后是多少)。如果没有，那你就知道有问题了。

**双重检查生产流程**

在这一阶段，经常会有“意想不到的来源”的分布变化。理想情况下，您应该编写单元测试，以确保模型在生产中做出与测试数据相同的预测。我不能夸大这一点，检查你的输入数据。预处理中极小的差异往往会导致精度上的巨大差异。很多时候，人们会很快归咎于一个有缺陷的模型，但是很多时候不适当的数据清理和改变数据格式是罪魁祸首。您还应该与您的数据工程/后端团队沟通，看看他们是否预计到数据格式的变化。最后，您可以编写端到端的测试，以确保模型与预处理和后处理相结合产生合理的结果。

**单个型号或多个型号**

初始模型选择的另一个区别是您需要部署单个还是多个模型。例如，您可以为每个要预测的商店训练一个单独的 DNN，或者为所有商店训练一个 DNN。在后者中，您的模型将需要在推理时访问商店 id(和其他信息)以及时态信息。在这种情况下，您还需要跟踪模型输出(尤其是当您一次将多个商店位置分批处理时)。在前一种情况下，您将需要部署更多的模型，但是由于它们是独立的，它们至少在推理方面更具并行性。

## 通过流量预测为部署准备好模型

Flow Forecast 有许多内置工具可帮助您完成模型部署过程。我们有一个易于使用的自动推理 API，它提供了 evaluator 类的全部功能。除非您需要用不同的语言部署您的模型，或者需要非常低的推理速度，否则我们建议您只需将该类封装到您的 Python (web)应用程序中，或者使用我们预先构建的 Docker 容器之一来创建自动推理 API。然而，即使您决定需要导出它，您仍然希望从推理 API 开始，因为它使下面的两个步骤变得容易。

1.  **鲁棒性测试**

使用流量预测推理 API，您可以轻松地绘制出模型在不同时间段的表现。我们的标准可解释性度量套件已经自动记录到权重和偏差中。要查看如何工作的完整示例，您可以查看这个笔记本。

使用 FF 推理模式实例化模型的示例。

**2。推断速度测试和加速**

我们在流量预测中的另一个功能是自动计时您的模型在各种设备上预测不同预测长度所需的时间，以及 vanilla 模型、TorchScript 和 ONNX 之间的差异。此外，我们正在研究几个新的增强功能，以加快推断速度，例如在大批量中生成置信区间，以及更快地记录绘图。

**3。导出到 TorchScript 和 ONNX**

截至流量预测 0.95，我们已经支持 TorchScript，我们计划在 0.96 之前支持 ONNX。然而，使用这些方法有几个缺点，包括置信区间的损失。要将模型放入 TorchScript/ONNX 中，需要调用`model.eval()`,这意味着所有预测都是相同的，因此没有置信区间。也就是说，如果您想要将模型转换为 TorchScript(假设您已经遵循了上面要点中的步骤),您基本上应该这样做:

```
from flood_forecast.deployment.inference import convert_to_torch_script convert_to_torch_script(d, "torch_script_save_path.pt")
```

更多信息见[此链接。](https://github.com/AIStream-Peelout/flow-forecast/blob/a750601743695d8cc7bef00dd964f32a070b49c1/flood_forecast/deployment/inference.py#L118)

**4。当前数据接收和未来版本**

目前，推理模式仅支持从 CSV 加载推理数据。然而，我们希望在不久的将来改变这种情况，允许从许多不同的数据源加载数据。具体来说，我们优先考虑直接从 SQL 表、Parquet 文件和 HDFS 加载数据。稍后在我们的路线图中，我们计划允许流数据源，如 Kafka 订阅、Redis 或 Pub/Sub。

在本文中，我们介绍了部署模型的一些准备步骤。一旦你完成了这些事情，你就可以开始关注实际的部署阶段了。在第二篇文章中，我们将研究如何通过使用流量预测推理 Docker 容器、我们的 Terraform 模板和 Google 云平台来执行实际部署。这篇文章将更加直观，包含更多代码示例。如果你有任何问题，请随时提问。