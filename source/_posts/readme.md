---
title: 编写规范的 README 文档
date: 2018-11-02 16:59:24
categories: CheatSheet
tags:
---

代码不仅是写给计算机的，也是写给人的，一篇文档的好坏直接影响着使用此代码的人的心情，针对小的项目，一般使用 **README** 文件来做整体描述，README 这个名字也极好的反映了此文件的目的，即“**读我**”。有趣的是，README 这 6 个字母通常都是大写的，这是因为**在 Linux 中大写的文件名往往意味着醒目和值得注意**。实际上，并没有任何人规定 README 文档应该写成什么样子，但在本文中，我将介绍一些被公认的所谓优秀的 README 文档应该是什么样子的。
<!--more-->
README 文档通常是用 **Markdown** 编写的，但有时你也会看到其他格式的 README 文档，比如：有关 Python 的项目喜欢用 **reStructuredText** 编写 README 文档，这也是一种类似于 Markdown 的标记语言。一个优秀的 README 文档中应包含：**简短的项目说明**、**安装说明**、**使用说明**、**如何参与贡献**、**许可协议**等。此外，随着代码量的增加，**已知 BUG**、**常见问题**等也可以加入到 README 文档中。

一个规范的 README 文档模板应该像下面这样的：

```markdown
# Project Name
填写简短的项目说明
# Installation
填写安装说明
# Usage
填写使用说明
# Contributing
填写如何参与此项目的贡献方法
# License
填写许可协议
```

有趣的是，在日常使用中，经常会见到各种各样的徽章或进度条，比如：

![Travis (.org)](https://img.shields.io/travis/rust-lang/rust.svg)

![GitHub release](https://img.shields.io/github/release/qubyte/rubidium.svg)

![GitHub stars](https://img.shields.io/github/stars/git/git.svg)

它们的本质就是一个个的图片而已，要想自定义这些图片可以访问 [Shields.io](https://shields.io/#/)。

最后，我将给出几个 GitHub 中项目的文档，它们的 README 文档都写得不错：

- [Rails](https://github.com/rails/rails)
- [factory_bot](https://github.com/thoughtbot/factory_bot)
- [Walle](https://github.com/meolu/walle-web)
- [Ledbetter](https://github.com/github/ledbetter)
- [Create-Your-Own-Adventure](https://github.com/udacity/create-your-own-adventure)
- [can.viewify](https://github.com/zkat/can.viewify)
