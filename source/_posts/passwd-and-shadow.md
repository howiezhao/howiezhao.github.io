---
title: Linux中/etc/passwd与/etc/shadow的区别
date: 2018-04-29 15:32:14
categories: CheatSheet
tags:
  - Linux
  - 渗透
---

简单来说，`/etc/passwd`存储一般的用户信息，任何人都可以访问；`/etc/shadow`存储用户的密码信息，只有 root 用户可以访问。下面来详细介绍：

## /etc/passwd

早期的Linux中，用户的密码也存储在此文件中，但因为此文件所有人都可以访问，对密码的存储不安全，但又不能把它的权限改为仅 root 用户，因为系统的其他程序可能会用到此文件中存储的用户其他信息，所以，后来Linux将用户密码存储到了`/etc/shadow`文件中，并将其权限设为仅 root 用户。在渗透过程中，这两个文件最好都检查。
`/etc/passwd`的文件格式为：**用户名:密码:用户ID:用户组ID:注释:用户目录:登录shell**，共7项，默认情况下，root的用户ID为0，1-99表示预定义用户，100-999表示其他系统帐户，新建的其他用户ID从1000起，用户组ID代表的详细信息存储在`/etc/group`文件中，如果密码被存储在了`/etc/shadow`文件中，则此文件中密码项为x，常见形式如下：

```bash
root:x:0:0:root:/root:/bin/bash
```

## /etc/shadow

`/etc/shadow`的文件格式为：**用户名:密码:上次修改密码日期(从1970年1月1日起的天数):密码在两次修改期间的最小天数(0表示可在任何时间修改):密码需要被变更的天数(99999表示不需要变更):密码变更前提前几天警告:账号失效日期:账号失效后被禁用的天数:保留字段**，共9项，如果密码项以 ! 或 \*  起始，则代表此账号被锁定，不能用于登录，密码项中更为详细的格式为：**\$加密方法ID\$Salt\$加密值**，常见形式如下：

```bash
root:$6$Fsf6Q6SH$MlagWih0lcGFxtAo7/s8Z5.wywJyCqH6qateZ6yPFOPm8bNYTGAEPygZxSOPR1A9Rtw.WxJp2fNMOoeB1wj890:17524:0:99999:7:::
```
