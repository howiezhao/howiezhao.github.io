---
title: Docker 入坑指南
date: 2018-08-31 16:59:28
categories: CheatSheet
tags:
---

Docker 是一种基于 Linux 的容器化技术，类似于轻量的虚拟机。它采用 **C/S** 架构，使用 Go 语言开发。

## 版本

Docker 分为 2 个版本：**社区版**（Community Edition, CE）和**企业版**（Enterprise Edition, EE），顾名思义，企业版是收费的。

针对 macOS 10.10.3 和 Windows 10，Docker 还推出了 [Docker Desktop](https://www.docker.com/products/docker-desktop)，Docker Desktop 又分为 2 个渠道（channel），**稳定渠道**（Stable）和**抢先渠道**（Edge），需要注意的是，Docker Desktop 对系统是有要求的，例如，针对 Win10 的 [Docker for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows) 因为要用到 Hyper-V 虚拟机，所以要求系统是 64 位专业版或企业版并开启 Hyper-V 功能。

针对老版本的 Windows 或 macOS，可以使用 [Docker Toolbox](https://docs.docker.com/toolbox/overview/)，它会附带安装一个 VirtualBox 虚拟机。

使用 `docker version` 可以查看 docker 版本号，使用 `docker info` 可以查看 docker 详细信息，直接输入 `docker` 可以查看 docker 相关命令。
<!--more-->
## 镜像

**镜像**（image）文件可以用来生成容器实例，其类似于在虚拟机中安装操作系统时所使用的 ISO 镜像。

镜像文件可以包含一个标签（tag），即版本号。

你可以使用远程仓库中别人制作好的镜像文件，也可以自己制作镜像文件。要制作镜像文件就要编写 **Dockerfile** 文件，其类似于 Makefile 文件。

与 image 相关的常用命令如下：

```bash
# 列出本机的所有image文件
docker image ls
docker images

# 删除指定的image文件
docker image rm <image-name>
docker rmi <image-name>

# 将指定的image文件从远程仓库拉取到本地
docker image pull <image-name>[:tag]
docker pull <image-name>[:tag]

# 利用当前文件夹中的Dockerfile制作一个名为demo、tag为0.0.1的image文件
# 若不指定tag，则默认的标签为latest
docker image build -t demo:0.0.1 .
docker build -t demo:0.0.1 .
```

## 容器

镜像文件生成的容器（container）实例，本身也是一个文件，称为**容器文件**。当关闭容器时，并不会删除容器文件，只是容器停止运行而已。

类似于在虚拟机中安装的操作系统，其本身会在硬盘中创建一系列文件，当关闭操作系统时，相应的文件并不会删除。

与 container 相关的常用命令如下：

```bash
# 从指定的image文件生成一个正在运行的容器实例，
# 若本地没有指定的image文件，会从远程仓库中自动拉取下来并运行
# 使用参数`-it`返回容器实例的终端
# `--rm`
# 使用参数`-p`将容器内端口映射到主机端口
# 使用参数`-v`将主机目录和容器内目录进行绑定
docker container run <image-name>[:tag]
docker run <image-name>[:tag]

# 列出本机正在运行的容器，使用参数`-all`列出所有容器文件
docker container ls
docker ps

# 删除指定的容器文件
docker container rm <container-id>
docker rm <container-id>

# 启动指定的容器实例
docker container start <container-id>
docker start <container-id>

# 重启指定的容器实例
docker container restart <container-id>
docker restart <container-id>

# 关闭指定的容器实例
docker container stop <container-id>
docker stop <container-id>

# 强制关闭指定的容器实例
docker container kill <container-id>
docker kill <container-id>

docker cp
docker attach
docker exec（重要）
```

## 仓库

**仓库**（repository）是不同标签的镜像的集合，注册处（registry）又是不同仓库的集合，Docker 的官方注册处是 [Docker Hub](https://hub.docker.com/)，类似于 GitHub。使用 `docker login` 可以登录到自己在 Docker Hub 上注册的帐号。值得注意的是，国内访问 Docker Hub 速度较慢，建议设置代理或使用国内镜像站。一般来说，国内镜像站只包含流行的公有镜像，私有镜像仍需要从 Docker Hub 中拉取。

与 repository 相关的命令如下：

```bash
# 从Docker Hub中搜索某个 image
docker search [image-name]
```

## Dockerfile

## 代理

阿里云镜像加速

## 常见问题

### Drive has not been shared

在 Windows 10 上启动 Docker 可能会遇到 `Unhandled exception: Drive has not been shared` 这样的问题，可以通过勾选 Settings ——> Resources ——> FILE SHARING 中相应的磁盘以解决此问题。若提示 `Cannot change shared directories`，则你可能需要重启 Docker 后再次进行上述操作。
