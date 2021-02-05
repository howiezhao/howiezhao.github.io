---
title: vCard 是什么
categories: CheatSheet
date: 2021-02-04 17:00:58
tags:
---

vCard 是广为使用的电子名片的文件格式标准，常用于手机通讯录文件中，其后缀名常为 `.vcf`。

一个典型的 vCard 文件内容如下所示：

```text
BEGIN:VCARD
VERSION:2.1
N;CHARSET=UTF-8;ENCODING=QUOTED-PRINTABLE:testa
FN;CHARSET=UTF-8;ENCODING=QUOTED-PRINTABLE:testa
TEL;CELL:12345678910
END:VCARD
BEGIN:VCARD
VERSION:2.1
N;CHARSET=UTF-8;ENCODING=QUOTED-PRINTABLE:testb
FN;CHARSET=UTF-8;ENCODING=QUOTED-PRINTABLE:testb
TEL;CELL:12345678910
END:VCARD
```

每个 vCard 条目通过 `BEGIN:VCARD` 与 `END:VCARD` 包裹，其中 `VERSION` 字段表示 vCard 版本号，`N` 和 `FN` 字段分别表示 *姓名* 和 *名*，`TEL` 字段表示电话号码。

GitHub 上的 [vCards](https://github.com/metowolf/vCards) 项目提供了类似中国黄页的功能。
