---
title: 代理链工具：proxychains
date: 2018-10-18 10:21:58
categories: CheatSheet
tags:
  - Linux
---

[proxychains](https://github.com/haad/proxychains)，顾名思义，是一种代理链工具，它可以强制任何 Linux 下的命令行应用使用其提供的代理连接到网络。Linux 中有的应用本身并不支持代理，这时便可以使用 proxychains 强制其使用代理。
<!--more-->
## 安装及使用
在 Ubuntu 下可以使用 `sudo apt install proxychains` 直接安装，安装完成后会在 `/etc` 文件夹下生成 `proxychains.conf` 配置文件，在这个配置文件中可以配置代理链的工作模式和代理地址等。

proxychains 提供了 3 种代理模式，分别是**动态链**（dynamic_chain）、**严格链**（strict_chain）、**随机链**（random_chain），建议选择动态链。此外，proxychains 默认设置的代理地址为 Tor 的地址，但其实最新版的 Tor 已经更改端口为 9150，用户可以根据自己的需求按照示例格式配置地址。

配置完成后，要使用 proxychains，只需在相应命令前加上 `proxychains` 即可，例如 `proxychains nmap -sS 192.168.1.1`，即可强制 nmap 使用 proxychains 中设置的代理进行扫描。

## 与 proxychains-ng
[proxychains-ng](https://github.com/rofl0r/proxychains-ng) 是 proxychains 的升级版，其中 ng 寓意为 new generation（新一代），目前并不知晓 proxychains-ng 与 proxychains 是否为同一组织开发，但二者的配置与使用极为相似。

在 Ubuntu 下可以使用 `sudo apt install proxychains-ng` 直接安装，要使用 proxychains-ng，只需在相应命令前加上 `proxychains4` 即可。

## Windows
由于 Windows 与 Linux 的设计哲学不同，Linux 偏向使用命令行，Windows 偏向使用图形界面，所以 proxychains 并未提供 Windows 版。在 Windows 下可以使用另一款代理工具 [Proxifier](https://www.proxifier.com/)，它可以看作是 proxychains 的图形界面版，值得注意的是，Proxifier 是收费的，但你可以免费体验 31 天。
