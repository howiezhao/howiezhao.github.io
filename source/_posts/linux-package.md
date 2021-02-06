---
title: Linux 的包管理机制
date: 2018-05-09 13:43:55
categories: CheatSheet
tags:
  - Linux
---

不同 Linux 发行版的主要区别是其包管理机制不同，Linux 发行版大致可以分为 2 个派别：一派以 Red Hat 为首，主要包括 CentOS（社区版）、Fedora（桌面版）等；另一派以 Debian 为首，主要包括 Ubuntu、Kali 等。Red Hat 系采用 `rpm` 为其包格式，`yum` 为其包管理工具；Debian 系采用 `dpkg` 为其包格式，`apt-get` 为其包管理工具。

## rpm 与 yum

`rpm` 全称 Red-Hat Package Manager（RPM 软件包管理器），是 Red Hat 系中的包格式，同时也是其**本地**包管理工具，常用命令有：

```sh
rpm -i a.rpm  # 安装a
rpm -e a      # 卸载a
```

`yum` 全称 Yellow dog Updater, Modified（修改后的黄色狗更新器），是 Red Hat 系中的包管理工具，常用命令有：

```sh
yum update     # 更新包列表
yum upgrade    # 更新包
yum install a  # 安装a
yum remove a   # 卸载a
```
<!-- more -->
## dpkg 与 apt-get

`dpkg` 全称 Debian Packager（Debian 包工具），是 Debian 系中的包格式，同时也是其**本地**包管理工具，常用命令有：

```sh
dpkg -i a.dpkg  # 安装a
dpkg -r a       # 卸载a
```

`apt-get` 是 apt 中的一个子程序，apt 全称 Advanced Packaging Tool（先进的包工具），是 Debian 系中的包管理工具，apt 的程序包来源列表文件位于 `/etc/apt/sources.list`，`apt-get` 的常用命令有：

```sh
sudo apt-get update     # 更新包列表
sudo apt-get upgrade    # 更新包
sudo apt-get install a  # 安装a
sudo apt-get purge a    # 卸载a并删除其配置文件（即彻底删除），命令作用等同于apt-get --purge remove a
```

同样的，`apt-cache` 也是 apt 中的一个子程序，它的常用命令有：

```sh
sudo apt-cache depends a  # 查看包a的依赖包
```

值得注意的是，随着新版系统的到来，出现了更为强大的 `apt` 命令，可以简单认为 `apt` 集合了 `apt-get`、`apt-cache`、`apt-config` 中的最常用命令选项。例如，`apt install` 相比 `apt-get install` 增加了色彩显示以及进度条显示等功能。因此，更建议使用 `apt` 命令，常用命令有：

```sh
sudo apt update     # 更新包列表
sudo apt upgrade    # 更新包
sudo apt install a  # 安装a
sudo apt purge a    # 卸载a并删除其配置文件（即彻底删除），命令作用等同于apt --purge remove a
sudo apt list --installed  # 查看已安装的包
```

关于 Ubuntu 中程序包的搜索可以使用 [Ubuntu Packages Search](https://packages.ubuntu.com/)。
