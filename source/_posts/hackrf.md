---
title: HackRF 初体验
categories: CheatSheet
date: 2020-01-22 20:25:55
tags:
---

[HackRF](https://greatscottgadgets.com/hackrf/) 是由 Great Scott Gadgets 设计和制造的[开源](https://github.com/greatscottgadgets/hackrf) SDR 硬件，其可以发送或接收 1 MHz 到 6 GHz 的无线电信号。
目前 HackRF 的具体版本为 HackRF One。你可以通过其[官网上列出的购买网址](https://greatscottgadgets.com/wheretobuy/)购买它，也可以在万能的淘宝上购买。![HackRF One](https://greatscottgadgets.com/images/h1-preliminary1-445.jpeg)

<!-- more -->

## 硬件

HackRF One 硬件设备的两侧有一堆接口和指示灯，其中一侧有两个 SMA 接口，分别是 **CLKIN**（Clock In）和 **CLKOUT**（Clock Out）接口，和一个 **USB** 接口（用于连接电脑）；
另一侧有一个 SMA 接口，为 **ANT**（Antenna）天线接口，和两个按键，分别为 **RESET** 和 **ISP**，此外，还有一系列指示灯，**3V3**、**1V8**、**RF**、**USB**、**RX**（Receive）和 **TX**（Transmit）。

通过 USB 将 HackRF One 连接到电脑时，3V3、1V8、RF 和 USB 四个指示灯应该亮起，当进行接收或发射操作时，相应的 RX 和 TX 指示灯会亮起。

## 软件

在 Ubuntu 上，你需要安装如下软件以使用 HackRF One：

```shell
sudo add-apt-repository -y ppa:bladerf/bladerf
sudo add-apt-repository -y ppa:myriadrf/drivers
sudo add-apt-repository -y ppa:myriadrf/gnuradio
sudo add-apt-repository -y ppa:gqrx/gqrx-sdr
sudo apt update

sudo apt install gqrx-sdr hackrf
```

## 常用命令

```shell
hackrf_info    # 查看 Hack RF 连接信息

hackrf_transfer    # 基于文件进行发送和接收 SDR
hackrf_transfer -h    # 查看 hackrf_transfer 帮助信息

# 录制信号
# -r：将数据存储到文件中
# -f：中心频率，单位 Hz
# -s：采样率，单位 Hz（4/8/10/12.5/16/20 MHz，默认 10 MHz）
# -n：采样数量（默认值是无限的）
# -a：设置功放（1 表示开启，0 表示关闭）
# -g：设置 Rx VGA 增益（0 到 62 dB 之间，每次增加 2 dB）
# -l：设置 Rx LNA 增益（0 到 40 dB 之间，每次增加 8 dB）
hackrf_transfer -r capture.raw -f 315000000 -l 8/16/24 -g 20/40 [-s 2000000 -n 10000000 -a 1]

# 重放信号
# -t：从文件中读取数据
# -x：设置 Tx VGA 增益（0 到 47 dB 之间，每次增加 1 dB）
# -R：重复发送模式（默认为关闭）
hackrf_transfer -t capture.raw -f 315000000 -x 40 [-s 2000000 -a 1]
```

一般无线钥匙工作频段都在 315 Mhz、433.92 Mhz。

## 更多

以下列举了一些 HackRF 的相关资料：

- HackRF 的官方文档：https://hackrf.readthedocs.io/en/latest/
- HackRF 的官方视频教程：https://greatscottgadgets.com/sdr/
