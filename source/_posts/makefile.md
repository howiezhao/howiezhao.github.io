---
title: Makefile小记
categories: CheatSheet
date: 2019-04-18 12:40:39
tags:
  - Linux
---

Linux中使用最广的构建工具是**make**，而make会读取**Makefile**文件中的配置信息来完成构建，一个简单的Makefile文件如下所示：
```bash
editor : main.o text.o
    gcc -o editor main.o text.o
main.o : main.c def.h
    gcc -c main.c  #-c参数指定生成.o文件
text.o : text.c com.h
    gcc -c text.c
install : editor
    mv editor /usr/local
```
具体而言，冒号前面为**target**，即要生成的文件；冒号后面为**dependencies**，即被依赖的文件；每一个**target:dependencies对**的下一行为要执行的**命令**（注意要以Tab键起首）。当make不带参数时，默认执行第一个target。target也可以是要求make要完成的动作，执行这种target后并不能得到和target同名的文件，因此，也称做**phony target**（即伪target），如第7行所示。dependencies也可以为空，如常用的target为`clean`时，就没有依赖，只有命令，一般用于清理工作。

当输入`make`或`make editor`，即可开始构建。若`editor`这个target文件不存在，或者`main.o`、`text.o`这两个依赖文件被修改，都会导致make调用其下的命令`gcc -o editor main.o text.o`；接下来，由于引用到`main.o`和`text.o`，make会检查`main.o`的依赖`main.c`、`def.h`有无更新，如果有，则执行其下的命令`gcc -c main.c`；同理，也适用于`text.o`。当输入`make install`，make会检查install的依赖`editor`是否是最新，如果是，则执行其下的命令`mv editor /usr/local`。
<!--more-->
## 注释
Makefile中以`#`开头的均为注释。

## 回声
正常情况下，make会打印每条命令，然后再执行，这就叫做**回声**。在命令的前面加上`@`，就可以关闭回声。由于在构建过程中，需要了解当前在执行哪条命令，所以通常只在注释和纯显示的echo命令前面加上`@`。

## 内置目标名
**内置目标名**指示了如果某些名称作为target（目标名）出现，则具有特殊含义，常用的如下所示：
- `.PHONY`：明确声明伪目标
- `.SUFFIXES`：消除默认后缀规则
- `.DELETE_ON_ERROR`：如果遇到错误（或make中断）则删除目标文件

更多的内置目标名可以参考[make官方手册](https://www.gnu.org/software/make/manual/html_node/Special-Targets.html#Special-Targets)。

## 变量
Makefile中也可以使用变量，如下所示：
```bash
TXT = Hello World
test:
    echo $(TXT)
```
这类似于C语言中的宏，按照传统，变量名一般大写，使用变量时要放在`$()`之中。

有时，变量的值可能指向另一个变量，比如：`V1 = $(V2)`，这时会出现一个问题，V1的值到底在定义时扩展（静态扩展），还是在运行时扩展（动态扩展）？如果V2的值是动态变化的，这两种扩展方式的结果可能会差异很大。为了解决类似问题，Makefile一共提供了四个赋值运算符，如下所示：
```bash
VARIABLE = value
# 在运行时扩展，允许递归扩展。

VARIABLE := value
# 在定义时扩展。

VARIABLE ?= value
# 只有在该变量为空时才设置值。

VARIABLE += value
# 将值追加到变量的尾端。
```
## 内置变量
Makefile提供了一系列的内置变量，常见的如下所示：
- `$(CC)`：指向当前使用的编译器

更多的内置变量可以参考[make官方手册](https://www.gnu.org/software/make/manual/html_node/Implicit-Variables.html)。
## 自动变量
## 判断
使用条件判断，可以让make根据运行时的不同情况选择不同的执行分支。如下所示：
```bash
ifeq ($(CC),gcc)
  libs=$(libs_for_gcc)
else
  libs=$(normal_libs)
endif
```
上面代码判断当前编译器是否为gcc，然后指定不同的库文件。其中`ifeq`比较参数`arg1`和`arg2`是否相同，类似的，`ifneq`比较参数`arg1`和`arg2`是否不相同。

除此之外，还有`ifdef`判断变量是否被定义，`ifndef`判断变量是否没有被定义。

## 函数
Makefile中还内置了许多函数，可供调用，格式如下：
```bash
$(function arguments)
# 或者
${function arguments}
```
常用的函数有：
- `$(shell)`：用来执行shell命令
- `$(wildcard)`：用来在Makefile中，替换Bash的通配符。
- `$(patsubst)`：用于模式匹配的替换，语法为`$(patsubst <pattern>,<replacement>,<text>)`
- `$(filter)`：
- `$(addsuffix)`：
- `$(addprefix)`：
- `$(if)`：
- `$(foreach)`：
- `$(call)`：唯一一个可以用来创建新的参数化的函数，语法为`$(call <expression>,<parm1>,<parm2>,...,<parmn>)`，值得注意的是，call函数在处理参数时，第2个及其之后的参数中的空格会被保留，因而在向call函数提供参数时，最安全的做法是去除所有多余的空格，避免造成一些奇怪的效果。

相关示例如下：
```bash
# shell函数用法
contents := $(shell cat foo) # 将foo文件中的内容赋值给contents

# call函数用法
reverse =  $(2) $(1)
foo = $(call reverse,a,b) # 最终foo的值为b a
```

更多的内置函数可以参考[make官方手册](https://www.gnu.org/software/make/manual/html_node/Functions.html)

## 引用其它的Makefile
在Makefile中可以使用`include`关键字把别的Makefile包含进来，这很像C语言的`#include`，被包含的文件会原模原样的放在当前文件的包含位置。`include`的语法是：`include <filename>`，其中被包含的Makefile文件通常以`.mk`结尾。