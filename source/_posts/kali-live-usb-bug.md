---
title: Kali持久加密USB安装所遇问题总结
date: 2017-12-04 23:54:56
categories: Bug
tags:
  - Kali
---

## Writing superblocks and filesystem accounting information
今天在将Kali安装到U盘上时遇到了上面所示的问题，也可以翻译成“写入超级块和文件系统账户统计信息”，具体情况是当使用`mkfs.ext4`格式化加密分区时，程序运行到上面所示的地方停止不动，无论等多久都无法完成，其间还会发生U盘挂掉又重连上的情况，使用`dmesg`命令诊断故障时发现如下错误：
```bash
...
device descriptor read/8, error -110
...
```
经判断是因为主板无法提供给U盘足够的电量所导致的，因为我的U盘和虚拟机之间是3.0连接的，3.0连接要比2.0连接耗电，所以将U盘和虚拟机之间的连接改为2.0即可解决这个问题。

## 时间问题
安装好Kali并启动之后，会发现Kali的系统时间始终无法和Windows的系统时间保持一致，具体表现如下：
>开始时，Windows系统时间准确，启动Kali之后，Kali系统时间错误，将其更新正确之后，关闭Kali，进入Windows，发现Windows系统时间又错误。

出现这种情况的原因是Windows和Linux的时间机制不一样，具体而言，Windows的时间就是硬件BIOS的时间，而Linux的时间则是硬件BIOS加上所在时区的时间。解决方法是，在Kali中执行如下命令：
```bash
sudo timedatectl set-local-rtc 1 --adjust-system-clock
```