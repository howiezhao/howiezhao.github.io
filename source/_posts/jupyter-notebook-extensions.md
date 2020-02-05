---
title: Jupyter Notebook 常用扩展
date: 2018-09-25 17:01:20
categories: CheatSheet
tags:
---

## 扩展机制

在介绍常用扩展之前，有必要先来介绍一下 Jupyter Notebook 的扩展机制：本质上来说，所有的 Jupyter Notebook 扩展都是一个个的 Python 包，所以大部分可以通过 `pip` 快速安装，另外，Jupyter Notebook 是一个典型的 **B/S** 架构的应用，用户通过访问浏览器来使用 Jupyter Notebook，因此，Jupyter Notebook 的扩展可以只针对服务器端，也可以针对前端资源页面，而如果一个扩展增强了 Jupyter Notebook 的前端资源页面，则它还必须使用如下命令安装资源：

```bash
jupyter nbextension install helpful_package --py # or --sys-prefix if using virtualenv or conda
```

安装完资源后，如果这个资源需要在每次 Jupyter Notebook 启动后被加载，则还应使用如下命令启用资源：

```bash
jupyter nbextension enable helpful_package --py # or --sys-prefix if using virtualenv or conda
```

## [jupyter_contrib_nbextensions](https://github.com/ipython-contrib/jupyter_contrib_nbextensions)

与其说这是一个扩展，倒不如说这是**一群**扩展，该扩展集合了大多数的 Jupyter Notebook 常用扩展。

使用 `pip install jupyter_contrib_nbextensions` 命令即可安装，安装完成后使用 `jupyter contrib nbextension install --user` 命令进行些许配置，参数 `--user` 指定安装到当前用户家目录下的 `.jupyter` 文件夹下。

等到安装并配置完成后，打开 Jupyter Notebook 网页，会出现 `Nbextensions` 选项卡，点击进入此选项卡中，可以启用或禁用相应的扩展。

## [RISE](https://github.com/damianavila/RISE)

该扩展可以将 Jupyter Notebook 中的一个个单元格转换为一张张的幻灯片。

使用 `pip install RISE` 命令即可安装，安装完成后使用 `jupyter-nbextension install rise --py --sys-prefix` 命令安装前端资源，接着使用 `jupyter-nbextension enable rise --py --sys-prefix` 命令启用前端资源。
