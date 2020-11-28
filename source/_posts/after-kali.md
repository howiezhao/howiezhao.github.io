---
title: 安装 Kali Linux 后要做的 10 件事
categories: Translation
date: 2019-02-25 17:45:28
tags:
  - Kali
---

本文翻译自 <https://null-byte.wonderhowto.com/how-to/top-10-things-do-after-installing-kali-linux-0186450/> ，正文如下：

默认情况下，对于完成日常的渗透测试，[Kali Linux](https://null-byte.wonderhowto.com/how-to/hack-like-pro-getting-started-with-kali-your-new-hacking-system-0151631/) 可能没有你所需的一切。但通过一些提示，技巧和应用程序，我们可以像专业的白帽子一样快速开始使用 Kali。

大多数 Linux 发行版都是高度可定制的。这使得个性化你的渗透测试发行版有点令人生畏。只需几个命令，我们就可以自动执行任务，安装我们喜欢的软件，创建其他用户帐户，正确配置匿名软件，以及优化我们与终端的互动。我们可以采取一些措施来改善与操作系统的交互。
<!--more-->
{% youtube 8VL0K0rFgxw %}

## 1、安装 Git

[Git](https://git-scm.com/) 是一个开源软件版本控制应用程序。它可以用于协作共享和编辑代码，但在 Null Byte 中通常被引用作为复制（或“[克隆](https://www.git-scm.com/docs/git-clone)”）GitHub 上的代码存储库的主要工具。Git 是渗透测试人员必备的工具，他们希望将自己的工具集扩展到默认 Kali 存储库中可用的工具集之外。

可以使用下面的 [apt-get](https://null-byte.wonderhowto.com/how-to/hack-like-pro-linux-basics-for-aspiring-hacker-part-5-installing-new-software-0147591/) 命令安装 Git。

```sh
apt-get install git
```

## 2、配置 Bash 别名

Bash 别名非常适合创建自定义命令行快捷方式。例如，我们可以重新分配 [ls](https://null-byte.wonderhowto.com/how-to/hack-like-pro-linux-basics-for-aspiring-hacker-part-2-creating-directories-files-0147234/) 命令以自动使用我们最喜欢的参数。下面是正常 **ls** 输出的示例。

```sh
ls

 androidbins.txt                                      folder-pictures.png     smtp.cracked         text-x-generic.png
 bogus_gmail.creds                                    folder.png              smtp.list            Windows-10
 dumpzilla-b3075d1960874ce82ea76a5be9f58602afb61c39   package-x-generic.png   text-x-generic.ico  'Windows 10 Icons'
```

在创建 **ls** 别名后再次输出的示例。

```sh
ls

total 220K
-rw-------  1 root root  15K Aug 24  2015  folder-pictures.png
-rw-------  1 root root 8.7K Aug 24  2015  folder.png
-rw-------  1 root root  11K Aug 24  2015  package-x-generic.png
-rw-------  1 root root 5.5K Sep  3  2015  text-x-generic.png
drwxr-xr-x 12 root root 4.0K May 31 00:44 'Windows 10 Icons'/
drwxr-xr-x 18 root root 4.0K May 31 00:44  Windows-10/
-rwxr-x---  1 root root 103K May 31 00:49  text-x-generic.ico*
drwxr-xr-x  5 root root 4.0K Jun 11 21:57  dumpzilla-b3075d1960874ce82ea76a5be9f58602afb61c39/
-rw-r--r--  1 root root   52 Jul  5 18:13  bogus_gmail.creds
-rw-r--r--  1 root root  15K Jul  5 18:28  smtp.list
-rw-r--r--  1 root root  181 Jul  5 18:43  smtp.cracked
-rw-r--r--  1 root root  23K Jul 23 18:18  androidbins.txt
drwxr-xr-x  5 root root 4.0K Jul 23 19:22  ./
drwxr-xr-x 23 root root 4.0K Aug  9 04:25  ../
```

我们得到了更详细的输出。**ls** 命令现在自动使用 **-l**，**-a**，**-t**，**-h** 和 **-r** 参数。所有这些参数都将指示 **ls** 使用列表（**-l**）格式，列出所有（**-a**）文件 —— 包括隐藏文件 —— 并以人类可读（**-h**）的格式打印文件大小（例如，1K，234M，5G）。

我的别名还将按修改时间（**-t**）对输出进行排序，并反转（**-r**）列表的顺序，以便最近修改的文件出现在终端的底部。这个参数集合是我个人的 **ls** 偏好，但你的可能会有所不同。

要创建别名，请使用 **nano** 或你喜欢的文本编辑器打开 `/root/.bash_aliases`。添加以下行以创建别名。

- 不要错过：[Vim 简介，每个黑客都应该知道的 Unix 文本编辑器](https://null-byte.wonderhowto.com/how-to/intro-vim-unix-text-editor-every-hacker-should-be-familiar-with-0174674/)

```sh
alias ls='ls --color=always -rthla'
```

我们还可以进一步向 `.bash_aliases` 文件添加更复杂的函数。下面是一个简单的函数示例，旨在使 Kali 保持最新状态。

```sh
function apt-updater {
    apt-get update &&
    apt-get dist-upgrade -Vy &&
    apt-get autoremove -y &&
    apt-get autoclean &&
    apt-get clean &&
    reboot
    }
```

保存对 `.bash_aliases` 文件所做的更改后，打开一个新终端以使更改生效。运行新创建的 **apt-updater** 函数将调用一系列 **apt-get** 命令，这些命令将自动更新和维护你的系统。如果先前的命令失败，＆ 符号（**&&**）确保该函数不会继续执行以下命令。

```sh
apt-updater
```

有关 Bash 别名的更多信息，请查看 Kody 的“[为 Wi-Fi 数据包捕获设置 MacOS 系统](https://null-byte.wonderhowto.com/how-to/mac-for-hackers-set-up-macos-system-for-wi-fi-packet-capturing-0186354/)”一文。

## 3、创建一个新的低权限用户

许多应用程序（如 Chromium 浏览器和 Tor 浏览器）都不应该以 root 用户身份打开或使用。此类应用程序在很大程度上依赖于低级别权限来提供某种程度的安全性。某些用户为这些活动创建低特权用户帐户可能是有益的。

Takhion 的“[锁定 Kali Linux 以用于安全桌面使用](https://null-byte.wonderhowto.com/how-to/install-lock-down-kali-linux-for-safe-desktop-use-0184531/#jump-step2)”一文中详细介绍了这一概念，因此请务必查看帮助。

## 4、安装一个终端复用器

复用器是一种平铺终端仿真器，允许我们在一个窗口内打开多个终端会话。这样做的主要好处是能够立即看到我们所有打开的终端会话，而不是将窗口叠加在一起。以下是复用器示例。

![复用器](https://img.wonderhowto.com/img/10/19/63669458451029/0/top-10-things-do-after-installing-kali-linux.w1456.jpg)

有许多值得注意的复用器。如上面的屏幕截图所示，[Tilix](https://github.com/gnunn1/tilix) 是一个开源且可靠的选项。替代方案包括 [tmux](https://github.com/tmux/tmux/) 和 [screen](https://savannah.gnu.org/projects/screen)。

Tilix 可在 Kali 的 APT 存储库中使用，可以使用以下命令进行安装。

```sh
apt-get install tilix

Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  libgtkd-3-0 libphobos2-ldc-shared78 libvted-3-0 tilix-common
Suggested packages:
  python-nautilus
The following NEW packages will be installed:
  libgtkd-3-0 libphobos2-ldc-shared78 libvted-3-0 tilix tilix-common
0 upgraded, 5 newly installed, 0 to remove and 466 not upgraded.
Need to get 10.7 MB of archives.
After this operation, 49.1 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
```

亚马逊推荐：[William E. Shotts Jr. 撰写的“Linux命令行大全”](https://www.amazon.cn/dp/B00BQTWC0U)

## 5、安装你喜爱的黑客工具

某些版本的 Kali 面向极简主义的渗透测试者，他们不希望预先安装数百个黑客工具。这意味着我们必须手动安装我们喜欢的工具。我们使用的工具类型根据我们的技能和专业领域而有所不同，但以下是一些流行的黑客工具。

- [Aircrack-ng](https://www.aircrack-ng.org/)：无线 [WEP/WPA 破解实用程序](https://null-byte.wonderhowto.com/how-to/hack-wi-fi-getting-started-with-aircrack-ng-suite-wi-fi-hacking-tools-0147893/)。
- [BeEF](https://beefproject.com/)：通过 Web 应用程序的浏览器[漏洞利用框架](https://null-byte.wonderhowto.com/how-to/hack-like-pro-hack-web-browsers-with-beef-0159961/)。
- [Burp Suite](https://portswigger.net/burp/)：专为 [Web 应用程序安全性](https://null-byte.wonderhowto.com/how-to/hack-like-pro-hack-web-apps-part-4-hacking-form-authentication-with-burp-suite-0163642/)而设计的图形应用。
- [Hydra](https://github.com/vanhauser-thc/thc-hydra)：登录[密码暴力破解](https://null-byte.wonderhowto.com/how-to/hack-like-pro-crack-online-web-form-passwords-with-thc-hydra-burp-suite-0160643/)实用程序。
- [Nikto](https://cirt.net/Nikto2)：Web [服务器安全扫描器](https://null-byte.wonderhowto.com/how-to/hack-like-pro-find-vulnerabilities-for-any-website-using-nikto-0151729/)。
- [Maltego](https://www.paterva.com/web7/)：开源取证和情报收集。
- [Nmap](https://nmap.org/)：端口扫描器和[网络映射器](https://null-byte.wonderhowto.com/how-to/hack-like-pro-advanced-nmap-for-reconnaissance-0151619/)。
- [Wireshark](https://www.wireshark.org/download.html)：用于[网络流量分析](https://null-byte.wonderhowto.com/news/8-wireshark-filters-every-wiretapper-uses-spy-web-conversations-and-surfing-habits-0134508/)的图形应用程序。

可以使用以下命令安装这些工具。

```sh
apt-get install maltego metasploit-framework burpsuite wireshark aircrack-ng hydra nmap beef-xss nikto

Reading package lists... Done
Building dependency tree
Reading state information... Done
hydra is already the newest version (8.6-1kali1).

The following NEW packages will be installed:
  beef-xss binfmt-support burpsuite fastjar fonts-droid-fallback fonts-lato
  fonts-noto-mono ghostscript gsfonts imagemagick imagemagick-6-common
  imagemagick-6.q16 jarwrapper java-wrappers javascript-common libc-ares2
  libcupsfilters1 libcupsimage2 libdjvulibre-text libdjvulibre21 libdouble-conversion1
  libfftw3-double3 libgmp-dev libgmpxx4ldbl libgs9 libgs9-common libhttp-parser2.8
  libijs-0.35 libilmbase23 libjbig2dec0 libjs-jquery libjs-jquery-easing
  libjs-jquery-fancybox libjs-jquery-mousewheel libjs-jquery-ui libjs-source-map
  libjs-uglify libjxr-tools libjxr0 liblqr-1-0 liblua5.2-0 libmagickcore-6.q16-6
  libmagickcore-6.q16-6-extra libmagickwand-6.q16-6 libnetpbm10 libnl-route-3-200
  libopenexr23 libpaper-utils libpaper1 libpcre2-16-0 libqt5core5a libqt5dbus5
  libqt5gui5 libqt5multimedia5 libqt5multimedia5-plugins libqt5multimediagsttools5
  libqt5multimediawidgets5 libqt5network5 libqt5opengl5 libqt5printsupport5 libqt5svg5
  libqt5widgets5 libruby2.5 libsbc1 libsmi2ldbl libspandsp2 libssh-gcrypt-4 libuv1
  libwhisker2-perl libwireshark-data libwireshark11 libwiretap8 libwmf0.2-7
  libwscodecs2 libwsutil9 libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-randr0
  libxcb-render-util0 libxcb-xinerama0 libxcb-xkb1 libxkbcommon-x11-0 libyaml-0-2
  maltego netpbm nikto nodejs nodejs-doc openjdk-8-jre openjdk-8-jre-headless
  qt5-gtk-platformtheme qttranslations5-l10n rake ruby ruby-addressable ruby-ansi
  ruby-atomic ruby-buftok ruby-celluloid ruby-celluloid-io ruby-daemons
  ruby-dataobjects ruby-dataobjects-mysql ruby-dataobjects-postgres
  ruby-dataobjects-sqlite3 ruby-dev ruby-did-you-mean ruby-diff-lcs ruby-dm-core
  ruby-dm-do-adapter ruby-dm-migrations ruby-dm-serializer ruby-dm-sqlite-adapter
  ruby-docile ruby-domain-name ruby-em-websocket ruby-equalizer ruby-erubis
  ruby-eventmachine ruby-execjs ruby-faraday ruby-geoip ruby-hitimes ruby-http
  ruby-http-cookie ruby-http-form-data ruby-http-parser.rb ruby-json ruby-librex
  ruby-libv8 ruby-memoizable ruby-mime-types ruby-mime-types-data ruby-minitest
  ruby-mojo-magick ruby-msfrpc-client ruby-msgpack ruby-multi-json ruby-multipart-post
  ruby-naught ruby-net-telnet ruby-nio4r ruby-oj ruby-parseconfig ruby-power-assert
  ruby-public-suffix ruby-qr4r ruby-rack ruby-rack-protection ruby-ref ruby-rqrcode
  ruby-rspec-expectations ruby-rspec-support ruby-rubydns ruby-simple-oauth
  ruby-simplecov ruby-simplecov-html ruby-sinatra ruby-sqlite3 ruby-term-ansicolor
  ruby-test-unit ruby-therubyracer ruby-thread-safe ruby-tilt ruby-timers ruby-tins
  ruby-twitter ruby-uglifier ruby-unf ruby-unf-ext ruby-xmlrpc ruby-zip ruby2.5
  ruby2.5-dev ruby2.5-doc rubygems-integration thin wireshark wireshark-common
  wireshark-qt zip
The following packages will be upgraded:
  aircrack-ng libcups2 libnl-3-200 libnl-genl-3-200 libxkbcommon0 metasploit-framework
  nmap nmap-common
8 upgraded, 182 newly installed, 0 to remove and 458 not upgraded.
Need to get 381 MB of archives.
After this operation, 616 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
```

## 6、安装最新版本的 Tor

Tor 可以在 Kali 的存储库中使用，但匿名软件应该直接从源代码获取（torproject.org）。此外，Kali 的 Tor 版本无法可靠地维护或更新。这意味着我们可能会缺少关键的稳定性和安全性更新。

将 Tor 项目存储库添加到 APT 存储库列表中。

```sh
echo 'deb https://deb.torproject.org/torproject.org stretch main
deb-src https://deb.torproject.org/torproject.org stretch main' > /etc/apt/sources.list.d/tor.list
```

然后，下载 [Tor Project 包签名密钥](https://www.torproject.org/docs/debian.html.en)并将其导入 APT 密钥环。

```sh
wget -O- https://deb.torproject.org/torproject.org/A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89.asc | sudo apt-key add -

--2019-02-18 19:28:23--  https://deb.torproject.org/torproject.org/A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89.asc
Resolving deb.torproject.org (deb.torproject.org)... 138.201.14.197
Connecting to deb.torproject.org (deb.torproject.org)|138.201.14.197|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 19665 (19K) [text/plain]
Saving to: ‘STDOUT’

-                                              100%[=================================================================================================>]  19.20K  47.5KB/s    in 0.4s

2019-02-18 19:28:25 (47.5 KB/s) - written to stdout [19665/19665]

OK
```

将签名密钥添加到密钥环后，您将看到“OK”输出。接下来，使用以下 apt-get 命令更新 APT。

```sh
apt-get update

Hit:1 http://downloads.metasploit.com/data/releases/metasploit-framework/apt lucid InRelease
Get:2 https://deb.torproject.org/torproject.org stretch InRelease [4,965 B]
Get:4 https://deb.torproject.org/torproject.org stretch/main Sources [1,169 B]
Get:5 https://deb.torproject.org/torproject.org stretch/main amd64 Packages [2,400 B]
Hit:3 http://archive-3.kali.org/kali kali-rolling InRelease
Fetched 8,534 B in 8s (1,091 B/s)
Reading package lists... Done
```

使用以下命令安装 Tor，你就完成了。

```sh
apt-get install tor deb.torproject.org-keyring

Reading package lists... Done
Building dependency tree
Reading state information... Done
Suggested packages:
  mixmaster torbrowser-launcher socat tor-arm apparmor-utils obfs4proxy
The following NEW packages will be installed:
  deb.torproject.org-keyring
The following packages will be upgraded:
  tor
```

## 7、使用 Syncthing 配置文件共享

由 [Jakob Borg](https://twitter.com/jakobborg) 创建的 [Syncthing](https://github.com/syncthing/syncthing) 是一种[跨平台](https://github.com/syncthing/syncthing/releases/)，私有，轻量级文件同步（Dropbox）替代方案。作为渗透测试人员，在 [VPS](https://null-byte.wonderhowto.com/how-to/white-hats-guide-choosing-virtual-private-server-0183135/) 和本地 Kali 机器之间传输按键日志，屏幕截图，网络摄像头录像和[敏感的战利品文件](https://null-byte.wonderhowto.com/how-to/hacking-windows-10-capture-exfiltrate-screenshots-remotely-0183646/#jump-step4)可能是一项令人沮丧的任务。Syncthing 使安全的文件共享完全无痛。

我在前一篇文章中介绍了 [Syncthing 的安装和配置](https://null-byte.wonderhowto.com/how-to/securely-sync-files-between-two-machines-using-syncthing-0185999/)。读者应参考该详细的分步指南。

## 8、安装代码编辑器

[Atom](https://atom.io/) 是一个免费的，开源的，功能丰富且高度可定制的文本编辑器。其功能包括实时协作共享代码，直观的编码自动补全功能，以及[安装软件包](https://atom.io/packages)的能力，这些都进一步增强了 Atom 的多功能性。其他值得注意的文本编辑包括 [Geany](https://wiki.geany.org/doku.php) 和 [Gedit](https://wiki.gnome.org/Apps/Gedit)。

要安装 Atom，请访问他们的网站并下载最新的 [Debian 安装程序](https://atom.io/download/deb)。接下来，使用下面的 apt-get 命令打开终端并安装所需的依赖项。

```sh
apt-get install gvfs gvfs-common gvfs-daemons gvfs-libs gconf-service gconf2 gconf2-common gvfs-bin psmisc

Reading package lists... Done
Building dependency tree
Reading state information... Done
Correcting dependencies... Done
The following NEW packages will be installed:
   gconf-service (3.2.6-4.1)
   gconf2 (3.2.6-4.1)
   gconf2-common (3.2.6-4.1)
   gvfs-bin (1.36.2-1)
   libgconf-2-4 (3.2.6-4.1)
   psmisc (23.1-1+b1)
The following packages will be upgraded:
   gvfs (1.36.1-1 => 1.36.2-1)
   gvfs-common (1.36.1-1 => 1.36.2-1)
   gvfs-daemons (1.36.1-1 => 1.36.2-1)
   gvfs-libs (1.36.1-1 => 1.36.2-1)
4 upgraded, 6 newly installed, 0 to remove and 462 not upgraded.
1 not fully installed or removed.
Need to get 3,317 kB of archives.
After this operation, 8,909 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
```

最后，使用命令行包管理器 **dpkg** 和 install（**-i**）参数。

```sh
dpkg -i ~/Downloads/atom-amd64.deb

(Reading database ... 191882 files and directories currently installed.)
Preparing to unpack atom-amd64.deb ...
Unpacking atom (1.29.0) over (1.29.0) ...
Setting up atom (1.29.0) ...
Processing triggers for desktop-file-utils (0.23-3) ...
Processing triggers for mime-support (3.60) ...
```

完成后，Atom 将显示在“应用程序”菜单中。

![Atom](https://img.wonderhowto.com/img/original/05/68/63669459068404/0/636694590684040568.jpg)

## 9、克隆橡皮鸭（Rubber Ducky）编码器

USB 橡皮鸭是臭名昭著的按键注入工具。利用 [DuckToolKit 网站](https://ducktoolkit.com/)可以很容易地创建 [ducky payloads](https://null-byte.wonderhowto.com/how-to/use-usb-rubber-ducky-disable-antivirus-software-install-ransomware-0180418/#jump-step2)，但作为一个渗透测试人员，与随机网站共享客户信息是不安全的。将有效载荷内容上载到第三方网站可能很危险。

相反，我们可以使用 **Git** 克隆 USB 橡皮鸭[存储库](https://github.com/hak5darren/USB-Rubber-Ducky)并在本地编码有效载荷。

```sh
git clone https://github.com/hak5darren/USB-Rubber-Ducky

Cloning into 'USB-Rubber-Ducky'...
remote: Counting objects: 1657, done.
remote: Total 1657 (delta 0), reused 0 (delta 0), pack-reused 1657
Receiving objects: 100% (1657/1657), 31.88 MiB | 162.00 KiB/s, done.
Resolving deltas: 100% (745/745), done.
Checking out files: 100% (1509/1509), done.
```

然后，将当前目录更改（[cd](https://null-byte.wonderhowto.com/how-to/hack-like-pro-linux-basics-for-aspiring-hacker-part-2-creating-directories-files-0147234/)）为 `USB-Rubber-Ducky/Encoder/` 目录，并使用以下 **java** 命令开始编码没有第三方网站的 [ducky payloads](https://www.hak5.org/gear/duck/writing-your-first-usb-rubber-ducky-payload)。

```sh
cd USB-Rubber-Ducky/Encoder/
java -jar encoder.jar -i input_payload.txt -o inject.bin
```

## 10、更改 SSH 密钥和默认密码

每个 Kali Linux 安装的默认密码都是相同的（toor），这使得自动化攻击非常容易。此外，当你通过 SSH 控制树莓派之类的东西时，默认的 SSH 密钥可以允许攻击者拦截你的通信。

要更改 SSH 密钥，请首先切换目录。执行以下两个命令将重置 SSH 密钥的默认值。

```sh
cd /etc/ssh/
dpkg-reconfigure openssh-server

rescue-ssh.target is a disabled or a static unit, not starting it.
```

现在，对于你的 Kali 系统密码，输入 **passwd root**，然后输入你的新密码。然后，重新输入以确认。如果你未以 root 用户身份登录，则可能会在执行此操作之前询问你当前的密码。

```sh
passwd root

Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

## 安装 Kali 后你做的第一件事是什么？

我们都有不同程度的兴趣，技能和经验水平。这使得编写完整的安装后步骤列表变得棘手。我错过了任何关键步骤吗？你如何个性化和定制新安装的Kali？请务必在下面发表评论。
