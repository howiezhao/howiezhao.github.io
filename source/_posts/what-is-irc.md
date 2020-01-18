---
title: IRC是什么
date: 2018-09-12 21:59:18
categories: CheatSheet
tags:
  - 计算机网络
---

**IRC**，全称Internet Relay Chat，即**因特网中继聊天**，是早期经常使用的网络聊天方式，其主要用于群体聊天，但同样也可以用于个人对个人的聊天。
IRC协议属于应用层协议，使用的传输层协议为TCP，使用的端口为**6667**(明文传输，如irc://chat.freenode.net)或**6697**(SSL加密传输，如ircs://chat.freenode.net:6697)。
IRC是一个**分布式**的**C/S**架构，一个IRC服务器可以连接其他的IRC服务器以扩展为一个**IRC网络**，通过连接到一个IRC服务器，我们可以访问这个服务器以及它所连接的其他服务器上的**频道**，频道存在于一个IRC服务器上，一个频道类似于一个聊天室，频道名称必须以`#`符号开始，例如`#irchelp`。大多数的IRC服务器不需要客户注册登录，虽然在连接前必须设定好昵称（nickname），但客户端一般都会自动分配一个。目前使用最广的IRC服务器为[freenode](https://freenode.net/)，而IRC客户端软件有多种，比如基于Firefox浏览器的IRC插件[ChatZilla](http://chatzilla.hacksrus.com/)，基于网页的[Webchat](https://webchat.freenode.net/)，基于命令行的[Irssi](https://irssi.org/)等等。
个人经常使用的IRC客户端为Irssi，在Ubuntu中可以使用`apt install irssi`安装，之后直接输入`irssi`即可启动，输入`irssi --help`可查看更多命令参数。启动irssi后可输入更多的命令，输入`/help`可查看所有可用命令，输入`/connect Freenode`即可连接到freenode服务器，之后再输入`/join #linuxba`即可加入`#linuxba`频道。这里需要注意，freenode服务器由于种种原因，在国内无法访问，而irssi又不支持代理，所以推荐使用[proxychains](https://github.com/haad/proxychains)代理irssi。
最后，值得推荐的IRC频道有下(基于freenode)：
- `#ubuntu-cn`：Ubuntu中文社区频道
- `#archlinux-cn`：Arch Linux中文社区频道
- `#linuxba`：Linux贴吧频道
- `#haskell`：Haskell语言频道
- `#vim`：Vim社区频道