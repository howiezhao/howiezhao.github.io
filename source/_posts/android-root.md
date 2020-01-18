---
title: 谈谈Android的root
date: 2018-09-18 12:13:24
categories: CheatSheet
tags:
  - Android
---

Android的内核是Linux，所以Android的root和Linux的root有些许关系，不妨先回顾一下Linux中是如何获取root的。
## Linux相关
在Linux中获得root权限有2个命令，`su`与`sudo`，`sudo`只是为了短暂的获得root权限以执行某些操作(superuser do)，而`su`其实是为了切换用户(switch user)，但当其不带参数直接执行时，默认为切换到root用户。使用`sudo`执行某些需要root权限的操作时，需要输入当前用户的密码；而直接使用`su`切换到root用户时，需要输入root用户的密码。
在Linux中，文件的权限有`rwx`三种，即可读(read)、可写(write)、可执行(execute)，其中`r`又等于4，`w`等于2，`x`等于1。所以，如果一个文件同时具有`rwx`权限，那么它的权限位就等于7。
<!--more-->
## Android相关
Android本身是不愿意让用户获得root权限的，所以Android中没有`su`或`sudo`这些命令。所以，获得root权限的第一步就是要把`su`命令拷贝到Android的`/system/bin`或`/system/xbin`目录下。但是拷贝之后并不能直接使用`su`命令，因为Android中`su`的运行机制和Linux中不同。在Android中只有root用户才能使用`su`命令，非root用户无权使用`su`命令。这其实是一个逻辑闭环：使用`su`命令可以切换到root，但只有root用户才可以使用`su`命令。好在Linux中文件的权限除了`rwx`三种之外，还有`s`权限，`s`代表当任何一个用户执行该文件时都拥有文件所有者的权限，换句话来说，如果一个文件的所有者是root，且它的执行权限标志位是`s`，那么不管谁执行这个文件，他执行的时候都是以root身份执行的。
基于以上，Android获取root权限大致可以分为如下3步：
```bash
# 拷贝su到指定目录下
cp /data/tmp/su /system/bin/

# 将su所有者设为root
chown root:root su

# 将su标志位设为-rwsr-xr-x
chmod 4775 /system/bin/su
```
但是，除了上面第一步以外，剩下两步都需要root权限才能成功执行，这就又造成了一个逻辑闭环：即通过上面的代码可以获得root权限，但必须有root权限才能执行上面的代码。这时的解决办法就是寻找Android系统的漏洞，系统中有些进程是以root权限运行的，只有找出那些有漏洞的进程，然后利用缓冲区溢出让其执行我们上面的命令，即可完成root。
所以，总的来说，Android获取root权限最重要的一步，就是寻找系统的漏洞，然后利用之。
## 术语
了解了Android root的基本原理后，需要理清一些常用术语：
### 刷机
### Bootloader
### 线刷
### 卡刷
## Nexus的root
Nexus系列作为Google的亲儿子，自然少不了root解决方案，目前root Nexus设备使用最多的软件是[Nexus Root Toolkit(NRT)](http://www.wugfresh.com/nrt/)。请注意，此软件运行前会先进行更新，这会花费较长的时间，需要耐心等待。