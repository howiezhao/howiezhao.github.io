---
title: HTTP协议分析
date: 2018-05-11 16:39:06
categories: CheatSheet
tags:
  - 计算机网络
---

HTTP(Hypertext Transfer Protocol，超文本传输协议)
## 报文格式
### HTTP请求报文
![](/images/http-request.PNG)
<!-- more -->
方法字段可以取几种不同的值，包括**GET**、**POST**、**HEAD**、**PUT**和**DELETE**。绝大部分的HTTP请求报文使用GET方法。

**Host**首部行指明对象所在的主机，该信息是Web代理高速缓存所要求的；**Connection**首部行指明采用非持续连接还是持续连接；**User-Agent**首部行指明用户代理；**Accept-Language**首部行指明用户想得到的语言版本。

使用GET方法时实体体(entity body)为空，而使用POST方法时才使用该实体体。

HEAD方法类似于GET方法。当服务器收到使用HEAD方法的请求时，将会用一个HTTP报文进行响应，但是并不返回请求对象。应用程序开发者常用HEAD方法进行调试跟踪。PUT方法常与Web发行工具联合使用，它运行用户上传对象到指定的Web服务器上指定的路径(目录)。PUT方法也被那些需要向Web服务器上传对象的应用程序使用。DELETE方法允许用户或者应用程序删除Web服务器上的对象。

### HTTP响应报文
![](/images/http-response.PNG)
**Date**首部行指示服务器产生并发送该响应报文的日期和时间；**Last-Modified**首部行指示了对象创建或者最后修改的日期和时间；**Server**首部行指示服务器类型，类似于User-Agent首部行；**Content-Length**首部行指示了被发送对象中的字节数；**Content-Type**首部行指示了实体体中的对象的MIME类型。

常见的状态码和其对应的短语：
200 OK：请求成功，信息在返回的响应报文中。
301 Moved Permanently：请求的对象已经被 **永久** 转移了，新的URL定义在响应报文的Location首部行中。客户软件将自动获取新的URL。
302 Moved Temporarily：请求的对象已经被 **暂时** 转移了，新的URL定义在响应报文的Location首部行中。客户软件将自动获取新的URL。
400 Bad Request：一个通用差错代码，指示该请求不能被服务器理解。
403 Forbidden：客户端没有权限访问此资源。
404 Not Found：被请求的文档不在服务器上。
505 HTTP Version Not Supported：服务器不支持请求报文使用的HTTP协议版本。

一般而言，200系列代表正常，300系列代表重定向，400系列代表客户端错误，500系列代表服务端错误。
## Web缓存
**条件GET(conditional GET)方法**：请求报文使用GET方法，并且请求报文中包含一个**If-Modified-Since**首部行。

Web缓存器为了验证所缓存的对象是否是最新的，会使用条件GET方法向目标服务器发送一个请求报文，If-Modified-Since首部行的值为当初缓存对象时响应报文中Last-Modified首部行的值。如果所要验证的对象是最新的，即没有被修改过，则目标服务器会返回一个“304 Not Modified”响应报文，其中实体体为空。

## 注意
1. HTTP是一个无状态协议(stateless protocol)。
2. HTTP可以采用非持续连接或持续连接，默认采用持续连接。