---
title: 版本号的意义
date: 2018-09-21 20:51:08
categories: CheatSheet
tags:
---

软件版本号的确定没有一个统一的规范，但大都遵循一个固定的格式，即`X.Y.Z`格式，其中：

- X代表**主版本号**，一般当软件整体重写，或出现不向后兼容的改变等重大更新时，增加X，同时重置Y、Z为0，X为0时表示软件还在开发阶段；
- Y代表**次版本号**，增删功能时增加Y，同时重置Z为0；
- Z代表**修订号**，修复Bug时增加Z。

除此之外，还会有一些修饰词，比如：

- `alpha`表示内部测试版；
- `beta`表示公开测试版；
- `rc`即Release Candidate，表示候选版本，即将作为正式版发布；
- `release`表示正式发行版；
- `lts`即Long Term Support，表示长期支持版。

有的项目有自己的一套规则，比如Ubuntu、Visual Studio等，它们采用发布年份作为版本号；Node.js规定X为偶数的是稳定版，X为奇数的是开发版；TeX的版本号不断趋近于π。
随着版本号定义的越来越混乱，GitHub起草了一个[语义化版本(Semantic Versioning)](https://semver.org/lang/zh-CN/)规范，为开源项目做出了一定指导意义。
