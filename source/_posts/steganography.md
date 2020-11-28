---
title: 隐写术
date: 2018-09-22 23:45:31
categories: CheatSheet
tags:
  - CTF
---

## 第一步

拿到一个被隐写的文件，第一步当然是判断该文件是哪种类型的文件，一般可以通过文件后缀名判断之，若不能通过文件后缀名判断，则可以使用 Linux 中的 `file` 命令，直接输入 `file a` 即可检查 a 文件的类型。

知道文件类型后，就可以对症下药，依据相应的类型使用相应的办法，此时，不妨再查看一下文件对应的二进制数据，所有电子信息的本质无非是二进制，可以在二进制数据中搜索 `CTF` 或 `FLAG` 等关键字，发现是否存在隐藏信息。Windows 下可以使用 Sublime Text 3 的插件 [HexViewer](http://facelessuser.github.io/HexViewer/) 查看二进制信息。Linux 下可以使用 `xxd` 命令查看文件二进制数据。

## 图片隐写

### 图片内容

首先应该检查图片内容本身是否存在某些隐藏信息，遇到不熟悉的图片可以尝试[谷歌搜图](https://www.google.com/imghp)，或许可以发现更多信息。

### Exif

Exif，即可交换图像文件格式（Exchangeable image file format），可以记录 JPEG 格式图片的属性信息和拍摄数据。有的 JPEG 格式图片会具有 Exif 信息，在 Windows 中查看属性选项卡中的详细信息项即可查看。别的格式的图片不具备 Exif 信息。如下图片：

![exif](/images/meinv.jpg)

<!--more-->

### JPEG

### PNG

### GIF

### BMP

## 音频隐写

音频隐写一般会用到 [MP3stego](http://www.petitcolas.net/steganography/mp3stego/)，该软件会将信息编码到 MP3 文件中，同时也可以从被隐写的 MP3 文件中解码所需信息。

下载该软件后在其 `MP3Stego` 文件夹下会有 2 个命令：`Encode` 和 `Decode`，`Encode` 命令用于隐写信息，`Decode` 命令用于解密被隐写的信息，使用 `decode -X -P pass svega_stego.mp3` 即可从 `svega_stego.mp3` 文件中解码所需信息，`-P` 指定解密密码。

## 视频隐写

## 其他隐写

### Word 文档

Word 文档可能会隐藏某些信息，遇到 `doc` 文档可以尝试在 `Word 选项`中选择`显示`并打开`隐藏文字`选项。如下所示：

![word](/images/word.PNG)

像 Word 文档或 Excel 表格这样的富文本文件，可以直接解压之，查看其中是否包含某些特殊文件。

类似的题可以参考 [Fonts](http://www.shiyanbar.com/ctf/1927)，[认真你就输了](http://www.shiyanbar.com/ctf/1849)等等。
