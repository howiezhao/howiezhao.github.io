---
title: HackRF 初体验
categories: CheatSheet
date: 2020-01-22 20:25:55
tags:
---

[HackRF](https://greatscottgadgets.com/hackrf/) 是由 Great Scott Gadgets 设计和制造的开源 SDR 硬件，其可以发送或接收 1 MHz 到 6 GHz 的无线电信号。目前 HackRF 的具体版本为 HackRF One。你可以通过其[官网上列出的购买网址](https://greatscottgadgets.com/wheretobuy/)购买它，也可以在万能的淘宝上购买。![HackRF One](https://greatscottgadgets.com/images/h1-preliminary1-445.jpeg)

<!-- more -->

## 软件

你需要安装如下软件以使用 HackRF One：

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
Tx Mode：发射模式
Rx Mode：接收模式
