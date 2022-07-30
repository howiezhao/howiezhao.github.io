---
title: 白帽子 VPS 选购指南
categories: Translation
date: 2019-02-25 18:17:38
tags:
---

本文翻译自 <https://null-byte.wonderhowto.com/how-to/white-hats-guide-choosing-virtual-private-server-0183135/> ，正文如下：

从受信任的 VPS 进行网络钓鱼活动和托管 Metasploit 会话对于任何专业安全研究人员，渗透测试人员或白帽黑客都很重要。但是，可供选择的 VPS 非常有限，因为大多数提供商对任何类型的黑客都有零容忍政策，无论好坏。在研究了数十种产品之后，我们选出了 5 个理想的产品，非常适合 Null Byte 读者。
<!--more-->
首先要理解的事情是......什么是 VPS？嗯，它代表虚拟专用服务器，是许多用户认为的专用或私有服务器的虚拟化形式，即使它安装在同时运行多个操作系统的物理计算机上。VPS 最常用于在线托管网站。

当我们从提供商处购买 VPS 时，我们实际上是在一个有着许多虚拟服务器的功能强大的高性能物理机器上“租用”一个分区。每个 VPS 都连接到互联网，使个人客户能够使用不同的操作系统，并提供对操作系统的完全 root 访问权限。每个客户（或服务器管理员）独立于共享 VPS 公司提供的物理计算机上的其他客户运营。

- 不要错过：[什么是白帽黑客？](https://null-byte.wonderhowto.com/news/what-is-white-hat-hacker-0166878/)

从本质上讲，虚拟专用服务器是我们可以从世界上任何连接互联网的设备远程控制的计算机。这给了我们很大的能力。对于远程服务器而言，下面是它可以完成的一些事情：

- 创建 VPN 连接
- 托管网络钓鱼站点
- 进行暴力攻击
- 创建 IRC 机器人
- 服务器代理
- 托管有效载荷
- 使用端口扫描器
- 创建蜜罐
- 托管 Metasploit 会话

为了做到这一点，从我们的研究来看，BulletShield 是迄今为止最好的白帽和渗透测试人员的 VPS 提供商，紧随其后的是 [BuyVM](https://buyvm.net/) 和 [ClientVPS](https://www.clientvps.com/)。亚军是 [VPSDime](https://vpsdime.com/) 和 [OneHost Cloud](https://onehostcloud.hosting/)。你可以在下面的图表中看到原因，但跳到下面可以深入研究每个比较点的含义。
![图表](https://img.wonderhowto.com/img/36/31/63655508941243/0/white-hats-guide-choosing-virtual-private-server.w1456.jpg)

## 关键比较点

网上有几个 VPS 对比图表，但没有一个对我来说是与渗透测试人员和白帽子有所联系的。在大多数专业的渗透测试场景中，我们需要在几天内启动 VPS 来托管有效载荷，接收泄漏数据或执行网络钓鱼攻击。

无论 VPS 提供商是否提供实时技术支持，难以理解的硬件规格或过多的操作系统选择都很重要。理想情况下，我们希望使用比特币（BTC）从位于尊重隐私的国家的 VPS 提供商处快速购买最新的 Debian 版本。

在比较本文中介绍的 VPS 提供商时，我试图尽可能客观公正。本文中没有 VPS 提供商付费参与比较图表。我使用下面的标准来得出上面的图表。

- 不要错过：[如何在比特币和以太坊中出售你的 Stellar，Ripple 和其他替代币？](https://smartphones.gadgethacks.com/how-to/binance-101-sell-your-stellar-ripple-other-alt-coins-for-bitcoin-ethereum-0182373/)

### 最好的价钱（Best Price）

我相信定价透明度。这意味着提供商完全诚实地说他们的月费是多少。我的图表中列出的价格可能并不总是反映出给定提供商在主页上公布的价格。我的图表中的价格是计算所有强制性和隐藏费用后的结账价格。这些也是我在网站上找到的最便宜的 VPS 计划的价格。在大多数情况下，这通常有着 512 MB 的 RAM 和 1 个 CPU 内核。

### 渗透测试人员友好型（Pentester-Friendly）

服务条款（ToS）和可接受的使用政策（AUP）可能是进入此比较图表的最高优先项。虽然最初考虑了数十个 VPS 提供商，但大多数明确禁止或阻止端口扫描器，有效载荷分发，网络钓鱼和（或）任何类型的黑客攻击。除了少数例外，这会立即取消 VPS 提供商在比较图表中的资格。

IT 专业人员，安全研究人员和自学成才的白帽黑客在远程服务器上做了大量工作。对我来说很重要的是，这里的 VPS 提供商保留了最符合 Null Byte 受众需求的 ToS 政策。我的图表中的 VPS 提供商是少数几个没有完全敌视“黑客攻击”的 ToS 政策的提供商。

那些被认为是对渗透测试人员友好的提供商并没有在他们的 ToS 中明确声明允许“黑客攻击”（或任何相关术语）。没有一个 VPS 提供商会这样做。大多数这些提供商要么没有提及他们的 ToS 中的黑客攻击，要么他们的网站上根本没有提供 ToS。这被认为表明黑客攻击活动非常不受欢迎，但可能不会导致帐户终止。

### 请求个人信息（Requests Personal Info）

向任何网站提交我们的真实姓名，地址，电话号码和其他个人身份信息都是不可取的。即使匿名不是你的首要任务，VPS 提供商仍有一天可能会受到攻击，并且所有客户数据都会在网上泄露。

购买 VPS 订阅是理想的匿名完成，因为没有人知道我们在研究或渗透测试期间会遇到什么麻烦。对于你购买的服务器上发生的事情，有朝一日可能会对 VPS 提供商采取法律行动，因此最好将有关你自己的少量信息存储在提供商的客户数据库中。

在大多数情况下，我发现在注册期间可以提交一个完全虚假的姓名，地址和电话号码，但我并不认为这是提供商的“好功能”。向任何合法公司提交虚假信息几乎肯定会违反提供商的服务条款并导致帐户立即终止。

VPS 提供商要求的电子邮件地址不属于“个人信息”，因为匿名获取一次性电子邮件地址很容易。毕竟 VPS 提供商需要建立与客户沟通的有效方法。

### 接受比特币付款（Accepts BTC Payments）

如果获得比特币（BTC）不是障碍，这可能是你的首选付款方式。目前大多数提供商都接受比特币，但使用匿名加密货币的好处大部分都被 VPS 提供商对个人身份信息的请求所抵消。我发现使用比特币进行在线购物比使用信用卡更快更方便。

### 接受预付信用卡（Accepts Prepaid Credit Cards）

获取比特币进行匿名交易可能很困难。用现金购买[预付卡或一次性借记卡](https://null-byte.wonderhowto.com/how-to/securely-anonymously-spend-money-online-0131351/)可能更方便。如果没有使用预付借记卡实际提交付款，很难验证这一点。在大多数情况下，我能够联系客户服务代表，并从他们那里获得有关使用预付卡进行交易的直接答复。

### Tor 友好型网站（Tor-Friendly Website）

如果你通过安全的 VPN 连接使用信用卡进行在线购买或通过 Tor 匿名进行在线购买，VPS 提供商有时会暂停你的帐户。联系客户支持并解决暂停可能需要数天时间。

我使用同一个常用的 Firefox 浏览器通过 Tor 浏览了每个站点。要求访问者填写验证码以查看其网站或处理结帐的提供商被标记为对希望保持匿名的用户不友好。这并不意味着可以通过 Tor 进行事务处理。在查看这些网站时，我只尽可能地进入结账过程，而不实际提交付款。

- 不要错过：[如何使用 Tor 匿名的访问暗网？](https://null-byte.wonderhowto.com/how-to/access-dark-web-while-staying-anonymous-with-tor-0179341/)

### 公司总部所在国（Company HQ's Country）

认为提供安全加密交易的公司将与当局充分[合作以捕获黑客](https://www.theregister.co.uk/2011/09/26/hidemyass_lulzsec_controversy/)并不是不切实际的。VPS 的 IP 地址是否来自尊重隐私的国家并不总是重要的。如果向你提供 VPS 的公司位于美国或英国，他们很可能会毫不犹豫地将你的个人信息交给任何权威人士。

进一步涉及隐私问题，[UKUSA 协议](https://zh.wikipedia.org/wiki/%E8%8B%B1%E7%BE%8E%E5%8D%94%E5%AE%9A)是英国，美国，澳大利亚，加拿大和新西兰之间的协议，旨在合作收集，分析和共享情报。这个群体的成员被称为[五眼联盟](https://zh.wikipedia.org/wiki/%E4%BA%94%E7%9C%BC%E8%81%AF%E7%9B%9F)。这些国家因拥有侵犯隐私的法律和政策而臭名昭著。

在最尊重隐私的国家选择 VPS 提供商可能不是最优先考虑的问题，但至少考虑具有[良好隐私法律的国家](https://nomadcapitalist.com/2013/12/15/top-5-best-countries-host-website-data-privacy/)的提供商是有意义的。

### 离岸解决方案（Offshore Solutions）

“离岸 VPS”意味着服务器位于公司的国家边界位置之外，并且可能允许一定程度的自由裁量权。这对你作为渗透测试人员以及你受委托保护的公司非常重要，因为你可能会收到不应共享或泄露的妥协和敏感信息。我们鼓励读者独立询问 VPS 提供商，以确定他们的离岸解决方案是否适合你。

提供商指出，提供离岸解决方案通常要付出一定的代价。不应该假设他们最便宜的 VPS 解决方案也是其离岸选项的价格。

## 1、BulletShield

BulletShield 是我的首选，是 Null Byte 读者的最佳 VPS 提供商。BulletShield 在注册账户或准备提交比特币交易时不要求任何类型的个人信息。他们还强制要求比特币交易，并且没有明确禁止任何渗透测试活动的 ToS。
![BulletShield](https://img.wonderhowto.com/img/36/93/63655505111133/0/white-hats-guide-choosing-virtual-private-server.w1456.jpg)
缺点是他们不接受预付信用卡，最便宜的价格有点贵，但如果你重视隐私，价格不一定是主要考虑因素。

在涉及公司总部时，BulletShield 不会透露这些信息。快速域名搜索显示，它是由加拿大公司 Tucows Domains Inc. 购买的，是从位于西印度群岛偏远岛屿的 Charlestown 购买的。但是，这并不意味着这就是 BulletShield 的总部所在地，这只是域名注册商 BulletShield 使用注册域名的地方。

他们提供离岸解决方案和 Tor 友好型网站，使 BulletShield 整体处于领先地位。但是，一位客户服务代表向我提到“渗透测试”是“仅允许......防弹服务”，这可能是成本方面的问题。

- ToS：无可用
- AUP：无可用
- 隐私：无可用

## 2、BuyVM

[BuyVM](https://buyvm.net/) 是允许合法渗透测试的亚军，如果公司或相关人员给出明确和合法的书面同意。一位代表证实了这一点，他们说“他们需要一份来自法律团队的完整文件，代表有关目标的授权书”。
![BuyVM](https://img.wonderhowto.com/img/33/95/63655505142883/0/white-hats-guide-choosing-virtual-private-server.w1456.jpg)
他们的起价确实提升了他们的排名，VPS 解决方案每月只需 2.42 美元。但是，他们确实要求你提供个人信息，并且为了注册帐户，“帐户详细信息必须与付款方式提供的信息相符”，这可能意味着匿名预付卡将无法使用。不过，比特币是可以被接受的。

虽然他们确实有一个 Tor 友好的网站，但他们总部设在加拿大，并不提供离岸解决方案，这可能是负面的，取决于你使用 VPS 的目的。

- ToS：[链接](https://buyvm.net/terms-of-service/)
- AUP：[链接](https://buyvm.net/acceptable-use-policy/)
- 隐私：[链接](https://buyvm.net/privacy-policy/)

## 3、ClientVPS

[ClientVPS](https://www.clientvps.com/zh-cn) 有一个 ToS，即你所执行的任何导致对人身或财产“受到伤害”，侵犯版权等的行为都要你自己承担全部责任。
![ClientVPS](https://img.wonderhowto.com/img/69/58/63655505152117/0/white-hats-guide-choosing-virtual-private-server.w1456.jpg)
总的来说，他们的价格是最昂贵的，但亮点包括接受比特币（预付 Visa 卡尚不清楚），拥有 Tor 友好的网站，总部设在俄罗斯（信息请求经常被忽略），并提供离岸解决方案，所有这些都巩固了其目前在排名中的地位。

除了高昂的价格外，其他缺点包括他们缺乏有关合法渗透测试的信息（他们没有回复我的询问），他们确实要求你提供个人数据。

- ToS：[链接](https://www.clientvps.com/terms-of-service)
- AUP：无公开链接
- 隐私：[链接](https://www.clientvps.com/privacy-policy)

## 4、VPSDime

[VPSDime](https://vpsdime.com/) 不是一个非常理想的选择，因为它们没有比特币支付选项，不允许客户匿名查看他们的网站，也没有任何离岸 VPS 解决方案。但是，他们的 ToS 只是明确禁止“端口扫描”。他们没有提及渗透测试，漏洞扫描，网络钓鱼或其他常见的渗透活动。
![VPSDime](https://img.wonderhowto.com/img/00/36/63655505163524/0/white-hats-guide-choosing-virtual-private-server.w1456.jpg)
当询问澄清他们的合法渗透测试政策时，他们没有回复我的电子邮件。他们的 ToS 太模糊了，我无法确定是否允许这样的（合法）活动。出于这个原因，我建议读者在使用他们的服务之前联系 VPSDime 澄清。

虽然 VPSDime 没有明显的好处，但它们是最便宜的选择之一。

- ToS：[链接](https://vpsdime.com/tos.html)
- AUP：[链接](https://vpsdime.com/aup.html)
- 隐私：[链接](https://vpsdime.com/privacy.html)

## 5、OneHost Cloud

[OneHost Cloud](https://onehostcloud.hosting/) 是我能找到的唯一提供 Kali Linux VPS 和渗透测试解决方案的 VPS 提供商。他们的价格仅为每月 6.59 美元，这是该提供商的另一个主要好处，并且他们接受比特币付款。
![OneHost Cloud](https://img.wonderhowto.com/img/55/35/63655505173336/0/white-hats-guide-choosing-virtual-private-server.w1456.jpg)
对于那些不打算在未经同意的情况下非法扫描网站或入侵实体的白帽子来说，OneHost Cloud
似乎是最佳选择。毕竟如果它们提供 Kali 解决方案但不允许合法的渗透测试，那么对于客户来说也会非常混乱。但是，当我询问合法渗透测试时，他们只是回答：
> 来自此地址的所有未来电子邮件都将被阻止。

这是在没有任何理由或解释的情况下发给我的。出于这个原因，OneHost Cloud 排在最后，我建议读者在执行任何类型的渗透测试之前，独立地向 OneHost Cloud 询问他们的 ToS 策略。

该提供商的其他缺点是要求提供个人信息；位于英国伦敦；没有匿名网站；并且缺乏有关离岸解决方案和预付卡的信息。

- ToS：[链接](https://onehostcloud.hosting/terms-and-conditions/)
- AUP：无公开链接
- 隐私：[链接](https://onehostcloud.hosting/privacy-policy/)

## 意见

专业和独立渗透测试人员的选择是非常有限的。大多数 VPS 提供商都有检测系统，如果检测到任何类型的扫描，网络钓鱼或垃圾邮件，它们会自动暂停客户帐户。在我们的测试计划中，可能需要数天才能解决暂停并造成重大挫折。

选择愿意与我们合作以更好地保护公司网站的提供商是至关重要的。如果你是一个专业的渗透测试者，或者只是一个希望以安全和匿名的方式加强技能的新手黑客，那么选择最能满足你需求并获得乐趣的提供商。

- 不要错过：[如何使用生日卡片破解任何人的 Wi-Fi 密码？](https://null-byte.wonderhowto.com/how-to/hack-anyones-wi-fi-password-using-birthday-card-part-1-creating-payload-0183043/)

## 一些评论

Pulkit Singhania：
> Cloudsigma 实际上也是一个不错的选择。
  他们提供免费的 vps，没有任何登录或任何注册的免费，但只有一个小时。
  我亲自尝试过，它提供 2GB 内存和 50GB 硬盘，最高可达 25兆字节/秒的互联网流量。
  如果你使用公司电子邮件注册，则可免费试用 7 天
