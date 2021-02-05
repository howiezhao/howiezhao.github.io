---
title: Windows10的传递优化
date: 2018-07-16 11:27:28
categories: CheatSheet
tags:
  - Windows
---

为了方便快速的下载Windows更新，微软在Windows10中启用了一种新的更新机制，即[**传递优化**](https://privacy.microsoft.com/zh-CN/windows-10-windows-update-delivery-optimization)(Delivery Optimization)，这本质上是一种P2P架构，换句话来说，倘若开启了传递优化功能，更新时将会额外的从别的已更新的且开启传递优化功能的电脑上下载，同时也会上传已更新的文件到需要更新的电脑上。值得注意的是，传递优化对局域网进行了特殊处理，即当局域网内一台电脑完成更新后，传递优化会使得此局域网内的其他电脑依次完成更新。
开启或关闭传递优化的设置路径为：设置 ——> 更新和安全 ——> Windows更新 ——> 高级选项 ——> 传递优化。传递优化用于上传的文件路径位于：C:\Windows\Logs\dosvc。
