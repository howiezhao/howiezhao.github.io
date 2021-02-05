---
title: Linux系统加固
date: 2018-05-19 13:59:05
categories: CheatSheet
tags:
  - Linux
---

## 帐户与口令

此方面的加固主要为了防止针对帐户的暴力破解。

禁用或删除无用帐户：
使用命令`userdel <用户名>`删除不必要的帐户，使用参数`-r`即可删除相应用户的家目录和邮箱目录。
使用命令`passwd -l <用户名>`锁定不必要的帐户，解锁可使用`passwd -u <用户名>`。

检查特殊帐户：
使用命令`awk -F: '($2=="")' /etc/shadow`查看空口令帐户，若存在，则使用命令`passwd <用户名>`为空口令帐户设定密码。
使用命令`awk -F: '($3==0)' /etc/passwd`查看uid为0的帐户，确认uid为0的帐户只有root帐户。

添加口令策略：
使用命令`change -m 0 -M 30 -E 2020-01-01 -W 7 <用户名>`修改帐户口令策略，`-m`表示密码最小使用天数，`-M`表示密码最大使用天数，`-E`表示密码到期时间，`-W`表示密码到期前多少天提醒。或者可以直接编辑/etc/login.defs文件进行修改。
<!--more-->
设置用户锁定：
在CentOS7中，编辑/etc/pam.d/system-auth文件，添加`auth required pam_tally2.so onerr=fail deny=6 unlock_time=300`此行，表示当密码连续输错6次后锁定，锁定时间300秒。
限制能su到root的用户：
编辑/etc/pam.d/su文件，添加`auth required pam_wheel.so group=test`此行，表示只允许test组用户su到root。

## 服务安全

服务越少，系统越安全。

关闭不必要的服务：
在CentOS中，使用命令`chkconfig --level <init级别> <服务名> on|off|reset`设置服务在指定init级别下开机是否启动。

SSH服务安全：
编辑/etc/ssh/sshd_config文件，修改默认端口，即`Port`项；禁止root用户远程登录，即`PermitRootLogin`项，应使用普通用户登录，特殊权限时使用`sudo`命令；禁止空密码登录，即`PermitEmptyPasswords`项；限制登录密码输错次数；最好使用密钥登录而不是密码登录，即`PasswordAuthentication`项值改为`no`。修改完后，需要使用`service sshd restart`重启SSH服务。

## 文件系统安全

权限越小，系统越安全

设置umask值：
编辑/etc/profile文件，修改umask值为027。

设置登录超时：
编辑/etc/profile文件，添加`TIMEOUT=180`，即登录后无操作3分钟将超时断开连接。
