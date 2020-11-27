---
title: Nexus/Pixel 相关问题解决
categories: Bug
date: 2019-07-21 10:15:55
tags:
  - Android
  - 硬件
---

## 移动网络/WiFi 出现叹号或叉号

Captive Portal 是从 Android 5 开始引入的一项新功能，其主要用于检测网络连接是否正常，当用户连接网络后，系统会通过 HTTP 访问一个 Google 的服务器，若返回 200 状态码，则表示用户可能处在一个需要登录认证的网络环境中；若返回 204 状态码，则表示网络连接正常；若连接超时，则表示网络连接不正常，此时网络图标会显示一个叹号或叉号。

显然，Google 的服务器是连接不上的，我们可以通过修改服务器地址来解决此问题。具体而言，连接 ADB，针对不同的系统版本，下方分别给出了相关命令：

Android 9.0/8.1/8.0/7.1.2/7.1.1：

```shell
adb shell settings put global captive_portal_https_url https://www.google.cn/generate_204
```

Android 7.1/7.0：

```shell
adb shell settings delete global captive_portal_server  
adb shell settings put global captive_portal_detection_enabled 0
```

Android 5.0-6.x：

```shell
adb shell settings put global captive_portal_server www.google.cn
```

执行之后，开启飞行模式，接着关闭飞行模式即可。
<!--more-->
## 搜索不到 WiFi

因为美国 2.4GHz 频段的 WiFi 信道为 1-11，而中国 2.4GHz 频段的 WiFi 信道为 1-13，所以当 2.4GHz 频段的 WiFi 信道位于 12 或 13 时，美版的 Nexus/Pixel 会搜索不到 WiFi，此时可通过重启路由器，使其自动更换信道，或进入路由器设置页面，将信道改为 11 以内任意信道即可。

## 4G 信号问题

由于联通的网络制式一直采用的是国际通用的网络制式，所以 Nexus/Pixel 可以完美支持联通 2G/3G/4G。

移动的 3G 网络制式采用的是自主研发的技术，所以 Nexus/Pixel 并不支持移动 3G，然而移动 4G 网络制式采用的是自主研发和国际通用并行的方式，所以 Nexus/Pixel 只支持部分移动 4G 频段。

简单来说，Nexus/Pixel 完美支持联通 2G/3G/4G，支持移动 2G，不支持移动 3G，部分支持移动 4G（具体表现为在城市有 4G 网络，在农村没有 4G 网络），电信 2G/3G/4G 可通过破解（本文不讨论这点）实现支持。

## Google（即负一屏）无法使用

## 接听电话时黑屏，且无法点亮屏幕以挂断电话（插耳机时一切正常）

严格来说，这不算是 Nexus/Pixel 特有的问题，究其原因是距离感应器坏了，可通过设置使用电源键挂断电话，具体方法为在**设置** —> **辅助功能/无障碍**中开启**按电源按钮结束通话**。

## 蓝牙传输失败，显示不支持此内容

由于版权问题，原生 Android 不支持传输以 `.apk` 结尾的文件，可通过将其改为 `.jpg` 结尾传输。

## Google Play 商店更新应用卡住

在 Android 9.0 之前，Play 商店是通过**下载管理器**下载应用的，出现这种情况可以直接将**下载管理器**强行停止，然后重新启动 Play 商店即可更新应用。在 Android 9.0 之后，可直接将 Play 商店强行停止再重新启动即可。

## 系统无法更新

具体表现为**系统更新**处永远显示**正在安装系统更新**，一般来说，这是由于网络原因引起的，目前并没有一个稳定的解决办法，建议直接下载新系统镜像并线刷。你可以在[这个官方地址](https://developers.google.cn/android/images)找到有关 Nexus/Pixel 的所有出厂镜像，其中也附带有详细的安装方法。

具体而言，你需要先解锁 Bootloader，然后连接 ADB，紧接着执行 `adb reboot bootloader` 进入 fastboot 模式，最后执行相应系统的 `flash-all` 脚本即可。

## Pixel/Pixel XL Verizon 版解锁 Bootloader 教程

教程来源自 xda 上的一篇[文章](https://www.xda-developers.com/unlock-bootloader-verizon-google-pixel-xl/)，具体步骤如下：

1. 从您的设备中删除 Google 帐户和任何类型的屏幕锁定（指纹，PIN，图案等）。
2. 从您的设备中取出 SIM 卡。
3. 重置您的设备。在设置向导中，跳过所有内容，不要连接到 WiFi，不要添加指纹或任何类型的屏幕锁定。
4. 转到开发人员选项并启用 USB 调试。
5. 将手机连接到 PC。
6. 在 adb 目录中打开 CMD 并输入：`adb shell pm uninstall --user 0 com.android.phone`
7. 重启您的设备。
8. 连接到 WiFi，打开 Chrome 并转到 google.com（或任何网站）。
9. 转到开发人员选项并启用 OEM 解锁。
10. 重启到 bootloader 并通过 CMD 运行：`fastboot oem unlock` 或 `fastboot flashing unlock`。
11. 完成。
