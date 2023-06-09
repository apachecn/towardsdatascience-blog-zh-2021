# py 使用 Python 在 30 分钟内编写一个命令行界面模拟游戏

> 原文：<https://towardsdatascience.com/writing-a-command-line-interface-simulation-game-in-under-30-minutes-using-python-239934f34365?source=collection_archive---------14----------------------->

## 用一些简单的 Python 代码在几分钟内制作的快速游戏

![](img/dd9b78b0d66993437cdf6de9b3f0ef84.png)

(图片由作者提供)

# 介绍

我非常喜欢给计算机编程，并让编程和软件工程变得如此诱人和有益的一点是，你可以通过一路上创建的数据系统，真正释放你的创造力和对问题的思考。我觉得有时候我有很酷的想法来处理问题，而且通常所有这些想法都可以很好地结合在一起，有时候——没那么好。这当然可以用来说明编码前计划的有效性。

也就是说，在最近写一篇关于 Click 模块的文章时，我决定用一个完整的软件来演示这个模块会很有趣，但是我也发现很难想象我到底想做什么。我认为这将是一个有趣的项目，因为这将是一个伟大的点击模块的应用程序，但我也认为这将是非常有趣的编程。

![](img/3cabc685d5dcff5dfbf3617a64752b75.png)

> 看一下我的 Github 统计就知道了！

多有问题啊，看来我这辈子都没离开过笔记本。然而，本例中使用的语言有点像骗局，因为它是根据文件大小来确定的——Jupyter 笔记本包含各种不同内容的大量数据，它的代码比普通代码多得多，这就是我的观点。也就是说，Python 只占我在 Github 上的文件大小的 0.08%，我认为我应该着手开始一个 Python 项目。该项目的代码可在以下存储库中找到:

<https://github.com/emmettgb/characterclash/tree/main>  

# 获得基本视觉效果

今天，我们将创建一个简洁的可视化界面，通过带有 ASCII 艺术的 CLI 来查看游戏的输出…这是本文前半部分的 Github 链接。以下是该分支机构的链接:

<https://github.com/emmettgb/characterclash/tree/0.0.1-basic-functionality>  

让我们首先导入我们所有的依赖项，以及我们可能得到的任何新的依赖项:

```
import click as clk
from numpy import random as rnd
from time import sleep
from os import system, name
```

现在让我们开始学习一个基础课程，让我们可以开始制作这个的视觉效果:

```
class PlayGrid:def __init__(self, players):
        self.players = players
```

我们真正需要初始化这个新类的是一个未来的玩家字典，每当我们加载这个游戏时，我们将在我们的主函数中提供这个字典。现在，我将编写一些未来的函数，随着我们逐步编写这些函数，它们将变得更加有用，让我们来看看结果:

```
class PlayGrid:def __init__(self, players):
        self.players = players
        draw_grid()
    def update(self, message):
        passdef move(dir, speed):
        pass
def draw_grid():
    pass
```

像往常一样，我要练习提取技术。如果你想更深入地了解这项技术，以及它将如何应用到这个项目的未来代码中，我有一整篇关于它的文章，你可以在这里阅读——它有助于清理你的代码，使它运行得更好！

</more-methods-means-better-code-1d3b237f6cf2> [## 更多的方法意味着更好的代码

towardsdatascience.com](/more-methods-means-better-code-1d3b237f6cf2) 

回到我们的网格，我还将创建一个单独的函数来绘制一个空网格。因为我们在其他地方不需要这个函数，所以我将私下声明它。现在，我不会太关注任何细节，所以我会画一些空白的地方。我将把这些值存储在一个字典中。字典将包含带有整数索引的字符串，类似于我可能用来处理不同玩家数量的玩家类的方法。

无论如何…如果我先写代码，然后再解释，这将会更好，因为我认为这样的组合可能会更合适，并使系统作为一个整体更有意义。

## 网格

```
def empty_grid():
        self.grid = dict()
        str = ""
        for row in range(1, 10):
            str = ""
            for i in range(1, 10):
                str += "`"
            self.grid[row] = str
        return(self.grid)
```

我添加到这个类的第一个函数是用来创建一个空版本来添加我们的小玩家的函数。我将简单地用`“`"`字符填充一些字符串。我们将能够通过调用 self.grid 字典来索引我们正在处理的实际行，并且我们将能够使用字典字符串值对来分别按 char 设置索引。我们将在另一个网格函数中调用它:

```
def draw_grid():
        self.empty_grid()
```

请允许我通过一些简单的交互代码来解释这将会是什么，我将把这些代码写入我们的主函数中。在我们通过调用刚刚编写的 empty_grid()函数清空网格之后，我们现在将有一个新的表面可以查看。让我们继续绘制网格，首先用正则表达式创建一个新的打印字符串，返回 0 并跳过当前行。

```
def draw_grid():
        self.empty_grid()
        print_s = "\n"
```

别名 print_s 是 print string 的缩写。我们之前的数据，以及它未来的变化和一系列的正则表达式将成为我们最终的单行打印语句，只提供一种类型，这非常方便。我们将使用这个函数来测试 empty_grid()函数，方法是迭代地连接字符串，然后打印它们。这是我想到的:

```
def draw_grid():
        empty_grid()
        print_s = "\n"
        for key in self.grid:
            print_s = print_s + self.grid[key] + "\n"
        return(print_s)def empty_grid():
        self.grid = dict()
        str = ""
        for row in range(1, 10):
            str = ""
            for i in range(1, 10):
                str += "`"
            self.grid[row] = str
```

这两个函数完美地结合在一起，在视觉上改变了我们的类型。我想说的一件事是，如果这没有意义，或者看起来像我们在随机组件上工作，这是对形势的明智看法。目前，这看起来并不多，但是在编程中最大的障碍总是开始。这是您开始软件流程的地方，事物被抽象地定义，以便它们可以适合另一个组件。在许多情况下，程序员可能会选择先做逻辑，再做视觉。然而，在这种情况下，我认为首先处理视觉效果是很有意义的，这样我们就可以根据屏幕上实际需要发生的事情来设计逻辑。毕竟，这个项目的主要组成部分是视觉效果。不管怎样，现在已经完成了，我们要测试这两个函数，以确保它能正常工作。

## 布局初始化

现在，我们将花一点时间来关注初始化，以及更新整个打印输出所需的函数。这个更新函数现在将调用网格函数。我还必须创建一个清晰的()函数。

```
def clear():
    if name == 'nt':
        _ = system('cls')
    else:
        _ = system('clear')
```

这个函数是系统化的，并且是全局定义的，因为它的目的是用这个命令快速清除整个 REPL。它只是为相应的终端类型调用系统的 clear 命令。我们问名字是不是 NT，就像在 Windows NT 中一样，如果是就用 cls。如果不是这样，我们使用 clear，因为在大多数情况下，其他系统将是 Unix-line。下面是更新函数:

```
def update(self, message):
        clear()
        grid = self.draw_grid()
        print(grid)
        print(string("\n", message))
```

这里发生了几件事，首先，任何先前的输出被清除。之后我们在这个函数的作用域里赋一个变量叫做 grid，这个变量就是 self.draw_grid 的返回。我们不需要在这里调用 return，但是在这种情况下这是很方便的，因为我们根本不希望我们的网格在工作的时候被改变。如果我们为这样的定义使用类作用域，那么当这个函数运行时，它可能会在其他地方发生变化。

我们的 __init__ 函数就是用来总结所有这些的。将有更多的功能添加到这将扩展功能，但目前这是这个项目的核心功能。

```
def __init__(self, players):
        self.players = players
        update()
```

我在这里做的只是把类属性 players 赋给提供的参数 players，然后调用 update。现在，让我们全面看看这个类:

```
class PlayGrid:def __init__(self, players):
        self.players = players
        self.update("Hello")def update(self, message):
        clear()
        grid = self.draw_grid()
        print(grid)
        print(string("\n", message))def draw_grid(self):
        self.empty_grid()
        print_s = "\n"
        for key in self.grid:
            print_s = print_s + self.grid[key] + "\n"
        return(print_s)def empty_grid(self):
        self.grid = dict()
        str = ""
        for row in range(1, 10):
            str = ""
            for i in range(1, 10):
                str += "`"
            self.grid[row] = str
```

希望里面的一切都是正确的，但我想我们很快就会知道了。让我们运行这个宝贝:

```
[emmac@fedora CharacterClash]$ python3 character_clash.py
`````````
`````````
`````````
`````````
`````````
`````````
`````````
`````````
`````````Traceback (most recent call last):
  File "/home/emmac/dev/CharacterClash/character_clash.py", line 48, in <module>
    main()
  File "/home/emmac/dev/CharacterClash/character_clash.py", line 8, in main
    game = PlayGrid(players)
  File "/home/emmac/dev/CharacterClash/character_clash.py", line 16, in __init__
    self.update("Hello")
  File "/home/emmac/dev/CharacterClash/character_clash.py", line 22, in update
    print(string("\n", message))
```

> 哎哟

我犯了一个严重的“对不起，我是 Julia 程序员”的错误。我们需要使用加法运算符来连接这些字符串:

```
print("\n" + message)`````````
`````````
`````````
`````````
`````````
`````````
`````````
`````````
`````````Hello
Hello
```

# 演员

幸运的是，这个游戏是关于输出的—

> 在你的网络浏览器中，看着迷失的人工智能灵魂为你的娱乐而战斗到死。

因此，这些类在某种程度上可以完全随机化。这就是作为旁观者的好处，你不必参与其中。因此，对于这个奇观，我们不需要编程任何类型的输入，这使得这个玩家的过程容易得多。在以后的文章中，我将添加命令行参数，并进一步推进这个小项目。

另一件要注意的事情是，我们需要对网格做一些工作，也许是它未来的内容。我在想，如果我们在网格中添加一些不同的角色，它可能看起来更像随机的地面纹理——也就是说，因为它们不是让核心游戏工作所必需的，也许我会在未来的文章中讨论这个问题。让我们继续用所有的标准初始化材料创建一个玩家类，在此之前，我将为这个类列出一些数据值以供参考，以便为每个单独的类获得不同的统计数据:

```
# Sword # bow # assassin
# Classes = ["o/", "o)", "o-"]
# stats = [speed, damage, range, time]stats_dict = {"o/" : [2, 25, 2, 3],
"o)" : [2, 35, 3, 5],
"o-" : [3, 20, 3, 2]}
```

这是我们的基本类:

```
class Player:
    def __init__(self, pos):
        pass
```

## 加载数据

接下来，我们将把这些数据加载到这个类型中，还有一些其他的默认数据。

```
class Player:
    def __init__(self, pos):
        self.pos = []
        self.health = 100
        self.blocking = True
        self.attacking = False
        type = random.choice(stats_dict.keys())
        self.speed = stats_dict[type][1]
```

注意最后两行，首先我得到一个键的数组放入 random.choice 函数，然后产生一个选择，然后我们通过索引该键并从数组中提取值来应用数据。另外，Python 中的索引是从零开始的——所以我刚刚意识到代码中有一个小错误。无论如何，我们将对这些属性中的每一个都这样做:

```
class Player:
    def __init__(self, pos):
        self.pos = []
        self.health = 100
        self.blocking = True
        self.attacking = False
        type = random.choice(stats_dict.keys())
        self.speed = stats_dict[type][0]
        self.damage = stats_dict[type][1]
        self.range = stats_dict[type][2]
        self.time = stats_dict[type][3]
```

现在所有的数据都已经初始化了，让我们开始移动实际的字符。虽然我们可以使用 vector two 类型，或者类似的东西——也许可以创建我们自己的，但这不是我在这个例子中要做的。我觉得没有必要，因为索引这个位置向量很容易。查看添加了两个新方法头的完整类:

```
stats_dict = {"o/" : [2, 25, 2, 3],
"o)" : [2, 35, 3, 5],
"o-" : [3, 20, 3, 2]}
class Player:
    def __init__(self, pos):
        self.pos = []
        self.health = 100
        self.blocking = True
        self.attacking = False
        type = random.choice(stats_dict.keys())
        self.speed = stats_dict[type][0]
        self.damage = stats_dict[type][1]
        self.range = stats_dict[type][2]
        self.time = stats_dict[type][3]
        self.symbol = type def walk(self, pos):
        pass def move(self, players):
        pass
```

move(players)函数用于获取玩家数组，并基于此做出某种选择。现在，这一切都将被搁置，因为我们现在实际上要回到我们的旧 PlayGrid 类，然后开始映射这些球员的位置。

# 组合元素

我们需要在我们的 PlayGrid 类中定义一个新函数，以便从前面的网格字典中获取并修改它来包含这些字符。好消息是，我们可以简单地使用索引在适当的位置显示我们的玩家。

```
class PlayGrid:
        # Essentials
    def __init__(self, players):
        self.players = players
        self.update("Character Crash Game Started")def update(self, message):
        clear()
        grid = self.draw_grid()
        print(grid)
        print("\n" + message)# Player Management
    def draw_players(grid):
```

## 绘图播放器

我们的新功能 draw_players(grid)将简单地获取玩家及其各自的索引，然后将玩家角色放在这些索引处，取代之前的位置。我们要做的第一件事是决定向哪个方向绘制字符。换句话说，字符是面向右还是面向左:

```
for player in self.players:
            # True = right, False = left
            if player.facing == True
                modifier = 1
            else:
                modifier = -1
```

我们需要将这个修饰符添加到一个索引中，以确定该值应该在字符的后面还是前面。我们将在玩家类中处理剩下的部分。我们暂时不会做所有的事情，因为我们有一个函数要写。你可能已经注意到我也打开了一个 for 循环。这是至关重要的，因为我们需要单独调用每个球员的数据来做我们需要用它做的工作。

这背后的方法很简单。在字典中，坐标平面的 y 是键。正如我们在 empty_grid()函数中所做的那样，这些只是由一个范围生成器生成的。然后我们有 x，它是字典的值对。记住，要在一个特定的位置设置一个字符，我们需要用我们的 y 键索引字典，这是我们的 pos 列表中的位置 2，然后我们需要用我们的 x 值索引它的返回，这是我们需要替换的字符在我们的字符串中的位置。

```
# [0] = x, [1] = y
            newpos = player.pos
            x, y = newpos[0]
            grid[y][x] = player.symbol[0]
            grid[y][x + modifier] = player.symbol[1]
```

最后，我们将返回网格，正如我之前提到的，我们将不再使用 class 属性，因为我们将在最后更新它。

```
def draw_players(grid):
        for player in self.players:
            # True = right, False = left
            if player.facing == True
                modifier = 1
            else:
                modifer = -1
                # [0] = x, [1] = y
            newpos = player.pos
            x, y = newpos[0]
            grid[y][x] = player.symbol[0]
            grid[y][x + modifier] = player.symbol[1]
        return(grid)
```

现在我们已经写好了这个函数，我们要再写一个函数，叫做 make_moves(players)。这个函数将调用我们玩家的移动函数。

```
def make_moves(players):
        [player.move(players) for player in players]
        return
```

从这个意义上说，移动不像从[x，y]到[x，y]，这就是我们 walk()函数的作用。相反，我们的移动功能指定轮到他们做什么。现在，我们将回到我们的球员类，并整理出一个基本的结构，这个东西最初可能会对其环境作出反应。在未来，我将为这个项目实现一个机器学习算法，这将使这个项目变得更酷。

现在，我只想看看一些运动可能是什么样子，记住，我要试着写一个简单的小行走模式:

```
def move(self, players):
        if self.blocking == False
            self.pos += 1
            self.blocking = True
        elif self.blocking == True:
            self.pos -= 1
            self.blocking = Falseself.blocking = False
```

这个基本的小函数只是让我们的玩家在网格上走来走去，让我们稍微包装一下我们的主函数，测试一下数据和显示的关系。

```
def move(self, players):
        if self.blocking == False:
            self.pos += 1
            self.blocking = True
        if self.blocking == True:
            self.pos -= 1
            self.blocking = False# self.blocking = False
```

在不久的将来，唯一保留下来的代码是被注释掉的部分。在未来，这将完全是随机的，直到我在下一篇文章中加入一些人工智能。既然我们在这里，我们不妨添加前面的 facing 属性:

```
class Player:
    def __init__(self, pos):
        self.pos = []
        self.health = 100
        self.blocking = True
        self.attacking = False
        type = random.choice(stats_dict.keys())
        self.speed = stats_dict[type][0]
        self.damage = stats_dict[type][1]
        self.range = stats_dict[type][2]
        self.time = stats_dict[type][3]
        self.symbol = type
        self.facing = True
```

# 到目前为止…

到目前为止，我们已经制作了一个玩家网格和将居住在该网格上的玩家。我们需要看看到目前为止所有的代码是否都有效。我们现在需要做的就是稍微调整一下我们的主函数，将一个玩家添加到我们的玩家列表中。另一个随机注意，我也调整了 REPL 打印输出的尺寸。这意味着网格现在比以前大得多。

```
def main():
    players = []
    game = PlayGrid(players)
    game.update("Hello")
#    while len(game.players) < 1:
    sleep(2)
```

我们需要在玩家列表中添加一个玩家。这相当简单，我们将创建一个新玩家——毕竟，它目前唯一需要的是一个位置。下面是修改后的 main()函数:

```
def main():
    players = []
    players.append(Player([5, 6]))
    game = PlayGrid(players)
    game.update("Up")
#    while len(game.players) < 1:
    sleep(2)
    game.update("Down")
    sleep(2)
    game.update("Up")
    sleep(2)
    game.update("Down")
```

希望我没记错！

```
[emmac@fedora CharacterClash]$ python3 character_clash.pyFile "/home/emmac/dev/CharacterClash/character_clash.py", line 43, in draw_players
    x, y = newpos[0], newpos[1]
IndexError: list index out of range
```

> 让我们看一看…

问题来自这里:

```
class Player:
    def __init__(self, pos):
        self.pos = []
```

我的意思是提供 pos，然后把它设置成那样，但是它被设置成一个空列表——有趣。

```
File "/home/emmac/dev/CharacterClash/character_clash.py", line 44, in draw_players
    grid[y][x] = player.symbol[0]
TypeError: 'str' object does not support item assignment
```

哦，糟糕，看起来我解决这个问题的方法是愚蠢的。这可能比预期的要多一点。幸运的是，有一些很好的方法可以解决这个问题，其中一些我可能在我的 Pythonic 标签处理综合指南中提到过，您可以在这里查看:

</essential-python-string-processing-techniques-aa5be43a4f1f>  

> 这次失败的真正原因是，Julia 允许你做任何事情，所以如果我想替换一个字符串索引，我可以导入并扩展索引方法来实现… Julia 太棒了，它毁了我的这个项目。

# 解决我们的问题

为了解决这个问题，我们将通过使它变得非常简单来反抗 Python 之类的东西。我们要做的第一件事是将字符串转换成列表类型。我们知道我们可以设置这种类型的索引，所以我们知道这种方法会有效。然后，我们将使用 str.join()将我们的字符串与新的字符串列表连接起来。

```
>>> list("Hello")
['H', 'e', 'l', 'l', 'o']
>>> "".join(list("Hello"))
'Hello'
>>>
```

让我们回头看看导致这种情况的函数:

```
def draw_players(self, grid):
        for player in self.players:
            # True = right, False = left
            if player.facing == True:
                modifier = 1
            else:
                modifer = -1
                # [0] = x, [1] = y
            newpos = player.pos
            x, y = newpos[0], newpos[1]
            grid[y][x] = player.symbol[0]
            grid[y][x] + modifier] = player.symbol[1]
        return(grid)
```

我们将从将网格转换成 for 循环底部的列表开始:

```
newpos = player.pos
current = list(grid[newpos[1]])
```

现在我们有了 current，这是我们当前列的一个字符串，它是通过获取我们的 y 值获得的，y 值是我们的 newpos 列表中的第二个位置(1，不是 2)。

这是最后一个新函数:

```
def draw_players(self, grid):
        for player in self.players:
            # True = right, False = left
            if player.facing == True:
                modifier = 1
            else:
                modifer = -1
                # [0] = x, [1] = y
            newpos = player.pos
            current = list(grid[newpos[1])current[newpos[0]] = player.symbol[0]
            current [newpos + modifier] = player.symbol[2]
            current = "".join(current)
            grid[y] = current
        return(grid)
```

老实说，这里有很多地方我不得不修改，但这里是对该函数的最后一次检查，它现在工作得非常完美:

```
def draw_players(self, grid):
        for player in self.players:
            # True = right, False = left
            if player.facing == True:
                modifier = 1
            else:
                modifer = -1
                # [0] = x, [1] = y
            newpos = player.pos
            current = list(grid[newpos[1]])
            current[newpos[0]] = player.symbol[0]
            current[newpos[0] + modifier] = player.symbol[1]
            current = "".join(current)
            self.grid[newpos[1]] = current
```

我也不得不在这里和那里做一些调整，主要是

*   不得不调整播放器的 move()函数，位置正在调用。由于某种原因，它们没有被编入索引。
*   有几个愚蠢的索引错误，还有一些地方我忘了写自己。
*   我必须稍微修改一下主函数，以及 draw_grid()、empty_grid()和 update()函数的返回。

这是我们的新班级:

```
class PlayGrid:
        # Essentials
    def __init__(self, players):
        self.players = players
        self.update("Character Clash Game Started")def update(self, message):
        clear()
        self.empty_grid()
        self.draw_players(self.grid)
        self.make_moves()
        print(self.draw_grid())
        print("\n" + message)# Player Management
    def draw_players(self, grid):
        for player in self.players:
            # True = right, False = left
            if player.facing == True:
                modifier = 1
            else:
                modifer = -1
                # [0] = x, [1] = y
            newpos = player.pos
            current = list(grid[newpos[1]])
            current[newpos[0]] = player.symbol[0]
            current[newpos[0] + modifier] = player.symbol[1]
            current = "".join(current)
            self.grid[newpos[1]] = currentdef make_moves(self):
        [player.move(self.players) for player in self.players]# Grid
    def draw_grid(self):
        print_s = "\n"
        for key in self.grid:
            print_s = print_s + self.grid[key] + "\n"
        return(print_s)def empty_grid(self):
        self.grid = dict()
        str = ""
        for row in range(1, 30):
            str = ""
            for i in range(1, 100):
                str += "`"
            self.grid[row] = str
```

这是我们新的 main()函数:

```
def main():
    players = []
    players.append(Player([5, 6]))
    game = PlayGrid(players)
    game.update("Up")
#    while len(game.players) < 1:
    sleep(2)
    game.update("Down")
    sleep(2)
    game.update("Up")
    sleep(2)
    game.update("Down")
```

现在让我们运行它！

```
[emmac@fedora CharacterClash]$ python3 character_clash.py
```

![](img/7595e258b0e9554f0604b8476398f135.png)

> 还不错！

# 运动/寻路

我们需要克服的下一个大障碍是运动。我们如何让角色决定如何在每一帧上移动？好吧，我们将从在课堂上加入一些新的数据开始，来表明我们周围世界的一些事情。每当我为这个项目编写一些人工智能程序时，这些都会成为我们模型的特征。在我们深入研究之前，我还想提一件事——到目前为止，该项目的代码在核心功能分支中，我们现在将转移到战斗分支。这个分支将会更加专注于移动和战斗，这样我们的新外形将会真正的发挥作用。

这是我们之前工作过的分支的链接:

<https://github.com/emmettgb/characterclash/tree/0.0.1-basic-functionality>  

这里有一个链接指向我们现在所在的网站:

<https://github.com/emmettgb/characterclash/tree/0.0.2-combat>  

让我们回到移动函数:

```
def move(self, players):
        if self.blocking == False:
            self.pos[1] -= 1
            self.blocking = True
        elif self.blocking == True:
            self.pos[1] += 1
            self.blocking = False
```

如前所述，我们可以删除所有这些代码，除了将 blocking 设置为 false 的第一件事，如果玩家决定阻止，可以在最后将其切换回来。

## 移动()

```
def move(self, players):
         self.blocking = False
```

我们需要做的第一件事是评估其他玩家的位置，以及我们作为玩家的状态。这个类可以帮我们做到这一点，所以我添加了更多的属性:

```
class Player:
    def __init__(self, pos):
        self.pos = pos
        self.health = 100
        self.blocking = True
        self.attacking = False
        type = random.choice(["o/", "o)", "o-"])
        self.speed = stats_dict[type][0]
        self.damage = stats_dict[type][1]
        self.range = stats_dict[type][2]
        self.time = stats_dict[type][3]
        self.symbol = type
        self.facing = True
        self.attacking = False
        self.pursuing = None
        self.attackavailable = False
        self.attacks_available = []
        self.turns = 0
```

self.turns 值将在 turn 系统中发挥作用，我们将在此之后为其创建一个经理。一旦我们到了那里，我们将详细讨论这个问题。现在，让我们把重点放在指导这些玩家做什么的功能上:

```
def move(self, players):
         self.blocking = False
         self.attacking = False
         selection = 1
         selections = []
         param = ""
```

第一件事是初始化一些变量。有很多这样的方法，但有一个很好的理由——这是一种创建一些基于条件的行为的简单方法，但该算法肯定是有意义的，并且有可能被扩展。一旦该说的都说了，该做的都做了，我打算让这个类调用 AI。我还添加了将攻击设置为假，因为如果我们现在移动，我们不能做任何一件事——当我们回顾核心游戏规则和管理系统如何工作时，这可能更有意义。

接下来，我们将进入一个奇怪的迭代循环，它只需要评估事物，以得出三个结论之一，走到某个地方，阻止或攻击某个东西:

```
for player in players:
             if player.pos[1] == self.pos[1] and player.pos[0] == self.pos[0]:
                 pass
             else:
                 if attackavailable == True:
                     # walk = 1, block = 2, attack = 3
                     if self.health > 45 and index in attacks_available:
                         if player.attacking == True:
                             selection = 3
                             self.pursuing = index
                         else:
                         if player.health > 35 and self.health < 50:
                                 self.pursuing = player.pos
                                 selection = 2
                 else:
                     selection = random.choice([1, 2, 3])
             selections.append(selection)
```

那里的格式转换很糟糕，但仍然清晰可辨，只是不要把这种缩进当成现实。这个循环也很可怕，而且它出现在主事件循环中有点吓人，但是我怀疑我们会遇到很多这样的问题，此外，这只是我将在以后的文章中做的一些迭代工作的临时占位符。无论如何，接下来我要对选择进行舍入，得到一组选择的平均值。

```
mu = sum(selections) / len(selections)
         selection = int(round(mu))
```

最后，我会对每个决策进行函数调用:

```
if selection == 1:
             if self.pursuing != None:
                 self.pursue()
             else:
                 self.random_walk()
         if selection == 2:
              pass
         if selection == 3:
              pass
```

这也使得机器学习部分主要只是猜测分类特征，尽管只有一个参数。目前，我们所有可能被调用或实际执行的操作将是 random_walk()方法，这是我刚刚编写的——然而，我实际上并没有添加 pursue()函数，这是一个原因，我想用一秒钟的时间在这里展示，但首先让我们看看 random_walk 函数:

```
def random_walk(self):
                # 1 r, 2 l, 3 up, 4, down
        dir = random.choice([1, 2, 3, 4])
        if dir == 1:
            self.pos[0] += self.speed
        elif dir == 2:
            self.pos[0] -= self.speed
        elif dir == 3:
            self.pos[1] += self.speed
        self.turns = 1
```

这个函数所做的基本上就是选择一个随机的方向行走，然后朝那个方向行进。你可能已经注意到了最后的回合功能，每当我们用主控制器完成这个并运行我们的第一个 REPL 中角色间战争的模拟时，这个功能会更有意义。

## 阻挡/攻击

如果您还记得，前面我说过我没有在这个类中添加 pursue()函数。我这样做的原因是为了测试追求价值的保真度。这是因为无论何时调用该方法，我们都会得到一个错误。然而，我们还需要一个函数来实现这个功能，这个函数就是攻击可用函数。为了开始这个函数，我要写一个和我们之前写的一样的循环。唯一不同的是，这次我想确定一个值是否在攻击范围内，这是我第一次尝试这样的函数:

```
def attack_available(self, players):
        for player in players:
            if player.pos[0] != self.pos[0] and self.pos[1] != player.pos[1]:
                if abs(player.pos[0] - self.pos[0]) <= self.range:
                    self.attacks_available.append(player.id)
                elif abs(player.pos[1] - self.pos[1]) <= self.range:
                    self.attacks_available.append(player.id)
```

这有些完美，有些不完美。现在，我相信它会很好地为我们服务。现在让我们转到 main()函数，并向我们的输出添加另一个播放器类:

```
def main():
    players = []
    players.append(Player([5, 6], 1))
    players.append(Player([40, 20], 2))
    game = PlayGrid(players)
    for i in range(1, 25):
        sleep(3)
        game.update("".join(["Iteration: ", str(i)]))
```

这段代码运行完美。现在让我们稍微润色一下。

## 润色

我决定放弃任何级别的路径寻找，并期待将人工智能放在它的位置上，因为代码相当粗糙，也不是真的需要。所有这一切意味着，就目前而言，这些角色没有遵循任何策略，除了随机性。我想复习一下我做的修饰。首先，我重写了行走函数，包括随机行走和行走函数。

```
def random_walk(self):
                # 1 r, 2 l, 3 up, 4, down
        dir = random.choice([1, 2, 3, 4])
        self.walk(dir)def walk(self, dir):
        if dir == 1:
            if not self.pos[0] + self.speed >= CHAR_H - 1:
                self.pos[0] += self.speed
                self.facing = Trueelif dir == 2:
            if not self.pos[0] - self.speed <= 2:
                self.pos[0] -= self.speed
                self.facing = Falseelif dir == 3:
            if not self.pos[0] - self.speed <= 2:
                self.pos[1] -= self.speed
        elif dir == 4:
            if not self.pos[0] + self.speed >= CHAR_W - 1:
                self.pos[1] += self.speed
        self.turns += 1
```

在这个函数中，我还必须添加一个条件来确保字符不会离开边缘。最后，我更新了主函数，它现在将运行 50 步棋，假设所有 50 步棋都有效，那么这应该是一个工作项目！这是最后一次查看这些类和 main()函数:

```
def main():
    players = []
    players.append(Player([11, 20], 0))
    players.append(Player([5, 6], 1))
    players.append(Player([20, 10], 2))
    game = PlayGrid(players)
    for i in range(1, 50):
        sleep(.5)
        game.update("".join(["Iteration: ", str(i)]))class PlayGrid:
        # Essentials
    def __init__(self, players):
        self.players = players
        self.update("Character Clash Game Started")def update(self, message):
        clear()
        self.empty_grid()
        self.draw_players(self.grid)
        self.make_moves()
        print(self.draw_grid())
        print("\n" + message)# Player Management
    def draw_players(self, grid):
        for player in self.players:
            modifier = 0
            # True = right, False = left
            if player.facing == True:
                modifier = 1
            else:
                modifer = -1
                # [0] = x, [1] = y
            newpos = player.pos
            current = list(grid[newpos[1]])
            current[newpos[0]] = player.symbol[0]
            current[newpos[0] + modifier] = player.symbol[1]
            current = "".join(current)
            self.grid[newpos[1]] = currentdef make_moves(self):
        [player.move(self.players) for player in self.players]# Grid
    def draw_grid(self):
        print_s = "\n"
        for key in self.grid:
            print_s = print_s + self.grid[key] + "\n"
        return(print_s)def empty_grid(self):
        self.grid = dict()
        str = ""
        for row in range(1, CHAR_W):
            str = ""
            for i in range(1, CHAR_H):
                str += "`"
            self.grid[row] = str# Sword # bow # assassin
# Classes = ["o/", "o)", "o-"]
# stats = [speed, damage, range, time]stats_dict = {"o/" : [2, 25, 2, 3],
"o)" : [2, 35, 3, 4],
"o-" : [3, 20, 1, 2]}
class Player:
    def __init__(self, pos, id):
        self.id = id
        self.pos = pos
        self.health = 100
        self.blocking = True
        self.attacking = False
        type = random.choice(["o/", "o)", "o-"])
        self.speed = stats_dict[type][0]
        self.damage = stats_dict[type][1]
        self.range = stats_dict[type][2]
        self.time = stats_dict[type][3]
        self.symbol = type
        self.facing = True
        self.attacking = False
        self.pursuing = None
        self.attackavailable = False
        self.attacks_available = []
        self.turns = 0
        # Base
    def random_walk(self):
                # 1 r, 2 l, 3 up, 4, down
        dir = random.choice([1, 2, 3, 4])
        self.walk(dir)def walk(self, dir):
        if dir == 1:
            if not self.pos[0] + self.speed >= CHAR_H - 1:
                self.pos[0] += self.speed
                self.facing = Trueelif dir == 2:
            if not self.pos[0] - self.speed <= 2:
                self.pos[0] -= self.speed
                self.facing = Falseelif dir == 3:
            if not self.pos[0] - self.speed <= 2:
                self.pos[1] -= self.speed
        elif dir == 4:
            if not self.pos[0] + self.speed >= CHAR_W - 1:
                self.pos[1] += self.speed
        self.turns += 1# Behaviors
    def attack_available(self, players):
        for player in players:
            if player.pos[0] != self.pos[0] and self.pos[1] != player.pos[1]:
                if abs(player.pos[0] - self.pos[0]) <= self.range:
                    self.attacks_available.append(player.id)
                elif abs(player.pos[1] - self.pos[1]) <= self.range:
                    self.attacks_available.append(player.id)def move(self, players):
         self.attacks_available = []
         self.blocking = False
         self.attacking = False
         self.attack_available(players)
         selection = 1
         selections = [1, 1, 1, 1, 2, 2]
         if len(self.attacks_available) > 0:
             selections.append(3)
         selection = random.choice(selections)
         if selection == 1:
             if self.pursuing != None:
                 self.pursue()
             else:
                 self.random_walk()
         if selection == 2:
              self.blocking = True
              self.turns += 1
         if selection == 3:
             self.attacking = True
             self.call_attack()
    def call_attack(self):
        pass
    def pursue(self):
        pass
```

# 结论

我发现这个项目非常有趣和令人兴奋，我希望那些阅读的人也一样。我想通过构建这个软件来展示这么多随机的很酷的东西，但总的来说，我认为做这样的事情然后交流它们只是娱乐性的。这个项目肯定是一个了不起的项目。

当我们继续这部分的工作时，这段代码所需要的只是一些攻击代码，以及一个运行这些攻击的管理器，以及其他与游戏逻辑规则相比较的东西。非常感谢你的阅读，我希望这个项目对你来说是尽可能愉快的，我希望你对我将要把它进行到的长度感到兴奋！祝你有美好的一天！

> 还有一件事，这是我们创作的 GIF:

![](img/621f6a5137b9d497c5d6dc50d769e852.png)