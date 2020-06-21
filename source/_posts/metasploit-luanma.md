---
title: Metasploit 中 shell 中文乱码解决方案
date: 2017-12-04 23:46:32
categories: Bug
tags:
  - Kali
---

有时在 Kali Linux 中获得了一个 Windows shell 或者在 meterpreter 中进入 shell 后，执行命令可能会出现中文乱码，其原因是 Windows 和 Linux 的编码不同，导致 Windows 中的中文在 Linux 中无法正常显示。

**解决方法：**

1. 在 shell 窗口的工具栏选择“编辑”——>“首选项”——>“编码”，选中简体中文的三个编码：GB18030，GB2312，GBK，打勾并退出
2. 接着在“终端”——>“设定字符编码”中选择添加的三个简体中文编码之一即可

**注意：**

1. 这个设置会随着操作系统的重启而失效
2. 设定简体中文编码之后，Linux 中的中文字符就会乱码，因为 Linux 使用 UTF-8 编码
3. 建议只在需要的时候设定简体中文编码
