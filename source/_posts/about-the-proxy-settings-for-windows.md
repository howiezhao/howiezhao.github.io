---
title: 关于 Windows 的代理设置
categories: CheatSheet
date: 2019-07-29 12:21:18
tags:
  - Windows
---
Windows 的**系统代理**使用的其实是 **IE 的代理设置**，此外，对于**绝大多数**的应用程序而言，它们默认使用的也是 IE 的代理设置，比如，Chrome、Firefox、Microsoft Store 等。因此，如果想让绝大多数的应用程序使用代理，一个简单的方法是直接设置 IE 的代理（即系统代理）。不过，对于一小部分没有使用 IE 代理设置的应用程序，比如 Android Studio 等，你可能需要单独设置它们的代理（一般在软件的设置项中）。

值得注意的是，同为应用程序的 **Shell**（包括**命令提示符**和 **PowerShell**）就没有使用 IE 的代理设置，它们各自有自己的代理设置。具体而言，要为命令提示符设置代理，可使用如下两条命令：

```sh
set HTTP_PROXY=http://user:password@proxy.domain.com:port
set HTTPS_PROXY=https://user:password@proxy.domain.com:port
```

而要为 PowerShell 设置代理则要使用[这个脚本](todo)。

对于 Shell 中运行的程序，有一部分使用的是 IE 的代理设置，比如 `pip`、`npm` 等，另一部分则使用的是 Shell 的代理设置，比如 `curl`、`gem` 等。

此外，有一些程序的代理设置相对比较复杂，比如 {% post_link git git %}、{% post_link docker docker %} 等，详见它们各自的介绍文章。
