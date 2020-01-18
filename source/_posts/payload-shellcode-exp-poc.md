---
title: 渗透中PoC、Exp、Payload与Shellcode的区别
date: 2018-04-29 16:33:17
categories: CheatSheet
tags:
  - 渗透
---

PoC，全称“Proof of Concept”，中文“概念验证”，常指一段漏洞证明的代码。
Exp，全称“Exploit”，中文“利用”，指利用系统漏洞进行攻击的动作。
Payload，中文“有效载荷”，指成功exploit之后，真正在目标系统执行的代码或指令。
Shellcode，简单翻译“shell代码”，是Payload的一种，由于其建立正向/反向shell而得名。

几点注意：
PoC是用来证明漏洞存在的，Exp是用来利用漏洞的，两者通常不是一类，或者说，PoC通常是无害的，Exp通常是有害的，有了PoC，才有Exp。
Payload有很多种，它可以是Shellcode，也可以直接是一段系统命令。同一个Payload可以用于多个漏洞，但每个漏洞都有其自己的Exp，也就是说不存在通用的Exp。
Shellcode也有很多种，包括正向的，反向的，甚至meterpreter。
Shellcode与Shellshcok不是一个，Shellshock特指14年发现的Shellshock漏洞。

<!-- more -->
另外：
在Metasploit Framework 6大模块中有一个Payload模块，在该模块下有Single、Stager、Stages这三种类型，Single是一个all-in-one的Payload，不依赖其他的文件，所以它的体积会比较大，Stager主要用于当目标计算机的内存有限时，可以先传输一个较小的Stager用于建立连接，Stages指利用Stager建立的连接下载后续的Payload。Stager和Stages都有多种类型，适用于不同场景。

尾巴：
想象自己是一个特工，你的目标是监控一个重要的人，有一天你怀疑目标家里的窗子可能没有关，于是你上前推了推，结果推开了，这是一个PoC，于是你回去了，开始准备第二天的渗透计划，第二天你通过同样的漏洞渗透进了它家，仔细查看了所有的重要文件，离开时还安装了一个隐蔽的窃听器，这一天你所做的就是一个Exp，你在他家所做的就是不同的Payload，就把窃听器当作Shellcode吧！