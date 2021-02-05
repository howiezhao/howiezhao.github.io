---
title: Kali Rolling 2017 更新后无法启动解决方案
date: 2017-11-25 19:04:29
categories: Bug
tags:
  - Kali
---

## BusyBox v1.27.2 (Debian 1:1.27.2-1) built-in shell (ash)

有时更新 Kali 后重新启动会出现如下显示，并无法进入系统界面

```sh
BusyBox v1.27.2 (Debian 1:1.27.2-1) built-in shell (ash)
Enter 'help' for a list of built-in commands.

(initramfs)
```

**解决方法：**

1. 在此界面输入 `blkid` 命令，查看自己的分区号
2. 依据自己的分区号输入 `fsck -y /dev/sda1`，我的分区号是 sda1。
3. 输入 `exit` 命令退出重启电脑
