---
title: 使用 BOINC 来挖掘格雷德币
categories: CheatSheet
date: 2018-12-16 17:06:10
tags:
---

## BOINC

[BOINC](https://boinc.berkeley.edu/)，全称 Berkeley Open Infrastructure for Network Computing，即伯克利开放式网络计算平台，是由加州大学伯克利分校发展出的分布式计算平台。BOINC 会利用志愿者电脑的空闲资源来对各个项目下发的任务进行运算，目前 BOINC 平台上有如下知名项目：

- [SETI@home](https://setiathome.berkeley.edu/)：由加州大学伯克利分校主办，主要目的为搜索外太空文明。
- [Einstein@Home](https://einsteinathome.org/zh-cn/home)：由威斯康星大学密尔沃基分校主办，主要目的为搜索脉冲星的引力波。
- [GPUGrid.net](http://www.gpugrid.net/index.php)：主要目的为做分子生物动力学相关的研究。
- [IBM World Community Grid](https://www.worldcommunitygrid.org/discover.action)：中文翻译为“世界公共网格”，由 IBM 主办，主要目的为利用分布式计算来帮助查找人类疾病的治疗方法，和改善人类生活的相关研究。随着项目的不断扩大，World Community Grid 逐渐发展成为一个医药、生物和环境等各种方面研究类的更高层次分布式计算平台。目前正在该平台上运行的知名子项目包括：
  - [FightAIDS@Home](https://www.worldcommunitygrid.org/research/faah/overview.do?language=zh_CN)：主要目的为研究 HIV 的治疗方法。

<!-- more -->

### 安装

在 Ubuntu 中，执行如下命令即可安装：

```shell
sudo apt install boinc-client boinc-manager
```

如果你想使用 BOINC 来挖掘格雷德币，请不要在首次启动后按照提示添加项目，具体的操作可参考下面的步骤。

## Gridcoin

[Gridcoin](https://gridcoin.us/)，简称 GRC，中文翻译为“格雷德币”，一种开源的数字货币，其主要用于奖励在 BOINC 平台上参与计算的志愿者。

值得注意的是，并非所有的 BOINC 项目都会奖励格雷德币，只有参与特定的项目才会获得格雷德币，具体的项目列表可参考 Gridcoin 官方的[项目白名单](https://gridcoin.us/Guides/whitelist.htm)，这份白名单里也列出了哪些项目会使用到 GPU 进行运算。

### 矿池

Gridcoin 官网中提到了 2 个矿池：[grcpool](https://www.grcpool.com/) 和 [Arikado Pool](https://grc.arikado.ru/)，建议使用 grcpool，以下是为 BOINC 配置 grcpool 矿池的具体过程：

1. 前往 grcpool 注册一个账号。
2. 切换到 BOINC 的高级视图：依次点击 `View` ——> `Advanced View`。
3. 配置 grcpool 矿池：依次点击 `Tools` ——> `Use Account Manager`，打开对话框，选择 `grcpool`，输入之前注册的账号和密码，并确定。
4. 转到 grcpool 的个人信息页面，点击 `Hosts` 下的 `My Hosts`，你将会看到刚刚添加的计算机名，点击进去，选择 `choose project`，挑选自己感兴趣的项目，点击 `add`，最后点击页面左上方的 `save project settings` 进行保存。
5. 在 BOINC 中进行同步：依次点击 `Tools` ——> `Synchronize with grcpool.com`，并按照提示完成。
