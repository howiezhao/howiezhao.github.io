---
title: Kali Rolling 2017 下安装 w3af 出错解决方案
date: 2017-11-08 11:57:43
categories: Bug
tags:
  - Kali
---

## Run error: "'module' object has no attribute 'SSL_ST_INIT'"."

**解决方法 1：**

修改 `/usr/local/lib/python2.7/dist-packages/OpenSSL/SSL.py` 文件，将下面四行注释掉

```python
# SSL_ST_INIT = _lib.SSL_ST_INIT
# SSL_ST_BEFORE = _lib.SSL_ST_BEFORE
# SSL_ST_OK = _lib.SSL_ST_OK
# SSL_ST_RENEGOTIATE = _lib.SSL_ST_RENEGOTIATE
```

**解决方法 2：**

1. 卸载 w3af 要求的 pyOpenSSL 版本

   ```sh
   pip uninstall pyOpenSSL
   ```

2. 安装最新版 pyOpenSSL

   ```sh
   pip install pyOpenSSL
   ```

3. 编辑 w3af 安装目录中的 `/w3af/core/controllers/dependency_check/requirements.py` 文件，将要求的 pyOpenSSl 版本号改为你安装的最新版，即修改下面这一行代码

   ```python
   PIPDependency('OpenSSL', 'pyOpenSSL', 'Version of pyOpenSSL you are using')
   ```

<!-- more -->

## error: command 'x86_64-linux-gnu-g++' failed with exit status 1

**解决方法：**

使用如下命令安装相关依赖

```sh
apt-get build-dep python-lxml
apt-get install libxslt-dev libssl-dev
```

## ImportError: No module named webkit

启动 GUI 界面时可能会报此错误，原因是未安装相关模块

**解决方法：**

执行如下命令

```sh
apt-get install python-webkit python-webkit-dev
```

在 Kali 下，因为 python-webkit、python-webkit-dev 不在 Kali 默认的源中，所以需要执行下面的命令

```sh
wget http://ftp.cn.debian.org/debian/pool/main/p/python-support/python-support_1.0.15_all.deb
dpkg -i python-support_1.0.15_all.deb
wget http://ftp.cn.debian.org/debian/pool/main/p/pywebkitgtk/python-webkit_1.1.8-3_amd64.deb
dpkg -i python-webkit_1.1.8-3_amd64.deb
apt install python-gtk2-dev
wget http://ftp.cn.debian.org/debian/pool/main/p/pywebkitgtk/python-webkit-dev_1.1.8-3_all.deb
dpkg -i python-webkit-dev_1.1.8-3_all.deb
```

安装过程中可能需要安装相关依赖，可执行如下命令

```sh
apt --fix-broken install
```

## ImportError: No module named gtksourceview2

同样，启动 GUI 时也可能报此错误

**解决方法：**

执行如下命令

```sh
apt-get install python-gtksourceview2
```
