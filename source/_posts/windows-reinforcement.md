---
title: Windows系统加固
date: 2018-05-19 13:58:51
categories: CheatSheet
tags:
  - Windows
---

## 基本配置
下面这几项应为每一个使用Windows的用户的最最基本安全配置：
1. 开启Windows防火墙
2. 设置用户帐户控制(UAC)为合适级别
3. 保持Windows更新

<!--more-->
## 帐户安全
此方面的加固主要是为了防止针对帐户的暴力破解，帐户是黑客入侵系统的突破口，帐户越多，危险系数越高。

停用Guest帐户：
在**计算机管理**的**本地用户和组**中禁用Guest帐户，并为Guest帐户设置复杂密码，并拒绝远程访问。

重命名或禁用Administrator帐户：
在**计算机管理**的**本地用户和组**中为Administrator帐户重命名，或直接禁用。

创建陷阱帐户：
在**计算机管理**的**本地用户和组**中创建一个名为Administrator的本地帐户，并将它的权限设置成最低，加上一个超过10位的强密码。可通过将其隶属于Guest组已达到权限最低。

限制用户数量：
在**计算机管理**的**本地用户和组**中删除所有的测试帐户、共享帐户和普通部门帐户，一般情况下，如果系统用户超过10个，一般总会存在一两个弱口令帐户。

开启帐户锁定策略：
在**本地安全策略**的**帐户锁定策略**中设置帐户锁定阈值为3次，帐户锁定时间为30分钟，重置帐户锁定计数器为30分钟之后。
## 系统安全
一个安全操作系统的基本原则是：最小的权限+最少的服务=最大的安全。

开启密码策略：
在**本地安全策略**的**密码策略**中启用密码复杂性要求，设置密码长度最小值为7，密码最短使用期限为1，密码最长使用期限为42，强制密码历史为24，禁用以可还原的加密储存密码。

设置双重加密帐户保护：
在运行对话框中输入syskey，启用SAM数据库加密工具，为Windows登录设置双重加密，注意此功能在Windows10中已被剔除。

取消默认共享：
编辑注册表键HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\LanmanServer\Parameters，新建项AutoShareServer，值为0，即可关闭盘符默认共享，新建项AutoShareWks，值为0，即可关闭ADMIN默认共享。

开启审核策略：
在**本地安全策略**的**审核策略**中审核所有的成功失败操作，记录的信息可以在**事件查看器**的**Windows日志**中查看。

修改TTL值：
编辑注册表键HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\Tcpip\Parameters，新建项defaultTTL，随便赋值，以防黑客通过ping获取TTL以鉴别操作系统类型。

关闭不必要的服务：
Windows默认会启动多个服务，可以在**计算机管理**的**服务**中禁用相关服务，下面列出了一些可以禁用的服务：

- COM+ Event System
- Computer Browser
- Distributed Link Tracking Client
- Routing and Remote Access