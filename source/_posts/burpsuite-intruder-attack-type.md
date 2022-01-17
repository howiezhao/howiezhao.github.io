---
title: Sniper、Battering ram、Pitchfork、Cluster bomb 的区别
date: 2018-05-01 22:45:55
categories: CheatSheet
tags:
  - 渗透
---

Burp Suite 中的 Intruder 模块里有 4 种攻击模式，分别为 Sniper、Battering ram、Pitchfork、Cluster bomb，在这里假设 Payload set1=[1, 2]，Payload set2=[a, b, c, d]：

## Sniper

Sniper，中文“狙击手”，每次只针对 1 个 Payload Position，使用 1 个 Payload set，示例如下：

Request | Position1(default:x) | Position2(default:y)
--- | --- | ---
\#1 | 1 | y
\#2 | 2 | y
\#3 | x | 1
\#4 | x | 2

## Battering ram

Battering ram，中文“攻城槌”，每次针对多个 Payload Position，使用 1 个 Payload set，示例如下：

Request | Position1 | Position2
--- | --- | ---
\#1 | 1 | 1
\#2 | 2 | 2

## Pitchfork

Pitchfork，中文“杈子”，每次针对多个 Payload Position，使用多个 Payload set，最多支持 5 个列表，也即 5 个位置，采用平行模式，请求次数以最小列表项为准，示例如下：

Request | Position1 | Position2
--- | --- | ---
\#1 | 1 | a
\#2 | 2 | b

## Cluster bomb

Cluster bomb，中文“集束炸弹”，每次针对多个 Payload Position，使用多个 Payload set，最多支持 5 个列表，也即 5 个位置，采用交叉模式，请求次数为各列表项之积，示例如下：

Request | Position1 | Position2
--- | --- | ---
\#1 | 1 | a
\#2 | 1 | b
\#3 | 1 | c
\#4 | 1 | d
\#5 | 2 | a
\#6 | 2 | b
\#7 | 2 | c
\#8 | 2 | d
