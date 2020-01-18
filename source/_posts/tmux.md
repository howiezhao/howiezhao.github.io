---
title: tmux小记
date: 2018-09-18 12:10:07
categories: CheatSheet
tags:
  - Linux
---

[tmux](https://github.com/tmux/tmux)是一款优秀的**终端复用**工具，在Ubuntu下，使用`sudo apt install tmux`即可安装，输入`tmux`即可开始使用。与tmux相似的软件还有[Screen](https://www.gnu.org/software/screen/)等。

## 名词解释
### Session（会话）
当输入`tmux`后，实际上创建了一个Session，你可以在这个Session里创建多个Window，在Window里创建多个Pane。
### Window（窗口）
Window是显示给你的一整片窗口，你可以创建多个Window，在一个Window里面你又可以创建多个Pane，以此来执行多个任务。
### Pane（窗格/面板）
Pane是tmux中的最小单位，每个Pane相当于一个终端。
<!--more-->
一个常见的tmux运行效果可能如下图所示：
![tmux](/images/tmux.jpg)
其中，Window被分成了3个Pane，每个Pane之间通过**Pane Border**（面板分隔符）加以区分。Window底部则是**Status Bar**（状态栏），状态栏从左往右依次被分为**左面板**、**窗口列表**、**右面板**。按照上图所示，其中左面板显示了Session的名称，窗口列表则显示了当前Window的索引值和名称，最后右面板依次显示了计算机名称、时间、日期。

## 命令
`tmux`命令拥有众多参数，如下所示：
- `tmux -V`：显示tmux版本号
- `tmux ls`或`tmux list-sessions`：列出所有tmux Session
- `tmux a`或`tmux attach`：连接（attach）到上一次的Session
- `tmux a -t 0`：连接到名为0的Session
- `tmux new -s basic`或`tmux new-session -s basic`：新建名为basic的Session，若不指定`-s`参数，则默认按数字命名
- `tmux kill-session -t foo`：删除名为foo的Session
- `tmux kill-server`：删除所有Session
- `tmux source ~/.tmux.conf`：重载配置文件

## 快捷键
tmux中的绝大部分操作都需要一个**快捷键前缀**加上相应的指令，tmux中默认的快捷键前缀是`Ctrl + b`，举例来说，使用`prefix + %`可以将当前Window分为左右两个Pane，这实际上是说，先按下`Ctrl + b`，再按下`%`，即可完成操作。值得注意的是，tmux默认的快捷键前缀是很糟糕的，因为很多程序都会使用到`Ctrl + b`，但同时，快捷键前缀也是可以自定义的。常用的快捷键如下：
- Session
    - `prefix + d`：离开（datach）当前Session，即退出tmux
- Window
    - `prefix + c`：创建（create）一个新的Window
    - `prefix + n`：切换到下一个（next）Window
    - `prefix + p`：切换到上一个（previous）Window
    - `prefix + &`：关闭当前Window
- Pane
    - `prefix + %`：将当前光标所在Pane分为左右两个Pane
    - `prefix + "`：将当前光标所在Pane分为上下两个Pane
    - `prefix + o`：在多个Pane之间切换光标，或按上下左右键
    - `prefix + x`：关闭当前光标所在Pane
    - `prefix + ?`：查看快捷键列表
    - `prefix + :`：进入命令行模式（类似Vim）
    - `prefix + 空格键`：依次轮回使用tmux预定义的Pane布局

值得注意的是，当创建Session后，默认会创建一个Window，当创建Window后，默认会创建一个Pane。

## .tmux.conf
`$HOME/.tmux.conf`文件是tmux的配置文件，tmux在启动时会按照此文件中的命令进行相关配置，个人常用的配置如下：
```
# 设定快捷键前缀
unbind-key C-b
set-option -g prefix C-x
bind-key C-x send-prefix
set-option -g escape-time 0

# 开启鼠标模式
set -g mouse on
```

## 插件
tmux支持许多插件，在安装插件之前最好先安装插件管理器[TPM](https://github.com/tmux-plugins/tpm)，使用如下命令即可下载TPM：
```
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```
下载完之后，只需在`.tmux.conf`文件底部添加相关配置，然后进入tmux输入`prefix + I`，即可自动下载并安装相应的插件，升级插件可使用`prefix + U`。个人常用的插件如下：
相应的，`.tmux.conf`文件中插件相关的配置项如下：
```
# 插件
# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'git@github.com/user/plugin'
# set -g @plugin 'git@bitbucket.com/user/plugin'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run -b '~/.tmux/plugins/tpm/tpm'
```
值得注意的是，在更改`.tmux.conf`文件后，应该重启tmux，或者重载配置文件。

## 更多
有关tmux的更多使用技巧可以参考[《tmux: Productive Mouse-Free Development》](https://www.kancloud.cn/kancloud/tmux)一书。