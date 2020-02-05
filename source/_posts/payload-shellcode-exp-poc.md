---
title: 渗透中 PoC、Exp、Payload 与 Shellcode 的区别
date: 2018-04-29 16:33:17
categories: CheatSheet
tags:
  - 渗透
---

PoC，全称“Proof of Concept”，中文“概念验证”，常指一段漏洞证明的代码。

Exp，全称“Exploit”，中文“利用”，指利用系统漏洞进行攻击的动作。

Payload，中文“有效载荷”，指成功 exploit 之后，真正在目标系统执行的代码或指令。

Shellcode，简单翻译“shell 代码”，是 Payload 的一种，由于其建立正向/反向 shell 而得名。

几点注意：
PoC 是用来证明漏洞存在的，Exp 是用来利用漏洞的，两者通常不是一类，或者说，PoC 通常是无害的，Exp 通常是有害的，有了 PoC，才有 Exp。

Payload 有很多种，它可以是 Shellcode，也可以直接是一段系统命令。同一个 Payload 可以用于多个漏洞，但每个漏洞都有其自己的 Exp，也就是说不存在通用的 Exp。

Shellcode 也有很多种，包括正向的，反向的，甚至 meterpreter。

Shellcode 与 Shellshcok 不是一个，Shellshock 特指 14 年发现的 Shellshock 漏洞。

<!-- more -->
另外：
在 Metasploit Framework 6 大模块中有一个 Payload 模块，在该模块下有 Single、Stager、Stages 这三种类型，Single 是一个 all-in-one 的 Payload，不依赖其他的文件，所以它的体积会比较大，Stager 主要用于当目标计算机的内存有限时，可以先传输一个较小的 Stager 用于建立连接，Stages 指利用 Stager 建立的连接下载后续的 Payload。Stager 和 Stages 都有多种类型，适用于不同场景。

尾巴：
想象自己是一个特工，你的目标是监控一个重要的人，有一天你怀疑目标家里的窗子可能没有关，于是你上前推了推，结果推开了，这是一个 PoC，于是你回去了，开始准备第二天的渗透计划，第二天你通过同样的漏洞渗透进了它家，仔细查看了所有的重要文件，离开时还安装了一个隐蔽的窃听器，这一天你所做的就是一个 Exp，你在他家所做的就是不同的 Payload，就把窃听器当作 Shellcode 吧！
