---
title: 关于Windows的代理设置
categories: CheatSheet
date: 2019-07-29 12:21:18
tags:
  - Windows
---
Windows的**系统代理**使用的其实是**IE的代理设置**，此外，对于**绝大多数**的应用程序而言，它们默认使用的也是IE的代理设置，比如，Chrome、Firefox、Microsoft Store等。因此，如果想让绝大多数的应用程序使用代理，一个简单的方法是直接设置IE的代理（即系统代理）。不过，对于一小部分没有使用IE代理设置的应用程序，比如Android Studio等，你可能需要单独设置它们的代理（一般在软件的设置项中）。

值得注意的是，同为应用程序的**Shell**（包括**命令提示符**和**PowerShell**）就没有使用IE的代理设置，它们各自有自己的代理设置。具体而言，要为命令提示符设置代理，可使用如下两条命令：
```
set HTTP_PROXY=http://user:password@proxy.domain.com:port
set HTTPS_PROXY=https://user:password@proxy.domain.com:port
```
而要为PowerShell设置代理则要使用[这个脚本]()。

最后，对于Shell中运行的程序，有一部分使用的是IE的代理设置，比如`pip`、`git`、`npm`等，另一部分则使用的是Shell的代理设置，比如`curl`、`gem`等。