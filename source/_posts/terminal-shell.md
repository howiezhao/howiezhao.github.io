---
title: terminal与shell
date: 2018-09-19 17:00:22
categories: CheatSheet
tags:
  - Linux
---

terminal，常被翻译为**终端**，一般指黑色的窗口，终端可以设置字体、大小、布局和颜色等。Windows中常见的第三方终端有ConEmu、Cmder等。

shell，有时也被翻译为壳层，通常指操作系统中位于用户与内核之间的一层，主要用于和用户交互，因此，shell分为两类：命令行界面（CLI）和图形用户界面（GUI）。现在所指的shell通常指命令行shell，Linux中常见的命令行shell有bash、Zsh等。

通俗点说，terminal属于外层，shell属于内层，terminal包裹着shell，输入进terminal的命令要由shell去解释执行。
<!--more-->
和terminal很像的一个东西叫console，常被翻译为**控制台**，它也是一个黑色的窗口，用来输入命令，但与terminal不同的是，console与物理相关，且具有**唯一性**。举例来说，没有图形界面的Linux开机后，显示在屏幕上的就是console，它是与这台电脑相关的，且只有一个；而有图形界面的Linux开机后，打开的黑色窗口就是terminal，你可以打开多个。

在Windows中，这一切有点混乱，具体就表现在：那个黑色的窗口应该叫**命令提示符**还是**控制台窗口**？就如下图所示：
![cmd](/images/cmd.jpg)
首先，命令提示符的本意指的是命令行前面的提示符，在Linux中常被称为prompt，如下所示：
![prompt](/images/prompt.jpg)
显然，在Windows中，命令提示符指的是一种解释执行命令的shell，此外，控制台窗口应该指的是终端。因此，在Windows中有两种shell，即命令提示符和PowerShell，它们都共用了同一终端，即控制台窗口。这么理解的原因可参考微软的[官方文档](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)，摘录如下：
>Windows has two command shells: The Command shell and PowerShell.

与Linux不同的是，Windows为每个shell都做了一个可执行程序，如命令提示符是`cmd.exe`，而PowerShell是`powershell.exe`，所以在Windows中我们习惯说“打开命令提示符”或者“打开PowerShell”；而在Linux中，我们更习惯说“打开终端”。

值得注意的是，在Windows 10的最新版本中，微软推出了全新的**Windows Terminal**，用以取代老旧且功能匮乏的控制台窗口。