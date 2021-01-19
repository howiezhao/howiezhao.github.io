---
title: Markdown 小记
date: 2018-07-21 08:50:42
categories: CheatSheet
tags:
---

Markdown 是一种轻量**标记语言**，其文件后缀名为 `.md`，它允许人们采用其规定的语法编写文档，而后 Markdown 解析器会将其转化为有效的 HTML 文档，以便在网页中显示，时至今日，有许多 Markdown 解析器增强了 Markdown 的基本语法，这就造成了 Markdown 有多种**风格**（flavor）。

因为 Markdown 要被转化为 HTML 才能在网页上显示，所以在 Markdown 中仍然可以使用 HTML，如果有 Markdown 无法完成的工作，完全可以再用回 HTML。

## 基本语法

### 标题

```markdown
# 一级标题
#### 四级标题
```

对应 HTML，最高 6 级标题。

### 列表

```markdown
- 无序列表项
  - 这是是嵌套列表项
  - 这里也是嵌套列表项
- 无序列表项
- 无序列表项

1. 有序列表项
2. 有序列表项
3. 有序列表项
```

无序列表项常以 `-` 或 `*` 起始，个人习惯使用 `-`。
<!--more-->
### 链接

```markdown
[Howie's Blog](https://howiezhao.com)
```

超文本链接必须带 http/https。

### 图片

```markdown
![一张图片](/images/abc.jpg)
```

当图片无法显示时，则显示中括号中的语句。

图片的路径为相对路径，即当前 Markdown 文件所在路径下的 `images` 中的 `abc.jpg`。

### 字体

```markdown
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

```markdown
表头1 | 表头2
--- | ---
单元格1 | 单元格2
单元格3 | 单元格4
```

上下应该各空一行

### 引用

```markdown
> 这是引用
```

### 横线

```markdown
----
```

这是一条水平区分线，用 3 个或以上的短横线表示，个人习惯使用 4 个短横线。

### 转义

和传统编程语言一样，Markdown 使用 `\` 转义以上特殊字符。

## 最佳实践

1. 在特殊字符与要书写的文字之间加上空格
2. 不同段之间加一空行
3. 链接后加一个空格

## GitHub Flavored Markdown

GitHub Flavored Markdown，简记为 **GFM**，即 **GitHub 风格的 Markdown 语法**，是 GitHub 中编辑器使用的 Markdown 语法格式，略微区别于标准的 Markdown 语法，主要如下：

1. 链接自动识别：GFM 会自动为标准的 URL 加上链接
2. 语法着色：在 <code>```</code> 后输入语言名称，即可着色，要查看支持的语言列表，请参考[官方文档](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml)
3. 删除线：使用 `~~` 表示删除线
4. 任务列表：使用 `- [ ]` 或 `- [x]` 表示未勾选或已勾选的任务列表
5. Emoji：使用 `:EMOJICODE:` 可以显示 Emoji 表情，比如 `:+1:` 表示一个👍，要查看完整的 Emoji 编码，可参考 [Emoji cheat sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet/)

要了解 GFM 的更多特性，可以参考 [GitHub 官方的文档](https://docs.github.com/cn/github/writing-on-github)。

## CommonMark

为了解决 Markdown 风格太多的问题，诞生了 [CommonMark](https://commonmark.org/) 项目，其制定了一系列的语法规范，按照此语法规范书写的 Markdown 文档可以得到更好的兼容性。

## 更多

[Dillinger](https://dillinger.io/) 是一个开源在线的 Markdown 编辑器。

Sublime Text 拥有众多的 Markdown 插件，其中 [Markdown​Preview](https://packagecontrol.io/packages/MarkdownPreview) 可以在浏览器中预览 Markdown 文件，而 [Markdown​Editing](https://packagecontrol.io/packages/MarkdownEditing) 可以快速的编辑 Markdown 文件。

为了检查你书写的 Markdown 是否符合规范，可以使用相应的 linter [markdownlint-cli](https://github.com/igorshubovych/markdownlint-cli) 命令行工具。
