---
title: PGP 与 GPG
categories: CheatSheet
date: 2023-08-26 16:00:20
tags:
  - 密码学
---

1991 年 Phil Zimmermann 开发了商业加密软件 PGP（Pretty Good Privacy），随着 PGP 的流行，[OpenPGP](https://www.openpgp.org/) 标准被制定，后来，GNU 开发了遵循 OpenPGP 标准的开源版本的 PGP，即 [GPG](https://www.gnupg.org/)（GNU Privacy Guard）。现在 GPG 被人们所广泛使用。

GPG 本质上是一个命令行工具，为了和别的操作系统更深入的融合，衍生出了不同的基于 GPG 开发的软件。Windows 下推荐使用 [Gpg4win](https://www.gpg4win.org/)，macOS 下推荐使用 [GPGTools](https://gpgtools.org/)。

<!-- more -->
## 生成密钥

使用 `gpg --gen-key` 命令即可生成自己的密钥，在生成过程中你需要完成以下步骤：

1. 选择加密算法
2. 选择密钥长度
3. 设定密钥有效期
4. 输入个人信息，包括姓名和邮箱，以生成用户ID
5. 设定私钥的保护密码

## gpg 常用命令

```bash
# 列出本机中的所有密钥
gpg --list-keys

# 从密钥列表中删除某个密钥
gpg --delete-key [用户ID]

# 生成公钥指纹
gpg --fingerprint [用户ID]

# 导入某个密钥
gpg --import [密钥文件]

# 导出指定用户ID的公钥
gpg --armor --output public-key.txt --export [用户ID]

# 导出指定用户ID的私钥
gpg --armor --output private-key.txt --export-secret-keys [用户ID]

# 使用接收者的公钥加密文件
gpg --recipient [用户ID] --output demo.en.txt --encrypt demo.txt

# 使用自己的私钥解密文件
gpg --decrypt demo.en.txt --output demo.de.txt

# 使用自己的私钥对文件签名，这会生成二进制的签名文件demo.txt.gpg
gpg --sign demo.txt

# 使用自己的私钥对文件签名，这会生成ASCII码的签名文件demo.txt.asc
gpg --clearsign demo.txt

# 使用自己的私钥对文件签名，这会生成单独的二进制的签名文件demo.txt.sig，与文件内容分开存放
gpg --detach-sign demo.txt

# 使用自己的私钥对文件签名，这会生成单独的ASCII码的签名文件，与文件内容分开存放
gpg --armor --detach-sign demo.txt

# 使用对方的公钥验证签名是否为真
gpg --verify demo.txt.asc demo.txt

# 使用接收者的公钥加密文件，同时使用发信者（自己）的私钥对文件签名
gpg --local-user [发信者ID] --recipient [接收者ID] --armor --sign --encrypt demo.txt
```

## 公钥服务器

公钥服务器是网络上专门储存用户公钥的服务器，目前主流的公钥服务器为 keys.openpgp.org。我们可以使用以下命令与公钥服务器交互：

```bash
# 将公钥上传到服务器
gpg --keyserver hkps://keys.openpgp.org --send-keys [用户公钥指纹]

# 查找某个用户的公钥
gpg --keyserver hkps://keys.openpgp.org --search-keys [用户公钥指纹]
```

公钥服务器就像一个目录，解决了公钥在哪里的问题，但它无法保证服务器上的公钥的可靠性，换句话说，任何人都可以用你的名义上传公钥。[Keybase](https://keybase.io) 是一个有趣的服务，它试图解决这个公钥到底属于谁。

## 使用 gpg 对 commit 签名

让我们以 GitHub 为例，首先，你需要将自己的公钥添加到 GitHub 上。具体流程，可以参考[官方文档](https://docs.github.com/zh/authentication/managing-commit-signature-verification/about-commit-signature-verification)。

其次，你需要在 Git 中配置要使用的密钥，使用命令 `git config --global user.signingkey [用户ID]` 即可。随后，每次 commit 时加上 `-S` 参数，即 `git commit -S -m "YOUR_COMMIT_MESSAGE"` 即可对提交进行签名。

如果不想每次都输入 `-S`，可以设置为默认对所有提交进行签名，即 `git config --global commit.gpgsign true`。

请注意，生成密钥时输入的邮箱应与 git config 配置中的邮箱一致。

此外，如果是在 Windows 上，为了避免使用 Git 内部自带的 gpg 命令，你可能还需要配置：`git config --global gpg.program (Get-Item (Get-Command gpg).Source).FullName`。
