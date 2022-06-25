---
title: 关于 PowerShell
date: 2018-07-16 14:56:07
categories: CheatSheet
tags:
  - Windows
---

PowerShell 是微软用来取代 CMD 的一个强大的 Shell。

## 版本

在不同版本的 Windows 中已经内置了不同版本的 PowerShell，常见情况如下：

- Windows XP SP2 / Server 2003 SP1：PowerShell 1.0
- Windows 7 / Server 2008：PowerShell 2.0，此版本包含了 PowerShell ISE，即 Integrated Scripting Environment（集成的脚本环境），更方便的编写 PowerShell 脚本。
- Windows 8 / Server 2012：PowerShell 3.0，从此版本开始，PowerShell 被集成进了 WMF 中，即 Windows Management Framework（Windows 管理框架）。
- Windows 8.1 / Server 2012 R2：PowerShell 4.0
- Windows 10：PowerShell 5.0，此版本的 WMF 包含了 PowerShellGet，可用于在线下载、安装模块。

<!-- more -->
## 优势及劣势

PowerShell 相较于 CMD 的优势是不言而喻的，相较于 Unix 中的 Shell，它的优势主要体现在两方面：面向对象特性以及与 .NET 的深度结合。

劣势当然也有，相较于 CMD，至今为止它的启动速度仍然较慢，相较于 Unix 中的 Shell，它的生态环境还欠火候，可以期待未来有更多的人关注到 PowerShell。

## Cmdlets 与 pipeline

Cmdlets 与 pipeline 是 PowerShell 中的两个核心概念，

## 常用命令

PowerShell 中的大多数常用命令都有对应于 Linux 中相关命令的别名，比如 `ls`、`mv`、`ps`、`cat`、`kill`、`wget`、`clear` 等，下面介绍的命令为 PowerShell 所不同于 Linux 中的命令。

```bash
# 查看PowerShell版本信息
Get-Host

# 查看帮助信息
help

# 查看所有已经设置的别名
Get-Alias

# 从powershellgallery.com下载安装第三方模块
Install-Module

# 导入模块，安装的模块需要先导入才能使用
Import-Module

# 卸载模块
Uninstall-Module

# 更新模块
Update-Module

# 列出已安装模块
Get-InstalledModule

# 查看PowerShellGet模块有哪些命令
Get-Command -Module PowerShellGet

# 升级帮助手册
Update-Help
```

## 常用模块

- [posh-git](https://github.com/dahlbyk/posh-git)：PowerShell 中的 Git 增强模块
- [DockerCompletion](https://github.com/matt9ucci/DockerCompletion)：PowerShell 中的 Docker 命令补全
- [Carbon](https://github.com/webmd-health-services/Carbon)：一系列有用的工具集
- [PSReadline](https://github.com/lzybkr/PSReadLine)：一个增强的命令行编辑模块
- [windows-screenfetch](https://github.com/JulianChow94/Windows-screenFetch)：Windows 下的 screenfetch 模块

## Microsoft.PowerShell_profile.ps1

和一般的 Linux 中的 Shell 一样，PowerShell 也有一个配置文件，即 `Microsoft.PowerShell_profile.ps1`，当 PowerShell 运行时会默认加载此配置文件中的设置。一般而言，用户级别的配置文件位于 `%HOMEPATH%\Documents\WindowsPowerShell` 下，当然，你也可以使用 `echo $profile`命令查看具体的位置。
