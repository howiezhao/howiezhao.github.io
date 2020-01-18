---
title: Markdown小记
date: 2018-07-21 08:50:42
categories: CheatSheet
tags:
---

Markdown是一种轻量标记语言，其文件后缀名为`.md`，它允许人们采用其规定的语法编写文档，而后Markdown解析器会将其转化为有效的HTML文档，以便在网页中显示，时至今日，有许多Markdown解析器增强了Markdown的基本语法，这就造成了Markdown有多种**风格**（flavor）。因为Markdown要被转化为HTML才能在网页上显示，所以在Markdown中仍然可以使用HTML，如果有Markdown无法完成的工作，完全可以再用回HTML。

## 基本语法

### 标题
```
# 一级标题
#### 四级标题
```
对应HTML，最高6级标题。

### 列表
```
- 无序列表项
    - 这是是嵌套列表项
    - 这里也是嵌套列表项
- 无序列表项
- 无序列表项

1. 有序列表项
2. 有序列表项
3. 有序列表项
```
无序列表项常以`-`或`*`起始，个人习惯使用`-`。
<!--more-->
### 链接
```
[Howie's Blog](http://howiezhao.com)
```
超文本链接必须带http。
### 图片
```
![一张图片](/images/abc.jpg)
```
当图片无法显示时，则显示中括号中的语句。
图片的路径为相对路径，即当前Markdown文件所在路径下的`images`中的`abc.jpg`。
### 字体
```
*斜体*
**粗体**
***粗斜体***
```
### 代码

\`\`\`
这里是多行代码
\`\`\`

\`这里是单行代码`

### 表格
```
表头1 | 表头2
--- | ---
单元格1 | 单元格2
单元格3 | 单元格4
```
上下应该各空一行
### 引用
```
> 这是引用
```
### 横线
```
----
```
这是一条水平区分线，用3个或以上的短横线表示，个人习惯使用4个短横线。
### 转义

和传统编程语言一样，Markdown使用`\`转义以上特殊字符。

## 最佳实践

1. 在特殊字符与要书写的文字之间加上空格
2. 不同段之间加一空行
3. 链接后加一个空格

## GitHub Flavored Markdown

GitHub Flavored Markdown，简记为**GFM**，即**GitHub风格的Markdown语法**，是GitHub中编辑器使用的Markdown语法格式，略微区别于标准的Markdown语法，主要如下：

1. 链接自动识别：GFM会自动为标准的URL加上链接
2. 语法着色：在<code>```</code>后输入语言名称，即可着色，要查看支持的语言列表，请参考[官方文档](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml)
3. 删除线：使用`~~`表示删除线
4. 任务列表：使用`- [ ]`或`- [x]`表示未勾选或已勾选的任务列表
5. Emoji：使用`:EMOJICODE:`可以显示Emoji表情，比如`:+1:`表示一个👍，要查看完整的Emoji编码，可参考[Emoji cheat sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet/)

要了解GFM的更多特性，可以参考[GitHub官方的文档](https://help.github.com/categories/writing-on-github/)。
## 更多
[Dillinger](https://dillinger.io/)是一个在线的Markdown编辑器。
Sublime Text拥有众多的Markdown插件，其中[Markdown​Preview](https://packagecontrol.io/packages/MarkdownPreview)可以在浏览器中预览Markdown文件，而[Markdown​Editing](https://packagecontrol.io/packages/MarkdownEditing)可以快速的编辑Markdown文件。
