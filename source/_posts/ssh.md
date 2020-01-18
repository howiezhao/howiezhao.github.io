---
title: SSH协议分析
date: 2018-08-24 19:44:35
categories: CheatSheet
tags:
  - 计算机网络
---
SSH(Secure Shell)即**安全外壳协议**，是一种位于应用层的加密的网络传输协议，虽然任何网络服务都可以通过SSH实现安全传输，但其最常见的用途还是远程登录，是Telnet等非安全Shell的替代品。

## OpenSSH的运行机制
SSH是一种协议，其实现多种多样，目前使用最广泛的实现是OpenSSH项目。当使用`ssh user@host`命令进行登录时，所完成的整个过程如下：
1. 远程主机收到用户的登录请求，把自己的公钥发给用户
2. 用户使用这个公钥，将登录密码加密后，发送给远程主机
3. 远程主机用自己的私钥，解密登录密码，若密码正确，则同意用户登录
4. 后续过程中，用户发送的信息都采用此方式进行加密发送
<!--more-->
因为不像HTTPS协议，SSH协议的公钥是没有证书中心(CA)公证的，所以为了防止中间人攻击，当用户第一次登录远程主机时，系统会提示如下信息：
```bash
The authenticity of host 'host (12.18.429.21)' can't be established.
RSA key fingerprint is 98:2e:d7:e0:de:9f:ac:67:28:c2:42:2d:37:16:58:4d.
Are you sure you want to continue connecting (yes/no)?
```
即系统无法确认远程主机的真实性(远程主机有可能是中间人)，只知道远程主机的公钥指纹，询问用户是否继续连接。公钥指纹就是对公钥进行哈希计算得到的，为了方便用户的比较。用户并没有什么好的办法得知自己想要连接的真实远程主机的公钥指纹，一个可行的办法是远程主机在其官方网站上贴出自己的公钥指纹，方便用户和系统提示的指纹进行比较。

假定当用户进行风险衡量后决定继续连接，接下来的过程就如上述提到的一样。远程主机的公钥会被保存在`$HOME/.ssh/known_hosts`文件中，当用户下次再连接时，系统就会认出它的公钥已经保存在本地了，从而跳过警告部分，直接提示输入密码。

除了采用口令登录外，还可使用**公钥登录**，原理为：用户将自己的公钥储存在远程主机上，登录时，远程主机会向用户发送一段随机字符串，用户用自己的私钥加密后，再发回来，远程主机用事先储存的公钥进行解密，如果成功，就证明用户是可信的，直接允许登录shell，不再要求密码。

OpenSSH提供了一个工具 —— `ssh-keygen`，使用它可以方便的生成一对公私钥，生成的公钥为`id_rsa.pub`，私钥为`id_rsa`，保存在`$HOME/.ssh`目录下，当然你可以使用`-t`（type）参数指定密钥的类型（默认生成类型为RSA），使用`-f`（file）参数指定生成的目录文件名，使用`-C`（Comment）参数指定注释，更多的参数可以使用`--help`参数查看。

生成的公钥格式为`<protocol> <key-blob> <comment>`，其中注释项通常用来指代要登录的用户名。

有了密钥对后，可以使用`ssh-copy-id user@host`命令将自己的公钥上传至远程主机，远程主机会将用户的公钥，保存在登录后的用户主目录的`$HOME/.ssh/authorized_keys`文件中。实际上，`ssh-copy-id`命令的整个过程就如下命令一样：
```bash
ssh user@host 'mkdir -p .ssh && cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
```
实际上，`ssh-copy-id`还会对创建的文件及文件夹进行相关的权限设置，这里不过多介绍。

最后还要对远程主机的SSH服务端配置文件，即`/etc/ssh/sshd_config`文件进行相关配置，并重启SSH服务即可生效。具体而言，涉及到的配置项如下：
```
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```
紧接着使用`service sshd restart`重启SSH服务。

## 快速登录
`$HOME/.ssh`目录下的`config`文件可配置快速登录选项，若没有，可以新建一个，具体而言，如下：
```
host aliyun
    user howie
    hostname 192.168.0.41
    port 22
    identityfile ~/.ssh/id_rsa
```
这代表当输入`ssh aliyun`时，其默认执行`ssh howie@192.168.0.41 -p 22 -i ~/.ssh/id_rsa`。当有多个别名需要设置时，其中间要空上一行。

## 常见问题
使用密钥连接后仍然需要输入登录密码：
这种情况一般是由于密钥登录失败所导致的，请检查`$HOME/.ssh`目录是否为700权限，`$HOME/.ssh/authorized_keys`文件是否为600权限，除此之外的其他权限均不能成功。