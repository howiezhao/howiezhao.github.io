---
title: Android刷机指南
categories: CheatSheet
date: 2019-03-23 11:42:58
tags:
  - Android
---

## 名词解释

### 软重启与硬重启

**软重启**（又称**热重启**）是指从操作系统层面上关机再开机，而**硬重启**（又称**冷重启**）是指直接关掉电源再开机。类似的，也有**软（热）关机**和**硬（冷）关机**，其区别类似于在 Windows “开始”菜单中点击关机和直接关掉主机电源的区别。一般而言，软（热）关机对设备更好。
<!--more-->
### Bootloader/fastboot/Recovery

### Full OTA Image 与 Factory Image

## 刷机流程

1. 提前备份必要的数据（下载的音乐、视频，QQ、微信的聊天记录，通话记录、短信、通讯录，相册等），尽量保持电量满。
2. 恢复出厂设置（亦或，取消所有安全机制，如屏幕锁定等，并退出 Google 账号。）。
3. 在开发者选项中开启 USB 调试。
4. 解锁 Bootloader（需要的话）。
5. 刷入第三方 Recovery，如 [TWRP](https://twrp.me/)。
6. 从 TWRP 中安装第三方 ROM，顺便 root。

## 常见问题

### 开机无限进入 TWRP

碰到这种情况，你可能需要格式化 Data 分区。
