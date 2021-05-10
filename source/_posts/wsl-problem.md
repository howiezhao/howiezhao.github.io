---
title: WSL 相关问题解决
date: 2018-08-21 19:23:05
categories: Bug
tags:
  - Windows
  - Linux
  - WSL
---

随着时间的发展，WSL 变化了很多，本文所描述的主体为 WSL 1，有关 WSL 2 的相关内容请参考 {% post_link update-to-wsl-2 %}。

## 名称问题

最早这个项目命名为 **Bash on Ubuntu on Windows**，随后改名为 **Windows Subsystem for Linux**（适用于 Linux 的 Windows 子系统），即 **WSL**，值得肯定的是，随着 Windows 10 逐渐更新，慢慢统一了命名。

<!--more-->

## 安装及运行

在安装前，需要在 **启用或关闭 Windows 功能** 中勾选 **适用于 Linux 的 Windows 子系统**，或者直接在管理员权限的 PowerShell 中输入 `Enable-WindowsOptionalFeature -Online -FeatureName "Microsoft-Windows-Subsystem-Linux"` 此条命令，也能达到同样的效果。

完成上述操作后，可直接在 **Microsoft Store** 中搜索 Linux，到本文书写为止，商店中已经有 Ubuntu、SUSE、Debian、Kali 等 Linux 发行版，个人建议下载 Ubuntu。

到 Ubuntu 的下载页，可以看到发布者为 Canonical 公司，这也正是 Ubuntu 的维护公司，值得注意的是，Canonical 公司还发布了特定版本的 Ubuntu 系统，例如 Ubuntu 16.04 LTS、Ubuntu 18.04 LTS 等，个人建议直接下载无版本号的 Ubuntu，而不要下载特定版本的 Ubuntu，因为无版本号的 Ubuntu 会在新版本 Ubuntu 发布之后切换到最新版，所以它始终指向最新的 Ubuntu。同时请注意，应用商店里 Ubuntu 软件的更新并不会升级 Ubuntu 版本，如果你恰好安装的是旧版本，想要升级到新版本，可以在 WSL 中运行 `do-release-upgrade` 命令升级到最新版。

下载完成后，要启动 Ubuntu 有多种方式，可以在 **PowerShell** 或 **cmd** 中输入 `wsl` 或 `bash` 或 `ubuntu` 都可启动，也可以直接在 **开始菜单** 中点击 Ubuntu 图标启动。

## SSH 问题

要想在 WSL 中开启 SSH 服务，需要在配置文件（`/etc/ssh/sshd_config`）中作如下修改：

```text
Port 2222  #将22改为2222，因Win10中自带的SSH服务也在监听22端口
ListenAddress 0.0.0.0  #取消注释，监听所有IP
UsePrivilegeSeparation no  #将yes修改为no
PermitRootLogin yes  #将prohibit-password修改为yes，允许root用户登录，视个人情况而定
PasswordAuthentication yes  #将no修改为yes，允许密码登录
```

修改完成后用 `sudo service ssh start` 启动 SSH 服务，可能会报如下错误：

```text
Could not load host key: /etc/ssh/ssh_host_rsa_key
Could not load host key: /etc/ssh/ssh_host_dsa_key
Could not load host key: /etc/ssh/ssh_host_ecdsa_key
Could not load host key: /etc/ssh/ssh_host_ed25519_key
```

并且此时无法使用 SSH 客户端连接到服务器端，客户端会报如下错误：

```text
Connection closed by 127.0.0.1 port 2222
```

造成这种情况的原因是服务端在启动 SSH 服务时发现加密过程中需要用到的密钥文件未找到，可依次用如下命令生成所需文件：

```sh
ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key
ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key
```

其中 `-t` 参数表示加密类型，`-f` 参数表示生成的密钥文件名，错误信息中缺少什么密钥按需生成即可。之后再重新启动 SSH 服务即可正常工作。

## 图形界面问题

在你当前所使用的 shell 的配置文件里（比如 `.bashrc` 或 `.zshrc`），添加如下命令：

```sh
export DISPLAY=localhost:0
```

随后打开 X Server 客户端（比如 [Xming](https://sourceforge.net/projects/xming/) 或 [VcXsrv](https://sourceforge.net/projects/vcxsrv/)）并将 Display 项设为 0 即可运行图形化应用。笔者所使用的是 [MobaXterm](https://mobaxterm.mobatek.net/)，其设置路径为 **Settings** —> **Configuration** —> **X11** —> **Display offset**。

## EXE 程序问题

## netstat 和 ps

## systemd

WSL 中至今还没有使用 systemd，因此执行类似 `sudo systemctl start nginx` 这样的命令，会报如下这样的错误：

```text
System has not been booted with systemd as init system (PID 1). Can't operate.
```

一个替代方法是使用 service，如 `sudo service nginx start`。

## 后台运行问题

## 无法使用的软件

以下软件在 WSL 中暂时无法正常使用：

- `nmap`，详情请参见 [nmap not working](https://github.com/microsoft/WSL/issues/1349)。
- `proxychains`

## 更多

有关 WSL 的更多内容，可以查看 [WSL 官方文档](https://docs.microsoft.com/zh-cn/windows/wsl)，在使用 WSL 的过程中遇到任何问题，可以去 [WSL 的 GitHub 地址](https://github.com/microsoft/WSL)提 Issues。
