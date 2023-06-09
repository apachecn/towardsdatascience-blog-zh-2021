# 区块链的数据科学:了解当前形势

> 原文：<https://towardsdatascience.com/data-science-for-blockchain-understanding-the-current-landscape-c136154c367e?source=collection_archive---------2----------------------->

## 数据科学和区块链技术是天生的一对。但是到底有多少和什么样的真实世界的应用程序呢？

![](img/7804030971b654df4bdeccce5eb17d97.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上由[zdenk macha ek](https://unsplash.com/@zmachacek?utm_source=medium&utm_medium=referral)拍摄的照片

B 锁链技术是当今的热门话题，尤其是随着最近[去中心化金融](https://en.wikipedia.org/wiki/Decentralized_finance)的繁荣，比特币和其他加密货币的指数增长，以及正在进行的 [NFT](https://en.wikipedia.org/wiki/Non-fungible_token) 热潮。从数据科学家的角度来看，区块链也是一个令人兴奋的高质量数据来源，可用于使用统计和机器学习来解决各种有趣的问题。但这些问题到底是什么？区块链行业是否有足够的需求来培养数据科学家？本文试图回答这些问题，对数据科学和区块链技术的交叉领域的现状和趋势进行了全面的概述。

*免责声明*:我既不附属于也不支持本文提及的任何公司。提及这些公司及其产品仅用于说明目的。

# 首先是术语

术语“*数据科学*”没有普遍接受的定义。在这里，我将坚持我最喜欢的[定义](https://hackernoon.com/what-on-earth-is-data-science-eb1237d8cb37)，它是由 [Cassie Kozyrkov](https://medium.com/u/2fccb851bb5e?source=post_page-----c136154c367e--------------------------------) (谷歌决策情报主管)提出的:

> "数据科学是让数据变得有用的学科."

这是一个包罗万象的定义，因此对数据科学的实践方式进行更详细的划分会有所帮助。Kozyrkov ( [2018](https://hackernoon.com/what-on-earth-is-data-science-eb1237d8cb37) )根据数据科学应用支持的决策数量提出了以下分类:

*   *数据挖掘/描述性分析* —探索性分析，以识别数据中有趣的、先前未知的模式，并对导致这些模式的潜在过程提出假设。这里*还没有决定*要做——我们只是在手边的数据集中“寻找灵感”。
*   *统计推断*——做出*一个或几个*关于世界的风险可控的结论，这些结论超越了被分析的数据集。
*   *机器学习/人工智能* —构建“决策配方”，可以(重新)用于以自动化的方式做出*许多决策*。

尽管这些类型的数据科学项目之间的差异并不总是那么明显，但让我们接受这种分类法，因为它足以满足我们的目的。

根据[维基百科](https://en.wikipedia.org/wiki/Blockchain)，

> 区块链是一个不断增长的记录列表，称为*块*，它们使用加密技术链接在一起

区块链被实现为分散的、分布式的、只写的数据库，运行在对等计算机网络上。传统上，区块链一直被用作*总账*来记录加密货币交易(例如，比特币、以太坊、Dash 等)。).然而，如今这项技术正在获得许多其他用例。

区块链上的交易发生在两个或更多的*地址之间——由字母数字组成的字符串，充当用户的假名，作用类似于电子邮件地址。一个真实的人，区块链的用户，可以拥有多个地址。此外，一些区块链(例如，比特币)鼓励其用户为新交易创建新地址，以保持高度的匿名性。*

区块链上本地生成的记录被称为*链上数据*。在他们的分析过程中，这些记录通常会增加来自任何外部来源的*非链数据*(例如，拥有某些区块链地址的实体的名称有时可以从公共论坛和[网站](https://ens.domains/)中收集到)。

类似于陈等人( [2020](https://arxiv.org/pdf/1909.06189.pdf) )，我们将与相关的数据科学应用分为两类——【为】、【在】。第一种类型的应用对链上数据和可能的链外数据做一些有用的事情，但是不一定部署在区块链的基础设施上(例如，部署在云提供商的基础设施上的基于链上数据的仪表板)。第二种类型的应用程序是区块链本身的一部分。

“在区块链”应用程序可以部署为 [*智能合同*](https://ethereum.org/en/developers/docs/smart-contracts/) 。简而言之，智能协定是一段代码，它驻留在自己的地址上，并执行某些预定义的逻辑来响应特定于协定的触发器。智能合约可以用各种编程语言编写，既有通用的也有专用的，比如 [Solidity](https://docs.soliditylang.org/en/latest/) 或 [Vyper](https://vyper.readthedocs.io/en/stable/) 。

# 数据科学和区块链技术是天生的一对

与传统数据源(例如，集中控制的企业数据库)相比，区块链在设计上提供了几个对数据科学应用非常重要的优势:

*   *高数据质量*:所有新记录都经过严格的、区块链特有的验证流程，该流程由众多“[共识机制](https://www.investopedia.com/terms/c/consensus-mechanism-cryptocurrency.asp#:~:text=A%20consensus%20mechanism%20is%20a,systems%2C%20such%20as%20with%20cryptocurrencies.)中的一个提供动力。一旦经过验证和批准，这些记录就变得不可改变——没有人可以出于任何目的修改它们，无论是善意的还是恶意的。区块链数据通常结构良好，其模式也有据可查。这使得处理此类数据的数据科学家的工作变得更加容易，也更容易预测。
*   *可追溯性*:区块链记录包含跟踪其来源和背景所需的所有信息，例如，哪个地址发起了一项交易，交易发生的时间，转移的资产金额，以及接收该资产的地址。此外，大多数公共区块链都有“探索者”——任何人都可以在网站上查看各自区块链上产生的任何记录(例如，见[比特币](https://www.blockchain.com/explorer)、[以太坊](https://etherscan.io/)和[涟漪](https://livenet.xrpl.org/)探索者)。
*   内置匿名功能:区块链不要求用户提供任何个人信息，这在一个保护个人隐私已经成为现实问题的世界里非常重要。从数据科学家的角度来看，这有助于克服与一些法规(例如，欧洲的 [GDPR](https://www.legislation.gov.uk/eur/2016/679/article/5) 法规)相关的难题，这些法规要求在处理之前对个人数据进行匿名处理。
*   *大数据量:*很多机器学习算法需要大量的数据来训练模型。这在成熟的区块链不是问题，他们提供千兆字节的数据。

# 从区块链收集数据很棘手，但还是有选择的

![](img/c51606fef47c32c9c727d0804484b421.png)

照片由[爆裂](https://unsplash.com/@burst?utm_source=medium&utm_medium=referral)上[未飞溅](https://unsplash.com?utm_source=medium&utm_medium=referral)

收集与手头问题相关的数据是数据科学家在区块链相关项目中可能遇到的第一个障碍。使用前面提到的浏览器网站很容易检查单个区块链记录。然而，*程序化地*收集适用于数据科学目的的大型数据集可能是一项艰巨的任务，可能需要专业技能、软件和财政资源。有三个主要的选择可以考虑。

## *选项 1——使用其他人已经准备好的数据集*

作为其 [BigQuery 公共数据集](https://cloud.google.com/bigquery/public-data/)计划的一部分，谷歌云[为](https://cloud.google.com/blog/products/data-analytics/introducing-six-new-cryptocurrencies-in-bigquery-public-datasets-and-how-to-analyze-them)[比特币](https://console.cloud.google.com/bigquery?utm_source=bqui&utm_medium=link&utm_campaign=classic&project=betspeed-1192&d=crypto_bitcoin&p=bigquery-public-data&page=dataset)、[比特币现金](https://console.cloud.google.com/bigquery?utm_source=bqui&utm_medium=link&utm_campaign=classic&project=betspeed-1192&d=crypto_bitcoin_cash&p=bigquery-public-data&page=dataset)、 [Dash](https://console.cloud.google.com/bigquery?utm_source=bqui&utm_medium=link&utm_campaign=classic&project=betspeed-1192&d=crypto_dash&p=bigquery-public-data&page=dataset) 、 [Dogecoin](https://console.cloud.google.com/bigquery?utm_source=bqui&utm_medium=link&utm_campaign=classic&project=betspeed-1192&d=crypto_dogecoin&p=bigquery-public-data&page=dataset) 、[以太坊](https://console.cloud.google.com/bigquery?utm_source=bqui&utm_medium=link&utm_campaign=classic&project=betspeed-1192&d=crypto_ethereum&p=bigquery-public-data&page=dataset)、[以太坊经典](https://console.cloud.google.com/bigquery?utm_source=bqui&utm_medium=link&utm_campaign=classic&project=betspeed-1192&d=crypto_ethereum_classic&p=bigquery-public-data&page=dataset)、 [Litecoin](https://console.cloud.google.com/bigquery?utm_source=bqui&utm_medium=link&utm_campaign=classic&project=betspeed-1192&d=crypto_litecoin&p=bigquery-public-data&page=dataset) 和 [Zcash](https://console.cloud.google.com/bigquery?utm_source=bqui&utm_medium=link&utm_campaign=classic&project=betspeed-1192&d=crypto_zcash&p=bigquery-public-data&page=dataset) 提供了完整的交易历史。使用 SQL 可以轻松查询这些数据集，并且可以导出结果以供进一步分析和建模。方便的是，大多数数据集都使用相同的模式，这使得重用 SQL 查询更加容易。见[叶夫根尼·梅德维杰夫](https://medium.com/u/b6a4cbbd2e57?source=post_page-----c136154c367e--------------------------------)在 Medium 上的帖子以获取教程。

还存在可用于研究和开发目的的静态区块链数据集。以下是几个例子:

*   [椭圆数据集](https://www.kaggle.com/ellipticco/elliptic-data-set)，比特币图的子图，由 203769 个节点(交易)和 234355 条边(有向支付流)组成。这些节点被标记为“合法”、“非法”或“未知”。该数据集由[椭圆](https://www.elliptic.co/)公司发布，旨在激发学术界和密码界对建立更安全的基于加密货币的金融系统的兴趣(Bellei[2019](https://medium.com/elliptic/the-elliptic-data-set-opening-up-machine-learning-on-the-blockchain-e0a343d99a14)；韦伯等人 [2019](https://arxiv.org/pdf/1908.02591.pdf) 。
*   BigQuery 中的 [Medalla 数据集由](https://console.cloud.google.com/bigquery?page=dataset&d=crypto_ethereum2_medalla&p=public-data-finance&project=betspeed-1192) [Nansen.ai](https://nansen.ai/) 公司公开，作为[以太坊基金会](https://ethereum.org/en/eth2/get-involved/medalla-data-challenge/)于 2020 年举办的 [Medalla 数据挑战赛](https://ethereum.org/en/eth2/get-involved/medalla-data-challenge/)的一部分。该数据集包括描述以太坊[信标链](https://ethereum.org/en/eth2/beacon-chain/)上的[块和块验证器](https://research.nansen.ai/ethereum-2-0-etl-and-medalla-data-in-google-bigquery/)的变量。
*   [CryptoKitties 数据集](https://github.com/cryptocopycats/kitties)，它包含了来自著名的以太坊[游戏](https://www.cryptokitties.co/)的数千只“数码猫”的属性。
*   [数据集](https://github.com/epicprojects/blockchain-anomaly-detection)由里德和哈里根( [2012](https://arxiv.org/abs/1107.4524) )以及法姆和李( [2017a](https://arxiv.org/pdf/1611.03942.pdf) ， [2017b](https://arxiv.org/pdf/1611.03941.pdf) )用来检测比特币区块链上的异常交易。

## *选项 2 —使用区块链特定的 API 或 ETL 工具*

BigQuery 公共数据集确实涵盖了主要的区块链项目，但是如果感兴趣的区块链不在其中呢？好消息是，基本上所有的区块链都通过各自的 [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) 和/或[web socket](https://en.wikipedia.org/wiki/WebSocket)API 提供了一种与网络交互的编程方式。参见例如查询[比特币](https://www.blockchain.com/api)、[以太坊](https://infura.io/)、 [EOS](https://developers.eos.io/manuals/eos/latest/nodeos/plugins/chain_api_plugin/api-reference/index) 、 [NEM](https://docs.nem.io/en/nem-apis) 、 [NEO](https://docs.neo.org/docs/en-us/reference/rpc/latest-version/api.html) 、 [Nxt](https://nxtdocs.jelurida.com/API) 、[涟漪](https://xrpl.org/data-api.html)、[恒星](https://developers.stellar.org/api/)、 [Tezos](https://tzstats.com/docs/api#tezos-api) 、 [TRON](https://www.trongrid.io/) 、 [Zilliqa](https://dev.zilliqa.com/docs/apis/api-introduction) 的 API。

幸运的是，通常存在方便的客户端库，它们抽象出特定 API 的复杂性，并允许数据科学家使用他们喜欢的语言——Python 或 r。这种 Python 库的例子包括`[bitcoin](https://pypi.org/project/bitcoin/)`(比特币)、`[trinity](https://trinity.ethereum.org/)`和`[web3.py](https://web3py.readthedocs.io/en/stable/)`(以太坊)、`[blockcypher](https://github.com/blockcypher/blockcypher-python)`(比特币、莱特币、Dogecoin、Dash)、`[tronpy](https://pypi.org/project/tronpy/)`(创)、`[litecoin-utils](https://pypi.org/project/litecoin-utils/)`(莱特币)等。R 包的例子比较少但确实存在:`[Rbitcoin](https://cran.r-project.org/web/packages/Rbitcoin/index.html)`(比特币)`[ether](https://cran.r-project.org/web/packages/ether/index.html)`(以太坊)`[tronr](https://github.com/next-game-solutions/tronr)` (TRON)。

<https://levelup.gitconnected.com/introducing-tronr-an-r-package-to-explore-the-tron-blockchain-f0413f38b753>  

除了 API，还可以考虑使用专用的 ETL 工具从区块链收集数据。这个领域一个著名的开源项目是“[区块链 ETL](http://blockchainetl.io/) ”，这是一个由 [Nansen.ai](https://nansen.ai/) 开发的[Python 脚本集合](https://github.com/blockchain-etl)。事实上，正是这些脚本将数据输入到前面提到的 BigQuery 公共数据集。

虽然原生区块链 API 和开源 ETL 应用程序给了数据科学家很大的灵活性，但在实践中使用它们可能需要额外的努力和数据工程技能:设置和维护本地或基于云的区块链节点、执行脚本的运行时环境、存储检索数据的数据库等。相关的基础设施要求也可能产生大量成本。

## 选项 3 —使用商业解决方案

为了节省时间、精力和与基础设施相关的成本，还可以选择区块链数据收集的商业解决方案。此类工具通常使用跨多个区块链统一的模式，通过 API 或支持 SQL 的接口提供数据(例如，参见 [Anyblock Analytics](https://www.anyblockanalytics.com/) 、 [Bitquery](https://bitquery.io/) 、 [BlockCypher](https://www.blockcypher.com/) 、 [Coin Metrics](https://coinmetrics.io/) 、[Crypto API](https://cryptoapis.io/)、 [Dune Analytics](https://duneanalytics.com/) 、 [Flipside Crypto](https://flipsidecrypto.com/) )。这有助于各种比较分析，并且至少在理论上，使得开发在整个区块链可互操作的数据科学应用成为可能。

# 我们生活在描述性区块链分析的时代

![](img/9dd025d59c7d4b5594b510be37db3929.png)

科迪·菲茨杰拉德在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

区块链仍然是一项新技术，可以说，我们才刚刚开始理解它提供的数据的价值。在这个早期阶段，能够有效地收集、总结和可视化数据，也就是执行描述性分析，是至关重要的。毫不奇怪，迄今为止，描述性区块链分析的大多数用例都围绕着加密货币和监管合规性。已经开发了许多调查工具来帮助加密货币企业、金融机构、监管机构和执法部门完成以下常见任务:

*   跟踪和可视化地址之间的*资金流动*，以便例如发现被盗资金、揭露加密货币价格操纵、揭露窃贼身份以及防止洗钱；
*   *标记*区块链地址并将它们链接到现实世界的实体(例如，“暗网市场”、“勒索软件”、“诈骗”、“矿池”、“赌博应用”、“加密货币交易所”等)。);
*   *实时提醒*链上事件，如可疑交易、[大额资金转移、](https://whale-alert.io/)受制裁地址的活动；
*   使用统一数据模式的跨区块链搜索；
*   计算和可视化*定制链上* *指标*；
*   执行*自定义* *数据查询*。

调查性区块链分析领域的一些最大玩家包括 [AnChain.ai](https://www.anchain.ai/) 、 [Bitfury](https://bitfury.com/) 、 [CipherTrace](https://ciphertrace.com/) 、[chain analysis](https://www.chainalysis.com/)、 [Coin Metrics](https://coinmetrics.io/) 、 [Dune Analytics](https://duneanalytics.com/) 、 [Elliptic](https://www.elliptic.co/) 、 [Glassnode](https://glassnode.com/) 、 [Nansen.ai](https://www.nansen.ai/) 。

# 机器学习和区块链:很多学术研究，没有那么多现实世界的实现

![](img/19d420fea554b9ee3e2c164f2a5069d3.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上[科学高清](https://unsplash.com/@scienceinhd?utm_source=medium&utm_medium=referral)拍摄的照片

有大量的学术研究应用机器学习来解决各种与区块链相关的问题。刘等人( [2021](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9364978) )在他们的综述论文中，将这些问题分为以下三个主题(类似的讨论也可参见陈等人 [2020](https://arxiv.org/pdf/1909.06189.pdf) )。

*   *加密货币价格预测—* 这个话题是迄今为止最受欢迎的话题，考虑到散户和[机构投资者对加密货币日益增长的兴趣，这并不奇怪。大多数已发表的研究试图预测比特币或以太坊的未来价格，无论是绝对值还是价格方向(上涨或下跌)。这已经通过从简单的逻辑回归到 XGBoost 和基于深度学习的方法的算法完成(例如，Greaves 和 Au](https://cryptofundresearch.com/)[2015](http://snap.stanford.edu/class/cs224w-2015/projects_2015/Using_the_Bitcoin_Transaction_Graph_to_Predict_the_Price_of_Bitcoin.pdf)；阿拜等人[2019](https://arxiv.org/pdf/1908.06971.pdf)；巴里与起重机[2019](http://ceur-ws.org/Vol-2563/aics_5.pdf)；陈等 [2020](https://e-tarjome.com/storage/btn_uploaded/2020-08-23/1598154911_11132-etarjome%20English.pdf) )。模型输入通常包括链上变量(如活动地址数量、交易量、[挖掘难度](https://en.bitcoin.it/wiki/Difficulty)、[交易图](https://ciphertrace.com/glossary/transaction-graph/)指标)和链外变量(如交易所的交易量)的组合。总的来说，神经网络(特别是那些基于 LSTM 架构的网络)已经被发现优于基于树的算法，尽管即使在表现最好的模型中，预测的准确性也只比随机猜测高一点点。
*   *地址身份推断***——*按照设计，区块链地址所有者的身份通常是未知的。然而，能够将某些地址分类到预定义的组中，或者更好的是，将它们与现实世界的实体联系起来，可能具有巨大的价值。对于涉及非法活动的地址尤其如此，如洗钱、毒品分销、勒索软件、庞氏骗局、人口贩运，甚至恐怖主义融资。在几项研究中，地址分类问题已通过监督学习得到成功解决，这些研究开发了二元分类器(如 Weber 等人的前述论文 [2019](https://arxiv.org/pdf/1908.02591.pdf) )或多类分类器(如梁等人的[2019](https://www.researchgate.net/profile/Linjing-Li/publication/332786441_Targeted_Addresses_Identification_for_Bitcoin_with_Network_Representation_Learning/links/5cd3f04492851c4eab8cb540/Targeted-Addresses-Identification-for-Bitcoin-with-Network-Representation-Learning.pdf))；另见哈列夫等人 [2018](https://scholarspace.manoa.hawaii.edu/bitstream/10125/50331/1/paper0444.pdf) ，尹等人[2019](https://www.researchgate.net/profile/Raghava-Rao-Mukkamala/publication/332118587_Regulating_Cryptocurrencies_A_Supervised_Machine_Learning_Approach_to_De-Anonymizing_the_Bitcoin_Blockchain/links/5d0925f9458515ea1a709729/Regulating-Cryptocurrencies-A-Supervised-Machine-Learning-Approach-to-De-Anonymizing-the-Bitcoin-Blockchain.pdf)；米哈尔斯基等人 [2020](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9114987) )。各个模型是使用链上数据和各种标准机器学习算法开发的。有趣的是，与加密货币价格预测研究相比，基于树的方法(特别是随机森林)往往优于基于深度学习的算法(刘等人 [2021](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9364978) )。*
*   **异常检测* —区块链可能遭受多种恶意攻击和欺诈行为(如穆巴拉克等人[2018](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8371010)；拉胡蒂等人 [2018](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8528406) )，通过分析交易模式有可能发现这一点。由于异常交易的数量自然很少，这个问题已经用经验导出的规则或无监督的机器学习方法来解决，例如*k*-均值聚类、一类 SVM、Mahalanobis 基于距离的标记和隔离森林(例如，Camino 等人[2017](https://ieeexplore.ieee.org/document/8215741)；Pham 和 Lee [2017a](https://arxiv.org/pdf/1611.03942.pdf) ， [2017b](https://arxiv.org/pdf/1611.03941.pdf) 。刘等人( [2021](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9364978) )的结论是，这些研究中的大多数都存在低召回率，因此需要进一步研究。与此同时，Tann 等人( [2019](https://arxiv.org/pdf/1811.06632.pdf) )已经建立了一个高度准确的基于 LSTM 的二元分类器，用于检测智能合约中的代码漏洞。*

*除了上面描述的用例，许多研究人员已经提出甚至实验性地测试了机器学习驱动的区块链平台，旨在改进现有的电子健康记录管理系统，实现供应链中更好的可追溯性，增加[物联网](https://en.wikipedia.org/wiki/Internet_of_things)网络的安全性等。(萨拉赫等人[2018](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8598784)；陈等【2020】)。几篇论文还提出了基于区块链的平台和协议，用于机器学习模型的集体训练和传播(例如，Marathe 等人的“dine MMO”2018 年，Kurtumlus 和 Daniel 的“DanKu 协议”2018 年[和 Harris 和 Waggoner 的“区块链上的分散和协作 AI”](https://arxiv.org/pdf/1802.10185.pdf)[2019 年](https://arxiv.org/pdf/1907.07247.pdf))。*

*尽管在学术文献中看到了大量实验机器学习驱动的区块链系统的例子，但这种系统的实际实现仍然很少。这有很多原因，既有数据相关的，也有基础设施方面的(Salah et al. [2018](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8598784) )。例如，使用监督学习的区块链地址去匿名化需要足够大的*标记的*训练数据集。然而，高质量的标签通常只能用于一小部分地址，这阻碍了监督学习的使用(但请参见 Rodriguez [2019](https://medium.com/intotheblock/practical-machine-learning-for-blockchain-datasets-understanding-semi-and-omni-supervised-learning-2a2611695b2) 讨论可能的解决方案)。*

*得益于常用的纯文本格式[、](http://dmg.org/pmml/v4-4-1/GeneralStructure.html)、【PFA】、 [ONNX](https://onnx.ai/) (王 [2018](https://arxiv.org/ftp/arxiv/papers/1903/1903.08801.pdf) )，许多机器学习算法有可能通过智能合约部署在。然而，部署一些更复杂的算法，如在 GPU 上训练的基于张量流的深度神经网络，仍然是一项不平凡的任务。*

*由于交易的低带宽和高成本，缺乏技术标准和互操作性协议，以及需要外部数据的可信供应商(也称为“T8”甲骨文”)，在区块链部署和使用机器学习模型也可能很困难(Salah et al. [2018](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8598784) )。*

*然而，包括 [Algorithmia](https://algorithmia.com/research/ml-models-on-blockchain) 、 [AnChain.ai](https://anchainai.medium.com/our-ai-detects-your-ai-revealing-the-secret-world-of-blockchain-bots-part-2-tron-e6ad38522f9c) 、 [Bitfury](https://medium.com/meetbitfury/bitfury-ai-opens-offices-in-italy-and-netherlands-c2482685121c) 、 [Fetch.ai](https://fetch.ai/) 、 [IBM](https://www.ibm.com/blogs/blockchain/2021/01/blockchain-in-2021-accessibility-authenticity-and-ai/) 、 [IntoTheBlock](https://www.intotheblock.com/) 、 [SingularityNET](https://singularitynet.io/) 等在内的许多公司声称，他们正在他们的区块链产品中使用机器学习。毫无疑问，在不久的将来，我们将会看到更多这样的公司和产品。在其他发展中，通过甲骨文提供的链外信号，使智能合同“更智能”的更简单方法将极大地促进这种增长——C[hainlink](https://chain.link/)和 P [rovable](https://provable.xyz/) 已经提供了各自的解决方案。*

# *结论:如果你想成为一名区块链数据科学家，现在是最佳时机*

*区块链技术有可能改变许多行业和业务流程。在他们最近的文章中， [Forbes Technology Council](https://www.forbes.com/sites/forbestechcouncil/) 为区块链确定了 13 个不断发展和新兴的用例，包括艺术家的权利管理、跨行业数据整合、去中心化金融、供应链管理、用户认证和密码管理、电子健康记录等。所有这些发展都需要一批能够“让数据变得有用”的专家，也就是数据科学家。有趣的和未解决的区块链数据科学问题的范围是巨大的。此外，这些问题中有许多尚未形成。因此，如果你正考虑以数据科学家的身份进入区块链这个激动人心的世界，这个时机再好不过了。本文中提到的许多公司已经为数据科学家提供了空缺职位——请查看他们网站上的“职业”部分！*

# *在你走之前*

*我提供数据科学咨询服务。[取得联系](mailto:sergey@nextgamesolutions.com)！*