---
title: 代理链工具：proxychains
date: 2018-10-18 10:21:58
categories: CheatSheet
tags:
  - Linux
---

[proxychains](https://github.com/haad/proxychains)，顾名思义，是一种代理链工具，它可以强制任何Linux下的命令行应用使用其提供的代理连接到网络。Linux中有的应用本身并不支持代理，这时便可以使用proxychains强制其使用代理。
<!--more-->
## 安装及使用
在Ubuntu下可以使用`sudo apt install proxychains`直接安装，安装完成后会在`/etc`文件夹下生成`proxychains.conf`配置文件，在这个配置文件下可以配置代理链的工作模式和代理地址等。
proxychains提供了3种代理模式，分别是**动态链**（dynamic_chain）、**严格链**（strict_chain）、**随机链**（random_chain），建议选择动态链。此外，proxychains默认设置的代理地址未为Tor的地址，但其实最新版的Tor已经更改端口为9150，用户可以根据自己的需求按照示例格式配置地址。
配置完成后，要使用proxychains，只需在相应命令前加上`proxychains`即可，例如`proxychains nmap -sS 192.168.1.1`，即可强制nmap使用proxychains中设置的代理进行扫描。
## 与proxychains-ng
[proxychains-ng](https://github.com/rofl0r/proxychains-ng)是proxychains的升级版，其中ng寓意为new generation（新一代），目前并不知晓proxychains-ng与proxychains是否为同一组织开发，但二者的配置与使用极为相似。
在Ubuntu下可以使用`sudo apt install proxychains-ng`直接安装，要使用proxychains-ng，只需在相应命令前加上`proxychains4`即可。
## Windows
由于Windows与Linux的设计哲学不同，Linux偏向使用命令行，Windows偏向使用图形界面，所以proxychains并未提供Windows版。在Windows下可以使用另一款代理工具[Proxifier](https://www.proxifier.com/)，它可以看作是proxychains的图形界面版，值得注意的是，Proxifier是收费的，但你可以免费体验31天。