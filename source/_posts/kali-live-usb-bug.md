---
title: Kali 持久加密 USB 安装所遇问题总结
date: 2017-12-04 23:54:56
categories: Bug
tags:
  - Kali
---

## Writing superblocks and filesystem accounting information

今天在将 Kali 安装到 U 盘上时遇到了上面所示的问题，也可以翻译成“写入超级块和文件系统账户统计信息”，具体情况是当使用 `mkfs.ext4` 格式化加密分区时，程序运行到上面所示的地方停止不动，无论等多久都无法完成，其间还会发生 U 盘挂掉又重连上的情况，使用 `dmesg` 命令诊断故障时发现如下错误：

```text
...
device descriptor read/8, error -110
...
```

经判断是因为主板无法提供给 U 盘足够的电量所导致的，因为我的 U 盘和虚拟机之间是 3.0 连接的，3.0 连接要比 2.0 连接耗电，所以将 U 盘和虚拟机之间的连接改为 2.0 即可解决这个问题。

## 时间问题

安装好 Kali 并启动之后，会发现 Kali 的系统时间始终无法和 Windows 的系统时间保持一致，具体表现如下：

开始时，Windows 系统时间准确，启动 Kali 之后，Kali 系统时间错误，将其更新正确之后，关闭 Kali，进入 Windows，发现 Windows 系统时间又错误。

出现这种情况的原因是 Windows 和 Linux 的时间机制不一样，具体而言，Windows 的时间就是硬件 BIOS 的时间，而 Linux 的时间则是硬件 BIOS 加上所在时区的时间。解决方法是，在 Kali 中执行如下命令：

```sh
sudo timedatectl set-local-rtc 1 --adjust-system-clock
```
