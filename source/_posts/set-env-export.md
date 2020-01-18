---
title: set、env与export
date: 2018-05-09 19:20:18
categories: CheatSheet
tags:
  - Linux
---

## 环境变量

**环境变量**，顾名思义由**环境**和**变量**两部分组成，本质上就是一些变量，每个进程都有一个自己的运行环境，而在这些环境中又有一些定义的变量，Shell也是如此，同样的，通过Shell所运行的命令，相当于从父进程创建了一个子进程，它们共享同样的环境变量。

在Linux中，环境变量可以大致分为**Shell环境变量**和**用户环境变量**两大类，不同的Shell有不同的Shell环境变量，例如bash与Zsh的Shell环境变量就不相同，而用户环境变量通常是由用户自定义的，Shell环境变量包含了用户环境变量。

在Linux中可以使用`declare`命令直接定义**Shell环境变量**，如：
```bash
# 定义Shell环境变量A，值为hello，注意等号两边不能有空格
# 按照传统，环境变量一般为全大写
declare A=hello
```
同样的，在Linux中使用`echo`命令即可打印环境变量的值，如：
```bash
# 打印A的值，环境变量前需加“$”符号，
# 表示要打印的是环境变量而不是一般字符串
echo $A
```
值得注意的是，这种定义只对当前终端有效，关闭终端后失效。

常见的Shell环境变量有：
- COLUMNS：当前终端的宽度
- LINES：当前终端的高度

常见的用户环境变量有：
- PATH：用以指定命令的搜索目录
- HOME：用以指定用户的家目录
- SHELL：用以指定用户的登录Shell
- HTTP_PROXY：用以指定终端的HTTP代理信息，与下一个变量要同时设置
- HTTPS_PROXY：用以指定终端的HTTPS代理信息

<!-- more -->

## set

`set`命令用来显示或设置**Shell环境变量**，当不带参数运行时默认显示所有已定义的Shell环境变量，若要设置环境变量可采用：
```bash
set A=hello
```
值得注意的是，当`declare`命令不带任何参数运行时，也会显示所有的Shell环境变量，但它比`set`显示的结果要更加清晰。

关于set命令更多的参数使用说明可参考阮一峰的博文：[Bash脚本set命令教程](http://www.ruanyifeng.com/blog/2017/11/bash-set.html)

## env（仅限于Linux）

`env`命令用来显示或设置**用户环境变量**，当不带参数运行时默认显示所有已定义的用户环境变量，若要设置环境变量可采用：
```bash

```

## export（仅限于Linux）

`export`命令用来显示或设置当前导出至用户环境变量的Shell环境变量，当不带参数运行时默认显示所有已导出至用户环境变量的Shell环境变量，若要导出某Shell环境变量到用户环境变量可采用：
```bash
export a=hello
```
这一步操作实际上完成了两步操作，即：
```bash
declare a=hello  #定义一个Shell环境变量$a
export $a  #导出至用户环境变量
```