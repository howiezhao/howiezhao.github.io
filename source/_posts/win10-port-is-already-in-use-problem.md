---
title: Windows 10 中莫名其妙的“端口被占用”问题解决
categories: Bug
date: 2021-06-01 21:22:03
tags:
---

大约是自 Windows 10 1709 更新之后（或许是 1809？2004？），莫名其妙的存在类似“端口被占用”这样的问题，比如像下面这样的报错信息：

```text
Error: listen EACCES: permission denied 0.0.0.0:3000
...
```

或者启动 SS 时提示：

```text
Shadowsocks Error: Port already in use
...
```

又或者启动 Docker 时提示：

```text
Error starting userland proxy: Bind for 0.0.0.0:50051: unexpected error Permission denied.
```

电脑重启几次之后，以上报错可能会消失，一切又恢复正常。

<!-- more -->

这表面上像是端口 `3000` 被占用，实则不然，因为当你在 PowerShell 中输入 `netstat -ano | findstr "3000"` 查看端口占用信息时，它却无任何输出。实际上这个错误对应的 Windows 错误码是 [10013（WSAEACCES）](https://docs.microsoft.com/zh-cn/windows/win32/winsock/windows-sockets-error-codes-2) ：权限被拒绝。

出现这个错误的原因是 Windows 10 的补丁 [KB4074588](https://support.microsoft.com/zh-cn/topic/2018-%E5%B9%B4-2-%E6%9C%88-13-%E6%97%A5-kb4074588-%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E5%86%85%E9%83%A8%E7%89%88%E6%9C%AC-16299-248-b4e2ca66-dd7a-6fd5-a8f3-dc6683d4922b) 中存在一个已知问题：

> 安装此更新后，应用程序可能无法保留或绑定到以前工作的端口。

这些端口会被 Hyper-V 拿来保留备用，处于备用的端口无法被其他程序使用，用户登录后，系统会随机保留一些端口。使用 `netsh interface ipv4 show excludedportrange protocol=tcp` 可以查看被保留的端口段，每次重启都有可能是不同的端口。

因此，当你的系统启用 Hyper-V 或安装 Docker（安装 Docker Desktop 会启用 Hyper-V）之后，这个问题可能就会出现。

这个问题的解决方法（[workaround](https://en.wikipedia.org/wiki/Workaround)）有两种，最粗暴的方法就是如上所述多重启几次，让它的随机端口改变，但以后仍有可能会遇到同样的问题。另一种方法是排除掉需要使用的端口，具体来说：

1. 禁用 Hyper-V
2. 添加需要排除的端口范围，如：`netsh int ipv4 add excludedportrange protocol=tcp startport=50051 numberofports=1`
3. 重新启用 Hyper-V

----

参考：

1. <https://github.com/shadowsocks/shadowsocks-windows/issues/1835>
2. <https://github.com/docker/for-win/issues/3171>
