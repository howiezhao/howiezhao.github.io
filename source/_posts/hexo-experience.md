---
title: Hexo初体验
date: 2017-06-20 17:38:54
categories: CheatSheet
tags:
  - Hexo
---
[Hexo](https://hexo.io/zh-cn/index.html)是一个基于Node.js的开源静态博客框架，类似的项目还有基于Ruby的[Jekyll](https://jekyllrb.com/)，基于Go的[Hugo](https://gohugo.io/)，基于Python的[Pelican](https://blog.getpelican.com/)等等。之所以选择Hexo，主要是因为它不仅使用人数多，而且有中文文档。
## 安装

安装Hexo前，需要安装[Node.js](https://nodejs.org/en/download/)和[Git](https://git-scm.com/downloads)，安装Node.js的同时，npm(Node Package Manager)也已经被自动安装了，同时安装程序也自动配置了环境变量。确定安装完成后，可以输入`node -v`来测试Node.js是否成功安装，输入`npm -v`来测试npm是否成功安装。
npm成功安装后，可使用`npm install -g hexo-cli`来快速安装Hexo命令行工具。参数`-g`表示全局安装，npm的包安装分为本地安装（local）和全局安装（global）两种，区别在于：

**本地安装**
- 将安装包放在 ./node_modules 下（运行npm时所在的目录）
- 可以通过 require() 来引入本地安装的包

**全局安装**
- 将安装包放在 /usr/local下
- 可以直接在命令行里使用
<!-- more -->

关于npm更多的内容请参考[npm模块安装机制简介](http://www.ruanyifeng.com/blog/2016/01/npm-install.html)。

## 更新
在博客所在目录执行`hexo version`即可查看Hexo版本信息，在博客所在目录执行`npm update -g`即可更新Hexo。

## 常用命令

### 新建一个网站
``` bash
hexo init [folder]
```
如果没有设置`folder`，Hexo 默认在目前的文件夹建立网站。

### 新建一篇文章
``` bash
hexo n [layout] <title>
或 hexo new [layout] <title>
```
如果没有设置`layout`的话，默认使用 _config.yml 中的`default_layout`参数代替。如果标题包含空格的话，请使用引号括起来。

### 生成静态文件
``` bash
hexo g
或 hexo generate
```

### 启动服务预览
``` bash
hexo s
或 hexo server
```
默认情况下，访问网址为：http://localhost:4000/ 。

### 部署网站
``` bash
hexo d
或 hexo deploy
```

### 清除缓存文件(db.json)和已生成的静态文件(public)。
``` bash
$ hexo clean
```
在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

## 更多
### 目录结构
Hexo生成的网站目录结构如下：
- `public`：此目录下保存着已经生成的静态文件
- `scaffolds`：此目录下存放Hexo模板，当您新建文章时，Hexo会根据scaffold来建立文件。
- `source`：此目录下存放用户资源
    - `_posts`：此目录下存放Markdown格式的源文章
    - `images`：此目录下存放相关图片文件
- `themes`：此目录下保存着主题文件
- `_config.yml`：此文件为**站点配置文件**

### 最佳实践
站点配置文件（`_config.yml`）中的`url`字段务必要填写为自己站点的正确网址，否则分享自己站点内文章时会生成错误链接。
新建文章（`hexo n <title>`）时建议使用小写英文作为文件名，此文件名将作为文章链接的一部分，英文中的空格将自动用`-`替代，文章标题可以在文件中另行设置。
和传统的博客一样，建议开启**分类**（category）和**标签**（tag）功能，在Hexo中，分类具有**顺序性**和**层次性**，也就是说`Foo，Bar`不等于`Bar，Foo`，而标签没有顺序和层次。简单来说，分类应该是经过深思熟虑的，而标签则可适文章而决定，分类一般只有几个，而标签可以有一堆。具体而言，可以参考本站点的分类标签设计。

## 插件
Hexo支持[许多插件](https://hexo.io/plugins/)，个人经常使用的插件如下：
- [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)：为Hexo打造的Git部署插件，适用于将博客部署到GitHub仓库上。
- [hexo-symbols-count-time](https://github.com/theme-next/hexo-symbols-count-time)：适用于为文章添加字数统计和阅读时长统计，比同类型的[hexo-wordcount](https://github.com/willin/hexo-wordcount)插件要更好。
- [hexo-generator-searchdb](https://github.com/theme-next/hexo-generator-searchdb)：适用于为博客添加本地搜索功能。
- [hexo-generator-feed](https://github.com/hexojs/hexo-generator-feed)：适用于为博客添加RSS功能。

使用如下命令即可安装上面提到的所有插件：
```
npm install hexo-deployer-git hexo-symbols-count-time hexo-generator-searchdb hexo-generator-feed --save
```

## 主题
安装Hexo后，默认使用的主题为landscape，个人不是很喜欢这个主题，所幸的是Hexo提供[更多的第三方主题](https://hexo.io/themes/)，个人倾向于使用广为流行的[NexT主题](https://theme-next.org/)。
值得注意的是，NexT主题在6.0.0版本之前由iissnan个人维护，其官方仓库为https://github.com/iissnan/hexo-theme-next ，官网为https://theme-next.iissnan.com/ ，在6.0.0版本之后由theme-next组织维护，其官方仓库更改为https://github.com/theme-next/hexo-theme-next ，官网为https://theme-next.org 。这里所介绍的使用方法均以6.0.0版本之后为例。
### 安装
要安装NexT主题，首先要进入Hexo站点目录下，接着执行`git clone https://github.com/theme-next/hexo-theme-next themes/next`命令，即可将NexT仓库克隆到本地。要启用NexT主题，只需在**站点配置文件**中找到`theme`字段，并将其值更改为`next`即可。
### 更新
要查看正在使用的NexT主题的版本，有如下几种方法：
- 可直接打开**主题配置文件**（即站点目录下的`/themes/next/_config.yml`文件），在其底部`version`字段即可查看版本号。
- 在自己站点的底部一般会有Hexo和NexT的版本号

和传统的Git仓库更新一样，进入站点目录下的`/themes/next`文件夹，执行`git pull`命令即可从官方仓库拉取最新代码进行更新。
如果你使用的是6.0.0之前的版本，现在想要升级到6.0.0之后的版本，可参考NexT主题官方给出的[解决方案](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/UPDATE-FROM-5.1.X.md)。
### 主题配置

关于Hexo的更多问题，请参考[Hexo官方文档](https://hexo.io/zh-cn/docs/)，或YouTube上[Hexo系列教程](https://www.youtube.com/watch?v=bCj0iVVqkSg&feature=youtu.be)视频；关于NexT主题的更多问题，请参考[NexT使用文档](https://theme-next.iissnan.com/)；关于如何利用Hexo以及GitHub Pages搭建个人博客的更详细内容，请参考[GitHub + Hexo 搭建个人网站详细教程](https://zhuanlan.zhihu.com/p/26625249)。