---
title: 使用 IPython 替代原生 Python Shell
date: 2018-09-16 13:15:34
categories: CheatSheet
tags:
---

我算是个原教主义者，喜欢原生的东西，不太喜欢第三方的东西，但 IPython 相比原生 Python Shell 的众多优秀特性，让我不由得使用上它。

## 名称

[**IPython**](https://ipython.org/) 最初只是一种基于 Python 的交互式解释器（REPL），慢慢的，IPython 项目中集成了许多新的工具，比如 **IPython Notebook**，这是一种基于 Web 的强大编辑器。从 IPython 4.0 开始，IPython 项目中和语言无关的工具已独立出来形成一个新的项目 [**Jupyter**](http://jupyter.org/)，从此，IPython Notebook 升级为 **Jupyter Notebook**，开始支持更多的编程语言。而 IPython 将只专注于提供 Python 交互式解释器以及为 Jupyter 提供 Python 内核。当写这篇文章时，IPython 的最新版本为 7.8.0。

如今，当你去 IPython 官网下载时，它会跳转到 Jupyter 的下载页面，因为 Jupyter 中已经包含了 IPython，同时也建议下载 Jupyter，因为其包含了强大的 Jupyter Notebook，使用 `pip install jupyter` 即可下载，安装完成后直接输入 `ipython` 即可进入 IPython 交互式环境。
<!--more-->
## 优势

以下仅列出 IPython 相比原生 Python Shell 的一些优势：

- Tab 自动补全
- 自动缩进
- 语法高亮
- 支持命令历史记录
- 命令前加 `!` 可调用系统命令
- 命令后加 1 个或 2 个 `?` 可方便查看对象信息
- 有众多的魔法函数（Magic Functions）

## 魔法函数

以下仅列出 IPython 中使用较多的魔法函数：

```bash
%timeit #测试代码段执行时间
%hist   #查看历史记录
%debug  #激活交互的调试器(ipdb)
%load   #加载外部代码
%edit   #使用编辑器打开
```

要查看更多的魔法函数，可以访问 [IPython 的官方文档](https://ipython.readthedocs.io/en/stable/interactive/magics.html)

## Jupyter Notebook

要启动 Jupyter Notebook 直接在命令行输入 `jupyter notebook` 即可，它会监听本机的 8888 端口，并自动打开浏览器访问。输入 `jupyter notebook --help` 可以查看它的更多参数。

Jupyter Notebook 默认采用 **Token** 的方式进行登录，启动后在命令行中会显示当前的 token 值，若没有自动打开浏览器，则可以复制命令行中带 token 的链接并在浏览器中打开即可。

使用命令 `jupyter notebook --generate-config` 可生成 Jupyter Notebook 配置文件，默认为 `$HOME/.jupyter/jupyter_notebook_config.py` 文件。常用的配置项如下：

```bash
# 配置是否允许root用户运行，改为`True`则允许
c.NotebookApp.allow_root = False

# 配置监听地址，改为`*`可监听所有IP
c.NotebookApp.ip = 'localhost'

# 配置启动后显示的目录，默认为启动时输入命令的目录
c.NotebookApp.notebook_dir = ''

# 配置启动时是否自动打开浏览器，若在远程服务器上启动Jupyter Notebook，
# 则没必要打开浏览器，改为`False`即可
c.NotebookApp.open_browser = True

# 配置登录密码，需要存储密文形式，使用`jupyter notebook password`命令
# 可生成加密后的密码
c.NotebookApp.password = ''

# 配置监听端口
c.NotebookApp.port = 8888
```

最后，在 Linux 下，使用 `nohup jupyter notebook > jupyter.log &` 可使 Jupyter Notebook 在后台运行并记录日志到当前目录下的 `jupyter.log` 文件中。

要了解 Jupyter Notebook 的更多信息，可参考另一篇博文：[Jupyter Notebook 常用扩展](https://howiezhao.github.io/2018/09/25/jupyter-notebook-extensions/)。
