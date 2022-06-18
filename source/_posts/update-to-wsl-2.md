---
title: 升级到 WSL 2
categories: CheatSheet
date: 2021-05-02 17:31:15
tags:
  - Windows
  - Linux
  - WSL
---

从 2020 年末开始，微软逐步向 Windows 10 用户推送了 WSL 2 更新，WSL 2 相比 WSL 1 是一个巨大的变化，最显著的改变在于 WSL 2 开始采用 Hyper-V 虚拟机来运行 Linux，这会解决之前 WSL 的很多问题，但也可以看作是 WSL 项目的失败，本文所描述的主体为 WSL 2，有关 WSL 1 的相关内容请参考 {% post_link wsl-problem %}。

<!-- more -->

## 升级到 WSL 2

要查看当前安装的 WSL 版本，可通过 `wsl --list --verbose` 命令查看，其输出如下：

```text
  NAME                   STATE           VERSION
* Ubuntu                 Running         1
```

VERSION 下面的结果为其版本号，上述为 WSL 1。

具体升级步骤如下：

1. 在 **启用或关闭 Windows 功能** 中勾选 **虚拟机平台**，或直接在管理员权限的 PowerShell 中输入 `Enable-WindowsOptionalFeature -Online -FeatureName "VirtualMachinePlatform"`；
2. 下载并安装 [Linux 内核更新包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi) ；
3. 输入 `wsl --set-version Ubuntu 2` 将已安装发行版设置为 WSL 2。

## 直接安装 WSL 2

如果你之前没有安装过 WSL 1，可以通过在管理员权限的 PowerShell 中输入以下命令来直接安装 WSL 2：

```powershell
wsl --update
wsl --shutdown
wsl --install --distribution Ubuntu
```
