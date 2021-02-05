---
title: Vim小记
date: 2018-09-18 12:09:54
categories: CheatSheet
tags:
  - Linux
---

在几乎所有的Linux发行版中，都会自带vi文本编辑器，而[Vim](https://www.vim.org/)（Vi IMproved）则是vi的一个增强版，大多数Linux中也都预装了Vim，若没有安装，可使用相应的包管理工具进行安装，具体而言，在Ubuntu中，使用`sudo apt install vim`即可安装。输入`vim --version`可以查看所使用的Vim版本，当前最新版本为Vim 8.x。值得注意的是，在有的系统中，`vi`命令实际是指向`vim`命令的一个链接，使用`which vi`即可证实。

在2015年，开源组织发布了[Neovim](https://neovim.io/)项目，它是Vim的重构版本，需自行安装。另外，GVim是Vim的一个图形客户端。
<!--more-->
## 三种模式

Vim有许多模式，但常用的其实是普通模式、插入模式、命令行模式这三种。

### 普通模式（Normal）

Vim启动后默认为普通模式，此时Vim编辑器左下角将依次显示文件名、行数、字符数，右下角将依次显示当前光标所在的行与列、当前屏幕显示的字数占文件总字数的百分比。在普通模式下可以使用相当多的快捷键来完成相应的操作，常用的命令如下：

- `x`：删除当前光标所在字符
- `dd`：删除当前行
- `0`：到行头
- `$`：到行尾
- `u`：撤销

### 插入模式（Insert）

在普通模式下输入`i`(insert)，即可切换到插入模式，此时Vim编辑器左下角将显示`-- INSERT --`标识。在插入模式下，可完成输入文字等功能。最后，按下`Esc`键可退回普通模式。

### 命令行模式

在命令行模式下可以输入会被执行的相关命令，例如执行命令(`:`键)、搜索命令(`/`键)或者过滤命令(`!`键)。此时，Vim编辑器左下角将显示输入的命令。在命令执行之后，Vim将返回到命令行模式之前的模式，通常是普通模式。
在命令行模式下常使用的命令有：

- `:wq`：保存(write)并退出(quit)
- `:1`：跳转到第一行，类似的，跳转到第n行则为`:n`
- `:set nu`：显示行号(number)，类似的，`:set nonu`为不显示行号
- `:set ff=unix`：设置文件为unix格式

## vimrc

Vim有多个配置文件，当前用户的配置文件为用户家目录下的`.vimrc`隐藏文件，Vim启动时会按照该文件中的配置开启相应的功能。个人常做的基本配置项如下：

```text
" 这是一行注释
" 显示行号
set number

" 语法高亮
syntax enable

" tab缩进
set tabstop=4
set shiftwidth=4
set expandtab
set smarttab

" 鼠标可用
"set mouse=a

" 配色方案
set t_Co=256
set background=dark
colorscheme desert

" 匹配模式
set showmatch

" 自动缩进
set autoindent
set smartindent

" 显示命令
set showcmd
```

## 主题

Vim自带了多种主题，即配色方案，默认存放在Vim安装目录下的colors文件夹下，在Vim中输入命令`:echo $VIMRUNTIME`即可显示Vim的安装目录，以我的为例，其安装目录为`/usr/share/vim/vim80`。

如果你想更改默认的主题，可以按照上面的配置，在`vimrc`文件中使用`colorscheme <主题名>`进行配置。Vim默认使用的是`default`主题。如果你想使用第三方或自定义的主题，则需要将下载的主题文件存放到colors文件夹下（`~/.vim/colors`下也行），然后再进行相关配置。

## 插件

Vim支持很多插件，为了简化插件的安装，由此诞生了许多的插件管理器，[Vundle](https://github.com/VundleVim/Vundle.vim)是使用最多的Vim插件管理器，但个人倾向于使用[vim-plug](https://github.com/junegunn/vim-plug)插件管理器，vim-plug相比Vundle最大的优势是支持异步安装，该特性可以极大的加速多个插件的安装速度。
使用如下命令即可安装vim-plug：

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

安装完vim-plug插件管理器后，只需在`.vimrc`文件中做相关配置，然后进入Vim的命令行模式，输入`:PlugInstall`命令，即可自动下载并安装相应的插件，升级插件可使用`:PlugUpdate`命令，升级vim-plug本身，可使用`:PlugUpgrade`命令。个人常用的插件如下：

- [NERDTree](https://github.com/scrooloose/nerdtree)：显示文件树形目录
- [YouCompleteMe](https://github.com/Valloric/YouCompleteMe)：代码自动补全
- [startify](https://github.com/mhinz/vim-startify)：自定义起始页

相应的，`.vimrc`文件中插件相关的配置项如下：

```text
" vim-plug
call plug#begin('~/.vim/plugged')

function! BuildYCM(info)
  " info is a dictionary with 3 fields
  " - name:   name of the plugin
  " - status: 'installed', 'updated', or 'unchanged'
  " - force:  set on PlugInstall! or PlugUpdate!
  if a:info.status == 'installed' || a:info.force
    !./install.py
  endif
endfunction

Plug 'Valloric/YouCompleteMe', { 'do': function('BuildYCM') }
Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
Plug 'mhinz/vim-startify'

call plug#end()
```
