---
title: 使用 Sphinx 生成项目文档
categories: CheatSheet
date: 2020-01-22 20:21:54
tags:
---

[Sphinx](http://www.sphinx-doc.org/en/master/) 是一个用 Python 编写的文档生成工具，其使用 [reStructuredText](https://howiezhao.github.io/2018/09/17/restructuredtext/) 作为标记语言，目前广泛应用于 Python 相关项目的文档生成。比如 [Python 官方文档](https://docs.python.org/zh-cn/3/)就是基于 Sphinx 生成的，此外 [Linux 内核文档](https://www.kernel.org/doc/html/latest/index.html)的生成也于 2016 年从 [Doxygen](http://www.doxygen.nl/) 转向 Sphinx，要了解更多使用 Sphinx 的项目可参考其[官方列表](https://www.sphinx-doc.org/en/master/examples.html)。

<!-- more -->

使用 `pip install sphinx` 即可安装 Sphinx。

## 使用

按照最佳实践，项目文档一般是在项目的 `docs` 目录中，所以不妨先创建一个 `docs` 目录并进入，之后的一切有关 sphinx 的命令都在此目录中运行。

安装完 Sphinx 并进入 `docs` 目录后，输入 `sphinx-quickstart` 即可创建一个文档项目。该引导程序会询问你一些问题，并根据你给出的回答对生成的文档项目进行相关配置，当然，这些配置都可以在生成后的 `conf.py` 文件中进行重新设置。以下是它可能会问到的一些问题：

- 分隔“source”和“build”目录（y/n）[n]：默认不分隔即可
- 项目名称：项目名称将显示在左侧导航栏顶部
- 作者姓名：作者姓名将显示在页面底部
- 项目版本：可不填
- 项目语言[en]：默认为英文，要切换为中文请输入 `zh_CN`

执行完成后，会在当前目录下生成如下文件/文件夹：

- `_duild/`：存放构建之后的文件
- `_static/`：存放静态文件
- `_templates/`：存放模板文件
- `conf.py`：sphinx 的配置文件
- `index.rst`：文档主页
- `Makefile`：Linux 下 `make` 构建工具的配置文件
- `make.bat`：Windows 下的构建命令脚本

编写完文档后，使用 `make html` 命令即可将其构建为 HTML 文件，其中，`html` 被称为构建器（builder），当然，你也可以使用别的构建器，比如 `latex`、`epub` 等。

输入 `make help` 可查看 make 支持的相关命令。

## 主题

Sphinx 生成的 HTML 文件默认使用的主题为 [Alabaster](https://github.com/bitprophet/alabaster)（个人觉得挺好看的，[Requests](https://cn.python-requests.org/zh_CN/latest/) 和 [Flask](https://flask.palletsprojects.com/en/1.1.x/) 项目文档的主题都是基于此主题修改的），除此之外，Sphinx 还内置了一些别的主题，具体可见其[官方文档中列出的](https://www.sphinx-doc.org/en/master/usage/theming.html#builtin-themes)（个人觉得其余的主题不如 Alabaster 好看），当然，你也可以使用第三方主题。

第三方主题中最常见的非 [sphinx_rtd_theme](https://github.com/readthedocs/sphinx_rtd_theme) 莫属，[Scrapy](https://docs.scrapy.org/en/latest/) 项目的文档就使用的它，要使用 sphinx_rtd_theme，需要先执行 `pip install sphinx_rtd_theme` 命令下载它，然后修改 `conf.py` 配置文件中的 `html_theme` 变量为 `'sphinx_rtd_theme'` 并在 `extensions` 列表中添加 `'sphinx_rtd_theme'`。

要探索更多的第三方主题，可参考 [Sphinx Themes](https://sphinx-themes.org/) 网站上收录的。

## 扩展

Sphinx 支持扩展，安装完 Sphinx 后就已经内置了一些扩展，除此之外，你也可以下载第三方扩展。

### 内置扩展

#### sphinx.ext.autodoc

#### sphinx.ext.coverage

#### sphinx.ext.viewcode

#### sphinx.ext.napoleon

#### sphinx.ext.graphviz

#### sphinx.ext.todo

### 第三方扩展

#### recommonmark

#### nbsphinx

#### sphinx-autodoc-typehints

#### sphinx-gallery

## Read the Docs
