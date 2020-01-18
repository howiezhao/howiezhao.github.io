---
title: 网站统计与分析
date: 2018-09-22 17:59:29
categories: CheatSheet
tags:
  - Web
---

## 几个术语
- PV：Page View，即页面浏览量或点击量，用户每次刷新即被计算一次。
- UV：Unique Visitor，指独立访客数，以cookie为依据，访问网站的一台电脑客户端为一个访客。一天内相同的客户端只会被计算一次。
- IP：指独立IP数。一天内相同IP地址只被计算一次。

## 相关工具
有许多第三方的工具可以帮助站长统计和分析网站流量，比如[百度统计](https://tongji.baidu.com)、[腾讯分析](http://ta.qq.com/)、[Google Analytics(GA)](https://analytics.google.com/analytics/web)等。个人经常使用Google Analytics。
这类工具的原理大致为：它们会生成一段特定的JS代码，站长需要将这段代码插入到自己网站的页面中，当访客访问网站时，这段代码会收集访客的行为信息，并上传到它们的服务器上。