---
title: 关于PowerShell
date: 2018-07-16 14:56:07
categories: CheatSheet
tags:
  - Windows
---

PowerShell是微软用来取代CMD的一个强大的Shell。

## 版本

在不同版本的Windows中已经内置了不同版本的PowerShell，常见情况如下：
- Windows XP SP2 / Server 2003 SP1：PowerShell 1.0
- Windows 7 / Server 2008：PowerShell 2.0，此版本包含了PowerShell ISE，即Integrated Scripting Environment(集成的脚本环境)，用来方便的编写PowerShell脚本。
- Windows 8 / Server 2012：PowerShell 3.0，从此版本开始，PowerShell被集成进了WMF中，即Windows Management Framework(Windows管理框架)。
- Windows 8.1 / Server 2012 R2：PowerShell 4.0
- Windows 10：PowerShell 5.0，此版本的WMF包含了PowerShellGet，可用于在线下载、安装模块。

<!-- more -->
## 优势及劣势

PowerShell相较于CMD的优势是不言而喻的，相较于Unix中的Shell，它的优势主要体现在2方面：面向对象特性以及与.NET的深度结合。
劣势当然也有，相较于CMD，至今为止它的启动速度仍然较慢，相较于Unix中的Shell，它的生态环境还欠火候，可以期待未来有更多的人关注到PowerShell。

## Cmdlets与pipeline

Cmdlets与pipeline是PowerShell中的两个核心概念，

## 常用命令

PowerShell中的大多数常用命令都有对应于Linux中相关命令的别名，比如`ls`、`mv`、`ps`、`cat`、`kill`、`wget`、`clear`等，下面介绍的命令为PowerShell所不同于Linux中的命令。
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

- [posh-git](https://github.com/dahlbyk/posh-git)：PowerShell中的Git增强模块
- [oh-my-posh](https://github.com/JanDeDobbeleer/oh-my-posh)：类似于oh-my-zsh
- [PSReadline](https://github.com/lzybkr/PSReadLine)：一个增强的命令行编辑模块
- [windows-screenfetch](https://github.com/JulianChow94/Windows-screenFetch)：Windows下的screenfetch模块

## Microsoft.PowerShell_profile.ps1
和一般的Linux中的Shell一样，PowerShell也有一个配置文件，即`Microsoft.PowerShell_profile.ps1`，当PowerShell运行时会默认加载此配置文件中的设置。一般而言，用户级别的配置文件位于`%HOMEPATH%\Documents\WindowsPowerShell`下，当然，你也可以使用`echo $profile`命令查看具体的位置。