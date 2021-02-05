---
title: WSL相关问题解决
date: 2018-08-21 19:23:05
categories: Bug
tags:
  - Windows
  - Linux
---

## 名称问题

最早这个项目命名为**Bash on Ubuntu on Windows**，随后改名为**Windows Subsystem for Linux**，即**WSL**，值得肯定的是，随着Windows 10逐渐更新，慢慢统一了命名。

## 安装及运行

在安装前，需要在**启动或关闭Windows功能**中勾选**适用于Linux的Windows子系统**，或者直接在管理员权限的PowerShell中输入`Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`此条命令，也能达到同样的效果。
完成上述操作后，可直接在**Microsoft Store**中搜索Linux，到本文书写为止，商店中已经有Ubuntu、SUSE、Debian、Kali等Linux发行版，个人建议下载Ubuntu。
到Ubuntu的下载页，可以看到发布者为Canonical公司，这也正是Ubuntu的维护公司，值得注意的是，Canonical公司还发布了特定版本的Ubuntu系统，例如Ubuntu 16.04 LTS、Ubuntu 18.04 LTS等，个人建议直接下载无版本号的Ubuntu，而不要下载特定版本的Ubuntu，因为无版本号的Ubuntu会在新版本Ubuntu发布之后切换到最新版，所以它始终指向最新的Ubuntu。同时请注意，应用商店里Ubuntu软件的更新并不会升级Ubuntu版本，如果你恰好安装的是旧版本，想要升级到新版本，可以在WSL中运行`do-release-upgrade`命令升级到最新版。
下载完成后，要启动Ubuntu有多种方式，可以在**PowerShell**或**cmd**中输入`wsl`或`bash`或`ubuntu`都可启动，也可以直接在**开始菜单**中点击Ubuntu图标启动。
<!--more-->
## SSH问题

要想在WSL中开启SSH服务，需要在配置文件(/etc/ssh/sshd_config)中作如下修改：

```bash
Port 2222  #将22改为2222，因Win10中自带的SSH服务也在监听22端口
ListenAddress 0.0.0.0  #取消注释，监听所有端口
UsePrivilegeSeparation no  #将yes修改为no
PermitRootLogin yes  #将prohibit-password修改为yes，允许root用户登录，视个人情况而定
PasswordAuthentication yes  #将no修改为yes，允许密码登录
```

修改完成后用`sudo service ssh start`启动SSH服务，可能会报如下错误：

```bash
Could not load host key: /etc/ssh/ssh_host_rsa_key
Could not load host key: /etc/ssh/ssh_host_dsa_key
Could not load host key: /etc/ssh/ssh_host_ecdsa_key
Could not load host key: /etc/ssh/ssh_host_ed25519_key
```

并且此时无法使用SSH客户端连接到服务器端，客户端会报如下错误：

```bash
Connection closed by 127.0.0.1 port 2222
```

造成这种情况的原因是服务端在启动SSH服务时发现加密过程中需要用到的密钥文件未找到，可依次用如下命令生成所需文件：

```bash
ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key
ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key
```

其中`-t`参数表示加密类型，`-f`参数表示生成的密钥文件名，错误信息中缺少什么密钥按需生成即可。之后再重新启动SSH服务即可正常工作。

## 图形界面问题

在你当前所使用的shell的配置文件里（比如`.bashrc`或`.zshrc`），添加如下命令：

```sh
export DISPLAY=localhost:0
```

随后打开X Server客户端（比如[Xming](https://sourceforge.net/projects/xming/)或[VcXsrv](https://sourceforge.net/projects/vcxsrv/)）并将Display项设为0即可运行图形化应用。笔者所使用的是[MobaXterm](https://mobaxterm.mobatek.net/)，其设置路径为**Settings** —> **Configuration** —> **X11** —> **Display offset**。

## EXE程序问题

## netstat和ps

## 后台运行问题

## 无法使用的软件

以下软件在 WSL 中暂时无法正常使用：

- `nmap`，详情请参见 [nmap not working](https://github.com/microsoft/WSL/issues/1349)。
- `proxychains`

## 更多

有关WSL的更多内容，可以查看[WSL官方文档](https://docs.microsoft.com/zh-cn/windows/wsl/about)，或者[WSL官方博客](https://blogs.msdn.microsoft.com/wsl/)，在使用WSL的过程中遇到任何问题，可以去[WSL的GitHub地址](https://github.com/Microsoft/WSL)提Issues。
