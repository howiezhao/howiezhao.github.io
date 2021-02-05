---
title: 使用Let's Encrypt获取免费SSL证书
date: 2018-09-16 22:38:04
categories: CheatSheet
tags:
  - Web
---

[Let's Encrypt](https://letsencrypt.org/zh-cn/)是一个免费、自动化和开放的证书颁发机构，它提供了一个工具：[Certbot](https://certbot.eff.org/)，可以用来获取SSL证书。
进入Certbot的官网，根据自己的环境选择Web服务器和操作系统，即可得到详细的操作步骤，下面以Nginx Web服务器和CentOS 6操作系统为例，给出相关步骤：
<!--more-->
## 安装

```bash
# 下载certbot-auto脚本
wget https://dl.eff.org/certbot-auto

# 配置相关权限
chmod a+x certbot-auto
```

## 配置

请注意，获取或更新SSL证书之前需关闭相应的Web服务器，具体而言，需要执行`service nginx stop`。另外，第一次执行`certbot-auto`命令时，它会下载并安装相关环境，耐心等待即可。
Certbot提供了一个Nginx插件，直接使用`./certbot-auto --nginx`即可完成所有配置。
如果你想手动配置，可执行`./certbot-auto certonly --standalone`命令，此命令运行过程中会要求用户输入要获取SSl证书的域名，按要求输入即可，命令运行成功后会显示证书相关文件所在的目录。
接下来只需在Nginx的配置文件`nginx.conf`中进行如下配置即可(以howiezhao.com域名为例)：

```bash
ssl on;
ssl_certificate /etc/letsencrypt/live/howiezhao.com/fullchain.pem;
ssl_certificate_key /etc/letsencrypt/live/howiezhao.com/privkey.pem;
```

## 更新

Let's Encrypt的证书默认时间为90天，当到期后，需要使用`./certbot-auto renew`命令进行证书更新。

## 更多

要查看`certbot-auto`的更多命令，可以使用`certbot-auto --help all`命令查看之。要了解SSL的详细知识，可参考我之前写的笔记[HTTPS运行机制](http://localhost:4000/2018/05/11/https/)。要了解Nginx的相关知识，可参考我之前写的笔记[利用Nginx进行反向代理](todo)。
