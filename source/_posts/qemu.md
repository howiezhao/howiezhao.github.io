---
title: QEMU 小记
categories: CheatSheet
date: 2019-04-18 17:17:11
tags:
  - Linux
---

[QEMU](https://www.qemu.org/) 是 Linux 中使用最广的模拟器，可以模拟出各种硬件环境，其便于调试的特性也适合于系统开发者。

## 安装

使用 `sudo apt install qemu` 即可在 Ubuntu 中安装 QEMU，安装完成后会有很多以 `qemu-` 开头的命令，如：

- `qemu-system-i386`：用于模拟 32 位的 80386 硬件环境
- `qemu-system-x86_64`：用于模拟 64 位的 x86 硬件环境
- `qemu-system-arm`：用于模拟 ARM 硬件环境

再进一步，这些命令又可以分为以 `qemu-system-` 开头和以 `qemu-` 开头，以 `qemu-system-` 开头的用于在模拟的硬件环境上运行整个系统，以 `qemu-` 开头的用于在模拟的硬件环境上运行某个程序，而非整个系统。

<!--more-->

## 运行

使用 QEMU 模拟一个硬件环境并运行整个系统的命令格式为 `qemu [options] [disk_image]`，其中 disk_image 即硬盘镜像文件。其常用的参数如下：

- `-hda file`：使用 file 作为硬盘 0 的镜像文件。
- `-m megs`：设定虚拟内存为 megs M 字节，默认为 128 M 字节。
- `-smp n`：设置为有 n 个 CPU 的 SMP 系统。

值得注意的是，QEMU 的启动需要有图形界面，若未安装图形界面，则会报错：

```bash
Could not initialize SDL(No available video device) - exiting
```

若要无图形界面启动需要加参数 `-nographic`。
