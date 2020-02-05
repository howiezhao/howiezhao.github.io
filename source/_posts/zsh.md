---
title: 使用 Zsh 替代 Bash
date: 2018-09-18 12:09:36
categories: CheatSheet
tags:
  - Linux
---

众所周知，Bash 几乎是所有 Linux 发行版预装的 Shell，但 Zsh 却能带给你更强大的功能。

## 安装

首先，执行 `echo $SHELL` 可以查看你当前所使用的 Shell，如果不是 Zsh，则可以接着执行 `cat /etc/shells` 查看你当前系统所支持的 Shell，如果里面没有 Zsh（在 macOS 中是自带 Zsh 的），则你需要下载安装 Zsh，在 Ubuntu 中，只需要 `sudo apt install zsh` 一条命令即可，启用也很简单，`chsh -s $(which zsh)` 即可（执行完此命令后通常需要重启一下才能生效），但它的配置却相当复杂，由此诞生了 [Oh My Zsh](https://ohmyz.sh/) 项目，该项目的主要目的是简化 Zsh 的配置。

Oh My Zsh 的官网给出了利用 `curl` 或 `wget` 安装的详细命令，具体如下：

```bash
# 安装 Oh My Zsh 前需要安装 git（`sudo apt install git`）
# 通过 curl 安装
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
# 通过 wget 安装
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

安装完成后，会在当前用户的家目录下生成多个隐藏文件：
其中 `.zshrc` 类似于 `.bashrc`，存放 zsh 的配置信息；
`.zsh_history` 类似于 `.bash_history`，存放 zsh 的命令历史记录；
`.oh-my-zsh` 的文件夹则是 Oh My Zsh 项目 GitHub 仓库的克隆版，其中的 `themes` 文件夹下主要存放自带的主题，`plugins` 文件夹下主要存放自带的插件，`custom` 文件夹下主要存放用户自己下载的主题和插件。
<!--more-->
## 配置

Oh My Zsh 的主要配置都位于 `$HOME/.zshrc` 文件中，主要配置如下：

```bash
# 配置主题，默认为自带的 robbyrussell 主题，
# 个人喜欢自带的 ys 主题
ZSH_THEME="ys"

# 启动错误命令自动更正，默认是注释的
ENABLE_CORRECTION="true"

# 在命令执行的过程中，使用小红点进行提示
# 默认是注释的
COMPLETION_WAITING_DOTS="true"

# 配置插件，默认只启用了自带的 git 插件,
# 要启用更多的插件可直接在括号中写入，
# 必须是自带的插件或已下载到指定位置的插件
plugins=(
  git
)
```

## 插件

Zsh 的强大之处就在于它有相当多的插件，只需安装相关插件，并进行配置，即可体验相应功能。Oh My Zsh 安装并启用插件相当简便，所以，可把 Oh My Zsh 当成是一个 Zsh 的插件管理器。个人常用的插件如下：

### git

Oh My Zsh 自带的插件，用于显示 Git 仓库的分支等信息。

### autojump

Oh My Zsh 自带的插件，实现快速跳转到指定文件夹，前提是要安装 autojump 命令行工具，`sudo apt install autojump` 即可。

### [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

Zsh 下的命令自动建议插件，使用如下命令即可安装：

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

### [zsh-completions](https://github.com/zsh-users/zsh-completions)

Zsh 下的命令自动补全插件，使用如下命令即可安装：

```bash
git clone https://github.com/zsh-users/zsh-completions ~/.oh-my-zsh/custom/plugins/zsh-completions
```

### [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

Zsh 下的命令语法高亮插件，使用如下命令即可安装：

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

当安装并启用以上的所有插件后，`$HOME/.zshrc` 文件中插件相关配置应该是下面这样的：

```bash
plugins=(
  git
  autojump
  zsh-autosuggestions
  zsh-completions
  zsh-syntax-highlighting
)

source $ZSH/oh-my-zsh.sh
source ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
# 值得注意的是，根据官方文档，zsh-syntax-highlighting 插件需放在最后，
# 并且要加上相应的 source 语句
```

## 尾巴

Oh My Zsh 自带了很多主题，[在这里](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)可以查看每个主题的显示效果，可根据自己的喜好选择合适的主题，值得注意的是，当在 `$HOME/.zshrc` 配置文件中将主题设置为 `random` 时，它每次会选择随机的主题。
