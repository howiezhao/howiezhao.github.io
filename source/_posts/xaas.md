---
title: 云服务的三种模式
date: 2018-07-15 16:58:01
categories: CheatSheet
tags:
---

云服务的模式一般有 IaaS、PaaS、SaaS 三种，既然是云服务，也即我们不用购买真实的计算设备，所有的模式都是基于此之上的。

## IaaS

**IaaS**，Infrastructure as a Service（基础设施即服务），云服务的最底层，服务商提供操作系统、存储设施、硬件配置等资源，典型的例子是 **VPS**，即 Virtual Private Server（虚拟专用服务器），这类服务一般提供必要的 Shell 接口，可使用户连接到操作系统进行相关配置，常见的 VPS 厂商有 [Amazon EC2](https://aws.amazon.com/cn/ec2/)、[阿里云 ECS](https://www.aliyun.com/product/ecs) 等。

## PaaS

**PaaS**，Platform as a Service（平台即服务），云服务的中间层，服务商提供必要的应用，用户无权访问操作系统及硬件等资源，典型的例子是**虚拟空间**，这类服务一般会提供必要的 Web 服务器、数据库等，用户可以直接在其上部署 Web 应用，常见的 PaaS 厂商有 [Google App Engine(GAE)](https://cloud.google.com/appengine/)、[Heroku](https://www.heroku.com/) 等。

## SaaS

**SaaS**，Software as a Service（软件即服务），云服务的最高层，直接提供现成的应用供用户使用，用户所付出的精力最少，例如本站采用的 Hexo、WordPress 等。
