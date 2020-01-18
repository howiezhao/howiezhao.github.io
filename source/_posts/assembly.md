---
title: 汇编语言小记
categories: CheatSheet
date: 2019-03-09 17:41:13
tags:
---

**汇编语言**（Assembly Language，简称**ASM**）由**汇编指令**、**伪指令**和**其他符号**组成，其中汇编指令有对应的机器码，而伪指令和其他符号没有对应的机器码，仅由汇编器识别执行。
## 架构
汇编语言是依赖底层CPU架构的，不同的CPU架构拥有不同的汇编语言，比如，常用于PC的**x86汇编**和常用于嵌入式设备的**ARM汇编**。由于x86架构又分为16位、32位、64位等，其相应的汇编也有稍许不同。本文主要以32位x86汇编为例做简要介绍。
<!--more-->
## 寄存器
汇编语言的大部分指令都是直接操作CPU中的寄存器的，所以有必要了解以下x86架构的CPU中常见的寄存器。

16位x86CPU中常见的寄存器有：
- 通用寄存器（**8个**）：
  - 数据寄存器：
    - AX：累加寄存器，Accumulator
    - BX：基址寄存器，Base
    - CX：计数寄存器，Count
    - DX：数据寄存器，Data
  - 指针寄存器：
    - SP：堆栈指针寄存器，Stack Pointer
    - BP：基址指针寄存器，Base Pointer
  - 变址寄存器：
    - SI：源变址寄存器，Source Index
    - DI：目的变址寄存器，Destinatin Index
- 段寄存器：
  - CS：代码段寄存器，Code Segment
  - DS：数据段寄存器，Data Segment
  - SS：堆栈段寄存器，Stack Segment
  - ES：附加段寄存器，Extra Segment
- 控制寄存器：
  - IP：指令指针寄存器，Instruction Pointer
  - FLAGS：标志寄存器

为了保证兼容性，AX、BX、CX、DX这四个寄存器都可分为两个可独立使用的8位寄存器来用，如AX可分为**AH**和**AL**，其中AH代表高（High）8位，AL代表低（Low）8位，其他3个也是如此。

32位x86CPU在16位的基础上增加了一些寄存器，那些和原来作用相同的寄存器一般会在前面加上`E`，其中常见的寄存器有：
- 通用寄存器（**8个**）：EAX、EBX、ECX、EDX、ESP、EBP、ESI、EDI
- 段寄存器：CS、DS、SS、ES、FS、GS，增加的FS、GS和ES一样，属于附加段寄存器
- 指令指针寄存器：EIP
- 标志寄存器：EFLAGS
- 系统表寄存器：GDTR、LDTR、IDTR、TR
- 控制寄存器：CR0、CR1、CR2、CR3、CR4
- 调试寄存器：DR0、DR1、DR2、DR3、DR4、DR5、DR6、DR7
- 测试寄存器：TR0、TR1、TR2、TR3、TR4、TR5、TR6、TR7

类似的，64位又在32位的基础上增加了一些寄存器，那些和原来作用相同的寄存器一般会将前面的`E`改为`R`，其中常见的寄存器有：
- 通用寄存器（**16个**）：RAX、RBX、RCX、RDX、RSP、RBP、RSI、RDI、R8、R9、R10、R11、R12、R13、R14、R15
- 指令指针寄存器：RIP
- 标志寄存器：RFLAGS

## 指令
常见的汇编指令如下：
- `mov`：传送指令，两个操作对象的位数应该一致，如`mov eax,ebx`，表示将EBX的值送入EAX中。8086CPU不支持将数据直接送入段寄存器的操作，要想实现此功能，只能用一个寄存器来进行中转。
- `add`：加法指令，两个操作对象的位数应该一致，如`add eax,ebx`，表示将EAX和EBX相加，其值赋给EAX。
- `sub`：减法指令，如`sub eax,ebx`，表示用EAX减EBX，其值赋给EAX。
- `push`：
- `pop`：
- `jmp`：跳转指令，属于转移指令，如`jmp 2AE3:3`，表示将CS设为2AE3H，将IP设为0003H，CPU将从CS:IP（即2AE33H）处读取指令；`jmp eax`表示将EAX的值赋给IP，CS保持不变。
- `jnz`：条件跳转指令，检查EFLAGS标志寄存器中的ZF位（零标志位）是否为0，若不为0，则跳转。
- `jz`：条件跳转指令，检查EFLAGS标志寄存器中的ZF位（零标志位）是否为0，若为0，则跳转。
- `in`：从I/O端口读取内容，如`in al,21H`，表示从21H端口读取内容到AL中。
- `out`：向I/O端口写入内容，如`out 21H,al`，表示将AL的值写入到21H端口中。
- `xor`：按位异或运算，即相同为0，不同为1，如`xor eax,ebx`，表示将EAX和EBX按位异或，其值赋给EAX。对同一个值进行异或，会使其得0，汇编中常用这种方法得到0，如`xor eax,eax`。
- `or`：按位或运算，如`or eax,ebx`，表示将EAX和EBX按位或，其值赋给EAX。

注意：汇编指令和寄存器名称不区分大小写。

## 伪指令
伪指令依赖于具体的汇编器，这里我们以GNU中的as汇编器（gas）为例，讲述常见的伪指令及其含义：
- `.set`：为变量设置一个值，如`.set CR0_PE_ON, 0x1`。
- `.globl`或`.global`：设置外部链接，使其在其他文件中可被调用，如`.globl start`。
- `.code16`：生成16位汇编代码。
- `.code32`：生成32位汇编代码。
- `.p2align`：
- `.word`：
- `.long`：

想要了解更多的伪指令可以参考[gas的官方文档](https://sourceware.org/binutils/docs/as/Pseudo-Ops.html#Pseudo-Ops)。
## 标号
标号代表一个地址，类似于高级语言中的函数，在需要时可以使用跳转指令跳转到标号处执行，利用标号还可以实现死循环，如下：
```Assembly
spin:
    jmp spin
```

## 风格
x86汇编语言的两大风格分别是**Intel风格**和**AT&T风格**，分别被Microsoft和GNU所采用，两种风格的详细区别如下表所示：

项目|Intel风格|AT&T风格
---|---|---
操作数顺序|目标操作数在前，如`mov eax,8`|源操作数在前，如`movl $8,%eax`
寄存器名字|原样，如`mov eax,8`|加`%`前缀，如`movl $8,%eax`
立即数|原样，如`mov eax,8`|加`$`前缀，如`movl $8,%eax`
16进制立即数|用后缀`b`与`h`分别表示二进制与十六进制，对于16进制字母开头的要加前缀`0`|加前缀`0x`
访问内存长度的表示|前缀`byte ptr`，`word ptr`，`dword ptr`|后缀`b`、`w`、`l`表示字节、字、长型
引用全局或静态变量var的值|[_var]|_var
引用全局或静态变量var的地址|_var|$_var
寄存器间址|[reg]|(%reg)
寄存器变址寻址|[reg + _x]|_x(%reg)
立即数变址寻址|[reg + 1]|1(%reg)
整数数组寻址|[eax*4 + array]|_array (,%eax, 4)
注释|:注释以英文分号开头|#注释以井号开头

本文的书写风格以Intel风格为主。

## 内联汇编
内联汇编（Inline Assembly）是指在C代码中嵌入汇编代码，显然，其语法是由具体的C编译器所决定的，这里主要以GNU中的gcc编译器为例简述其语法。

## 更多
要了解汇编语言更多的知识，可以阅读王爽的[《汇编语言》](https://book.douban.com/subject/25726019/)一书，这本书基于16位的8086CPU来讲解汇编，虽然处理器已过时，但思想永不褪色。

其次，[Linux汇编语言开发指南](https://www.ibm.com/developerworks/cn/linux/l-assembly/index.html)，也是一篇不错的介绍文章。