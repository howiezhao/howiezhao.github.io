---
title: Git小记
date: 2018-08-31 16:59:18
categories: CheatSheet
tags:
---

[Git](https://git-scm.com/)是目前**最流行**的**分布式版本控制系统**（Distributed Version Control System, **DVCS**），类似的工具还有[Mercurial](https://www.mercurial-scm.org/)（由`hg`命令操作）等；在早期，人们常使用**集中式版本控制系统**（Centralized Version Control System，**CVCS**），其典型有[CVS](https://www.nongnu.org/cvs/)、[Subversion](https://subversion.apache.org/)（SVN）等；现在，越来越多的人开始使用更为优秀的分布式版本控制系统，所谓版本控制，即可以随时记录并切换文件的不同版本。

## 安装

## 配置

Git共有3个配置文件，分别是：

- `/etc/gitconfig`文件用于配置所有用户的配置信息，使用`git config --system`命令配置
- 某个用户家目录下的`.gitconfig`文件只适用于该用户，使用`git config --global`命令配置
- 当前Git仓库的`.git/config`仅针对当前项目，直接使用`git config`命令进行配置

注意：每一个级别会覆盖上一级别的配置，所以`.git/config`的配置变量会覆盖`/etc/gitconfig`中的配置变量。
按照个人偏好，针对新安装的Git环境，会配置如下信息：

```bash
# 配置提交时使用的用户名和邮箱，必须配置
git config --global user.email "you@example.com"
git config --global user.name "Your Name"

# 开启颜色显示
git config --global color.ui true

# 配置别名
git config --global alias.lg1 "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"
git config --global alias.lg2 "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all"
git config --global alias.lg '!"git lg1"'
git config --global alias.adog "log --all --decorate --oneline --graph"

# 配置difftool为Meld（Windows）
git config --global diff.tool meld
git config --global difftool.meld.path "C:\Program Files (x86)\Meld\Meld.exe"
git config --global difftool.prompt false

# 配置mergetool为Meld（Windows）
git config --global merge.tool meld
git config --global mergetool.meld.path "C:\Program Files (x86)\Meld\Meld.exe"
git config --global mergetool.prompt false
```

另外，Git默认使用的编辑器是Vim，若要配置成自己喜欢的编辑器(如Emacs)，可使用命令：`git config --global core.editor emacs`。
最后，你可以使用`git config --list`来查看所有配置信息。
<!--more-->
## 结构

要开始对某个项目进行版本控制，需要先在其所在路径下执行`git init`进行初始化，此命令会在当前路径下创建一个`.git`的隐藏文件夹，这就是Git仓库目录。
Git分为3个区域，Git仓库、工作目录、暂存区域：

- **Git仓库目录**（Repository）是Git用来保存项目的元数据和对象数据库的地方。这是Git中最重要的部分，从其它计算机克隆仓库时，拷贝的就是这里的数据。
- **工作目录**（Working directory）是对项目的某个版本独立提取出来的内容。这些从Git仓库的压缩数据库中提取出来的文件，放在磁盘上供你使用或修改。
- **暂存区域**（Staging area）是一个文件，保存了下次将提交（commit）的文件列表信息，一般在Git仓库目录中。有时候也被称作“索引”，不过一般说法还是叫暂存区域。

基本的Git工作流程如下：

1. 在工作目录中修改文件。
2. 暂存文件，将文件的快照放入暂存区域。
3. 提交更新，找到暂存区域的文件，将快照永久性存储到Git仓库目录。

根据Git的三个区域，一个文件可以有如下几种状态：

- **未跟踪状态**（untracked）：指新创建且还没有添加到暂存区域的文件
- **已暂存状态**（staged）：指已经添加到暂存区域的文件
- **已提交状态**（committed）：指已经从暂存区提交到Git仓库的文件
- **已修改状态**（modified）：指作了修改但还没有放到暂存区域的文件

## 分支

每一次提交都是文件的一个版本，可以将这一系列提交看作一条**链表**，链表的头指针（**HEAD**）始终指向最新的提交，即最新的版本。要检出到某一版本，本质上是将HEAD指针指向某一提交。链表中的节点（即提交）都有唯一的父节点和唯一的子节点，Git中**分支**（branch）的本质就是将链表变为**树**。当使用`git init`初始化Git仓库时，会默认创建`master`分支，这种一个分支等价于一条链表。
使用`git branch`可列出所有分支，使用`git branch dev`即可在当前提交点创建新分支`dev`，接着使用`git checkout dev`即可切换到`dev`分支，或者直接使用`git checkout -b dev`即可一步创建并切换到`dev`新分支。

## 命令

- `git version`：查看Git版本信息
- `git add test1.txt`：将需要被追踪的文件（test1.txt）添加到暂存区域
- `git reset test2.txt`：将误被追踪的文件（test2.txt）移除出暂存区域，文件仍会存在于工作目录
- `git commit -m 'first commit'`：将暂存区域的内容提交到本地仓库，参数`-m`指定提交时的附带信息，若不带参数`-m`执行此命令则会自动打开默认的Vim编辑器并要求输入附带信息
- `git push`：将本地仓库推送到远程仓库
- `git clone`：将远程仓库克隆到本地
- `git pull`：将远程仓库的更新拉取到本地仓库
- `git status`：查看Git仓库状态
- `git log`：查看commit记录，参数`--graph`可以图形化显示，参数`--oneline`可以一行显示。
- `git diff`：对比工作目录和暂存区域中文件之间的不同
- `git diff --staged`：对比暂存区域和Git仓库中最新commit文件之间的不同
- `git diff <first-commit-id> <second-commit-id>`：对比Git仓库中两个commit之间的不同，参数为两个commit ID，为方便可以取ID的前7个字符
- `git checkout <commit-id>`：切换到某个具体的commit，要切换回最新的commit可使用`git checkout master`

## .gitignore

## 思想

**直接记录快照，而非差异比较**：Git与其他版本控制系统的主要区别在于对待数据的方法，其他的VCS主要记录不同版本之间的差异，而Git则相当于直接记录不同版本的快照。
**近乎所有操作都是本地执行**：在Git中的绝大多数操作都只需要访问本地文件和资源，一般不需要来自网络上其它计算机的信息。
**Git保证完整性**：Git中所有数据在存储前都计算校验和(SHA-1)，然后以校验和来引用。这意味着不可能在Git不知情时更改任何文件内容或目录内容。若你在传送过程中丢失信息或损坏文件，Git就能发现。
**Git一般只添加数据**：你执行的Git操作，几乎只往Git数据库中增加数据。很难让Git执行任何不可逆操作，或者让它以任何方式清除数据。

## 原理

## GitHub

应明确一点，Git是由Linux创始人Linus Torvalds开发的分布式版本控制系统，而GitHub是使用Git实现的代码托管网站，两者并非一类。

## 更多

在命令行中直接输入`git`，可查看相关命令，要具体查看某个命令的帮助信息，可输入`git help <command>`，如`git help diff`，要了解更多关于Git的内容，可以参考[《Pro Git》](https://git-scm.com/book/zh/v2)一书。
