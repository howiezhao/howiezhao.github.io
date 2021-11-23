---
title: useradd 与 adduser
date: 2018-07-16 10:44:41
categories: CheatSheet
tags:
  - Linux
---

在 Linux 中创建用户可以用 `useradd` 或者 `adduser`，值得注意的是创建的用户并不一定可以登录，登录的用户肯定要有它的用户主目录、登录 Shell 等相关配置，而这两个命令之间的差异就在于此。

## adduser

当使用 `adduser howie` 命令时，系统除了创建 howie 用户，还会自动创建用户主目录、同名用户组、登录 Shell 等，并提示输入用户密码，这一切操作都将以一个对话的形式完成。

在某些新版本的 RedHat 系 Linux 中，`adduser` 是 `useradd` 的一个软链接，即别名。

## useradd

当使用 `useradd howie` 命令时，系统只会创建 howie 用户，而不会创建用户密码、用户主目录、同名用户组、登录 Shell 等，若要指定密码，可以接着采用 `passwd howie` 命令。其次，`useradd` 有众多参数，我们可以通过使用这些参数来达到和 `adduser` 一样的效果，如 `useradd -d /home/howie -m -s /bin/bash howie`，不过注意之后还得使用 `passwd` 命令创建密码，当然也可以使用 `-p` 参数直接设置密码，但这样会将密码直接显示在终端屏幕上，不安全。

## userdel

当使用 `userdel howie` 命令时，系统只会删除 howie 用户，并不会删除用户主目录以及用户邮箱目录，因此可以使用 `-r` 参数。
