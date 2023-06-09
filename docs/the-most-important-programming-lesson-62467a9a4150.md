# 最重要的编程课

> 原文：<https://towardsdatascience.com/the-most-important-programming-lesson-62467a9a4150?source=collection_archive---------44----------------------->

## 意见

## 学习编程的趣闻和调试技巧

![](img/6aee0bfa9d749d769d20bfb49e7c1ffd.png)

布雷特·乔丹

2012 年秋天，我走进研究生导师的办公室，问她推荐我报读哪个计算机科学班。我解释说我完全是编程新手。她建议介绍 C 编程。听了几次讲座后，我发现在这个*入门*课程中，我交谈过的大多数学生都有一些编程的经验。六周 80 小时的工作后，我放弃了这门课程。

进入 2013 年春季学期。我参加了一个更简单的计算机科学课程，通过网络的计算机编程入门。我轻松地通过了课程的前四分之一，轻松地执行 HTML 和 CSS。然后，我们开始了 Javascript (JS)。我之前的计算机科学课程带给我的那种持续的焦虑和压力感又回来了。学期太晚了，不能放弃这门课，所以我向一个朋友求助。

一天下午，他向我介绍了我的 JS 代码，并解释了如何在这里和那里添加一些代码来测试您的函数是否按预期工作。他向我展示的是一种非常基本的调试形式，即识别和消除计算机硬件或软件错误的过程。他和我都不明白这 60 分钟的辅导课可能会对我的职业轨迹产生的影响。回顾过去，毫不夸张地说，这是我在计算机科学和技术方面学到的最重要的一课。

如果你以前从未写过任何代码，想象你的任务是画一只完美的鸟。每次你完成画并把它交给老师，老师会立即决定它是正确的还是不正确的(即二元结果)。每当试卷有瑕疵时，老师就会把它撕掉。如果你问老师出了什么问题，他们会用外语(即计算机错误语言)向你解释这个问题。最终，在老师尝试了几十次后，他们可能会接受你的画，你的分数会从错误变为正确。读完这个故事，你可能不会认为我的下一个声明是如此大胆(双关语)。

**在学术界，没有什么比学习写代码更能考验你的耐心和承受不断拒绝的能力了。**

在学习编码时，唯一能给你安慰的是你是否理解了调试的基础。现在，当我画一只鸟时，老师会提供反馈，看鸟喙是否好看，颜色是否合适，大小是否合理。有了这些反馈，你的提交就更有可能是正确的，而不会被拒绝。

无论您是否定期编写代码，调试的基础知识在您的生活中都会非常有用。每当你需要使用任何种类的软件应用程序或工具时，它们都适用。根据我个人在技术方面的经验，这里列出了我最喜欢的各种软件应用程序和工具的调试技巧和诀窍。

# 使用 Web 应用程序

Web 应用程序是用户通过 web 浏览器访问的计算机程序。常见的网络应用程序有脸书、Gmail 和 Salesforce。如果您在使用 web 应用程序时遇到问题，通常可以通过以下方法之一解决问题:

*   尝试不同的浏览器。在某些浏览器中，各种功能可能无法工作
*   关闭插件。插件可以影响浏览器中的 web 应用程序
*   清除 web 浏览器中的缓存
*   重新启动 web 应用程序
*   检查该问题是否特定于您的应用程序版本。
*   确认您拥有哪些安全角色。某些功能可能不可见，因为您没有权限。
*   重新启动计算机

# 导入数据文件

导入数据文件(如 xls、CSV、pdf 等。)到 web 应用程序或一段代码中是一项常见的任务。常见问题往往与以下内容有关:

*   检查列名引用是否正确。它们可能区分大小写。
*   删除任何无法识别的字符。尝试用 UTF 8、UTF-16 或 ASCII 编码文件。
*   注意前导零和/或前导零被去除。检查数据类型，是字符串、浮点还是整数。
*   从数据中删除前导和尾随空白
*   检查文件是否为正确的文件类型(例如 xls、csv、pdf、jpg)
*   确认列中的所有值都在可接受的规则范围内。有些列需要特定的数据类型(如字符串、整数等)。)和/或它们可能要求该值存在于受控列表中(例如，在颜色列下仅接受“红色”和“蓝色”)
*   导入前删除所有空白行
*   导入后的电子邮件通知可能会发送到您的垃圾邮件文件夹

# 所有编程语言

*   检查整个脚本中的变量值，查看它们是如何变化的
*   打印出函数中的文本，以测试它们是否以及何时被执行
*   使用集成开发环境
*   在代码中使用大量的注释
*   Stackoverflow 和 Google 是你的朋友
*   检查您正在使用的编程语言或库的版本。不同版本之间的事情可能会发生巨大的变化。
*   将冗长的代码片段分解成较短的片段。例如，不要用一个巨大的 [JSON](https://thedatageneralist.com/tech101-who-is-json/) 字符串测试代码，试着在一个小的子集上测试它。更好的是，创建自己的 mini-JSON 字符串来进行测试。
*   为每一行代码一步一步写下计算机的动作。 [Python Tutor](http://pythontutor.com/) 提供了一个很棒的视觉效果，带你一行一行地执行代码。web 工具适用于 Python、Javascript、Java、C 和 C++。
*   检查是否有人为您的特定用例创建了一个可以让生活变得更简单的包。例如，在 [Pandas](https://pandas.pydata.org/docs/) 中操作数据要比使用原生 Python 容易得多。

# Javascript 编程

*   在函数中使用 console.log()打印文本或变量值，以测试它们是否以及何时在脚本中执行
*   经常清理你的浏览器缓存
*   尝试不同的网络浏览器——插件会干扰代码
*   升级您的 web 浏览器—旧版本可能不受支持

# Python 编程

*   对象名称区分大小写(例如，“变量名称”与“变量名称”不同)
*   请密切注意错误消息。他们通常会解释问题是从哪一行开始的。
*   检查这是否是 Python v2 相对于 Python v3 的变化
*   Python 有很棒的[文档](https://docs.python.org/3/library/index.html)

# SQL 编程

*   测试脚本时，利用限制来提高性能
*   检查是否由于您使用的 SQL 数据库而存在特殊的语法规则或限制。例如，MySQL 使用#作为注释行的开头，而 PostgreSQL 使用--作为注释
*   不要用[保留字](https://www.drupal.org/docs/develop/coding-standards/list-of-sql-reserved-words)来命名表格或变量
*   通过在 Excel 中复制对数据子集的预期操作，确认输出表是正确的。

# 最重要的调试建议

说到学习计算机科学和编程，我希望我的教授们强调学习调试代码的重要性。希望我的提示和技巧能减少你写代码时的焦虑和挫败感。哦，我把最好的建议留到了最后。

如果你不能解决一个问题，先睡一觉，稍后再回来。

说真的。带着更少的压力和全新的视角来帮助你在几分钟内找到解决方案，而不是前一天花几个小时。这个建议一次又一次给我带来了好处。前几天，我花了 5 个小时写一个 JS 脚本，但毫无进展。几天后我又回到了这个问题，当我重新打开浏览器时，我很快发现这是一个缓存问题。这个建议唯一不起作用的时候是没有时间的时候。小心点，拖延者们！

~ [数据通才](https://twitter.com/datageneralist)