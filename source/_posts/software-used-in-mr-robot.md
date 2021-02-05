---
title: 《黑客军团》中使用的软件
date: 2018-09-18 12:23:55
categories: Translation
tags:
---

本文翻译自 <https://alternativeto.net/list/66/software-used-in-mr-robot> ，正文如下：

![首页图片](https://p0.ssl.qhimg.com/t01708531e12a86f171.jpg)
本文盘点了获得艾美奖和金球奖剧情/惊悚系列电视剧——《黑客军团》中黑客使用的软件。
**下面的列表包含到了第二季第11集！**
<!--more-->

## [Kali Linux](https://www.kali.org/)

Kali Linux是针对安全研究人员进行渗透测试的Linux发行版，但同时也被黑客使用，因为它集成了很多黑客工具。由于它是黑客的首选操作系统，所以它在《黑客军团》中经常有过出现。

## [Wickr](https://wickr.com/)

Wickr是一个端到端的加密聊天应用程序，具有诸如消息可调到期时间等功能。在第二季中，fsociety组织使用它来保密通信。

## [Tor Browser](https://www.torproject.org/projects/torbrowser.html)

Tor浏览器被广泛认为是最好的匿名工具。它将使你的互联网活动难以被追踪，当第二季第8集中fsociety的成员Trenton用Tor浏览器向Vimeo上传一个泄露的关于非法群体监视的FBI电话会议时，利用到了它。

## [Raspberry Pi](https://www.raspberrypi.org/)

树莓派是一个小型的，可编程的计算机板，旨在教孩子们学习计算机科学。由于它的低成本，多功能性和简单性，它也是业余爱好者和程序员的最爱。第一季第5集中Elliot将一个树莓派安装到铁山的气候控制系统中，以便fsociety后期可以远程升高存储E公司磁带备份的存储空间的温度，从而实现美国消费者债务的很大一部分记录的备份被销毁。

## [FileZilla](https://filezilla-project.org/)

FileZilla是世界上最流行的FTP客户端，并且是最强大和用户友好的客户端之一。在第一季第4集中Trenton使用FileZilla上传一个漏洞利用程序到fsociety的FTP服务器上，即Elliot将安装在铁山的气候控制系统中的树莓派，以销毁美国消费者债务中很大一部分的记录。

## [Pwnix](https://www.pwnieexpress.com/mobile-line-shift-to-aopp)

Pwnix是一个为渗透测试人员定制的用于网络黑客和安全的Android ROM。Elliot在第二季第9集中使用了一个Pwnie Express Pwn Phone（Pwnix预装），以至于他和Darlene渗透进黑暗军团的电话。

## [DeepSound](http://jpinsoft.net/deepsound)

在第一季第8集中，Elliot使用DeepSound将文件隐藏在CD的常规音乐曲目中，以便隐藏文件只能使用DeepSound软件查看。这是一种被称为隐写术的技术。

## [ProtonMail](https://protonmail.com/)

ProtonMail是一个安全的端到端加密电子邮件服务，基于瑞士，Elliot在第一季第8集中使用过。《黑客军团》背后的团队研究安全电子邮件服务的程度很深，以至于他们实际上联系了ProtonMail开发者，询问用户是否有可能在ProtonMail中监控他们自己的电子邮件活动。ProtonMail开发者非常喜欢帐户访问日志的想法，他们最终在ProtonMail的v2.0版本中实现了这个功能。想要了解更多请访问：<https://protonmail.com/blog/protonmail-mr-robot-secure-email/>

## [HDShredder](https://www.miray-software.com/products/applications/hdshredder.html#)

HDShredder 4企业版在第一季第10集中用于在E公司被黑之后安全地擦除所有fsociety的硬盘信息，然后他们在狗狗火葬场焚烧所有的硬盘。

## [John the Ripper](https://www.openwall.com/john/)

John the Ripper是Kali Linux中包含的一个密码破解工具，用于检测简单的Unix密码，并试图通过每秒数千次的猜测来破解它们。这被称为暴力破解，Elliot在第一季第2集中通过使用它来破解E公司的临时首席技术官Tyrell Wellick的邮箱密码。

## [Wegt](https://www.gnu.org/software/wget/)

Wget是一个命令行工具，可以发出HTTP(S)请求。在《黑客军团》中它被用于与John the Ripper结合使用Shellshock漏洞来攻击E公司的邮件服务器。

## [Social-Engineer Toolkit](https://github.com/trustedsec/social-engineer-toolkit)

SET是一个专注于诸如网络钓鱼等社会工程攻击的测试框架。社会工程学欺骗受害者给予攻击者敏感信息。在第一季第5集中，Mobley使用SET的伪造短信功能让主管离开铁山，以便Elliot可以渗透进去。

## [OpenWrt](https://openwrt.org/)

OpenWrt是Angela在第二季第6集中黑进FBI时使用的路由器固件。

## [mimikatz](https://github.com/gentilkiwi/mimikatz)

mimikatz是一个后渗透工具，它将黑客可能需要执行的一些有用任务捆绑在一起。在第二季第6集中，它被装在USB橡皮鸭中并交给Angela，作为一个备份计划。

## [btscanner](https://www.pentest.co.uk/downloads.html)

btscanner是一个包含在Kali Linux中的工具，它可以在无需配对的情况下提取关于蓝牙设备的尽可能多的信息。在第一季第6集中，Elliot使用btscanner与Bluesniff和Metasploit结合，通过MultiBlue蓝牙USB加密狗连接到附近警车中的电脑，并渗透进监狱的网络，以帮助一个名叫Vera的毒贩越狱。

## [Bluesniff](http://bluesniff.shmoo.com/)

Bluesniff是一款蓝牙设备发现工具。在第一季第6集中，Elliot使用Bluesniff与Metasploit和btscanner结合，通过MultiBlue蓝牙USB加密狗连接到附近警车中的电脑，并渗透进监狱的网络，以帮助一个名叫Vera的毒贩越狱。

## [KVM(Kernel-base Virtual Machine)](http://www.linux-kvm.org/page/Main_Page)

KVM是一个管理程序，它是一个可以通过虚拟机运行其他操作系统的软件。Elliot使用KVM在Kali Linux内虚拟化Windows 7。在第一季第8集中，它使用KVM运行DeepSound。

## [Metasploit](https://metasploit.com/)

Metasploit框架是Kali Linux中包含的一个软件，可以使渗透测试人员更容易发现网络中的漏洞。Meterpreter是可以在Metasploit框架中运行的数百个Payload之一，并且在第一季第6集中使用到。在第一季第6集中，Elliot使用Metasploit Framwork和Metapreter与btscanner和Bluesniff结合，通过MultiBlue蓝牙USB加密狗连接到附近警车中的电脑，并渗透进监狱的网络，以帮助一个名叫Vera的毒贩越狱。

## [Framaroot](https://forum.xda-developers.com/apps/framaroot/root-framaroot-one-click-apk-to-root-t2130276)

在电视中称为RooterFrame的Framaroot，在第一季第3集中被Tyrell Wellick用来Root同事的Android手机，这样他就可以隐藏在手机上安装的FlexiSPY间谍软件，以便获得关于谁将成为E公司的下一任首席技术官的秘密信息。

## [Kingo Root](https://zh.kingoapp.com/)

Tyrell Wellick在第一季第3集中使用Kingo Root来Root同事的Android手机，这样他就可以在手机上隐蔽地安装FlexiSPY间谍软件，以便获得有关谁将成为下一任E公司首席执行官的秘密信息。

## [FlexiSPY](https://www.flexispy.com/zh/)

FlexiSPY是针对Android，iOS和BlackBerry的间谍软件，允许用户监控受害者手机上的所有活动。在第一季第3集中，Tyrell Wellick秘密地将其安装在同事的Android手机上，以获取有关谁将成为下一任E公司首席技术官的秘密信息。

## [SuperSU](http://www.supersu.com/)

SuperSU是一个在已Root的Android手机上管理超级用户权限的应用程序。在第一季第3集中，Tyrell Wellick在同事的Android手机上秘密安装了FlexiSPY —— 它使用SuperSU为它自己提供超级用户访问 —— 以便获得有关谁将成为下一任E公司首席技术官的秘密信息。

## [can-utils](https://packages.debian.org/sid/can-utils)

can-utils包含与汽车电脑有关的实用程序。其中一个工具被称为candump，它在《黑客军团》中被用于入侵汽车的电脑。

## [radare](https://www.radare.org/r/)

radare2是Tyrell Wellick在第二季第12集中使用的逆向工程框架。

## [PyCharm](https://www.jetbrains.com/pycharm/)

PyCharm是一个Python和Django的IDE（集成开发环境），它是一种代码编辑软件。Trenton在第一季第四集中使用它。

## [Tor](https://www.torproject.org/)

Tor被广泛认为是最好的匿名工具。它将使你的互联网活动难以被追踪，这个版本 —— 不像Tor浏览器 —— 可以用来托管隐藏服务，这是只能通过Tor访问的站点，并且其物理服务器位置被Tor匿名网络隐藏。Ray通过Tor隐藏服务运行着一条“丝绸之路”，他希望Elliot在第二季第5集中进行网站迁移。

## [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/)

PuTTY是用于连接到Linux服务器的客户端。Elliot在第二季第4集和第5集使用PuTTY连接到运行Kali Linux的VPS（虚拟专用服务器），以便他可以在Ray的计算机上使用安装在VPS上的IRC客户端与Darlene聊天。他还在第二季第5集中使用PuTTY，完成了Ray的“丝绸之路”网站的迁移。

## [Mozilla Firefox](https://www.mozilla.org/zh-CN/firefox/)

Elliot使用Firefox作为他的默认浏览器。Trenton在第二季第8集中使用了Firefox。

## [FFmpeg](https://ffmpeg.org/)

在第二季第8集中Trenton使用FFmpeg编码一个视频，其中包含一个泄露的关于进行非法大规模监视的FBI电话会议，并通过Tor浏览器向Vimeo上传。

## [Slackware](http://www.slackware.com/)

Slackware是1993年创建的一个Linux发行版，旨在提高设计的稳定性和简单性，并成为最“类Unix”的Linux发行版。Slackware最初是基于Softlanding Linux系统的，它已经成为许多其他Linux发行版的基础，尤其是SUSE Linux发行版的第一个版本，也是最早的发行版本。在第二季第10集中，当Elliot与黑暗军队达成拯救Darlene生命的交易时，Leon给了他一台安装有Slackware的笔记本电脑，用于将黑暗军队的项目移动到刚果。

## [VLC Media Player](https://www.videolan.org/vlc/)

VLC媒体播放器被用于第二季第4集，当时Elliot和Darlene一起观看了虚假恐怖片《Careful Massacre of the Bourgeoisie》的VHS版本。VLC也被用于第二季第8集，当fsociety预览一个他们将上传的关于非法大规模监视的泄露的FBI电话会议视频时。

## [Wayback Machine](http://web.archive.org/)

由Internet Archive运营的Waybach Machine是一个包含超过4,900亿个网页副本的数据库。在第二季第8集中FBI特工Dominique DiPierro向Mobley透露，联邦调查局使用了Wayback Machine，以便将他的黑客把柄与他为DJ Mobley创建的旧的粉丝页面联系起来。

## [µTorrent](https://www.utorrent.com/intl/zh_cn/utweb-index)

第二季第4集达琳用μTorrent下载了虚假恐怖电影《Careful Massacre of the Bourgeoisie》的VHS版本。
