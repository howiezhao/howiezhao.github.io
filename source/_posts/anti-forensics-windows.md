---
title: 反取证之Windows
date: 2018-05-02 14:02:03
categories: CheatSheet
tags:
  - 渗透
  - 计算机取证
  - Windows
---

## MACE时间
和[反取证之Linux](https://howiezhao.github.io/2018/05/02/anti-forensics-linux/)中的一样，Windows也有MAC时间，不过在Windows中，C指的是Created，即创建时间，Windows中默认显示的是修改时间，另外，在Windows的NTFS文件系统中还有E时间，即MFT entry，其中包含了文件的大量信息，包括大小、名称、目录位置、磁盘位置、创建日期等，在擦除痕迹时也要擦除E时间，同样，meterpreter中的`timestomp`命令可以方便的修改MACE时间。
## 隐藏新建账号
当在目标系统上新建了用户账号后，通常会在登录界面上显示出来，要实现隐藏，可以修改注册表项，采用如下命令：
```bash
REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\SpecialAccounts\UserList /v uname /t REG_DWORD /d 0
```
注意：这种隐藏只是在登录界面的隐藏，用户使用`net user`或“本地用户和组”仍然可以查到新建的账户。
## 日志文件
清除相关日志文件
### 系统日志
Windows系统日志文件一般存放在Windows文件夹下，可以使用如下命令删除之：
```bash
del %windir%\*.log /a/s/q/f
```
另外，meterpreter中的`clearev`命令可以删除事件查看器中的日志信息。
### Web日志
IIS的日志文件位于%windir%\System32\LogFiles目录下。

**最后，请不要忘记HIDS/IPS/WAF/集中的日志服务器的痕迹擦除。**