---
title: HTTP 协议分析
date: 2018-05-11 16:39:06
categories: CheatSheet
tags:
  - 计算机网络
---

**HTTP**，全称 Hypertext Transfer Protocol，即**超文本传输协议**。HTTP 定义了 Web 客户向 Web 服务请求 Web 页面的方式，以及服务器向客户传送 Web 页面的方式。HTTP 使用 TCP 作为它的支撑运输协议。

## 术语

在详细解释 HTTP 之前，应当回顾某些 Web 术语。

**Web 页面**（Web page）（也叫文档）是由对象组成的。一个**对象**（object）只是一个文件，诸如一个 HTML 文件、一个 JPEG 图形、一个 Java 小程序或一个视频片段这样的文件，且它们可通过一个 URL 地址寻址。多数 Web 页面含有一个 **HTML 基本文件**（base HTML file）以及几个引用对象。HTML 基本文件通过对象的 URL 地址引用页面中的其他对象。每个 URL 地址由两部分组成：存放对象的服务器主机名和对象的路径名。

因为 **Web 浏览器**（Web browser）（例如 Chrome 和 Firefox）实现了 HTTP 的客户端，所以在 Web 环境中我们经常交替使用“浏览器”和“客户”这两个术语。**Web 服务器**（Web server）实现了 HTTP 的服务器端，它用于存储 Web 对象，每个对象由 URL 寻址。流行的 Web 服务器有 Apache 和 Nginx。

<!-- more -->

## 报文格式

HTTP 规范包含了对 HTTP 报文格式的定义。HTTP 报文有两种：请求报文和响应报文。

### HTTP 请求报文

一个典型的示例如下：

```text
GET /somedir/page.html HTTP/1.1
Host: www.someschool.edu
Connection: close
User-Agent: Mozilla/5.0
Accept-Language: fr
```

HTTP 请求报文的第一行叫做**请求行**（request line），其后继的行叫做**首部行**（header line）。

请求行有 3 个字段：方法字段、URL 字段和 HTTP 版本字段。方法字段可以取几种不同的值，包括 **GET**、**POST**、**HEAD**、**PUT** 和 **DELETE**。绝大部分的 HTTP 请求报文使用 GET 方法。

**Host** 首部行指明对象所在的主机，该信息是 Web 代理高速缓存所要求的；**Connection** 首部行指明采用非持续连接还是持续连接；**User-Agent** 首部行指明用户代理；**Accept-Language** 首部行指明用户想得到的语言版本。

以下是请求报文的通用格式：

![http request](/images/http-request.PNG)

使用 GET 方法时实体体（entity body）为空，而使用 POST 方法时才使用该实体体。

HEAD 方法类似于 GET 方法。当服务器收到使用 HEAD 方法的请求时，将会用一个 HTTP 报文进行响应，但是并不返回请求对象。应用程序开发者常用 HEAD 方法进行调试跟踪。PUT 方法常与 Web 发行工具联合使用，它运行用户上传对象到指定的 Web 服务器上指定的路径（目录）。PUT 方法也被那些需要向 Web 服务器上传对象的应用程序使用。DELETE 方法允许用户或者应用程序删除 Web 服务器上的对象。

### HTTP 响应报文

一个典型的示例如下：

```text
HTTP/1.1 200 OK
Connection: close
Date: Tue, 18 Aug 2015 15:44:04 GMT
Server: Apache/2.2.3 (CentOS)
Last-Modified: Tue, 18 Aug 2015 15:11:03 GMT
Content-Length: 6821
Content-Type: text/html

(data data data data data ...)
```

上述响应报文有三个部分：一个初始**状态行**（status line），6 个**首部行**（header line），然后是**实体体**（entity body）。

实体体部分是报文的主要部分，即它包含了所请求的对象本身。状态行有 3 个字段：协议版本字段、状态码和相应状态信息。

**Date** 首部行指示服务器**产生并发送**该响应报文的日期和时间；**Server** 首部行指示服务器类型，类似于 User-Agent 首部行；**Last-Modified** 首部行指示了对象创建或者最后修改的日期和时间，该信息对 Web 缓存至关重要；**Content-Length** 首部行指示了被发送对象中的字节数；**Content-Type** 首部行指示了实体体中的对象的 MIME 类型。

以下是响应报文的通用格式：

![http response](/images/http-response.PNG)

常见的状态码和其对应的短语：

- 200 OK：请求成功，信息在返回的响应报文中。
- 301 Moved Permanently：请求的对象已经被 **永久** 转移了，新的 URL 定义在响应报文的 Location 首部行中。客户软件将自动获取新的 URL。
- 302 Moved Temporarily：请求的对象已经被 **暂时** 转移了，新的 URL 定义在响应报文的 Location 首部行中。客户软件将自动获取新的 URL。
- 400 Bad Request：一个通用差错代码，指示该请求不能被服务器理解。
- 403 Forbidden：客户端没有权限访问此资源。
- 404 Not Found：被请求的文档不在服务器上。
- 505 HTTP Version Not Supported：服务器不支持请求报文使用的 HTTP 协议版本。

一般而言，200 系列代表正常，300 系列代表重定向，400 系列代表客户端错误，500 系列代表服务端错误。

## Web 缓存

**Web 缓存器**（Web cache）也叫**代理服务器**（proxy server），它是能够代表初始 Web 服务器来满足 HTTP 请求的网络实体。Web 缓存器有自己的磁盘存储空间，并在存储空间中保存最近请求过的对象的副本。

值得注意的是 Web 缓存器即是服务器又是客户。当它接收浏览器的请求并发回响应时，它是一个服务器。当它向初始服务器发出请求并接收响应时，它是一个客户。

Web 缓存器通常由 ISP 购买并安装。实践中的**命中率**（即由一个缓存器所满足的请求的比率）通常在 **0.2 ~ 0.7** 之间。

在因特网上部署 Web 缓存器有两个原因：

- Web 缓存器可以大大减少对客户请求的响应时间
- Web 缓存器能够大大减少一个机构的接入链路到因特网的通信量

**条件 GET（conditional GET）方法**：请求报文使用 GET 方法，并且请求报文中包含一个 **If-Modified-Since** 首部行。

Web 缓存器为了验证所缓存的对象是否是最新的，会使用条件 GET 方法向目标服务器发送一个请求报文，If-Modified-Since 首部行的值为当初缓存对象时响应报文中 Last-Modified 首部行的值。如果所要验证的对象是最新的，即没有被修改过，则目标服务器会返回一个“**304 Not Modified**”响应报文，其中实体体为空。

通过使用 CDN（Content Distribution Network，内容分发网络），Web 缓存器正在因特网中发挥着越来越重要的作用。CDN 公司在因特网上安装了许多地理上分散的缓存器，因而使大量流量实现了本地化。

## 注意

- HTTP 是一个**无状态协议**（stateless protocol），即 HTTP 服务器并不保存关于客户的任何信息。但我们可以通过 cookie 机制实现有状态的访问。
- HTTP 可以采用非持续连接或持续连接，默认采用持续连接。
- 有些地方还将 HTTP 描述为无连接，纵观上述，找不到这样描述的原因。
