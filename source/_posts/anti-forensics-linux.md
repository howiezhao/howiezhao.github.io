---
title: 反取证之 Linux
date: 2018-05-02 00:02:31
categories: CheatSheet
tags:
  - 渗透
  - 计算机取证
  - Linux
---

后渗透测试阶段的重要工作便是擦除痕迹，也即**反取证**，文件系统访问都会留下痕迹，最好的避免计算机取证的方法就是不要碰文件系统，这也是 meterpreter 的先天优势，它完全基于内存，Linux 中的反取证主要涉及 MAC 时间、日志文件、history：

## MAC 时间

MAC 即 Modified/Accessed/Changed，也就是修改/访问/更改时间，修改时间指对文件内容修改时的时间，访问时间指对文件内容访问时的时间（例如通过 `cat` 查看时），更改时间指对文件属性、权限更改时的时间。

使用 `ls -l` 默认查看的是修改时间，要查看其余 2 个时间，可以加参数 `ls -l --time=atime/ctime`，另一个查看 MAC 时间的命令是 `stat`。

使用 `touch -d "5 days ago"` 或 `touch -t 1805021030` 可以修改 MAC 中的 MA 时间。meterpreter 中的 `timestomp` 命令可以方便的修改 MAC 时间。
<!-- more -->
## 日志文件

清除相关日志文件

### 系统日志

Linux 中的日志文件主要有 `/var/log/auth.log`、`/var/log/secure`、`/var/log/wtmp`、`/var/log/btmp`、`/var/log/lastlog`、`/var/log/faillog`。

Debian 系的 `auth.log` 文件与 RedHat 系的 `secure` 文件都记录了系统的登录日志，`last` 命令用于查看登录日志以及重启日志，文件位于 `/var/log/wtmp`；`lastb` 命令用于查看登录失败日志，文件位于 `/var/log/btmp`；`lastlog` 命令用于查看所有用户最近一次登录日志，文件位于 `/var/log/lastlog`；`faillog` 命令与 `lastlog` 命令一样，用于查看用户登录失败日志，文件位于 `/var/log/faillog`，此命令仅限于 Debian 系。

### Web 日志

Apache 的日志文件位于 `/var/log/apache2`；Nginx 的日志文件位于 `/var/log/nginx`。

## history

Linux 中，每次输入的命令都会记录在用户文件夹中的 `.bash_history` 文件中，默认记录 1000 条命令，使用 `history` 命令即可查看，清除记录的方法是使用 `history -c` 命令。另一种清除记录的方法是更改 `.bash_history` 文件的属性，使用命令：`chattr +i .bash_history` 使其不可被更改，从而无法向其写入任何数据。

**最后，请不要忘记 HIDS/IPS/WAF/集中的日志服务器的痕迹擦除。**
