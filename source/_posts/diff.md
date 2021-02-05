---
title: 如何比较两个文件之间的差异
date: 2018-10-19 14:05:51
categories: CheatSheet
tags:
  - Linux
---

## Windows

在Windows下，可以使用系统自带的`fc`命令（即file compare的缩写），比如`fc game_old.js game_new.js`，结果如下：

```text
正在比较文件 game_old.js 和 GAME_NEW.JS
***** game_old.js
KEY_CODES = {
  32: 'space',
***** GAME_NEW.JS
KEY_CODES = {
  13: 'enter',
  32: 'space',
*****

***** game_old.js
  37: 'left',
  38: 'up',
  39: 'right',
***** GAME_NEW.JS
  37: 'left',
  39: 'right',
*****

***** game_old.js

    if (KEY_STATUS.up) {
      var rad = ((this.rot-90) * Math.PI)/180;
***** GAME_NEW.JS

    if (KEY_STATUS.spacr) {
      var rad = ((this.rot-90) * Math.PI)/180;
*****
```

可见，`fc`命令会把两个文件中不同的片段显示出来，并分别标注属于哪个文件。输入`fc /?`可以查看`fc`命令的更多参数。
<!--more-->
## Linux

在Linux下，可以使用系统自带的`diff`命令（即difference的缩写），它要比Windows中的`fc`命令更为强大，比如`diff -u game_old.js game_new.js`，其中`-u`参数表示使用标准区别格式，这将使输出内容更容易阅读，结果如下：

```diff
--- game_old.js 2018-10-19 11:31:58.054834600 +0800
+++ game_new.js 2018-10-19 11:32:19.667759500 +0800
@@ -4,9 +4,9 @@
 //

 KEY_CODES = {
+  13: 'enter',
   32: 'space',
   37: 'left',
-  38: 'up',
   39: 'right',
   40: 'down',
   70: 'f',
@@ -392,7 +392,7 @@
       this.vel.rot = 0;
     }

-    if (KEY_STATUS.up) {
+    if (KEY_STATUS.spacr) {
       var rad = ((this.rot-90) * Math.PI)/180;
       this.acc.x = 0.5 * Math.cos(rad);
       this.acc.y = 0.5 * Math.sin(rad);
```

可见，`diff`命令的输出结果更加丰富，开始它展示了正在比较的2个文件，紧接着它显示了不同之处，其中`-`开始的段落代表只存在于前一个文件中，不存在于后一个文件中，同理，`+`开始的段落代表只存在于后一个文件中，不存在于前一个文件中，除此之外的所有段落代表共同存在于2个文件中。一般而言，我们将前一个文件表示为旧文件，后一个文件表示为新文件。输入`diff --help`可以查看`diff`命令的更多参数。

## 图形化程序

或许使用像前面所述的命令行程序观察结果不是很方便，因此有些人可能会倾向于使用图形化程序，而[Meld](http://meldmerge.org/)就是个不错的选择，它开源且跨平台，可用来可视化的观察文件之间的差异。使用Meld比较两文件差异的结果如下：![Meld结果](/images/meld.PNG)可见，Meld用高亮显示文件之间的差异，同时它还提供了前往上一个/下一个差异的按钮，方便用户快速跳转。
