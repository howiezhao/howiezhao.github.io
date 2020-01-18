---
title: reStructuredText 小记
date: 2018-09-17 20:32:11
categories: CheatSheet
tags:
---

**reStructuredText** 是一种类似于 Markdown 的轻量标记语言，其含义为“重新构建的文本”，也被简称为 **reST**，文件后缀名为 `.rst`，是 Python 的 Docutils 项目的一部分，目前 reST 被广泛应用于编写 Python 文档。

## 基本语法

### 标题

```reStructuredText
这是一级标题
============

这是二级标题
------------

这是三级标题
************
```

reST 使用这种不同的下标表示标题的大小，你可以按照自己的喜好使用不同的下标表示不同的标题，总之，一片文档中从上往下依次出现的第一种下标就表示一级标题，第二种不同于之前出现过的下标就表示二级标题，依次类推，个人喜欢用上面这种形式。
<!--more-->
### 列表

和 Markdown 一样：

```reStructuredText
- 无序列表项
- 无序列表项
- 无序列表项

1. 有序列表项
2. 有序列表项
3. 有序列表项
```

### 链接

```reStructuredText
`Howie's Blog <http://howiezhao.com>`_
```

### 横线

```reStructuredText
----
```

这是一条水平区分线，用 4 个或以上的短横线表示

### 转义

和传统编程语言一样，reST 使用 `\` 转义特殊字符。

### 注释

注释以两个点和一个空格开始。如下：

```reStructuredText
..  这是一行注释
```

## Interpreted Text Roles

**Interpreted Text Roles**（直译为“**解释文本角色**”）是 reST 中非常重要的一个概念，**Interpreted Text**（解释文本）是指以一对 <code>\`</code> 包裹起来的文本，**Role**（角色）是指 interpreted text（解释文本）的显示规则。Interpreted Text（解释文本）的语法为 <code>:role:\`text\`</code> 或 <code>\`text\`:role:</code>，功能是根据 `role`（角色）规则对 `text`（文本）进行 interprete（解释）。

### 字体

和 Markdown 一样：

```reStructuredText
*斜体*，等价于 :emphasis:`斜体`
**粗体**，等价于 :strong:`粗体`
```

### 单行代码

```reStructuredText
``这里是单行代码``，等价于:literal:`这里是单行代码`
```

要了解更多 reST 中内置的 roles，可参考 [Docutils 官方文档](http://docutils.sourceforge.net/docs/ref/rst/roles.html)。

当然，你也可以按照自己的需求自定义 roles，具体可参考 [Docutils 官方文档](http://docutils.sourceforge.net/docs/howto/rst-roles.html)。

## Directives

**Directives**（直译为“**指令**”）是 reST 中另一个非常重要的概念，Directive（指令）具有如下语法：

```reStructuredText
+-------+-------------------------------+
| ".. " | directive type "::" directive |
+-------+ block                         |
        |                               |
        +-------------------------------+
```

Directive（指令）以明确的标记开始（两个句点和一个空格），后跟 directive type（指令类型）和两个冒号，统称为“**directive marker（指令标记）**”。directive block（指令块）在 directive marker（指令标记）之后立即开始，并包括所有后续的缩进行。directive block（指令块）分为 arguments（参数），options（选项，即字段列表）和 content（内容，按此顺序），其中任何一个都可能出现。

### 多行代码

```reStructuredText
.. code:: python

  def my_function():
      print("hello")
```

### 图片

```reStructuredText
.. image:: picture.png
   :alt: 当图片无法显示时，则显示这里的语句。
```

### 表格

### 引用

要了解更多 reST 中内置的 directives，可参考 [Docutils 官方文档](http://docutils.sourceforge.net/docs/ref/rst/directives.html)。

当然，你也可以按照自己的需求自定义 directives，具体可参考 [Docutils 官方文档](http://docutils.sourceforge.net/docs/howto/rst-directives.html)。

## 最佳实践

1. 在特殊字符与要书写的文字之间加上空格，否则可能无法正常显示
2. 不同段之间加一空行

## 解析器

语言只是一种标准，实现该标准就需要相应的解析器，由于 reST 是 Docutils 项目的一部分，所以 reST 最初的解析器正是由 Docutils 提供的，当你使用 `pip install docutils` 命令安装 Docutils 之后，可以运行 `rst2html <rst file> <html file>` 命令，将 reST 文件转换为 HTML 文件。

要了解更多的命令可参考 [Docutils 官方文档](http://docutils.sourceforge.net/docs/user/tools.html)。

## 与 Markdown 相比

与 Markdown 相比，reST 更具扩展性，特别是 directives 的出现，可以按照需求自定义各种各样的 directives 来扩展 reST。

## 更多

[这里](http://rst.ninjs.org/)有一个在线的 reST 编辑器。

要了解更多关于 reST 的知识可参考 [Docutils 官方文档](http://docutils.sourceforge.net/rst.html)，或者 [Sphinx 官方文档](http://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html)。
