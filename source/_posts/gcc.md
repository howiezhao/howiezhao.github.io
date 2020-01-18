---
title: GCC小记
categories: CheatSheet
date: 2019-04-18 17:42:24
tags:
  - Linux
---

GCC一般有两层意思，大的意思是指GNU Compiler Collection（即GNU编译器套装），小的意思是指GNU C Compiler（即GNU C语言编译器），在本文中，我默认大写的GCC指大的意思，小写的gcc指小的意思。

使用gcc编译C语言源代码的一般格式如下：
```bash
$ gcc test.c -o test
```
<!-- more -->
## 常用参数
Linux下`gcc`命令常见的参数及其含义如下所示：
- `--help`：显示帮助信息
- `-o`：指定生成的文件名，若不指定，则默认生成a.out
- `-E`：生成`.i`格式的预处理文件
- `-S`：生成`.s`格式的汇编文件
- `-c`：生成`.o`格式的二进制文件
- `-save-temps`：保留所有生成的中间文件
- `-g`：生成必要的符号信息，为调试而用
- `-ggdb`：生成可特供于gdb使用的调试信息
- `-gstabs`：生成stabs格式的调试信息
- `-Wall`：显示所有常用的警告信息，即Warning all
- `-m32`：指定生成32位程序
- `-Os`：为减小代码大小而进行优化，即Optimizers small
- `-nostdinc`：不使用标准库
- `-fno-stack-protector`：不生成用于检测缓冲区溢出的代码
- `-I<dir>`：添加搜索头文件的路径
- `-fno-builtin`：除非用`__builtin_`前缀，否则不进行`builtin`函数的优化

## 跨平台
为了在Windows中使用GCC，诞生了[**MinGW**](http://www.mingw.org/) 项目，即Minimalist GNU for Windows(适用于Windows的极简GNU)，它是将GCC编译器和GNU Binutils移植到Win32平台下的产物，又被称为mingw32。另有可用于产生32位及64位Windows可执行文件的[**MinGW-w64**](https://mingw-w64.org/doku.php/start)项目，是从原MinGW项目产生的分支。
