---
title: Hexo 初体验
date: 2017-06-20 17:38:54
categories: CheatSheet
tags:
  - Hexo
---

[Hexo](https://hexo.io/zh-cn/index.html) 是一个基于 Node.js 的开源静态博客框架，类似的项目还有基于 Ruby 的 [Jekyll](https://jekyllrb.com/)，基于 Go 的 [Hugo](https://gohugo.io/)，基于 Python 的 [Pelican](https://blog.getpelican.com/) 等等。之所以选择 Hexo，主要是因为它不仅使用人数多，而且有中文文档。

## 安装

安装 Hexo 前，需要安装 [Node.js](https://nodejs.org/zh-cn/download/) 和 [Git](https://git-scm.com/downloads)，安装 Node.js 的同时，npm（Node Package Manager）也已经被自动安装了，同时安装程序也自动配置了环境变量。确定安装完成后，可以输入 `node -v` 来测试 Node.js 是否成功安装，输入 `npm -v` 来测试 npm 是否成功安装。

npm 成功安装后，可使用 `npm install -g hexo-cli` 来快速安装 Hexo 命令行工具。其次你还需要安装 npm-check-updates 包，它用于以后 Hexo 及其插件的更新。参数 `-g` 表示全局安装，npm 的包安装分为本地安装（local）和全局安装（global）两种，区别在于：

本地安装：

- 将安装包放在 `./node_modules` 下（运行 npm 时所在的目录）
- 可以通过 `require()` 来引入本地安装的包

全局安装：

- 将安装包放在 `/usr/local` 下
- 可以直接在命令行里使用
<!-- more -->

关于 npm 更多的内容请参考 [npm 模块安装机制简介](http://www.ruanyifeng.com/blog/2016/01/npm-install.html)。

## 更新

在 **博客所在目录** 执行 `hexo version` 即可查看 Hexo 版本信息。

要更新 Hexo 及其插件到最新 **主** 版本，需要在 **博客所在目录** 执行如下命令：

```sh
npm-check-updates -u
npm install
```

若只想更新 Hexo 及其插件到最新 **次** 版本，则只需在 **博客所在目录** 执行 `npm update` 即可。

要更新 hexo-cli，你只需要再次执行 `npm install -g hexo-cli` 安装即可。

## 常用命令

### 新建一个网站

```sh
hexo init [folder]
```

如果没有设置 `folder`，Hexo 默认在当前的文件夹建立网站。

### 新建一篇文章

```sh
hexo n [layout] <title>
# 或
hexo new [layout] <title>
```

如果没有设置 `layout` 的话，默认使用 `_config.yml` 中的 `default_layout` 参数代替。如果标题包含空格的话，请使用引号括起来。

### 启动服务预览

```sh
hexo s
# 或
hexo server
```

默认情况下，访问网址为：<http://localhost:4000/> 。

### 生成静态文件

```sh
hexo g
# 或
hexo generate
```

### 部署网站

```sh
hexo d
# 或
hexo deploy
```

### 清除缓存文件（`db.json`）和已生成的静态文件（`public/`）

```sh
hexo clean
```

在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

## 更多

### 目录结构

Hexo 生成的网站目录结构如下：

- `public/`：此目录下保存着已经生成的静态文件
- `scaffolds/`：此目录下存放 Hexo 模板，当您新建文章时，Hexo 会根据 scaffold 来建立文件。
- `source/`：此目录下存放用户资源
  - `_posts/`：此目录下存放 Markdown 格式的源文章
  - `images/`：此目录下存放相关图片文件
- `themes/`：此目录下保存着主题文件
- `_config.yml`：此文件为**站点配置文件**

### 最佳实践

站点配置文件（`_config.yml`）中的 `url` 字段务必要填写为自己站点的正确网址，否则分享自己站点内文章时会生成错误链接。

新建文章（`hexo n <title>`）时建议使用小写英文作为文件名，此文件名将作为文章链接的一部分，英文中的空格将自动用 `-` 替代，文章标题可以在文件中另行设置。

和传统的博客一样，建议开启**分类**（category）和**标签**（tag）功能，在 Hexo 中，分类具有**顺序性**和**层次性**，也就是说 `Foo，Bar` 不等于 `Bar，Foo`，而标签没有顺序和层次。简单来说，分类应该是经过深思熟虑的，而标签则可适文章而决定，分类一般只有几个，而标签可以有一堆。具体而言，可以参考本站点的分类标签设计。

## 插件

Hexo 支持[许多插件](https://hexo.io/plugins/)，个人经常使用的插件如下：

- [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)：为 Hexo 打造的 Git 部署插件，适用于将博客部署到 GitHub 仓库上。
- [hexo-generator-feed](https://github.com/hexojs/hexo-generator-feed)：适用于为博客添加 RSS 功能。
- [hexo-generator-sitemap](https://github.com/hexojs/hexo-generator-sitemap)：适用于为博客添加 Sitemap 功能。
- [hexo-symbols-count-time](https://github.com/theme-next/hexo-symbols-count-time)：适用于为文章添加字数统计和阅读时长统计，比同类型的 [hexo-wordcount](https://github.com/willin/hexo-wordcount) 插件要更好。
- [hexo-generator-searchdb](https://github.com/theme-next/hexo-generator-searchdb)：适用于为博客添加本地搜索功能。

使用如下命令即可安装上面提到的所有插件：

```sh
npm install hexo-deployer-git hexo-generator-feed hexo-generator-sitemap hexo-symbols-count-time hexo-generator-searchdb
```

## 主题

安装 Hexo 后，默认使用的主题为 [landscape](https://github.com/hexojs/hexo-theme-landscape)，个人不是很喜欢这个主题，所幸的是 Hexo 提供[更多的第三方主题](https://hexo.io/themes/)，个人倾向于使用广为流行的 [NexT 主题](https://theme-next.js.org/)。

值得注意的是，NexT 主题在 6.0.0 版本之前由 iissnan 个人维护，其官方仓库为 <https://github.com/iissnan/hexo-theme-next> ，官网为 <https://theme-next.iissnan.com/> ；在 6.0.0 版本之后由 theme-next 组织维护，其官方仓库更改为 <https://github.com/theme-next/hexo-theme-next> ，官网为 <https://theme-next.org> ；在 8.0.0 版本之后由 next-theme 组织维护，其官方仓库更改为 <https://github.com/next-theme/hexo-theme-next> ，官网为 <https://theme-next.js.org/> ；这里所介绍的使用方法均以 8.0.0 版本之后为例。

### NexT 主题安装

要安装 NexT 主题，首先要进入 Hexo 站点目录下，接着执行 `https://github.com/next-theme/hexo-theme-next themes/next` 命令，即可将 NexT 仓库克隆到本地。要启用 NexT 主题，只需在**站点配置文件**中找到 `theme` 字段，并将其值更改为 `next` 即可。

### NexT 主题更新

要查看正在使用的 NexT 主题的版本，有如下几种方法：

- 可直接打开**主题配置文件**（即站点目录下的 `/themes/next/_config.yml` 文件），在其底部 `version` 字段即可查看版本号。
- 在自己站点的底部一般会有 Hexo 和 NexT 的版本号

和传统的 Git 仓库更新一样，进入站点目录下的 `/themes/next` 文件夹，执行 `git pull` 命令即可从官方仓库拉取最新代码进行更新。

如果你使用的是 6.0.0 之前的版本，现在想要升级到 6.0.0 之后的版本，可参考 theme-next 官方给出的[解决方案](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/UPDATE-FROM-5.1.X.md)。

如果你使用的是 8.0.0 之前的版本，现在想要升级到 8.0.0 之后的版本，可参考 next-theme 官方给出的[解决方案](https://theme-next.js.org/docs/getting-started/upgrade.html#Upgrade)。

### 主题配置

关于 Hexo 的更多问题，请参考 [Hexo 官方文档](https://hexo.io/zh-cn/docs/)，或 YouTube 上 [Hexo 系列教程](https://www.youtube.com/watch?v=B0yVJ46CTR8&list=PLD5dyQmlN6xPqBV0cxO7zAe1C8OmDPqfX)视频；关于 NexT 主题的更多问题，请参考旧版的中文 [NexT 使用文档](https://theme-next.iissnan.com/)；关于如何利用 Hexo 以及 GitHub Pages 搭建个人博客的更详细内容，请参考 [GitHub + Hexo 搭建个人网站详细教程](https://zhuanlan.zhihu.com/p/26625249)。
