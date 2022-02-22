---
title: POP3、IMAP 和 SMTP
categories: CheatSheet
date: 2020-12-29 14:52:46
tags:
  - 计算机网络
---

因特网电子邮件系统由 3 个主要部分组成：

- **用户代理**（user agent）：允许用户阅读、回复、转发、保存和撰写报文，如微软的 Outlook 和 Apple Mail 等
- **邮件服务器**（mail server）：每个接收方在其中的某个邮件服务器上有一个邮箱（mailbox）
- **SMTP**

一个典型的邮件发送过程是：从发送方的用户代理开始，传输到发送方的邮件服务器（通过 SMTP 或 HTTP），再传输到接收方的邮件服务器（通过 SMTP），然后在这里被分发到接收方的邮箱中。如果发送方的邮件服务器不能将邮件交付给接收方的邮件服务器，发送方的邮件服务器在一个**报文队列**（message queue）中保持该报文并在以后尝试再次发送。

<!-- more -->

## SMTP

**SMTP**（Simple Mail Transfer Protocol，**简单邮件传输协议**）是因特网电子邮件中主要的应用层协议。它使用 TCP 可靠数据传输服务，从发送方的邮件服务器向接收方的邮件服务器发送邮件。每台邮件服务器既运行 SMTP 的客户端也运行 SMTP 的服务器端。

SMTP 一般不使用中间邮件服务器发送邮件。

SMTP 是如何将一个报文从发送邮件服务器传送到接收邮件服务器的呢？首先，客户 SMTP（运行在发送邮件服务器主机上）在 **25** 号端口建立一个到服务器 SMTP（运行在接收邮件服务器主机上）的 TCP 连接。如果服务器没有开机，客户会在稍后继续尝试连接。一旦连接建立，服务器和客户执行某些应用层的握手。在 SMTP 握手的阶段，SMTP 客户指示发送方的邮件地址（产生报文的那个人）和接收方的邮件地址。一旦握手完成，客户发送该报文。该客户如果有另外的报文要发送到该服务器，就在该相同的 TCP 连接上重复这种处理；否则，它指示 TCP 关闭连接。以下是一个例子（S 代表 SMTP 服务器，C 代表 SMTP 客户）：

```text
S: 220 hamburger.edu
C: HELO crepes.fr
S: 250 Hello crepes.fr, pleased to meet you
C: MAIL FROM: <alice@crepes.fr>
S: 250 alice@crepes.fr ... Sender ok
C: RCPT TO: <bob@hamburger.edu>
S: 250 bob@hamburger.edu ... Recipient ok
C: DATA
S: 354 Enter mail, end with "." on a line by itself
C: Do you like ketchup?
C: How about pickles?
C: .
S: 250 Message accepted for delivery
C: QUIT
S: 221 hamburger.edu closing connection
```

在上例中，该客户发送了 5 条命令：`HELO`（是 HELLO 的缩写）、`MAIL FROM`、`RCPT TO`、`DATA` 以及 `QUIT`。

当然，你也可以使用 Telnet 直接与一个 SMTP 服务器对话，如下：

```sh
telnet smtp.office365.com 25
```

### 与 HTTP 的对比

SMTP 与 HTTP 有一些共同的特征：

- 这两个协议都用于从一台主机向另一台主机传送文件
- 当进行文件传送时，持续的 HTTP 和 SMTP 都使用持续连接

然而，两者之间也有一些重要的区别：

首先，HTTP 主要是一个**拉协议**（pull protocol），即在方便的时候，某些人在 Web 服务器上装载信息，用户使用 HTTP 从该服务器拉取这些信息。特别是 TCP 连接是由想接收文件的机器发起的。另一方面，SMTP 基本上是一个**推协议**（push protocol），即发送邮件服务器把文件推向接收邮件服务器。特别是，这个 TCP 连接是由发送该文件的机器发起的。

第二个区别是由于问世较早， SMTP 要求每个报文（包括它们的体）采用 7 比特 ASCII 码格式。如果某报文包含了非 7 比特 ASCII 字符（如具有重音的法文字符）或二进制数据（如图形文件），则该报文必须按照 7 比特 ASCII 码进行编码。HTTP 数据则不受这种限制。

第三个重要区别是如何处理一个既包含文本又包含图形（也可能是其他媒体类型）的文档。HTTP 把每个对象封装到它自己的 HTTP 响应报文中，而 SMTP 则把所有报文对象放在一个报文之中。

### 邮件报文格式

如同 HTTP 协议，邮件报文也有相应的邮件首部行，每个首部行包含了可读的文本，是由关键词后跟冒号及其值组成的。某些关键词是必须的，另一些则是可选的。每个首部 *必须* 含有一个 `From:` 首部行和一个 `To:` 首部行；一个首部 *也许* 包含一个 `Subject:` 首部行以及其他可选的首部行。

一个典型的报文首部看看起来如下：

```text
From: alice@crepes.fr
To: bob@hamburger.edu
Subject: Searching for the meaning of life.
```

## POP3

**POP3**（Post Office Protocol——Version 3，**第三版的邮局协议**）是一个极为简单的邮件访问协议。

当用户代理（客户）打开了一个到邮件服务器（服务器）端口 **110** 上的 TCP 连接后，POP3 就开始工作了。随着建立 TCP 连接，POP3 按照 3 个阶段进行工作：

1. **特许**（authorization）：用户代理发送（以明文形式）用户名和口令以鉴别用户
2. **事务处理**：用户代理取回报文；同时在这个阶段用户代理还能进行如下操作，对报文做删除标记，取消报文删除标记，以及获取邮件的统计信息
3. **更新**：它出现在客户发出了 quit 命令之后，目的是结束该 POP3 会话；这时，该邮件服务器删除那些被标记为删除的报文

在 POP3 的事务处理过程中，用户代理发出一些命令，服务器对每个命令做出回答。回答可能有两种：

- `+OK`：（有时后面还跟有服务器到客户的数据），被服务器用来指示前面的命令是正常的
- `-ERR`：被服务器用来指示前面的命令出现了某些差错

特许阶段有两个主要的命令：`user <user name>` 和 `pass <password>`。你可以使用 Telnet 进行测试，如下：

```text
telnet outlook.office365.com 110
+OK The Microsoft Exchange POP3 service is ready.
user bob
+OK
pass hungry
+OK user successfully logged on
```

在特许阶段以后，用户代理仅使用 4 个命令 `list`、`retr`、`dele` 和 `quit`。

使用 POP3 的用户代理通常被用户配置为“**下载并删除**”或者“**下载并保留**”方式。POP3 用户代理发出的命令序列取决于用户代理程序被配置为这两种工作方式的哪一种。使用下载并删除方式，用户代理发出 `list` —— `retr` —— `dele` 命令，如下（C 代表客户，S 代表服务器）：

```text
C: list
S: 1 498
S: 2 912
S: .
C: retr 1
S: (blah blah ...
S: .................
S: ..........blah)
S: .
C: dele 1
C: retr 2
S: (blah blah ...
S: .................
S: ..........blah)
S: .
C: dele 2
C: quit
S: +OK POP3 server signing off
```

使用下载并保留方式，用户代理下载某邮件后，该邮件仍保留在邮件服务器上。

## IMAP

**IMAP**（Internet Mail Access Protocol，**因特网邮件访问协议**）是一个相比 POP3 更强大的邮件访问协议。

相比 POP3，IMAP 协议为用户提供了创建文件夹以及将邮件从一个文件夹移动到另一个文件夹的命令；还为用户提供了在远程文件夹中查询邮件的命令，按指定条件去查询匹配的邮件；它还提供了允许用户代理获取报文某些部分的命令。

## 其他

相比于 SMTP，POP3 和 IMAP 等邮件访问协议本质上属于拉协议，在基于 Web 的电子邮件中，则可以通过 HTTP 进行邮件的收发，此时，用户代理就是普通的浏览器。
