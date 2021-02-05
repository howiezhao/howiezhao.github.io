---
title: Android Studio模拟器相关问题解决
date: 2018-08-21 19:22:50
categories: Bug
tags:
---

## 网络问题
<!--more-->
## 命令行启动

Android SDK工具包中包含着一个模拟器的命令行程序 —— `emulator`，它可以在不启动Android Studio的情况下开启Android模拟器，在Windows系统中，`emulator`位于`%LOCALAPPDATA%\Android\Sdk\tools`文件夹下，`emulator -list-avds`命令可以列出所有已创建的AVD，`emulator -avd <avd-name>`命令即可启动相应的AVD，要查看`emulator`更多的参数，可以使用`emulator -help`。

## 最佳实践

建议创建的AVD为Pixel，版本为Android 7.1.1。
