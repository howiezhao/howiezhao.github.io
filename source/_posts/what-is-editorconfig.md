---
title: editorconfig 是什么
date: 2018-09-23 17:55:34
categories: CheatSheet
tags:
---

开发同一项目的不同的人，可能会使用不同的编辑器，又会有不同的设置，这就会造成不同的代码格式，为了统一同一项目的代码格式，由此诞生了 [EditorConfig](https://editorconfig.org/) ，它包含了**一个用于定义代码格式的文件**和**一批编辑器插件**，这些插件可以让编辑器读取配置文件并依此格式化代码。

一个典型的 EditorConfig 配置文件如下所示：

```
# 这是一行注释，以#开头

# 表示此文件为最顶级
root = true

# 设定每个文件每行以换行（LF）结束，文件末尾添加一个新行
[*]
end_of_line = lf
insert_final_newline = true

# 匹配所有以 js 和 py 为后缀名的文件
# 设定其编码为 UTF-8
[*.{js,py}]
charset = utf-8

# 匹配所有以 py 为后缀名的文件，设定其缩进为 4 个空格
[*.py]
indent_style = space
indent_size = 4

# 设定 Makefile 文件的缩进为 Tab
[Makefile]
indent_style = tab

# 匹配lib目录下所有以 js 为后缀名的文件，设定其缩进为 2 个空格
[lib/**.js]
indent_style = space
indent_size = 2

# 设定 package.json 和 .travis.yml 的缩进为 2 个空格
[{package.json,.travis.yml}]
indent_style = space
indent_size = 2
```

此配置文件应该保存为 `.editorconfig` 并放置在项目目录中，编辑器的 EditorConfig 插件会从文件打开目录开始依次向其父级目录查找并读取配置文件，直到遇见 `root = true` 为止。

有很多项目在初始化时都会生成相应的 `.editorconfig` 文件，比如 Angular。

另外，Visual Studio 和 JetBrains 家的大部分 IDE 都已经原生支持了 EditorConfig，因此不用再安装插件；对于 Sublime Text 和 Vim 等未原生支持的编辑器，EditorConfig 官网提供了相应的插件下载地址。要了解详细的支持列表，请访问 EditorConfig 官网。
