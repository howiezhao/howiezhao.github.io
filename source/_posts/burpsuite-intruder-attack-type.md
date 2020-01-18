---
title: Sniper、Battering ram、Pitchfork、Cluster bomb的区别
date: 2018-05-01 22:45:55
categories: CheatSheet
tags:
  - 渗透
---

Burp Suite中的Intruder模块里有4种攻击模式，分别为Sniper、Battering ram、Pitchfork、Cluster bomb，在这里假设Payload set1=[1, 2]，Payload set2=[a, b, c, d]：
## Sniper
Sniper，中文“狙击手”，每次只针对1个Payload Position，使用1个Payload set，示例如下：

Request | Position1(default:x) | Position2(default:y)
- | - | -
\#1 | 1 | y
\#2 | 2 | y
\#3 | x | 1
\#4 | x | 2

## Battering ram
Battering ram，中文“攻城槌”，每次针对多个Payload Position，使用1个Payload set，示例如下：

Request | Position1 | Position2
- | - | -
\#1 | 1 | 1
\#2 | 2 | 2

## Pitchfork
Pitchfork，中文“杈子”，每次针对多个Payload Position，使用多个Payload set，最多支持5个列表，也即5个位置，采用平行模式，请求次数以最小列表项为准，示例如下：

Request | Position1 | Position2
- | - | -
\#1 | 1 | a
\#2 | 2 | b

## Cluster bomb
Cluster bomb，中文“集束炸弹”，每次针对多个Payload Position，使用多个Payload set，最多支持5个列表，也即5个位置，采用交叉模式，请求次数为各列表项之积，示例如下：

Request | Position1 | Position2
- | - | -
\#1 | 1 | a
\#2 | 1 | b
\#3 | 1 | c
\#4 | 1 | d
\#5 | 2 | a
\#6 | 2 | b
\#7 | 2 | c
\#8 | 2 | d