---
title: QEMU小记
categories: CheatSheet
date: 2019-04-18 17:17:11
tags:
  - Linux
---

[QEMU](https://www.qemu.org/)是Linux中使用最广的虚拟机，其便于调试的特性也适合于系统开发者。

## 安装

使用`sudo apt install qemu`即可在Ubuntu中安装QEMU，安装完成后直接输入`qemu`来验证是否成功安装，如果出错，可再输入`qemu-system-i386`来验证其是否成功安装，若成功，可建立如下所示的软链接，以方便日后使用。

```bash
sudo ln -s /usr/bin/qemu-system-i386 /usr/bin/qemu
```

值得注意的是，QEMU的启动需要有图形界面，若未安装图形界面，则会报错：

```bash
Could not initialize SDL(No available video device) - exiting
```
<!--more-->
## 运行

使用QEMU运行一个虚拟机的命令格式为`qemu [options] [disk_image]`，其中disk_image即硬盘镜像文件。其常用的参数如下：

- `-hda file`：使用file作为硬盘0的镜像文件。
- `-m megs`：设定虚拟内存为megs M字节，默认为128M字节。
- `-smp n`：设置为有n个CPU的SMP系统。
