---
title: 编译与构建
date: 2018-07-15 14:29:13
categories: CheatSheet
tags:
---

## 编译

**编译（compile）**，一般而言是将源代码转换成汇编代码，用以实现这种过程的工具称为**编译器（compiler）**。但要注意，编译器在同一时刻只能转换一个编译单元，所谓**编译单元**是指单个的源文件。

目前在 Linux 中使用最广的编译器是 **[GCC](https://gcc.gnu.org/)** ，即 GNU Compiler Collection（GNU 编译器套件），GCC 的原名为 GNU C Compiler（GNU C 语言编译器），因为在后续逐渐支持了 C++、Java 等更多的语言，所以更改了其缩写的含义。

## 构建

程序通常由多个编译单元组成，倘若逐个的去编译，这多少显得有点琐碎，因此我们需要一个自动化工具用来从源代码生成用户可以使用的目标，而这个工具就是**构建系统（build system）**，构建系统所作的就是**构建（build）**，构建的过程中肯定会调用到编译。从这个意义上来说，构建的范围比编译更广。

在 Linux 中使用最广的构建系统是 **[GNU make](https://www.gnu.org/software/make/)** ，它会读取 **Makefile** 文件中的配置信息来完成构建，有关 Makefile 文件更详细的信息可参考 [Makefile 小记](http://howiezhao.github.io/2019/04/18/makefile/)。

## 另外的

Java 世界中使用最广的构建系统是 **[Maven](https://maven.apache.org/)** ，而在 Android Studio 中则使用到了后起之秀 **[Gradle](https://gradle.org/)** 。

C 语言从源代码到可执行文件的过程依次经过了**预处理**、**编译**、**链接**这几个步骤，即我们常说的 GCC 是编译器，但它实际可以完成的工作不止是编译，具体生成结果取决于我们的参数。

普通编译是生成当前系统平台下的目标文件，而**交叉编译**是指生成另一个系统平台下的目标文件。
