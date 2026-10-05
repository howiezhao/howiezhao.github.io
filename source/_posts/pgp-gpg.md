---
title: PGP 与 GPG
categories: CheatSheet
date: 2023-08-26 16:00:20
tags:
---

1991 年 Phil Zimmermann 开发了商业加密软件 PGP（Pretty Good Privacy），随着 PGP 的流行，
[OpenPGP](https://www.openpgp.org/) 标准被制定，后来，GNU 开发了遵循 OpenPGP 标准的开源版本的 PGP，即 [GPG](https://www.gnupg.org/)（GNU Privacy Guard）。
现在 GPG 被人们所广泛使用。

GPG 本质上是一个命令行工具，为了和别的操作系统更深入的融合，衍生出了不同的基于 GPG 开发的软件。
Windows 下推荐使用 [Gpg4win](https://www.gpg4win.org/)，macOS 下推荐使用 [GPGTools](https://gpgtools.org/)。

<!-- more -->
## 生成密钥

## gpg 常用命令

```bash
# 列出本机中的所有密钥
gpg --list-keys


```

## 公钥服务器

## 使用 gpg 对 commit 签名
