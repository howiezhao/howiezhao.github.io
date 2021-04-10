---
title: 为什么我不会放弃 Python 投向 Go
categories: Translation
date: 2021-04-10 15:22:25
tags:
---

本文翻译自 <https://uberpython.wordpress.com/2012/09/23/why-im-not-leaving-python-for-go/> ，原文标题为 *Why I’m not leaving Python for Go*，译文如下：

----

首先，Go 似乎是一门很棒的语言。它有一个[很棒的教程](https://tour.golang.org/welcome/1)，我乐此不疲地去看，发现：

- Go 很快。
- 在设计上支持并发。
- 类型化（对 JIT 和 IDE 来说很重要），但不像 C 或 C++ 的[螺旋形](http://c-faq.com/decl/spiral.anderson.html)那样繁琐和丑陋。
- 鸭子类型的接口。
- [延迟（defer）](http://golang.org/doc/effective_go.html#defer)机制真的很精巧。

但是有一个问题我不能接受。这是个遗憾，因为我很想以并发的名义进行信仰的飞跃。这个问题就是**用返回值来进行错误处理**。这简直像 70 年代的风格。

<!-- more -->

### 冗长而重复的错误处理

[go 的设计师认为这是一种优点。](https://blog.golang.org/error-handling-and-go)

> 在 Go 语言中，错误处理非常重要。语言的设计和规范鼓励开发人员显式地检查错误（与其他语言抛出异常然后 catch 住是不同的）。在某些情况下，这会使 Go 代码变得**冗长**，但是幸运的是，可以使用一些技术来减少**重复性**错误处理。

这是我在 C 语言中无法忍受的事情之一。**每一行都需要一个 if 语句**来防止程序做疯狂的事情。这是上述链接中的一个官方的规范示例，或许是“最小的重复性错误处理”：

```go
if err := datastore.Get(c, key, record); err != nil {
    return &appError{err, "Record not found", 404}
}
if err := viewTemplate.Execute(w, record); err != nil {
    return &appError{err, "Can't display record", 500}
}
```

在 Go 中调用函数的正确方法是将其包装在 if 语句中。即使 [Println](http://golang.org/pkg/fmt/#Println) 也会返回一个错误值，我敢肯定，这个星球上的大多数人都不会检查。这让我想到了...

### 错误悄悄忽略 —— 滴答作响的定时炸弹

引用 Tim Peters 的话：

> 错误绝不能悄悄忽略，
> 除非它明确需要如此。

Go 不仅停留在冗长而重复的错误处理上。它还使忽略错误变得容易和诱人。在以下程序中，即使我们未能保护总统（presidential）工作人员，我们也会触发世界末日的装置（trigger the doomsday device）。

```go
func main() {
    http.Get("http://www.nuke.gov/seal_presidential_bunker")
    http.Get("http://www.nuke.gov/trigger_doomsday_device")
}
```

多可惜。哎呀。

从理论上讲，我们可以要求程序员不要忽略返回的错误。通过静态分析或约定。在实践中，仅在最关键的错误编程任务中才能忍受这一痛苦。也许这就是 Go 的目的。

### panic/recover

只要标准库很少使用它们，panic 和 recover 就不够好。为什么一个数组越界比格式字符串损坏或连接中断更容易引起 panic？Go 想完全避免异常，但意识到它们不能 —— 这里和那里都加了几个异常，让我很困惑，不知道哪个错误什么时候发生。

### 或许下次吧

所以我说这句话的时候非常遗憾，因为 Go 有很多惊人的想法和功能，但是如果没有现代的错误处理 —— 我是不会**去**的。

我还在等待那个开源、并发、[左下角的语言](https://web.archive.org/web/20120922025809/http://shootout.alioth.debian.org/u64q/code-used-time-used-shapes.php)出现。有什么建议，欢迎大家多多指教。
