---
title: tmux 小记
date: 2018-09-18 12:10:07
categories: CheatSheet
tags:
  - Linux
---

[tmux](https://github.com/tmux/tmux) 是一款优秀的**终端复用**和**会话管理**工具，在 Ubuntu 下，使用 `sudo apt install tmux` 即可安装，输入 `tmux` 即可开始使用。与 tmux 相似的软件还有 [Screen](https://www.gnu.org/software/screen/) 等。

## 名词解释

### Session（会话）

当输入 `tmux` 后，实际上创建了一个 Session，你可以在这个 Session 里创建多个 Window，在 Window 里创建多个 Pane。

### Window（窗口）

Window 是显示给你的一整片窗口，你可以创建多个 Window，在一个 Window 里面你又可以创建多个 Pane，以此来执行多个任务。

### Pane（窗格/面板）

Pane 是 tmux 中的最小单位，每个 Pane 相当于一个终端。

<!--more-->

一个常见的 tmux 运行效果可能如下图所示：

![tmux](/images/tmux.jpg)

其中，Window 被分成了 3 个 Pane，每个 Pane 之间通过 **Pane Border**（面板分隔符）加以区分。Window 底部则是**Status Bar**（状态栏），状态栏从左往右依次被分为**左面板**、**窗口列表**、**右面板**。按照上图所示，其中左面板显示了 Session 的名称（`[basic]`），窗口列表则显示了当前 Window 的索引值和名称（`0:~*`），最后右面板依次显示了计算机名称、时间、日期（`"DESKTOP-06THPMM" 16:29 30-Jul-19`）。

## 命令

`tmux` 命令拥有众多参数，如下所示：

- `tmux -V`：显示 tmux 版本号
- `tmux ls` 或 `tmux list-sessions`：列出所有 tmux Session
- `tmux a` 或 `tmux attach`：连接（attach）到上一次的 Session
- `tmux a -t 0`：连接到名为 `0` 的 Session
- `tmux new -s basic` 或 `tmux new-session -s basic`：新建名为 `basic` 的 Session，若不指定 `-s` 参数，则默认按数字命名
- `tmux kill-session -t foo`：删除名为 `foo` 的 Session
- `tmux kill-server`：删除所有 Session
- `tmux source ~/.tmux.conf`：重载配置文件

## 快捷键

tmux 中的绝大部分操作都需要一个**快捷键前缀**加上相应的指令，tmux 中默认的快捷键前缀是 `Ctrl + b`，举例来说，使用 `prefix + %` 可以将当前 Window 分为左右两个 Pane，这实际上是说，先按下 `Ctrl + b`，再按下 `%`，即可完成操作。值得注意的是，tmux 默认的快捷键前缀是很糟糕的，因为很多程序都会使用到 `Ctrl + b`，但同时，快捷键前缀也是可以自定义的。常用的快捷键如下：

- Session
  - `prefix + d`：离开（datach）当前 Session，即退出 tmux
- Window
  - `prefix + c`：创建（create）一个新的 Window
  - `prefix + n`：切换到下一个（next）Window
  - `prefix + p`：切换到上一个（previous）Window
  - `prefix + &`：关闭当前 Window
- Pane
  - `prefix + %`：将当前光标所在 Pane 分为左右两个 Pane
  - `prefix + "`：将当前光标所在 Pane 分为上下两个 Pane
  - `prefix + o`：在多个 Pane 之间切换光标，或按上下左右键
  - `prefix + x`：关闭当前光标所在 Pane
  - `prefix + ?`：查看快捷键列表
  - `prefix + :`：进入命令行模式（类似 Vim）
  - `prefix + 空格键`：依次轮回使用 tmux 预定义的 Pane 布局

值得注意的是，当创建 Session 后，默认会创建一个 Window，当创建 Window 后，默认会创建一个 Pane。

## .tmux.conf

`$HOME/.tmux.conf` 文件是 tmux 的配置文件，tmux 在启动时会按照此文件中的命令进行相关配置，个人常用的配置如下：

```text
# 设定快捷键前缀
unbind-key C-b
set-option -g prefix C-x
bind-key C-x send-prefix
set-option -g escape-time 0

# 开启鼠标模式
set -g mouse on
```

## 插件

tmux 支持许多插件，在安装插件之前最好先安装插件管理器 [TPM](https://github.com/tmux-plugins/tpm)，使用如下命令即可下载 TPM：

```sh
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

下载完之后，只需在 `.tmux.conf` 文件底部添加相关配置，然后进入 tmux 输入 `prefix + I`，即可自动下载并安装相应的插件，升级插件可使用 `prefix + U`。个人常用的插件如下：
相应的，`.tmux.conf` 文件中插件相关的配置项如下：

```text
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

值得注意的是，在更改 `.tmux.conf` 文件后，应该重启 tmux，或者重载配置文件。

## 更多

有关 tmux 的更多使用技巧可以参考[《tmux: Productive Mouse-Free Development》](https://www.kancloud.cn/kancloud/tmux)一书。
