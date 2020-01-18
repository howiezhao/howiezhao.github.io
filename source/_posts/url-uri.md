---
title: URI与URL的区别
date: 2018-04-29 16:40:08
categories: CheatSheet
tags:
  - Web
---

URI，全称"Uniform Resource Identifier"，中文“统一资源标志符”，是一个用于标识某一互联网资源名称的字符串。URI的最常见的形式是统一资源定位符（URL），经常指定为非正式的网址。更罕见的用法是统一资源名称（URN），其目的是通过提供一种途径，用于在特定的名字空间资源的标识，以补充网址。

URL，全称"Uniform Resource Locator"，中文“统一资源定位符”，URL是URI的子集。示例如下：
`https://howiezhao.github.io/2018/04/29/url-uri/`
上面这个URL唯一标识了互联网中一台服务器上的一篇文章(即本篇文章)。
URL的格式一般为`scheme:[//[user[:password]@]host[:port]][/path][?query][#fragment]`

URN，全称"Uniform Resource Name"，中文“统一资源名称”，是另一种形式的URI，它通过特定命名空间中的唯一名称来标识资源。示例如下：
`urn:isbn:9780141036144`
上面这个URN唯一标识了乔治·奥威尔所著的《1984》。

简单说，URL代表一个人的位置，URN代表一个人的身份证号，通过URL和URN都可以唯一的找到这个人，所以它们都属于URI。