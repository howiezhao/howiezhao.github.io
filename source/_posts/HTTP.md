---
title: HTTP 协议分析
date: 2018-05-11 16:39:06
categories: CheatSheet
tags:
  - 计算机网络
---

HTTP，全称 Hypertext Transfer Protocol，即超文本传输协议。

## 报文格式

### HTTP请求报文

![http request](/images/http-request.PNG)

<!-- more -->

方法字段可以取几种不同的值，包括 **GET**、**POST**、**HEAD**、**PUT** 和 **DELETE**。绝大部分的 HTTP 请求报文使用 GET 方法。

**Host** 首部行指明对象所在的主机，该信息是 Web 代理高速缓存所要求的；**Connection** 首部行指明采用非持续连接还是持续连接；**User-Agent** 首部行指明用户代理；**Accept-Language** 首部行指明用户想得到的语言版本。

使用 GET 方法时实体体（entity body）为空，而使用 POST 方法时才使用该实体体。

HEAD 方法类似于 GET 方法。当服务器收到使用 HEAD 方法的请求时，将会用一个 HTTP 报文进行响应，但是并不返回请求对象。应用程序开发者常用 HEAD 方法进行调试跟踪。PUT 方法常与 Web 发行工具联合使用，它运行用户上传对象到指定的 Web 服务器上指定的路径（目录）。PUT 方法也被那些需要向 Web 服务器上传对象的应用程序使用。DELETE 方法允许用户或者应用程序删除 Web 服务器上的对象。

### HTTP 响应报文

![http response](/images/http-response.PNG)

**Date** 首部行指示服务器产生并发送该响应报文的日期和时间；**Last-Modified** 首部行指示了对象创建或者最后修改的日期和时间；**Server** 首部行指示服务器类型，类似于 User-Agent 首部行；**Content-Length** 首部行指示了被发送对象中的字节数；**Content-Type** 首部行指示了实体体中的对象的 MIME 类型。

常见的状态码和其对应的短语：

- 200 OK：请求成功，信息在返回的响应报文中。
- 301 Moved Permanently：请求的对象已经被 **永久** 转移了，新的 URL 定义在响应报文的 Location 首部行中。客户软件将自动获取新的 URL。
- 302 Moved Temporarily：请求的对象已经被 **暂时** 转移了，新的 URL 定义在响应报文的 Location 首部行中。客户软件将自动获取新的 URL。
- 400 Bad Request：一个通用差错代码，指示该请求不能被服务器理解。
- 403 Forbidden：客户端没有权限访问此资源。
- 404 Not Found：被请求的文档不在服务器上。
- 505 HTTP Version Not Supported：服务器不支持请求报文使用的 HTTP 协议版本。

一般而言，200 系列代表正常，300 系列代表重定向，400 系列代表客户端错误，500 系列代表服务端错误。

## Web缓存

**条件 GET（conditional GET）方法**：请求报文使用 GET 方法，并且请求报文中包含一个 **If-Modified-Since** 首部行。

Web 缓存器为了验证所缓存的对象是否是最新的，会使用条件 GET 方法向目标服务器发送一个请求报文，If-Modified-Since 首部行的值为当初缓存对象时响应报文中 Last-Modified 首部行的值。如果所要验证的对象是最新的，即没有被修改过，则目标服务器会返回一个“304 Not Modified”响应报文，其中实体体为空。

## 注意

1. HTTP 是一个无状态协议（stateless protocol）。
2. HTTP 可以采用非持续连接或持续连接，默认采用持续连接。
