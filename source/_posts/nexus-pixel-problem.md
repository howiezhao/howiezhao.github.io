---
title: Nexus/Pixel相关问题解决
categories: Bug
date: 2019-07-21 10:15:55
tags:
  - Android
  - 硬件
---

## 移动网络/Wifi出现叹号或叉号
Captive Portal是从Android 5开始引入的一项新功能，其主要用于检测网络连接是否正常，当用户连接网络后，系统会通过HTTP访问一个Google的服务器，若返回200状态码，则表示用户可能处在一个需要登录认证的网络环境中；若返回204状态码，则表示网络连接正常；若连接超时，则表示网络连接不正常，此时网络图标会显示一个叹号或叉号。

显然，Google的服务器是连接不上的，我们可以通过修改服务器地址来解决此问题。具体而言，连接ADB，针对不同的系统版本，下方分别给出了相关命令：

Android 9.0/8.1/8.0/7.1.2/7.1.1：
```
adb shell settings put global captive_portal_https_url https://www.google.cn/generate_204
```
Android 7.1/7.0：
```
adb shell settings delete global captive_portal_server  
adb shell settings put global captive_portal_detection_enabled 0
```
Android 5.0-6.x：
```
adb shell settings put global captive_portal_server www.google.cn
```
执行之后，开启飞行模式，接着关闭飞行模式即可。
<!--more-->
## 搜索不到WiFi
因为美国2.4GHz频段的WiFi信道为1-11，而中国2.4GHz频段的WiFi信道为1-13，所以当2.4GHz频段的WiFi信道位于12或13时，美版的Nexus/Pixel会搜索不到WiFi，此时可通过重启路由器，使其自动更换信道，或进入路由器设置页面，将信道改为11以内任意信道即可。

## 4G信号问题
由于联通的网络制式一直采用的是国际通用的网络制式，所以Nexus/Pixel可以完美支持联通2G/3G/4G。

移动的3G网络制式采用的是自主研发的技术，所以Nexus/Pixel并不支持移动3G，然而移动4G网络制式采用的是自主研发和国际通用并行的方式，所以Nexus/Pixel只支持部分移动4G频段。

简单来说，Nexus/Pixel完美支持联通2G/3G/4G，支持移动2G，不支持移动3G，部分支持移动4G（具体表现为在城市有4G网络，在农村没有4G网络），电信2G/3G/4G可通过破解（本文不讨论这点）实现支持。

## Google（即负一屏）无法使用

## 接听电话时黑屏，且无法点亮屏幕以挂断电话（插耳机时一切正常）
严格来说，这不算是Nexus/Pixel特有的问题，究其原因是距离感应器坏了，可通过设置使用电源键挂断电话，具体方法为在**设置** —> **辅助功能/无障碍**中开启**按电源按钮结束通话**。

## 蓝牙传输失败，显示不支持此内容
由于版权问题，原生Android不支持传输以`.apk`结尾的文件，可通过将其改为`.jpg`结尾传输。

## Google Play商店更新应用卡住
在Android 9.0之前，Play商店是通过**下载管理器**下载应用的，出现这种情况可以直接将**下载管理器**强行停止，然后重新启动Play商店即可更新应用。在Android 9.0之后，可直接将Play商店强行停止再重新启动即可。

## 系统无法更新
具体表现为**系统更新**处永远显示**正在安装系统更新**，一般来说，这是由于网络原因引起的，目前并没有一个稳定的解决办法，建议直接下载新系统镜像并线刷。你可以在[这个官方地址](https://developers.google.cn/android/images)找到有关Nexus/Pixel的所有出厂镜像，其中也附带有详细的安装方法。

具体而言，你需要先解锁Bootloader，然后连接ADB，紧接着执行`adb reboot bootloader`进入fastboot模式，最后执行相应系统的`flash-all`脚本即可。

## Pixel/Pixel XL Verizon版解锁Bootloader教程
教程来源自xda上的一篇[文章](https://www.xda-developers.com/unlock-bootloader-verizon-google-pixel-xl/)，具体步骤如下：
1. 从您的设备中删除Google帐户和任何类型的屏幕锁定（指纹，PIN，图案等）。
2. 从您的设备中取出SIM卡。
3. 重置您的设备。在设置向导中，跳过所有内容，不要连接到WiFi，不要添加指纹或任何类型的屏幕锁定。
4. 转到开发人员选项并启用USB调试。
5. 将手机连接到PC。
6. 在adb目录中打开CMD并输入：`adb shell pm uninstall --user 0 com.android.phone`
7. 重启您的设备。
8. 连接到WiFi，打开Chrome并转到google.com（或任何网站）。
9. 转到开发人员选项并启用OEM解锁。
10. 重启到bootloader并通过CMD运行：`fastboot oem unlock`或`fastboot flashing unlock`。
11. 完成。
