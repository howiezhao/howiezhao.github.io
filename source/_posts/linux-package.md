---
title: Linux的包管理机制
date: 2018-05-09 13:43:55
categories: CheatSheet
tags:
  - Linux
---

不同Linux发行版的主要区别是其包管理机制不同，Linux发行版大致可以分为2个派别：一派以Red Hat为首，主要包括CentOS(社区版)、Fedora(桌面版)等；另一派以Debian为首，主要包括Ubuntu、Kali等。Red Hat系采用`rpm`为其包格式，`yum`为其包管理工具；Debian系采用`dpkg`为其包格式，`apt-get`为其包管理工具。

## rpm与yum
`rpm`全称Red-Hat Package Manager(RPM软件包管理器)，是Red Hat系中的包格式，同时也是其**本地**包管理工具，常用命令有：
```bash
rpm -i a.rpm  #安装a
rpm -e a      #卸载a
```
`yum`全称Yellow dog Updater, Modified(修改后的黄色狗更新器)，是Red Hat系中的包管理工具，常用命令有：
```bash
yum update     #更新包列表
yum upgrade    #更新包
yum install a  #安装a
yum remove a   #卸载a
```
<!-- more -->
## dpkg与apt-get
`dpkg`全称Debian Packager(Debian包工具)，是Debian系中的包格式，同时也是其**本地**包管理工具，常用命令有：
```bash
dpkg -i a.dpkg  #安装a
dpkg -r a       #卸载a
```
`apt-get`是apt中的一个子程序，apt全称Advanced Packaging Tool(先进的包工具)，是Debian系中的包管理工具，apt的程序包来源列表文件位于`/etc/apt/sources.list`，`apt-get`的常用命令有：
```bash
sudo apt-get update     #更新包列表
sudo apt-get upgrade    #更新包
sudo apt-get install a  #安装a
sudo apt-get purge a    #卸载a并删除其配置文件（即彻底删除），命令作用等同于apt-get --purge remove a
```
同样的，`apt-cache`也是apt中的一个子程序，它的常用命令有：
```bash
sudo apt-cache depends a  #查看包a的依赖包
```
值得注意的是，随着新版系统的到来，出现了更为强大的`apt`命令，可以简单认为`apt`集合了`apt-get`、`apt-cache`、`apt-config`中的最常用命令选项。例如，`apt install`相比`apt-get install`增加了色彩显示以及进度条显示等功能。因此，更建议使用`apt`命令，常用命令有：
```bash
sudo apt update     #更新包列表
sudo apt upgrade    #更新包
sudo apt install a  #安装a
sudo apt purge a    #卸载a并删除其配置文件（即彻底删除），命令作用等同于apt --purge remove a
sudo apt list --installed  #查看已安装的包
```
关于Ubuntu中程序包的搜索可以使用[Ubuntu Packages Search](https://packages.ubuntu.com/)。