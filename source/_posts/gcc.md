---
title: GCC 小记
categories: CheatSheet
date: 2019-04-18 17:42:24
tags:
  - Linux
---

GCC 一般有两层意思，广义是指 GNU Compiler Collection（即 GNU 编译器套装），狭义是指 GNU C Compiler（即 GNU C 语言编译器），在本文中，我默认大写的 GCC 指广义，小写的 gcc 指狭义。

使用 gcc 编译 C 语言源代码的一般格式如下：

```bash
gcc test.c -o test
```
<!-- more -->
## 常用参数

Linux下 `gcc` 命令常用的参数及其含义如下所示：

- `--help`：显示帮助信息
- `-o`：指定生成的文件名，若不指定，则默认生成 `a.out`
- `-E`：生成 `.i` 格式的预处理文件
- `-S`：生成 `.s` 格式的汇编文件
- `-c`：生成 `.o` 格式的二进制文件
- `-save-temps`：保留所有生成的中间文件
- `-g`：生成必要的符号信息，为调试而用
- `-ggdb`：生成可特供于 gdb 使用的调试信息
- `-gstabs`：生成 stabs 格式的调试信息
- `-Wall`：显示所有常用的警告信息，即 Warning all
- `-m32`：指定生成 32 位程序
- `-Os`：为减小代码大小而进行优化，即 Optimizers small
- `-nostdinc`：不使用标准库
- `-fno-stack-protector`：不生成用于检测缓冲区溢出的代码
- `-I<dir>`：添加搜索头文件的路径
- `-fno-builtin`：除非用 `__builtin_` 前缀，否则不进行 `builtin` 函数的优化

## 跨平台

为了在 Windows 中使用 GCC，诞生了 [**MinGW**](http://www.mingw.org/) 项目，即 Minimalist GNU for Windows（适用于 Windows 的极简 GNU），它是将 GCC 编译器和 GNU Binutils 移植到 Win32 平台下的产物，又被称为 **mingw32**。另有可用于产生 32 位及 64 位 Windows 可执行文件的 [**MinGW-w64**](https://mingw-w64.org/doku.php/start) 项目，是从原 MinGW 项目产生的分支。
